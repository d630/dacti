Activate apps in selection menus (run or raise; launch). Works with desktop files. Default is dmenu, but you can use your own (fzf, selecta, tmenu, selecta etc.)

```bash
dacti (-h|-v|) [-C] [-a|-c|-k|-q]

    Cli
      -a   --update-applications Index all desktop files.
      -C,  --conf-file=<FILE>    Source a file as conf file.
      -c,  --update-categories   Index all categories.
      -h,  --help
      -k,  --update-keywords     Index all keywords.
      -q,  --quit                Quit before performing the main
                                 selection menu.
      -v,  --version

    Main selection menu
      [KEYWORDS]                 Browse keywords in a selection menu and
                                 select associated desktop files.
        :u [KEYWORDS]            Update the keyword index before.
        :q [KEYWORDS]            Invoke a query menu and look for desktop
                                 files.
      [CATEGORIES]               Browse all categories in a selection menu
                                 and select associated desktop files.
        :u [CATEGORIES]          Update the category index before.
      [BIN-ASC]                  Browse all binaries inside the enviroment
                                 variable <PATH> in a selection menu. Sort
                                 them in ascending order by its names.
      [BIN-DESC]                 Browse all binaries inside the enviroment
                                 variable <PATH> in a selection menu. Sort
                                 them in descending order by its names.
      [BIN-ATIME-ASC]            Browse all binaries inside the enviroment
                                 variable <PATH> in a selection menu. Sort
                                 them in ascending order by its access time.
      [BIN-ATIME-DESC]           Browse all binaries inside the enviroment
                                 variable <PATH> in a selection menu. Sort
                                 them in descending order by its access
                                 time.
      [LOG]                      Browse all log entries of dacti in a
                                 selection menu. Start applications from
                                 it by selecting
                                 entries with the event "launch".
      [OCCUR]                    Browse applications by its occurence
                                 based on the log file.

    Application
      <APP>                      Launch application.
        :b <APP>                 Declare status "block".
        :c <APP>                 App has a cli and needs a terminal (mode=cli).
        :i <APP>                 Declare status "ign".
        :n <APP>                 App should start in a new terminal instance.
        :p <APP>                 Dont check, if app is indexed. Launch it
                                 directly and create no new desktop file.
        :t <APP>                 Apps has a tui and needs a terminal (mode=tui).
        :u <APP>                 Dont check, if app is indexed. Launch it
                                 directly and create a new desktop file or
                                 entry.
```
