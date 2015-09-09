##### README

[dacti] is a simple menu driven run or raise bash shell script. By default, dacti works with [dmenu]() and [wmctrl](), but you may use your preferred tools.

I use dacti, because I want to have a DE indepent launcher in addtion to my shell in the terminal (keyboard driven and without much graphical stuff).

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

Just put `./dacti` on your PATH.

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

Main selecton menu: command prefixes
        :b                              Execute COMMAND in background
        :c                              Declare mode 'cli'
        :i                              Declare status 'ign'
        :k                              Keep the process. Wait for a key press
                                        or spawn a new shell instance
        :l                              Declare status 'block'
        :n                              Run COMMAND in a new terminal emulator
                                        window
        :p                              Don't check, wheater COMMAND is indexed.
                                        Launch it directly and create NO record.
                                        See env DACTI_PRETEND
        :t                              Declare mode 'tui'
        :u                              Don't check, wheater COMMAND is indexed.
                                        Launch it directly and create a new
                                        record.
```

###### ENVIRONMENT VARIABLES

```
        DACTI_CONF_FILE                 See function Dacti::Init
        DACTI_INDEX_FILE                ""
        DACTI_PRETEND                   Default: 0
```

###### Configuration

```
normal scalar variables
    prompt                      Default: >
    term                        Default: xterm
indexed array variables
    menu                        See entry section above
functions
    Dacti::CmdMenuCustom        See doc/examples/dactirc
    Dacti::ParseSelectionCustom ""
    Dacti::RaiseAppPlCustom     ""
    Dacti::RaiseAppSgCustom     ""
```

##### NOTICE

##### LICENCE

[Copyrights](../master/doc/COPYRIGHT)

[GNU GPLv3](../master/doc/LICENCE)
