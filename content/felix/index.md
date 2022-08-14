+++
title = "felix: TUI file manager written in Rust"
date = 2022-08-14
template = "felix.html"
+++

<p align=right>
<a href="https://crates.io/crates/felix">crates.io</a> <a href="https://github.com/kyoheiu/felix">repository</a>
</p>

---

<h1 align=center><i>felix</i></h1>

A tui file manager with vim-like key mapping, written in Rust. Fast, simple, and easy to configure & use.

![sample](/images/sample.gif)

- [New Release](#new-release)
- [Get started](#get-started)
  - [Status](#status)
  - [Installation](#installation)
  - [Integrations](#integrations)
- [Usage](#usage)
- [Key Manual](#key-manual)
  - [Move cursor / Change directory](#move)
  - [Open a file](#open)
  - [Manage items](#manage)
  - [Change the view, search and others](#view)
- [Configuration](#configuration)

<a id="new-release"></a>

## New Release

### v1.1.1 (2022-08-11)

#### Fixed

- In the filter mode and shell mode, when you don't have any input, `backspace` now means return to the normal mode. Also, during the filter mode, `Esc` now restores the cursor position.

### v1.1.0 (2022-08-08)

#### Important change about the preview feature

- From v1.1.0, felix uses [hpjansson](https://github.com/hpjansson) /
  [chafa](https://github.com/hpjansson/chafa) instead of `libsixel` & `viuer` to preview image files. This greatly improves the performance and code maintainability, and as a consequence, the number of dependencies is reduced (137 -> 53).
- Due to this change, the image preview does not work out of the box: **_Install `chafa` and it will be enabled without configuration_**. To install, please see https://hpjansson.org/chafa/.
- By `chafa`, the high-res image preview is enabled in terminals that support sixel, or kitty.
- In other terminals, images are displayed by characters.

For more details, see `CHANGELOG.md` in the [repository](https://github.com/kyoheiu/felix).

<a id="get-started"></a>

## Get Started

<a id="status"></a>

### Status

| OS      | Status                           |
| ------- | -------------------------------- |
| Linux   | works                            |
| NetBSD  | works                            |
| MacOS   | works (tested only on Intel Mac) |
| Windows | not supported yet                |

<a id="installation"></a>

### Installation

_Make sure that `gcc` is installed._

From crates.io:

```
cargo install felix
```

From AUR:

```
yay -S felix-rs
```

On NetBSD, package is available from the official repositories:

```
pkgin install felix
```

From this repository:

```
git clone https://github.com/kyoheiu/felix.git
cd felix
cargo install --path .
```

<a id="integrations"></a>

### Integrations

In addition, you can use felix more conveniently by installing the following two apps:

- [zoxide](https://github.com/ajeetdsouza/zoxide): A smarter `cd` command, which enables you to jump to a directory that matches the keyword in felix.
- [chafa](https://hpjansson.org/chafa/): Terminal graphics for the 21st century, by which you can preview images in felix.

These apps do not need any configuration to use with felix!

<a id="usage"></a>

## Usage

| command / options                  |                                                               |
| ---------------------------------- | ------------------------------------------------------------- |
| `fx`                               | Show items in the current directory.                          |
| `fx <directory path>`              | Show items in the path. Both relative and absolute available. |
| `fx -l [path]` / `fx --log [path]` | Launch the app and create a log file.                         |
| `fx -v` / `fx --version`           | Print the current version and check update.                   |
| `fx -h` / `fx --help`              | Print help.                                                   |

<a id="key-manual"></a>

## Key Manual

<a id="move"></a>

### Move cursor / Change directory

| Key                      | Explanation                                                                                                                                                                                                                                                                    |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| j / Up                   | Go up. If the list exceeds max-row, it "scrolls" before the top of the list.                                                                                                                                                                                                   |
| k / Down                 | Go down. If the list exceeds max-row, it "scrolls" before the bottom of the list.                                                                                                                                                                                              |
| h / Left                 | Go to the parent directory if exists.                                                                                                                                                                                                                                          |
| l / Right / Enter        | Open a file or change the directory. Commands for the execution can be managed in the config file.                                                                                                                                                                             |
| gg                       | Go to the top.                                                                                                                                                                                                                                                                 |
| G                        | Go to the bottom.                                                                                                                                                                                                                                                              |
| z + Enter                | Go to the home directory.                                                                                                                                                                                                                                                      |
| z \<keyword\> + Enter    | **_This command requires zoxide installed._** Jump to a directory that matches the keyword. Internally, felix calls [`zoxide query <keyword>`](https://man.archlinux.org/man/zoxide-query.1.en), so if the keyword does not match the zoxide database, this command will fail. |
| :cd + Enter / :z + Enter | Go to the home directory.                                                                                                                                                                                                                                                      |
| :z \<keyword\> + Enter   | Same as `z <keyword>`.                                                                                                                                                                                                                                                         |

<a id="open"></a>

### Open a file

| Key               | Explanation                                                                                                                                                                                                                  |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| l / Right / Enter | Open a file or change the directory. Commands for the execution can be managed in the config file.                                                                                                                           |
| o                 | Open a file in a new window. This enables you to use felix while working with the file. If you open a file in an editor that runs inside the terminal, no new window appears, and after exit some error messages may appear. |

<a id="manage"></a>

### Manage items

| Key             | Explanation                                                                                                                             |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| dd              | Delete and yank one item (it will go to the trash directory).                                                                           |
| yy              | Yank one item. If you yanked other item(s) before, it's replaced by this one.                                                           |
| p               | Put yanked item(s) in the current directory. If the item with same name exists, copied item will be renamed with the suffix "\_copied". |
| c               | Switch to the rename mode (enter the new name and press Enter to rename the item).                                                      |
| V               | Switch to the select mode, where you can move cursor to select items.                                                                   |
| d (select mode) | Delete and yank selected items, and return to the normal mode.                                                                          |
| y (select mode) | Yank selected items, and return to the normal mode.                                                                                     |
| u               | Undo put/delete/rename.                                                                                                                 |
| Ctrl + r        | Redo put/delete/rename.                                                                                                                 |

<a id="view"></a>

### Change the view, search and others

| Key             | Explanation                                                                                                                                                                                                              |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| v               | Toggle whether to show the item preview (text, image, or the contents tree) on the right half of the terminal. **_You must install [`chafa`](https://hpjansson.org/chafa/) in order to preview images._**                |
| backspace       | Toggle whether to show hidden items or not. This change remains after exit (stored in `.session`).                                                                                                                       |
| t               | Toggle sort order (by name <-> by modified time). This change remains after exit (same as above).                                                                                                                        |
| /               | Switch to the filter mode (enter the keyword and press Enter to show the filtered list). Press h or Left to exit the filter mode.                                                                                        |
| :               | **_Experimantal._** Switch to the shell mode. Type command and press Enter to execute it. You can use any command in the displayed directory, but some commands may fail, and the display may collapse during execution. |
| :e + Enter      | Reload the current directory. Useful when something goes wrong.                                                                                                                                                          |
| :empty + Enter  | Empty the trash directory. **Please think twice to use this.**                                                                                                                                                           |
| :h + Enter      | Show help. (scrolls by `j/k` or `Up/Down`)                                                                                                                                                                               |
| Esc             | Return to the normal mode.                                                                                                                                                                                               |
| :q + Enter / ZZ | Exit.                                                                                                                                                                                                                    |

Note that items moved to the trash directory are prefixed with Unix time (like `1633843993`) to avoid the name conflict. This prefix will be removed when put.

<a id="configuration"></a>

## Configuration

| OS    | path                                      |
| ----- | ----------------------------------------- |
| Linux | `$XDG_CONFIG_HOME/felix`                  |
| macOS | `$HOME/Library/Application Support/felix` |

```
felix
├─ config.toml # configuration file
├─ log         # log files
└─ trash       # trash directory

# All config file and directories will be automatically created.
```

Default config file will be created automatically when you launch the program for the first time.

Default config.toml:

```
# Default exec command when open files.
default = "nvim"

# (Optional) Whether to use the full width of terminal.
# If not set, this will be true.
# use_full_width = true

# (Optional) Set the max length of item name to be displayed.
# This works only when use_full_width is set to false.
# If the terminal size is not enough, the length will be changed to fit it.
# If not set, this will be 30.
# item_name_length = 30

# (Optional)
# key (the command you want to use) = [values] (extensions)
# [exec]
# feh = ["jpg", "jpeg", "png", "gif", "svg"]
# zathura = ["pdf"]

# The foreground color of directory, file and symlink.
# Pick one of the following:
#   AnsiValue(u8)
#   Black
#   Blue
#   Cyan
#   Green
#   LightBlack
#   LightBlue
#   LightCyan
#   LightGreen
#   LightMagenta
#   LightRed
#   LightWhite
#   LightYellow
#   Magenta
#   Red
#   Rgb(u8, u8, u8)
#   White
#   Yellow
# For more details, see https://docs.rs/termion/1.5.6/termion/color/index.html
[color]
dir_fg = "LightCyan"
file_fg = "LightWhite"
symlink_fg = "LightYellow"
```

### Command settings

For example, If you write

```
default = "nvim"

[exec]
feh = ["jpg", "jpeg", "png", "gif", "svg"]
zathura = ["pdf"]
```

then, .jpg, .jpeg, .png, .gif and .svg files are opened by `feh <file-name>`, .pdf files by `zathura <file-name>` and others by `nvim <file-name>` .
