<p align="center">
  <img src="/reflex.png" title="reflex-curses"/>
</p>

- [Description](#desc)
- [Changes](#changes)
- [Dependencies](#depend)
  - [Python](#python_dep)
  - [External](#ext_dep)
  - [Optional](#opt_dep)
- [Install](#install)
  - [Setuptools](#install_st)
  - [Manual](#install_manual)
- [Usage](#usage)
- [Default Keybinds](#def_keys)
  - [Page Navigation](#page_keys)
  - [Swap Views](#view_keys)
  - [Search](#search_keys)
  - [Quality Select](#quality_keys)
  - [Follow List](#follow_keys)
  - [Misc List](#misc_keys)
- [Configuration](#config)
  - [Config File](#conf_file)
  - [Followed List Import](#follow_import)


<a id="desc"></a>

# Description

Reflex-Curses is a TUI/CLI wrapper around streamlink, allowing for easy launching
of twitch.tv streams from your terminal.

Fork of [twitch-curses](https://gitlab.com/corbie/twitch-curses) with added features.

<a id="changes"></a>

# Changes

-   Rewritten with classes
-   Launch multiple streams at once
-   Stream process no longer tied to terminal (setsid)
-   Launch chat for selected stream (browser/weechat/irssi)
-   Copy channel URL to clipboard (xclip)
-   Locally follow channels (No account needed) (+Imports from file/twitch user)
-   Custom Config File
-   VOD Support
-   Search by game name
-   Top streams view
-   Language filter (Game search only)
-   Vim like keybinds
-   Updated to Twitch v5 API
-   Color support
-   Fixed crashing with super small terminal resizing
-   Run one off cli commands 


<a id="depend"></a>

# Dependencies


<a id="python_dep"></a>

## Python

-   Python 3.6
-   python-requests


<a id="ext_dep"></a>

## External

-   streamlink (launching streams)
-   mpv (default player)
-   xclip (clipboard support)
-   urxvt (default terminal)
-   setsid (detach player from terminal)


<a id="opt_dep"></a>

## Optional

-   firefox (default browser)
-   weechat / irssi (chat)


<a id="install"></a>

# Installation

<a id="install_st"></a>

## Setuptools

System: `python setup.py install`

User: `python setup.py install --user`

<a id="install_manual"></a>

## Manual

`sudo make install`

<a id="usage"></a>

# Usage

```
reflex-curses [OPTION]

OPTIONS
       NONE   Starts up the tui interface

       -a channel_name
              Add a twitch channel to your followed list

       -d channel_name
              Delete a twitch channel from your followed list

       -h, --help
              Print help message

       -f     Prints out any followed streams that are online.

       -i channel_name (--overwrite)
              Import channels followed by channel_name into your followed list.
              Default is to append to your current followed list, add --overwrite to replace it.
              NOTE: Currently limited to the results_limit (default: 75), large lists might not fully import.
```

An example dmenu script is [Here](./scripts/dmenu_streams.sh)

<a id="def_keys"></a>

# Default Keybinds

<a id="page_keys"></a>
## Page Navigation
| Key       | Description                               |
|---------  |-----------------------------------------  |
| h         | Go back                                   |
| j         | Move cursor down                          |
| k         | Move cursor up                            |
| l / Enter | Enter menu or launch stream               |
| n         | Next Page                                 |
| p         | Previous page                             |
| r         | Refresh last query                        |

<a id="view_keys"></a>
## Swap Views
| Key       | Description                               |
|---------  |-----------------------------------------  |
| f         | Go to followed view                       |
| s         | Go to top streams view                    |
| t         | Go to top games view                      |
| v         | Go to VOD view                            |

<a id="search_keys"></a>
## Search
| Key       | Description                               |
|---------  |-----------------------------------------  |
| /         | General Search                            |
| g         | Search by Game Name (exact)               |


<a id="quality_keys"></a>
## Quality Selection
| Key       | Description                               |
|---------  |-----------------------------------------  |
| -         | Decrease quality                          |
| =         | Increase quality                          |


<a id="follow_keys"></a>
## Follow List
| Key       | Description                               |
|---------  |-----------------------------------------  |
| a         | Add channel follow / Show all followed    |
| d         | Delete channel from followed list         |
| i         | Import follows from twitch user (limited) |
| o         | Show only online streams in followed list |

<a id="misc_keys"></a>
## Misc
| Key       | Description                               |
|---------  |-----------------------------------------  |
| c         | Open chat with chat method                |
| y         | Yank channel url                          |
| q         | Quit                                      |


<a id="config"></a>

# Configuration

Configuration files are stored in `~/.config/reflex-curses`


<a id="conf_file"></a>

## Config File

Config file is stored in `~/.config/reflex-curses/config`

Default Config Example:

```
[keys]
add = a
chat = c
delete = d
followed = f
game = g
back = h
down = j
up = k
forward = l
online = o
quit = q
refresh = r
t_stream = s
t_game = t
search = /
vods = v
yank = y
page+ = n
page- = p
qual+ = =
qual- = -

[exec]
browser = firefox
browser_flag = --new-window
chat_method = browser
player = mpv
term = urxvt
term_flag = -e

[twitch]
client_id = caozjg12y6hjop39wx996mxn585yqyk
lang = 
results_limit = 75
retry_limit = 3

[ui]
default_state = games
hl_color = blue
l_win_color = white
r_win_color = green
quality = best
show_borders = True
show_keys = True

[irc]
address = irc.chat.twitch.tv
network = reflex
port = 6697
```


<a id="follow_import"></a>

## Followed List Import

In addition to the -i flag, reflex-curses can also mass import a list of channel names from a file.

Place entries (one per line) in `~/.config/reflex-curses/followed`

Reflex-Curses will resolve the Channel IDs on startup.
