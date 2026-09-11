# Fun with Bash

> It is so very easy to find the solution with a prompt away from LLM, but where is the fun/learning in that. 

## Problem 1

I log in to check my work, and all prepared to review some PR(AI Slop in other words). But then an interesting problem appeared. For the sake of keeping thing abstract here it goes:

1. You have recently migrated your github repo to a fresh one(for whatever reason possible), with the complete git history.
2. You noticed that there are more than >300 branches(possibly stale) sitting idle in your repo. And you want to prune it.

One possible way that one can thing of is to delete one branch at a time from Github UI. But who wants to do that? :P  

Another way(that I thought of), is to look at how many a branch is behind(let's say from origin/main) and let's say clean the ones that is `> 150` commits behind. This stat is also displayed in Github UI btw.

How are you going to approach this solution?

## Approach (TBD)
