```
Usage
        dacti [ -h | --help | -v | --version ]

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

Environment variables
        DACTI_CONF_FILE                 See function Dacti::Init
        DACTI_INDEX_FILE                ""
        DACTI_PRETEND                   Default: 0

Configuration
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

