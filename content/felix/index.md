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

A tui file manager with Vim-like key mapping, written in Rust.  
Fast, simple, and easy to configure & use.

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

## v2.2.2 (2022-12-19)

### Fixed

- Disable commands with Ctrl or other modifiers unless explicitly implemented. (For now, `Ctrl + r` to redo, `Alt + j` and `Alt + k` to scroll the preview text are implemented) This avoids for example the situation where `Ctrl + d` unintentionally deletes an item.
- Add `create_dir_all` to `config_dir` and `data_local_dir` to avoid error.
- Check if the argument is directory.

## v2.2.1 (2022-12-15)

### Fixed

- Fix the compilation on NetBSD.

## v2.2.0 (2022-12-12)

### Changed

- **IMPORTANT**: Trash and log directory path changed.
  - from v2.2.0, felix will use `dirs::data_local_dir()` to store the deleted items and log files, instead of `dirs::config_dir()`.
  - Due to this change, the path for linux will be `$XDG_DATA_HOME/felix/{Trash, log}`, in most case `/home/user/.local/share/felix/{Trash, log}`. For Windows `{FOLDERID_LocalAppData}\felix\{Trash, log}`, typically `C:\Users\user\AppData\Local\felix\{Trash, log}`. No change for macOS users.
  - Note that config file path is unchanged for any OS!
  - Please don't forget deleting old trash diretory and log files if you don't want them anymore.
- Refactoring overall.

### Added

- `:trash` to go to the trash directory.

### Fixed

- Support NetBSD to open file in a new window.
- Properly remove broken symlink in Windows as well. Also, when deleting/puttiing a directory, broken symlink(s) in it won't cause any error and will be removed from the file system after deleting/putting.

For more details, see `CHANGELOG.md` in the [repository](https://github.com/kyoheiu/felix).

<a id="get-started"></a>

## Get Started

<a id="status"></a>

### Status

| OS      | Status               |
| ------- | -------------------- |
| Linux   | works                |
| NetBSD  | works                |
| MacOS   | works                |
| Windows | not fully tested yet |

_For Windows users: From v1.3.0, it can be at least compiled on Windows (see `.github/workflows/install_test.yml`.) If you're interested, Please try the native build and report any problems._

MSRV(Minimum Supported rustc Version): **1.60.0**

<a id="installation"></a>

### Installation

### Prerequisites

- Make sure that `gcc` is installed.
- MSRV(Minimum Supported rustc Version): **1.60.0**

Update Rust if rustc < 1.60:

```
rustup update
```

#### From crates.io

```
cargo install felix
```

#### Arch Linux

```
pacman -S felix-rs
```

*The launcher binary name is `felix` via pacman.  
Alias fx='felix' if you want, as this document (and other installations) uses `fx`.*

#### NetBSD

Package is available from the official repositories:

```
pkgin install felix
```

#### From repository

```
git clone https://github.com/kyoheiu/felix.git
cd felix
cargo install --path .
```

<a id="integrations"></a>

### Integrations

In addition, you can use felix more conveniently by installing the following two apps:

- [zoxide](https://github.com/ajeetdsouza/zoxide): A smarter `cd` command, which enables you to jump to a directory that matches the keyword in felix.
- [chafa](https://hpjansson.org/chafa/): Terminal graphics for the 21st century, by which you can preview images in felix. **_chafa must be v1.10.0 or later._**

These apps do not need any configuration to use with felix!

<a id="usage"></a>

## Usage

*If you install this app via pacman, the default binary name is `felix`.*

| command               |                                                               |
| --------------------- | ------------------------------------------------------------- |
| `fx`                  | Show items in the current directory.                          |
| `fx <directory path>` | Show items in the path. Both relative and absolute available. |

| option             |                                                      |
| ------------------ | ---------------------------------------------------- |
| `-l` / `--log`     | Launch the app, automatically generating a log file. |
| `-v` / `--version` | Print the current version and check update.          |
| `-h` / `--help`    | Print help.                                          |

<a id="key-manual"></a>

## Key Manual

<a id="move"></a>

### Move cursor / Change directory

| Key                      | Explanation                                                                                                                                                                                                                                                                    |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| j / Down                 | Go up. If the list exceeds max-row, it "scrolls" before the top of the list.                                                                                                                                                                                                   |
| k / Up                   | Go down. If the list exceeds max-row, it "scrolls" before the bottom of the list.                                                                                                                                                                                              |
| h / Left                 | Go to the parent directory if exists.                                                                                                                                                                                                                                          |
| l / Right / Enter        | Open a file or change the directory. Commands for the execution can be managed in the config file.                                                                                                                                                                             |
| gg                       | Go to the top.                                                                                                                                                                                                                                                                 |
| G                        | Go to the bottom.                                                                                                                                                                                                                                                              |
| z + Enter                | Go to the home directory.                                                                                                                                                                                                                                                      |
| z \<keyword\> + Enter    | **_This command requires zoxide installed._** Jump to a directory that matches the keyword. Internally, felix calls [`zoxide query <keyword>`](https://man.archlinux.org/man/zoxide-query.1.en), so if the keyword does not match the zoxide database, this command will fail. |
| :cd + Enter / :z + Enter | Go to the home directory.                                                                                                                                                                                                                                                      |
| :z \<keyword\> + Enter   | Same as `z <keyword>`.                                                                                                                                                                                                                                                         |
| :trash + Enter           | Go to the trash directory.                                                                                                                                                                                                                                                     |

<a id="open"></a>

### Open a file

| Key               | Explanation                                                                                                                                                                                                                   |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| l / Right / Enter | Open a file or change the directory. Commands for the execution can be managed in the config file.                                                                                                                            |
| o                 | Open a file in a new window. This enables you to use felix while working with the file. Works only if `exec` is set in the config file and the extension of the item matches one of the value.                                |
| e                 | Extract archived/compressed file to the current directory. Supported types: `tar.gz`(Gzip), `tar.xz`(lzma), `tar.zst`(Zstandard & tar), `zst`(Zstandard), `tar`, zip file format and formats based on it(`zip`, `docx`, ...). |

<a id="manage"></a>

### Manage items

| Key             | Explanation                                                                                                                                                    |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| dd              | Delete and yank one item, which will go to the trash directory.                                                                                                |
| yy              | Yank one item. If you yanked other item(s) before, it's replaced by this one.                                                                                  |
| p               | Put yanked item(s) in the current directory. If the item with same name exists, copied item will be renamed with the suffix `\_{count}`, such as `test_1.txt`. |
| c               | Switch to the rename mode (enter the new name and press Enter to rename the item).                                                                             |
| V               | Switch to the select mode, where you can move cursor to select items.                                                                                          |
| d (select mode) | Delete and yank selected items, and return to the normal mode.                                                                                                 |
| y (select mode) | Yank selected items, and return to the normal mode.                                                                                                            |
| u               | Undo put/delete/rename.                                                                                                                                        |
| Ctrl + r        | Redo put/delete/rename.                                                                                                                                        |

<a id="view"></a>

### Change the view, search and others

| Key             | Explanation                                                                                                                                                                                               |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| v               | Toggle whether to show the item preview (text, image, or the contents tree) on the right half of the terminal. **_You must install [`chafa`](https://hpjansson.org/chafa/) in order to preview images._** |
| Alt + j / Down  | Scroll down the preview text.                                                                                                                                                                             |
| Alt + k / Up    | Scroll up the preview text.                                                                                                                                                                               |
| s               | Toggle between vertical / horizontal split in the preview mode.                                                                                                                                           |
| backspace       | Toggle whether to show hidden items or not. This change remains after exit (stored in `.session`).                                                                                                        |
| t               | Toggle sort order (by name <-> by modified time). This change remains after exit (same as above).                                                                                                         |
| /               | Search items by the keyword.                                                                                                                                                                              |
| n               | Go forward to the item that matches the keyword.                                                                                                                                                          |
| N               | Go backward to the item that matches the keyword.                                                                                                                                                         |
| :               | Switch to the shell mode. Type command and press Enter to execute it. You can use any command in the displayed directory, but some commands may fail, and the display may collapse during execution.      |
| :e + Enter      | Reload the current directory. Useful when something goes wrong.                                                                                                                                           |
| :empty + Enter  | Empty the trash directory. **Please think twice to use this.**                                                                                                                                            |
| :h + Enter      | Show help. (scrolls by `j/k` or `Up/Down`)                                                                                                                                                                |
| Esc             | Return to the normal mode.                                                                                                                                                                                |
| :q + Enter / ZZ | Exit.                                                                                                                                                                                                     |

Note that items moved to the trash directory are prefixed with Unix time (like `1633843993`) to avoid the name conflict. This prefix will be removed when put.

<a id="configuration"></a>

## Configuration

### Linux

```
config file     : $XDG_CONFIG_HOME/felix/config.yaml
trash directory : $XDG_DATA_HOME/felix/Trash
log files       : $XDG_DATA_HOME/felix/log
```

### macOS

```
config file     : $HOME/Library/Application Support/felix/config.yaml
trash directory : $HOME/Library/Application Support/felix/Trash
log files       : $HOME/Library/Application Support/felix/log
```

### Windows

```
config file     : $PROFILE\AppData\Roaming\felix\config.yaml
trash directory : $PROFILE\AppData\Local\felix\Trash
log files       : $PROFILE\AppData\Local\felix\log
```

_All 3 items above will be automatically created._

Default config.yaml:

```
# (Optional)
# Default exec command when opening file.
# If not set, will default to $EDITOR.
# default: nvim

# (Optional)
# key (the command you want to use when opening file): [values] (extensions)
# exec:
#   feh:
#     [jpg, jpeg, png, gif, svg]
#   zathura:
#     [pdf]

# (Optional)
# Whether to use syntax highlighting in the preview mode.
# If not set, will default to false.
# syntax_highlight: true

# (Optional)
# Default theme for syntax highlighting.
# Pick one from the following:
#    Base16OceanDark
#    Base16EightiesDark
#    Base16MochaDark
#    Base16OceanLight
#    InspiredGitHub
#    SolarizedDark
#    SolarizedLight
# If not set, will default to "Base16OceanDark".
# default_theme: Base16EightiesDark

# (Optional)
# Path to .tmtheme file for the syntax highlighting.
# If not set, default_theme will be used.
# theme_path: "/home/kyohei/.config/felix/monokai.tmtheme"

# The foreground color of directory, file and symlink.
# Pick one of the following:
#     Black            // 0
#     Red              // 1
#     Green            // 2
#     Yellow           // 3
#     Blue             // 4
#     Magenta          // 5
#     Cyan             // 6
#     White            // 7
#     LightBlack       // 8
#     LightRed         // 9
#     LightGreen       // 10
#     LightYellow      // 11
#     LightBlue        // 12
#     LightMagenta     // 13
#     LightCyan        // 14
#     LightWhite       // 15
#     Rgb(u8, u8, u8)
#     AnsiValue(u8)
# For more details, see https://docs.rs/termion/1.5.6/termion/color/index.html
color:
  dir_fg: LightCyan
  file_fg: LightWhite
  symlink_fg: LightYellow
```

### Command settings

For example, If you write

```
default: nvim

exec:
  feh:
    [jpg, jpeg, png, gif, svg]
  zathura:
    [pdf]
```

then, `.jpg`, `.jpeg`, `.png`, `.gif` and `.svg` files are opened by `feh <file-name>`, `.pdf` files by `zathura <file-name>` and others by `nvim <file-name>` .
