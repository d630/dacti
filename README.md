##### README

[dacti](https://github.com/D630/dacti) is a simple menu driven run or raise bash shell script. By default, dacti works with [dmenu](http://tools.suckless.org/dmenu/) and [wmctrl](https://sites.google.com/site/tstyblo/wmctrl/), but you may [configure](../master/doc/examples/dactirc) and use your preferred tools.

![](https://raw.githubusercontent.com/D630/dacti/master/doc/dacti.png)

(Terminus 16)

##### BUGS & REQUESTS

Please feel free to open an issue or put in a pull request on https://github.com/D630/dacti

##### GIT

To download the very latest source code:

```
git clone https://github.com/D630/dacti
```

In order to use the latest tagged version, do also something like this:

```
cd ./dacti
git checkout $(git describe --abbrev=0 --tags)
```

##### INSTALL

Just put `./bin/dacti` on your PATH.

##### USAGE

###### INVOCATION

```
dacti [ -h | --help | -v | --version ]
```

###### COMMANDS

```
Main selection menu: entries
        [BIN-ASC]                       Browse executables within <PATH>. Sort
                                        them in ascending order by their names
        [BIN-DESC]                      "" Sort them in descending order by their
                                        names
        [BIN-ATIME-ASC]                 "" Sort them in ascending order by their
                                        access times
        [BIN-ATIME-DESC]                "" Sort them in descending order by their
                                        access times
        <COMMAND>                       Launch application (run or raise)

Main selecton menu: modifiers
        :c                              Declare mode 'cli'
        :i                              Declare status 'ign'
        :k                              Keep the process. Wait for a key press
                                        or spawn a new shell instance
        :n                              Run COMMAND in a new terminal emulator
                                        window
        :p                              Don't check, whether COMMAND is indexed.
                                        Launch it directly and create NO record.
                                        See env DACTI_PRETEND
        :t                              Declare mode 'tui'
        :u                              Don't check, whether COMMAND is indexed.
                                        Launch it directly and create a new
                                        record.
```

###### ENVIRONMENT VARIABLES

```
        DACTI_CONF_FILE                 See function Dacti::Init
        DACTI_INDEX_FILE                ""
        DACTI_PRETEND                   Default: 0
```

###### CONFIGURATION

```
normal scalar variables
        prompt                          Default: >
        term                            Default: xterm
indexed array variables
        menu                            See entry section above
functions
        Dacti::CmdMenuCustom            See doc/examples/dactirc
        Dacti::ParseSelectionCustom     ""
        Dacti::RaiseAppPlCustom         ""
        Dacti::RaiseAppSgCustom         ""
```

###### INDEX FILE

Without command modifiers, a record gets the status `reg` and the mode `gui` per default (the command has a gui and may run OR raise). With a status `ign`, a command is not allowed to raise an existing window; `block` stops raising and running as well.

A record looks like:

```
# STATUS MODE[:MODIFIERS] WM_CLASS COMMAND

reg gui chromium-browser.chromium-browser chromium
ign gui XTerm xterm
reg gui .*Iceweasel iceweasel
reg tui:n - htop
reg cli:nk - find
```

If a command has more than one record, the last entry is going to be used.

The WM_CLASS string is considered an extended regular expression (regex(3)) pattern.

##### NOTICE

dacti has been written in [GNU bash](http://www.gnu.org/software/bash/) on [Debian GNU/Linux 9 (stretch/sid)](https://www.debian.org) using these programs/packages:

- GNU Bash 4.3.42(1)-release
- GNU coreutils 8.23: cut, mkdir, printf, sort, tty, uniq
- GNU findutils 4.4.2: find
- GNU grep 2.22
- procps 3.3.10: pgrep, ps
- suckless-tools 41-1: dmenu-4.6, lsx 0.1
- util-linux 2.27.1: setsid
- wmctrl 1.07-7
- x11-utils 7.7+3: xprop 1.2.2

dacti is not portable; it does not work in [ksh](http://www.kornshell.com/), [mksh](https://www.mirbsd.org/mksh.htm) or [zsh](http://www.zsh.org/). Your bash version needs to handle associative arrays.

The usage of find is not BSD-like (grep -c find dacti => 2). Please open and issue with the correct invocation for your system.

##### CREDITS

dacti is a rewrite of acti (v0.8; GNU GPLv3) by D630.

dacti is affected by Scott Garretts dmenu-launch (v0.5.7).

##### LICENCE

[Copyrights](../master/doc/COPYRIGHT)

[GNU GPLv3](../master/doc/LICENCE)
