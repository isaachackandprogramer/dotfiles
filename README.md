# DOTFILES 
Hello guys, I want to introduce the modified dotfiles that I modified. These I changed some packages so I'm going to present them to you.

*https://github.com/gh0stzk/dotfiles/tree/master/config/bspwm* → *Original dotfiles*

#

The files I changed:
## ./config/bspwm/bspwmrc
## ./config/bspwm/sxhkdrc
#
# ./config/bspwm/bspwmrc

```bash
───────┬────────────────────────────────────────────────────────────────────────────────────────
       │ File: bspwmrc
───────┼────────────────────────────────────────────────────────────────────────────────────────
   1   │ #!/usr/bin/env bash
   2   │ #
   3   │ #  ██████╗ ███████╗██████╗ ██╗    ██╗███╗   ███╗██████╗  ██████╗
   4   │ #  ██╔══██╗██╔════╝██╔══██╗██║    ██║████╗ ████║██╔══██╗██╔════╝
   5   │ #  ██████╔╝███████╗██████╔╝██║ █╗ ██║██╔████╔██║██████╔╝██║
   6   │ #  ██╔══██╗╚════██║██╔═══╝ ██║███╗██║██║╚██╔╝██║██╔══██╗██║
   7   │ #  ██████╔╝███████║██║     ╚███╔███╔╝██║ ╚═╝ ██║██║  ██║╚██████╗
   8   │ #  ╚═════╝ ╚══════╝╚═╝      ╚══╝╚══╝ ╚═╝     ╚═╝╚═╝  ╚═╝ ╚═════╝
   9   │ #   Author  -   gh0stzk
  10   │ #   Repo    -   https://github.com/gh0stzk/dotfiles
  11   │ #   Copyright (C) 2021-2024 gh0stzk <z0mbi3.zk@protonmail.com>
  12   │
  13   │ # Current rice
  14   │ read -r RICETHEME <"${HOME}"/.config/bspwm/.rice
  15   │
  16   │ # Set environment variables
  17   │ export PATH="$HOME/.config/bspwm/src:$PATH"
  18   │ export XDG_CURRENT_DESKTOP='bspwm'
  19   │ ## Fix java applications
  20   │ export _JAVA_AWT_WM_NONREPARENTING=1
  21   │
  22   │ # Default 1 monitor with 6 workspaces
  23   │ for monitor in $(xrandr -q | grep -w 'connected' | cut -d' ' -f1); do
  24   │   bspc monitor "$monitor" -d '1' '2' '3' '4' '5' '6'
  25   │ done
  26   │
  27   │ # Load configuration
  28   │ bspc config external_rules_command "${HOME}"/.config/bspwm/src/ExternalRules
  29   │ bspc config window_gap 6
  30   │ bspc config split_ratio 0.51
  31   │ bspc config single_monocle true
  32   │ bspc config borderless_monocle false
  33   │ bspc config gapless_monocle false
  34   │ bspc config focus_follows_pointer true
  35   │ bspc config pointer_follows_focus false
  36   │ bspc config pointer_motion_interval 5
  37   │ bspc config pointer_modifier mod4
  38   │ bspc config pointer_action1 move
  39   │ bspc config pointer_action2 resize_side
  40   │ bspc config pointer_action3 resize_corner
  41   │
  42   │ bspc rule -a scratch sticky=on state=floating focus=on
  43   │
  44   │ # Set system vars for polybar
  45   │ "$HOME"/.config/bspwm/src/SetSysVars
  46   │
  47   │ # Load current theme
  48   │ "${HOME}"/.config/bspwm/rices/"${RICETHEME}"/Theme.sh
  49   │
  50   │ # Launch sxhkd daemon
  51   │ pidof -q sxhkd || sxhkd -c "${HOME}"/.config/bspwm/sxhkdrc &
  52   │
  53   │ # Launch picom
  54   │ pidof -q picom || picom --config "${HOME}"/.config/bspwm/picom.conf &
  55   │
  56   │ # Launch eww daemon
  57   │ pidof -q eww || eww -c "${HOME}"/.config/bspwm/eww daemon &
  58   │
  59   │ # Launch clipboard daemon
  60   │ pidof -q greenclip || greenclip daemon &
  61   │
  62   │ # Launch polkit
  63   │ pidof -q polkit-gnome-authentication-agent-1 || /usr/lib/polkit-gnome/polkit-gnome-auth
       │ entication-agent-1 &
  64   │
  65   │ # Fix cursor
  66   │ xsetroot -cursor_name left_ptr
  67   │
  68   │ # End one time code
───────┴────────────────────────────────────────────────────────────────────────────────────────
```
#
# ./config/bspwm/sxhkdrc
```bash
───────┬──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       │ File: sxhkdrc
───────┼──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1   │ #  ███████╗██╗  ██╗██╗  ██╗██╗  ██╗██████╗ ██████╗  ██████╗
   2   │ #  ██╔════╝╚██╗██╔╝██║  ██║██║ ██╔╝██╔══██╗██╔══██╗██╔════╝
   3   │ #  ███████╗ ╚███╔╝ ███████║█████╔╝ ██║  ██║██████╔╝██║
   4   │ #  ╚════██║ ██╔██╗ ██╔══██║██╔═██╗ ██║  ██║██╔══██╗██║
   5   │ #  ███████║██╔╝ ██╗██║  ██║██║  ██╗██████╔╝██║  ██║╚██████╗
   6   │ #  ╚══════╝╚═╝  ╚═╝╚═╝  ╚═╝╚═╝  ╚═╝╚═════╝ ╚═╝  ╚═╝ ╚═════╝
   7   │ #   z0mbi3          https://github.com/gh0stzk/dotfiles
   8   │ #
   9   │
  10   │ # Show help
  11   │ F1
  12   │     OpenApps --KeyHelp
  13   │
  14   │ #|||----- Applications -----|||#
  15   │
  16   │ # Open Terminal (alacritty)
  17   │ super + Return
  18   │     OpenApps --terminal
  19   │
  20   │ # Open floating Terminal
  21   │ super + alt + Return
  22   │     OpenApps --floating
  23   │
  24   │ # Application menu
  25   │ super + @space
  26   │     OpenApps --menu
  27   │
  28   │ #####
  29   │
  30   │ # Apps (browser, editor, filemanager)
  31   │ shift + alt + {b,g,n}
  32   │     OpenApps {--browser,--editor,--filemanager}
  33   │
  34   │ # Terminal apps (ranger, nvim, ncmpcpp)
  35   │ shift + alt + {r,v,k}
  36   │     OpenApps {--ranger,--nvim,--music}
  37   │
  38   │ # Pavucontrol
  39   │ shift + alt + p
  40   │     OpenApps --soundcontrol
  41   │
  42   │
  43   │ #|||----- System Keybindings -----|||#
  44   │
  45   │ # Theme Selector
  46   │ alt + @space
  47   │     RiceSelector
  48   │
  49   │ #Terminal Selector
  50   │ super + alt + t
  51   │     Term --selecterm
  52   │
  53   │ # jgmenu
  54   │ ~button3
  55   │   xqp 0 $(xdo id -N Bspwm -n root) && jgmenu --csv-file=~/.config/bspwm/src/jgmenu/menu.txt --config-file=~/.config/bspwm/jgmenurc
  56   │
  57   │ # Scratchpad
  58   │ super + alt + o
  59   │     tdrop -a -w 70% -h 35% -y 0 -x 15%  --class scratch alacritty --class=scratch
  60   │
  61   │ # Power off, Reboot, Log out, Lockscreen, kill an app
  62   │ ctrl + super + alt + {p,r,q,l,k}
  63   │     {systemctl poweroff, systemctl reboot,bspc quit,physlock -d,xkill}
  64   │
  65   │ # Hide/Show Bar (Polybar and/or eww)
  66   │ super + alt + {h,u}
  67   │     HideBar {-h,-u}
  68   │
  69   │ # Change transparency on focused window
  70   │ ctrl + alt + {plus,minus,t}
  71   │     picom-trans {-c -o +3,-c -o -1,-c -d}
  72   │
  73   │ # Random wallpaper
  74   │ super + alt + w
  75   │     WallSelect
  76   │
  77   │ # Mount Android phones
  78   │ super + alt + a
  79   │     OpenApps --android
  80   │
  81   │ # Network Manager
  82   │ super + alt + n
  83   │     OpenApps --netmanager
  84   │
  85   │ # Clipboard
  86   │ super + alt + c
  87   │     OpenApps --clipboard
  88   │
  89   │ # Screenshot
  90   │ super + alt + s
  91   │     OpenApps --screenshot
  92   │
  93   │ # Bluetooth
  94   │ super + alt + b
  95   │     OpenApps --bluetooth
  96   │
  97   │ # PowerMenu
  98   │ super + alt + p
  99   │     OpenApps --powermenu
 100   │
 101   │ # Manage brightness
 102   │ XF86MonBrightness{Up,Down}
 103   │     sh Brightness {up,down}
 104   │
 105   │ # Volume control
 106   │ XF86Audio{RaiseVolume,LowerVolume,Mute}
 107   │     Volume{ --inc, --dec, --toggle}
 108   │
 109   │ # Music Control
 110   │ XF86Audio{Next,Prev,Play,Stop}
 111   │     MediaControl {--next,--previous,--toggle,--stop}
 112   │
 113   │
 114   │ #|||----- Bspwm hotkeys -----|||#
 115   │
 116   │ # Reload BSPWM
 117   │ super + alt + r
 118   │     bspc wm -r
 119   │
 120   │ # close and kill
 121   │ super + {_,shift + }q
 122   │     bspc node -{c,k}
 123   │
 124   │ # Reload Keybindings
 125   │ super + Escape
 126   │     pkill -USR1 -x sxhkd; dunstify -u low -i ~/.config/bspwm/assets/reload.svg 'sxhkd' 'The configuration file has been reloaded successfully!'
 127   │
 128   │ #####
 129   │
 130   │ # alternate between the tiled and monocle layout
 131   │ super + m
 132   │     bspc desktop -l next
 133   │
 134   │ # set the window state
 135   │ super + {t,shift + t,s,f}
 136   │     bspc node -t {tiled,pseudo_tiled,floating,fullscreen}
 137   │
 138   │ # set the node flags
 139   │ ctrl + alt {m,x,s,p}
 140   │     bspc node -g {marked,locked,sticky,private}
 141   │
 142   │ # Hide/Unhide Window
 143   │ ctrl + alt + h
 144   │     BspHideNode
 145   │
 146   │ #####
 147   │
 148   │ # rotate desktop
 149   │ super + r
 150   │     bspc node @/ --rotate {90,-90}
 151   │
 152   │ # Change focus of the Node or Swap Nodes
 153   │ shift + super {_,ctrl + }{Left,Down,Up,Right}
 154   │     bspc node -{f,s} {west,south,north,east}
 155   │
 156   │ # Switch workspace
 157   │ super + {Left,Right}
 158   │     bspc desktop -f {prev,next}.local
 159   │
 160   │ # focus or send to the given desktop
 161   │ super + {_,alt + }{1-9,0}
 162   │     bspc {desktop -f,node -d} '^{1-9,10}'
 163   │
 164   │ # Send focused Node to workspace directionally
 165   │ super + alt + {Left,Right}
 166   │     bspc node -d {prev,next} '--follow'
 167   │
 168   │ # focus the last node/desktop
 169   │ super + {comma,Tab}
 170   │     bspc {node,desktop} -f last
 171   │
 172   │ #####
 173   │
 174   │ # preselect the direction
 175   │ super + {h,j,k,l}
 176   │     bspc node -p {west,south,north,east}
 177   │
 178   │ # cancel the preselection for the focused node
 179   │ super + alt + space
 180   │     bspc node -p cancel
 181   │
 182   │ #####
 183   │
 184   │ # expand a window
 185   │ ctrl + alt {Left,Down,Up,Right}
 186   │     bspc node -z {left -10 0,bottom 0 10,top 0 -10,right 10 0}
 187   │
 188   │ # contract a window
 189   │ ctrl + shift + alt + {Left,Down,Up,Right}
 190   │     bspc node -z {right -10 0,top 0 10,bottom 0 -10,left 10 0}
 191   │
 192   │ # move a floating window
 193   │ alt + shift {Left,Down,Up,Right}
 194   │     bspc node -v {-10 0,0 10,0 -10,10 0}
───────┴──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
```
#

# warning

*You should install the dotfiles mentioned above and then make those changes*
#

# CREDITS : 

## https://github.com/gh0stzk → Dotfile Creator Used
