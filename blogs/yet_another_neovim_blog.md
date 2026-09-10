# Yet Another Neovim Blog

I guess I always had this back of the mind thought about jotting down a blog someday, but never made it happen. But finally decided to start this habit and this is the first blog that I have decided to work on.

Lately, I have been watching some stream by the Legend [TsodingDaily](https://www.youtube.com/@TsodingDaily) and it got me excited about why I started coding in the first place. So here I am, taking a stab at building something that I was probably thought of trying out.

## The Background

I have been a Neovim user for sometime now, even though I sometime have to switch back to IntelliJ probably because I got too comfortable working on it for 7 years. Anyway, I love the fact that Neovim(being a successor of Vim itself) is so Keyboard friendly and also super customizable because of the addition of Lua as the configuration language.

As of writing this Blog, Neovim has a nightly release for the version 0.13. One of the significant feature is the addition of the [Image API](https://github.com/neovim/neovim/issues/30889) in the editor.

## The Problem

Recently I have mostly been navigating README docs in Neovim itself. One of the problem that we face in this workflow is the inability to render in-hosted image in the Markdown file itself. So the workaround was to render the markdown side-by-side in a live webserver in a browser.

I assume that the addition of the Image API will help solve this issue. So test this out, I am thinking of experimenting with possible solution in some exisiting in-editor markdown render. For example: [render-markdown](https://github.com/meanderingprogrammer/render-markdown.nvim).

Still not sure, how it will turn out but lets see.

## Phase 1

Since, Neovim hasn't released its 0.13 version yet and still in nightly build. I was hoping to build the project locally and start the editor in local.

What I wanted:

1. Easy to follow guide to clone and build the repo.
   1. This was pretty easy, since the guide [README.md](https://github.com/neovim/neovim#install-from-source) defines how to achive that.
2. Not mess up my existing setup for neovim and the beautiful plugin configuration I already have setup.
   1. Its possible to run the build pointing the target to a specific location using the flag.

Things that I learned along the way:

1. You can trigger the build and install in two easy steps:

```bash
make CMAKE_BUILD_TYPE=RelWithDebInfo
make install
```

2. Since I wanted to modify the build target it was easy to modify the previous command:

```bash
git checkout nightly
make CMAKE_EXTRA_FLAGS="-DCMAKE_INSTALL_PREFIX=$HOME/neovim
make install
```

## Phase 2

Its time to setup the configuration first. Neovim looks for its configuration in $HOME/.config/nvim directory, so it was easir to setup the directory structure using:

```bash
-- HOME is set to ~/Desktop/Projects/installs
cd $HOME
mkdir -p ~/.config/nvim
cd ~/.config/nvim
touch init.lua -- this is where all the magic lies
```

## Phase 3

Before I start experimenting with the new Image API, I want to do 3 things:

```lua
-- 1. Setup my basic vimsetup.lua configuration.
cd $HOME/.config/nvim
mkdir lua/
touch vimsetup.lua -- this is where all vim.o and vim.g configuration lines

require("setup.vimsetup")
```

```lua
-- 2. Setup the Tokyonight theme, why not cause the Editor needs to look a bit colorful

vim.pack.add({
	"https://github.com/folke/tokyonight.nvim",
})

vim.cmd([[colorscheme tokyonight ]])
```

```lua
-- 3. And lastly need to setup the render-markdown plugin itself(TODO - This needs to point to a local directory)


vim.pack.add({
	"https://github.com/meanderingprogrammer/render-markdown.nvim",
})
```

## TODO

- [ ] Figure out a way to setup the markdown library in pack:add using a locally checked in github repo
