name: title_inversed_whiteText
layout: false
class: center, middle

##Tmux + TMuxinator
![](/static/images.2016-Nov-16_GrenobleFLOSS_Tmux/logo-tmux.svg)
###Grenoble FLOSS Meetup, 16 Nov 2016
<h3> Mike Bright, <img src="/static/images.2016-Nov-16_GrenobleFLOSS_Tmux/Twitter_Bird.svg" width=24 /> @mjbright </h3>

.left[.footnote[.vlightgray[ @mjbright ]]]

???
SpeakerNotes:

Introduce ourselves.

Why this presentation?

---
name: section_overview
layout: false
class: center, left
## TMux + TMuxinator
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

.left[

- What is Tmux
- Related tools
- Using tmux
  - invoking from command-line
  - key-bindings
  - the Status bar
  - tmux command prompt
  - Configuration
- Extensions
  - Plugins
  - Tools and session management: Tmuxinator
-  GNU Screen
-  Byobu
-  Resources
]

.left[.footnote[.vlightgray[ @mjbright ]]]

---
name: section_history
layout: false
class: center, left
## .blue[Tmux: A terminal multiplexer]
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

.left[
This means
- you can detach from a tmux terminal session
- you can reattach, or attach from multiple places

Like *VNC* or *Remote Desktop* for terminal sessions

Lost connection to a remote server running your tmux session ?

Your work is not lost, programs continue to run
- just reconnect
    - ssh to the server
    - to see running tmux sessions: ```tmux ls```
    - attach to a session: ```tmux a -t <session>```

]
.left[.footnote[.vlightgray[ @mjbright ]]]

<!-- ![]( /static/images.2016-Nov-16_GrenobleFLOSS_Tmux/tmux0_session.gif) -->
<!-- <img src="/static/images.2016-Nov-16_GrenobleFLOSS_Tmux/tmux0_session.gif" width=400/> -->


???
SpeakerNotes:

No need I'm sure to remind you of Docker's meteoric rise since it's announcement in March 2013.

Although containers existed for quite some time before in various Unices ad Linux (LXC), Docker
popularized the technology by making containers so easy to use and share.

---
name: section_more
layout: false
class: center, left
## .blue[But **tmux** is so much more ...]
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

![](/static/images.2016-Nov-16_GrenobleFLOSS_Tmux/tmux-sessions-windows-panes-01.svg)

Use `tmux ls` to see currently running sessions

.left[.footnote[.vlightgray[ @mjbright ]]]

---
name: section_history
layout: false
class: center, left
## .blue[Related tools ...]
<!-- .red[ TEST ]  .blue[TEST]  .green[TEST]  .yellow[TEST]  .magenta[TEST]  .cyan[TEST]  .pink[TEST] -->

.left[

<br/> <br/> <br/> <br/> 

- tmux | : | started in 2011, very active
-|-|-|--
- GNU screen | : | much older, has many similar features
<img src="/static/images.2016-Nov-16_GrenobleFLOSS_Tmux/gnu-screen.png" />
 - Byobu | : | Orginally a wrapper around screen, now tmux is its default
 - tmuxinator | : | Ruby gem for complex tmux layouts

]

.left[.footnote[.vlightgray[ @mjbright ]]]

---
name: section_tmux_basic_commands
layout: false
class: center, left

## Basics - Invoking tmux from command-line
.left[
#### Some tmux commands

Command  | |
-|-|-|--
`tmux ls` | : | List currently running sessions
`tmux new` | : | Create a new session
`tmux new -n <session>` | : | Create a named session
`tmux attach` | : | Attached to last active session
`tmux attach -t <session> ` | : | Attached to selected target (e.g. session)
`tmux kill-session -t <session> ` | : | Deleted selected session (careful !)

#### Some tmux options

Option  | |
-|-|-|--
`-f <conf>` | : | Specify alternative user conf file (else ~/.tmux.conf)
`-L <socket-name>` | : | filename of server socket under TMUX_TMPDIR
`-S <socket-path>` | : | filepath of server socket 
`-v              ` | : | Verbose logging to tmux-client-PID.log
`-V              ` | : | Show tmux version

]
.left[.footnote[.vlightgray[ @mjbright ]]]

---
layout: false
class: center, left

## Basics - Key bindings within tmux: Sessions
.left[
Once attached to a tmux session, the session can be controlled by key combinations starting with a prefix 'C-b' (ctrl-B) by default.

Binding (C-b + ...) | |
-|-|-|--
? | : | Help !!
$ | : | Rename the current session (as seen by  'tmux ls')
d | : | Detach from the current session
C-z | : | Suspend the tmux client
f | : | Search for window containing text !
&lt;Space&gt; | : | Apply next layout

]

.left[.footnote[.vlightgray[ @mjbright ]]]

---
layout: false
class: center, left

## Basics - Key bindings within tmux: Windows
.left[
Once attached to a tmux session, the session can be controlled by key combinations starting with a prefix 'C-b' (ctrl-B) by default.

Binding (C-b + ...) | |
-|-|-|--
, | : | Rename the current window
c | : | Create and move to a new window
n | : | move to the next window
p | : | move to the previous window
l | : | move to the last visited window
i | : | show info about the current window
[0-9a-z] | : | Go to specfied window


]

.left[.footnote[.vlightgray[ @mjbright ]]]

---
layout: false
class: center, left

## Basics - More Key bindings within tmux: Panes

.left[

Binding (C-b + ...) | |
-|-|-|--
z | : | Show current pane as full-screen (C-z to exit)
&quot; | : | Split the current pane vertically
&#37; | : | Split the current pane horizontally
&#91; | : | Go into copy mode, allows to scroll in pane (C-c to exit)
o | : | Cycle through panes in current window
q | : | *Briefly* display pane numbers
x | : | Kill the current pane
&#33; | : | Break current pane out of window into a new one

]
.left[.footnote[.vlightgray[ @mjbright ]]]

---
layout: false
class: center, left

## Basics - The tmux status bar

.left[

The status bar shows *customizable* information about the current session

By default this displays
- current user, ip address, session-name ('0' below)
- A list of window-names (current-*, with current command)

![](/static/images.2016-Nov-16_GrenobleFLOSS_Tmux/tmux_statusbar_default_left.png)
![](/static/images.2016-Nov-16_GrenobleFLOSS_Tmux/tmux_statusbar_default_right.png)


Through tmux.conf (see later) we can customize as we wish, for example:

![](/static/images.2016-Nov-16_GrenobleFLOSS_Tmux/tmux_status_left.png)
![](/static/images.2016-Nov-16_GrenobleFLOSS_Tmux/tmux_status_right.png)

Note that if a window is in full-screen mode then 'Z' is appended to that window name

![](/static/images.2016-Nov-16_GrenobleFLOSS_Tmux/tmux_status_left_Z.png)

]
.left[.footnote[.vlightgray[ @mjbright ]]]


---
layout: false
class: center, left

## More - Key bindings within tmux

.left[

Binding (C-b + ...) | |
-|-|-|--
s | : | Select a new session for the current client (change session)
t | : | Show the current time
w | : | Choose a window
m | : | Mark the current pane (select-pane -m)
M | : | Unmark the current pane
{ | : | Swap the current pane with the previous pane
} | : | Swap the current pane with the next pane



]
.left[.footnote[.vlightgray[ @mjbright ]]]

---
layout: false
class: center, left

## More - Using the tmux command prompt

.left[

Binding (C-b + ...) | |
-|-|-|--
:setw synchronize-panes | : | Send keyboard input simultaneous to all panes of current window

]
.left[.footnote[.vlightgray[ @mjbright ]]]

---
layout: false
class: center, left

## Configuration - The tmux.conf file (1)

.left[
There are a set of tmux commands accessible through
``` ctrl-B : ``` which can also be used in a config file (default ~/.tmux.conf) to
set tmux default behaviours as you wish.

<pre>
# Set Ctrl-b r as shortcut to reload this config:
bind r source-file ~/.tmux.conf

# Rename terminals:
set -g set-titles on
set -g set-titles-string '^#(whoami::#h::#(curl ipecho.net/plain;echo)'

# Status bar custo:
#set -g status-utf8 on
set -g status-bg blue
set -g status-fg white
set -g status-interval 5
set -g status-left-length 90
set -g status-right-length 60
set -g status-left "#[fg=Green]#(whoami)#[fg=white]::#[fg=blue] \
    #(hostname - s)#[fg=white]::##[fg=yellow]#(curl ipecho.net/plain;echo)"

set -g status-justify left
set -g status-right '#[fg=Cyan]#S #[fg=white]%a %d %b %R'

</pre>

]
.left[.footnote[.vlightgray[ @mjbright ]]]

---
layout: false
class: center, left

## Configuration - The tmux.conf file (2)

.left[

#### use ctrl-b arrows - Pane navigation with vim-bindings:
```
unbind-key j;    bind-key j select-pane -D
unbind-key k;    bind-key k select-pane -U
unbind-key h;    bind-key h select-pane -L
unbind-key l;    bind-key l select-pane -R
```

]
.left[.footnote[.vlightgray[ @mjbright ]]]
---
layout: false
class: center, left

## Plugins
.left[

<a href="https://github.com/tmux-plugins"> tmux-plugins </a> Official tmux plugins

]
.left[.footnote[.vlightgray[ @mjbright ]]]

---
layout: false
class: center, left

## Tools and session management
.left[

Tools | |
-|-|-|--
powerline | Statusline plugin for vim, and provides statuslines and prompts for several other applications including tmux
tmux-cssh | TMUX with a "ClusterSSH"-like behaviour
tmuxifier | Tmuxify your Tmux. Powerful session, window & pane management for Tmux.
<a href="https://github.com/tmuxinator/tmuxinator">tmuxinator</a> | Manage complex tmux sessions easily
tmuxomatic | Intelligent tmux session management
tmuxp | tmux session manager and python library

]
.left[.footnote[.vlightgray[ @mjbright ]]]

---
layout: false
class: center, left

## Tools and session management: Tmuxinator
.left[

Tmuxinator allows to easily manage complex tmux sessions with multiple windows, panes with a specified layout all specified in a YAML file:


```yaml
project_name: 8panes
windows:
  - shell:
      layout: a506,379x84,0,0{125x84,0,0[125x26,0,0,4,125x31,0,27,83,125x25,0,59,82],125x84,126,0[125x42,
126,0,79,125x41,126,43,86],127x84,252,0[127x27,252,0,80,127x30,252,28,84,127x25,252,59,85]}
      panes:
        - banner pane1
        - banner pane2
        - banner pane3
        - banner pane4
        - banner pane5
        - banner pane6
        - banner pane7
        - banner pane8
```

]
.left[.footnote[.vlightgray[ @mjbright ]]]

---
layout: false
class: center, left

## Tools and session management: Tmuxinator-2
.left[

```yaml
windows:
  - work:
      layout: tiled
      panes:
         - messages:
            - exec ~/z/bin/Deployed/ssh_tunnel_b10.sh work
            - sudo tail -f /var/log/messages
         - shell:
            - exec ~/z/bin/Deployed/ssh_tunnel_b10.sh work
         - exec ~/z/bin/Deployed/ssh_tunnel_b10.sh work
  - b1machines:
      layout: tiled
      panes:
        - b0g1_logs:
          - exec ~/z/bin/Deployed/ssh_tunnel_b10.sh b0g1
          - banner $(hostname)
          - uptime; ip a | grep 10.3.222
          - cd /var/log
          - sudo tail -f syslog
        - b1g1_logs:
          - exec ~/z/bin/Deployed/ssh_tunnel_b10.sh b1g1
          - banner $(hostname)
          - uptime; ip a | grep 10.3.222
        - b2g1_machines:
          - exec ~/z/bin/Deployed/ssh_tunnel_b10.sh b2g1
          - banner $(hostname)
          - uptime; ip a | grep 10.3.222
          - watch docker-machine ls
        - b3g1_machines:
          - exec ~/z/bin/Deployed/ssh_tunnel_b10.sh b3g1
          - banner $(hostname)
          - uptime; ip a | grep 10.3.222
```

]
.left[.footnote[.vlightgray[ @mjbright ]]]

---
layout: false
class: center, left

## Tools and session management: Tmuxinator-3
.left[

```yaml
name: perfs
root: ~/
windows:
  - perfs:
      layout: main-horizontal
      root: ~/tmp
      panes:
        - htop: htop
        - sensors: ~/z/bin/Deployed/perf_monitor_CPUtrend.sh

```

]
.left[.footnote[.vlightgray[ @mjbright ]]]

---
layout: false
class: center, left

## GNU Screen
.left[
<img src="/static/images.2016-Nov-16_GrenobleFLOSS_Tmux/gnu-screen.png" />
https://www.gnu.org/software/screen/

Screen is a full-screen window manager that multiplexes a physical terminal between several processes, typically interactive shells.

Whilst tmux is a more active project Screen already has many of the same features, such as:
- session continues in detached mode when no client is connected
- has a prefix key for entering commands
  - It uses Ctrl+A though (tmux chose to be different)
- multiple windows
- ability to list windows or create them on the fly, switch windows
- ability to split windows horizontally or vertically
- ...

If GNU Screen works for you ... keep it ...
]
.left[.footnote[.vlightgray[ @mjbright ]]]

---
layout: false
class: center, left

## Byobu
.left[
<img src="/static/images.2016-Nov-16_GrenobleFLOSS_Tmux/byobu-logo.png" />
http://byobu.co/

Byobu is a GPLv3 open source text-based window manager and terminal multiplexer.

It was originally designed to provide elegant enhancements to the otherwise functional, plain, practical GNU Screen, for the Ubuntu server distribution.

Byobu now includes an enhanced profiles, convenient keybindings, configuration utilities, and toggle-able system status notifications for both the GNU Screen window manager and the more modern Tmux terminal multiplexer, and works on most Linux, BSD, and Mac distributions.

]
.left[.footnote[.vlightgray[ @mjbright ]]]

---
layout: false
class: center, left

## Resources
.left[

Tmux
  - home page https://tmux.github.io/
  - source https://github.com/tmux/tmux
  - awesome-tmux : <a href="https://github.com/rothgar/awesome-tmux"> awesome-tmux </a> 
  - Official tmux-plugins : <a href="https://github.com/tmux-plugins"> tmux-plugins </a>

TMuxinator : https://github.com/tmuxinator/tmuxinator

GNU Screen : https://www.gnu.org/software/screen/

Byobu : http://byobu.co/



]
.left[.footnote[.vlightgray[ @mjbright ]]]

