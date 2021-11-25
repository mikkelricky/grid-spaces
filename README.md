# Grid spaces

Grid spaces a la [TotalSpaces2](https://totalspaces.binaryage.com/), but for
[macOS Monterey](https://www.apple.com/macos/monterey/), built on
[yabai](https://github.com/koekeishiya/yabai) and
[skhd](https://github.com/koekeishiya/skhd).

## Installation

Check the [installation
requirements](https://github.com/koekeishiya/yabai/wiki#installation-requirements)
for `yabai` and install it:

```sh
brew install yabai --HEAD
```

Create the desired number of spaces [using
yabai](https://github.com/koekeishiya/yabai/wiki/Commands#create-and-destroy-spaces)
or [Mission Control](https://support.apple.com/en-us/HT204100).

Make sure that `yabai` works and can focus spaces by running a command like

```sh
yabai --message space --focus next
brew services start yabai
```

Create the file `~/.gridspacesrc` and define the number of columns in your grid:

```dotenv
GRID_COLUMNS=3
```

Install [skhd](https://github.com/koekeishiya/skhd#install):

```sh
brew install koekeishiya/formulae/skhd
brew services start skhd
```

Create or edit [the configuration file for
skhd](https://github.com/koekeishiya/skhd#configuration) and define keyboard
shortcuts for moving around in the grid, e.g.

```sh
cmd + ctrl - up    : «path to this directory»/navigate up
cmd + ctrl - down  : «path to this directory»/navigate down
cmd + ctrl - left  : «path to this directory»/navigate left
cmd + ctrl - right : «path to this directory»/navigate right
```

Run

```sh
for direction in up down left right; do printf "cmd + ctrl - %-8s: %s/navigate %s\n" $direction $PWD $direction; done
```

to easily generate the configuration.

That's it! Now you should be able to use your grid.

## Coding standards

[Install ShellCheck](https://github.com/koalaman/shellcheck#installing):

```sh
brew install shellcheck
```

Check to code:

```sh
shellcheck navigate
```
