## dacti v0.1.1.0 [GNU GPLv3]

`dacti`(1) is a stupid selection menu driven run or raise bash shell script. It combines the characteristic of application runners with the quality of structured menu based launchers. Therefore, `dacti`(1) organizes, reads, modifies and creates desktop files aka. "desktop entries", which are standardized by [freedesktop.org](http://standards.freedesktop.org). By default, `dacti`(1) works with `dmenu`(1) and `wmctrl`(1), but you may use your preferred tools.

Use `dacti`(1), if you want to have a DE indepent launcher in addtion to your shell (keyboard driven and without much graphical stuff). You do not have to be a heavy Klickibunti-user of desktop entries. You can use it in different ways:

* index all desktop files on your system, create new ones or modify the existing
* work with local desktop files only
* always use the `:p` or `--pretend` command and do not use desktop files at all; use `dacti`(1) as simple launcher without managing

![](https://raw.githubusercontent.com/D630/dacti/master/doc/dacti.png)

1. [Install](#install)
2. [Features](#features)
3. [Usage](#usage)
4. [Examples](#examples)
5. [Environment](#environment)
6. [Configurations](#configurations)
7. [Notes](#notes)
8. [Bugs & Requests](#bugs--requests)
9. [TODO](#todo)
10. [Credits](#credits)

### Install

Required: GNU bash, chmod, comm, cut, [dmenu](http://tools.suckless.org/dmenu/), GNU find, GNU grep, GNU sed, ln, [lsx](http://tools.suckless.org/lsx), mv, pgrep, ps, sort, stat, tee, uniq, [wmctrl](http://tomas.styblo.name/wmctrl/), xprop

* Get `dacti`(1) with `git clone https://github.com/D630/dacti.git` or download its last release on https://github.com/D630/dacti/tags
* Copy the script `dacti` elsewhere into `<PATH>`
* Copy the dir `Categories` into `<DACTI_DATA_DIR>` or its contents into `<DACTI_CATS_DATA_DIR>`
* Copy `doc/dacti_categories_{main,sub}.info` into `<DACTI_DATA_DIR>`
* Then create a keybind. In `openbox`(1) you could use:

```xml
<keyboard>
    <keybind key="W-p">
        <action name="Execute"><command>dacti</command></action>
    </keybind>
</keyboard>
```

### Features

* Run or raise applications (based on desktop entries, or directly with or without belated recording).
    * Running is dependent on: the invocation mode of `dacti`(1) (`cli` or `gui`), the application status (`block`, `ignore`, `regular`), the need for a terminal (with or without new terminal instance) and the execute key of the application (optional configured).
    * Raising is dependent on: the application status (`block`, `ignore`, `regular`), the application mode (`cli`, `gui`, `tui`), the number of existing windows of the application (`0`; `1`; `>1`) and the optional configured raise keys for its count (`singular`, `plural`).
* Index and browse all existing desktop entries in `<XDG_DATA_DIRS>` and `<XDG_DATA_HOME>`. Modify user specific desktop entries or create new ones with these extended keys:
    * `X-dacti_mode=(cli|gui|tui)`
    * `X-dacti_new_term=(1|true|yes|)`
    * `X-dacti_status=(block|ign|reg)`
    * `X-dacti_win_pl=LIST`
    * `X-dacti_win_sg=LIST`
* Browse all binaries (`<PATH>`) in ascending or descending order by their names or access times. Then run or raise them.
* Index and browse all desktop entries with a category key in hierarchical order. Then run or raise those desktop entries.
* Index and browse all desktop entries with a keyword key. Run or raise associated desktop entries.
* Browse all log entries of `dacti`(1). Run or raise entries with an "launch event".
* Browse all launches by application occurence (based on logfile).
* Modify the main selection menu and insert special "first class entries", preferably with other menu based scripts (`dacti`(1) becomes a launching pad).
* Use a configuration file and declare your selection menu launchers, your specific entries and the default raise command list.

### Usage

```
dacti (-h|-v|) [-C] [-a|-c|-k|-q] [-p]

    Cli
      -a   --update-applications Index all desktop files.
      -C,  --conf-file=<FILE>    Source a file as conf file.
      -c,  --update-categories   Index all categories.
      -h,  --help
      -k,  --update-keywords     Index all keywords.
      -p,  --pretend             Like ":p". Pretend indexing and building
                                 of desktop files.
      -q,  --quit                Quit before performing the main
                                 selection menu.
      -v,  --version

    Main selection menu
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
      [CATEGORIES]               Browse all categories in a selection menu
                                 and select associated desktop files.
        :u [CATEGORIES]          Update the category index before.
      [KEYWORDS]                 Browse keywords in a selection menu and
                                 select associated desktop files.
        :u [KEYWORDS]            Update the keyword index before.
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

### Examples

See file [TUT.md](../master/doc/TUT.md)

### Environment

* internal (info)
    * `xdg_data_dirs`: `${XDG_DATA_DIRS:-"/usr/local/share:/usr/share"}`

* modifiable:

| **evar**  | **default val** |
| ------------- | ------------- |
| `DACTI_APPS_CACHE_FILE` | `${DACTI_DATA_DIR}/dacti_applications.cache` |
| `DACTI_APPS_DIRS` | `$xdg_data_dirs` (separat by colon like in `<PATH>`) |
| `DACTI_APPS_DIR_HOME` | `${XDG_DATA_HOME:-"${HOME}/.local/share"}/applications` |
| `DACTI_APPS_INDEX_FILE` | `${DACTI_DATA_DIR}/dacti_applications.index` |
| `DACTI_CATS_DATA_DIR` | `${DACTI_DATA_DIR}/Categories` |
| `DACTI_CATS_INDEX_FILE` | `${DACTI_DATA_DIR}/dacti_categories.index` |
| `DACTI_CATS_MAIN_INFO_FILE` | `${DACTI_DATA_DIR}/dacti_categories_main.info` |
| `DACTI_CATS_SUB_INFO_FILE` | `${DACTI_DATA_DIR}/dacti_categories_sub.info` |
| `DACTI_CONF_FILE` | `${XDG_CONFIG_HOME:-"${HOME}/.config"}/dacti/dacti.conf` |
| `DACTI_DATA_DIR` | `${XDG_DATA_HOME:-"${HOME}/.local/share"}/dacti` |
| `DACTI_KEYWS_CACHE_FILE` | `${DACTI_DATA_DIR}/dacti_keywords.cache` |
| `DACTI_KEYWS_INDEX_FILE` | `${DACTI_DATA_DIR}/dacti_keywords.index` |
| `DACTI_LOG_FILE` | `${DACTI_DATA_DIR}/dacti.log` |

* not yet used:
    * `DACTI_TMP_DIR`

### Configurations

Along with this programme comes an exemplary [configuration file](../master/doc/examples/dacti.conf.examples). You can set following parameters:

* enviroment variables: all, but `<DACTI_CONF_FILE>`
* normal scalar variables:
    * `term=<TERM>` (fallback is `xterm`): your terminal.
    * `menu_0_prompt=<STRING>` (fallback is `>`): the default prompt.
* indexed array variables
    * `menu_0[<INTG>]=<STRING>` (fallback is `menu_0=(BIN-ASC BIN-ATIME-ASC BIN-ATIME-DESC BIN-DESC CATEGORIES KEYWORDS LOG OCCUR)`): specify special entries in the main selection menu.
* functions:
    * `__dacti_do_win_pl_custom`: decide, what do to with `${xids[@]}`.
    * `__dacti_do_win_sg_custom`: decide, what to do with `${xids[0]}`.
    * `__dacti_menu_cmd_custom "${menu_prompt}"`: specify the menu command list.
    * `__dacti_selection_custom "${selection}"`: specify, what to do, if special entries in the main menu has been chosen.

### Notes

* You may write all long name options without masking `--`. Instead of `--help` you may use `help`.

### Bugs & Requests

Report it on https://github.com/D630/dacti/issues

### TODO

All is work in progress. See file [TODO](../master/doc/TODO), which comes along with this programme.

### Credits

`dacti`(1) is a rewrite of [acti](https://github.com/D630/acti) (v0.8; GNU GPLv3) by D630.

`dacti`(1) is affected by Scott Garretts [dmenu-launch](https://github.com/Wintervenom/Scripts/blob/master/file/launch/dmenu-launch) (v0.5.7).
