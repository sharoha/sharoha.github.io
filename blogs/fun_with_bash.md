# Fun with Bash

> It is so very easy to find the solution with a prompt away from LLM, but where is the fun/learning in that.

## Problem 1

I log in to check my work, and all prepared to review some PR(AI Slop in other words). But then an interesting problem appeared. For the sake of keeping thing abstract here it goes:

1. You have recently migrated your github repo to a fresh one(for whatever reason possible), with the complete git history.
2. You noticed that there are more than >300 branches(possibly stale) sitting idle in your repo. And you want to prune it.

One possible way that one can thing of is to delete one branch at a time from Github UI. But who wants to do that? :P

Another way(that I thought of), is to look at how many a branch is behind(let's say from origin/main) and let's say clean the ones that is `> 150` commits behind. This stat is also displayed in Github UI btw.

How are you going to approach this solution?

## Approach

### rev-list

- `git rev-list` command allow us to list commit objects in reverse chronological order.

```bash
-- So the following provides all the commit id(sha value) from the current branch to the starting point of the project
git rev-list HEAD
-- And this command provides the commit objects that reachable from master but not from HEAD
-- So in a way, it says how many new commits were added to master that is not present in HEAD(considering HEAD was created from master at a point in time)
git rev-list HEAD..master
-- To count the number of commits objects you can either pair this up with wc -l, or use --count flag
git rev-list HEAD..master --count
-- or
git rev-list HEAD..master | wc -l
```

### Bash script

```bash
-- Pair the rev-list command with all branches present in repo

#!/bin/bash

-- in `rg` -v option negates the match, so it says match it with all lines that does not have a string master
git branch -r | rg -v "master" | while read branch; do
    -- a weird syntax to remove the prefix origin/ from all searched results.
    without_origin = "${branch#origin/}"

    git rev-list --count "$branch"..origin/master
```

- And then we can couple the above script(say `git_remote_branch_commit.sh`) with `awk` command to filter out result
- And finally send the result to `xargs` (a very useful command) to run git push on each filtered results

```bash
./git_remote_branch_commit.sh | awk -F ":" '{if ($2 > 150) {print $1}}' | xargs -n 1 git push origin --delete
-- $2 in awk says which column you want from the result, $0 refers to the complete row in context
-- -n 1 option in xargs says to process one line a time
```

I think this concludes the approach. Few things that we definitely explored here:

1. rev-list
2. some understanding of awk command
3. And a very useful xargs command
