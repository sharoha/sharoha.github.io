# Haskell local setup

## Some background

I have tried Haskell programming language way back, mainly because I was interested in Functional Programming and it's one of the language that support Pure Functional programming paradiam.  
To be honest, it never clicked and it still difficult to wrap my brain around the nuances of thinking in Functional way. But this is something that takes time(applies to almost all the learning process).

## Why??

Recently I have stumbled upon this Paper: [baastad.pdf](https://homepages.inf.ed.ac.uk/wadler/papers/marktoberdorf/baastad.pdf) and it talks about the concept of Monad in great detail.
Since this somewhat references Haskell as its pseudo code, so I tried following by writing my own implementation of the explanation.  
Also, since I am back to Haskell after some time, so why not document the process around setting it up.

## Things I want

1. Be able to run a program easily.
2. Be able to find the docs locally for api references.

## Tools

### GHCup

- GHCup is a package manager for tools related to Haskell

```bash
-- install GHCup
brew install ghcup
```

- GHCup install its packages inside ~/.ghcup/bin, so it's a good time to Pathisize this Path

```bash
-- add this in ~/.zshrc or ~/.bashrc
export PATH="~/.ghcup/bin:$PATH"
```

### ghc

- Compiler to compile Haskell source code

```bash
-- install ghc
ghcup install ghc
```

## Build/Run

### Using ghc

```bash
-- build the program
ghc test.hs
-- run the executable
./test
```

### Using runhaskell

```bash
-- run directly without generating the executable
runhaskell test.hs
-- I am not sure if runhaskell comes with ghc
```

### Using ghci(Interpreter)

```bash
-- Load ghci
ghci

-- load the file, this loads all functions from that module
ghci>>:load test.hs

-- run a function (Lets say main)
ghci>>main

```

## Docs

### From Hackage (Internet)

This following provide different Links for the APIs provided by different Modules

- https://hackage-content.haskell.org/package/base-4.22.0.0/docs/index.html

### ghci

```bash
-- Interpreter can help list down different apis provided by a module
ghci>>:load Data.Bits -- Loads the module
ghci>>:browse Data.Bits -- Lists the apis
ghci>>:info Bits -- gives a concise list of available apis
ghci>>:docs popCount
```

### Default ghcup installation

```bash
-- index everything inside ~/.ghcup
cabal update

-- With this, we can try to find files that matches a particular tag
-- Lets say, Data.Bits, then we can try finding this file
find ~/.ghcup -iname '*Data.Bits*'
-- above find the html file, and now it can be opened in Chrome for example
open -a "Google Chrome" full_path_of_file
-- or using xargs in a single command(But can open multiple find)
find ~/.ghcup -iname '*Data.Bits*' | xargs  open -a "Google Chrome" full_path_of_file

```
