# dacti v0.1.0.0 [GNU GPLv3] #

`dacti`(1) is a stupid selection menue driven run or raise bash shell script. It was written to combine the characteristic of application runners with the qualities of structured menu based launchers. Therefore, `dacti`(1) organizes, reads, modifies and creates desktop files aka. "desktop entries", which are standardized by [freedesktop.org](http://standards.freedesktop.org). By default, `dacti`(1) works with `dmenu`(1) and `wmctrl`(1), but you can use your preferred tools ([dmenu2](https://bitbucket.org/melek/dmenu2), [fzf](https://github.com/junegunn/fzf), [selecta](https://github.com/garybernhardt/selecta), [slmenu](https://bitbucket.org/rafaelgg/slmenu), [tmenu](https://github.com/dhamidi/tmenu) etc.).

Use `dacti`(1), if you want to have a DE indepent launcher in addtion to your shell (keyboard driven and without much graphical stuff). You do not have to be a heavy Klickibunti-user of desktop entries. `dacti`(1) simply uses the standard.

### Features ###

* Run or raise applications (based on desktop entries or directly with or without belated recording).
    * Running is dependent on: the invocation mode of `dacti`(1) (cli or gui), the application status (blocked, ignored, regular), the need for a terminal (with or without new terminal instance) and the execute key of the application (optional configured).
    * Raising is dependent on: the application status (blocked, ignored, regular), the application mode (cli, gui, tui), the number of existed windows of the application (0; 1; >1) and the optional configured raise keys for its count (singular, plural).
* Index and browse all existed desktop entries in `<XDG_DATA_DIRS>` and `<XDG_DATA_HOME>`. Modify user specific desktop entries or create new ones with these extended keys:
    * `X-dacti_mode=(cli|gui|tui)`
    * `X-dacti_new_term=(1|true|yes|)`
    * `X-dacti_status=(block|ign|reg)`
    * `X-dacti_win_pl=LIST`
    * `X-dacti_win_sg=LIST`
* Browse all binaries (`<PATH>`) in ascending or descending order by its names or access times. Then run or raise them.
* Index and brows all desktop entries with a category key in hierarchical order. Then run or raise those desktop entries.
* Index, browse or query (regextype: posix-egrep) all desktop entries with a keywords key. Run or raise associated desktop entries.
* Browse all log entries of `dacti`(1). Run or raise entries with an "launch event".
* Browse all launches by application occurence (based on logfile).
* Modify the main selection menu and insert special "first class entries", preferably with other menu based scripts (`dacti`(1) becomes a launching pad).
* Use a configuration file and declare your selection menu launchers, your specific entries and the default raise command list.

## Install ##

Required: GNU bash, chmod, comm, cut, [dmenu](http://tools.suckless.org/dmenu/), GNU find, GNU grep, GNU sed, ln, [lsx](http://tools.suckless.org/lsx), mv, pgrep, ps, sort, stat, tee, uniq, [wmctrl](http://tomas.styblo.name/wmctrl/), xprop

* Get `dacti`(1) with `git clone https://github.com/D630/dacti.git` or download it on https://github.com/D630/dacti/releases
* Copy the script `dacti` elsewhere into `<PATH>`.
* Copy the dir `Categories` into `<DACTI_DATA_DIR>` or its contents into `<DACTI_CATS_DATA_DIR>`.

## Usage ##

```
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

## Examples ##

TODO

## Enviroment ##

* internal (info)
    * `xdg_data_dirs`: ${XDG_DATA_DIRS:-"/usr/local/share:/usr/share"}

* modifiable:

| evar  | default val |
| ------------- | ------------- |
| DACTI_APPS_CACHE_FILE | ${DACTI_DATA_DIR}/dacti_applications.cache |
| DACTI_APPS_DIR_HOME | ${XDG_DATA_HOME:-"${HOME}/.local/share"}/applications |
| DACTI_APPS_DIRS | $xdg_data_dirs (separat by colon like in `<PATH>`) |
| DACTI_APPS_INDEX_FILE | ${DACTI_DATA_DIR}/dacti_applications.index |
| DACTI_CATS_DATA_DIR | ${DACTI_DATA_DIR}/Categories |
| DACTI_CATS_INDEX_FILE | ${DACTI_DATA_DIR}/dacti_categories.index |
| DACTI_CONF_FILE | ${XDG_CONFIG_HOME:-"${HOME}/.config"}/dacti/dacti.conf |
| DACTI_DATA_DIR | ${XDG_DATA_HOME:-"${HOME}/.local/share"}/dacti |
| DACTI_KEYWS_CACHE_FILE | ${DACTI_DATA_DIR}/dacti_keywords.cache |
| DACTI_KEYWS_INDEX_FILE | ${DACTI_DATA_DIR}/dacti_keywords.index |
| DACTI_LOG_FILE | ${DACTI_DATA_DIR}/dacti.log |

* not yet used:
    * `DACTI_CATS_MAIN_INFO_FILE`
    * `DACTI_CATS_SUB_INFO_FILE`
    * `DACTI_TMP_DIR`

## Configurations ##

Along with this programm comes an exemplary Conf File. You can set following parameters:

* enviroment variables: all, but `<DACTI_CONF_FILE>`
* normal scalar variables:
    * `term=<TERM>` (fallback is `xterm`)
    * `menu_0_prompt=<STRING>` (fallback is `>`)
* indexed array variables
    * `menu_0[<INTG>]=<STRING>` fallback is `menu_0=(CATEGORIES KEYWORDS BIN-ASC BIN-DESC BIN-ATIME-ASC BIN-ATIME-DESC LOG OCCUR)`
* functions:
    * `__dacti_do_win_pl_custom`: decide, what do to with "${xids[@]}".
    * `__dacti_do_win_sg_custom`: decide, what to do with "${xids[0]}".
    * `__dacti_menu_cmd_custom "$menu_prompt"`: specify the menu command list.
    * `__dacti_selection_custom "$selection"`: specify, what to do, if special entries in the main menu has been chosen.

## Notes ##

* You may write all long name options without masking `--`. Instead of `--help` you may use `help`.

## BUGS & REQUESTS ##

Report it on https://github.com/D630/dacti/issues

## TODO ##

All is work in progress. See file `TODO`, which comes along with this programm.

## Credits ##

`dacti`(1) is a rewrite of [acti](https://github.com/D630/acti) (v0.8; GNU GPLv3) by D630.

`dacti`(1) is affected by [dmnenu-launch](https://github.com/Wintervenom/Scripts/blob/master/file/launch/dmenu-launch) (v0.5.7) by Scott Garrett.
