## A little tutorial to learn using dacti ##

### Default behavior ###

Open your terminal up and type `dacti` or launch `dacti`(1) with your configured keybind. Without any configuration in the conf file, you would see the main selection menu, which looks in that case like this:

```
[BIN-ASC]
[BIN-ATIME-ASC]
[BIN-ATIME-DESC]
[BIN-DESC]
[CATEGORIES]
[KEYWORDS]
[LOG]
[OCCUR]
```

Since categories and keywords based on indexed desktop entries, there is no advantage to use them now. If you select `[KEYWORDS]`, you end up in an empty selection menu; if you select `[CATEGORIES]`, you can only browse categories without desktop files. The log file is still beeing empty: `[LOG]` and `[OCCUR]` have nothing to browse.

You can launch (run or raise) an application by browsing one of the BIN-entries or by typing a command. Without any prefixes `dacti`(1) looks for the command in the index file (`<DACTI_APPS_INDEX_FILE>`); since there are still no entries, the application would get the status `reg` and the mode `gui` per default. After launching the application, `dacti`(1) tries to create a new desktop file in `<DACTI_APPS_DIR_HOME>` and to record the application in `<DACTI_APPS_INDEX_FILE>`. Let us say, we enter the gui application `spacefm`(1) (but no instance of it is running):

```bash
spacefm
```

After launching it, `dacti(1)` will be closed. We have then a `<DACTI_APPS_DIR_HOME>` like this:

```bash
$ ls ~/.local/share/applications
defaults.list  mimeapps.list  mimeinfo.cache  spacefm.desktop
```

```bash
$ cat ~/.local/share/applications/spacefm.desktop
[Desktop Entry]
Actions=
Categories=
Comment=
DBusActivatable=
DocPath=
Exec=spacefm
GenericName=
Hidden=
Icon=
InitialPreference=
Keywords=
MimeType=
Name=spacefm
NoDisplay=
NotShowIn=
OnlyShowIn=
Path=
ServiceTypes=
StartupNotify=
StartupWMClass=spacefm
Terminal=
TryExec=
Type=Application
Version=1.1
X-dacti_mode=gui
X-dacti_new_term=
X-dacti_status=reg
X-dacti_win_pl=
X-dacti_win_sg=
```

And a `<DACTI_APPS_INDEX_FILE>` like this:

```bash
$ cat ~/.local/share/dacti/dacti_applications.index
reg gui spacefm /home/user/.local/share/applications/spacefm.desktop
```

Opened `dacti`(1) a second time, the main selection menu has now a new entry:

```
[BIN-ASC]
[BIN-ATIME-ASC]
[BIN-ATIME-DESC]
[BIN-DESC]
[CATEGORIES]
[KEYWORDS]
[LOG]
[OCCUR]
spacefm
```

Now let us empty the index file to see what is going on, when we start `spacefm`(1) with an existing desktop file for it.

```bash
$ > ~/.local/share/dacti/dacti_applications.index
$ cat ~/.local/share/dacti/dacti_applications.index

```

Opened `dacti`(1) a third time, we can see: no entry of `spacefm`(1) exits any longer. After typing and launching `spacefm`(1) without desktop entry, we will end up in a second selection menu, where we ether need to enter a name for this launcher or to skip it with `Escape`. We type `spacefm 2`, and the desktop file looks like this:

```bash
$ cat ~/.local/share/applications/spacefm.desktop
[Desktop Entry]
Actions=spacefm_12590;
Categories=
Comment=
DBusActivatable=
DocPath=
Exec=spacefm
GenericName=
Hidden=
Icon=
InitialPreference=
Keywords=
MimeType=
Name=spacefm
NoDisplay=
NotShowIn=
OnlyShowIn=
Path=
ServiceTypes=
StartupNotify=
StartupWMClass=spacefm
Terminal=
TryExec=
Type=Application
Version=1.1
X-dacti_mode=gui
X-dacti_new_term=
X-dacti_status=reg
X-dacti_win_pl=
X-dacti_win_sg=

[Desktop Action spacefm_12590]
Exec=spacefm
Name=spacefm2
StartupWMClass=spacefm
Terminal=
X-dacti_mode=gui
X-dacti_new_term=
X-dacti_status=reg
X-dacti_win_pl=
X-dacti_win_sg=
```

If there were already a desktop file but no index entry, `dacti`(1) would update its content. An application has only one desktop file, but may contain several launcher sections. Therefore, any desktop file is recorded once only in the index. The application entries in the main selection menu are based on the index file; you can treat them as bookmarks or clickable desktop icons on a Windows desktop.

### Modify launching in the input field ###

As mentioned before, any non-indexed application gets the mode `gui` and the status `reg`. We can modify that with prefixes (or you use an editor to modify the desktop files). When we want to launch a cli or tui application, we use `:c` for `cli` or `:t` for `tui`. Both commands bring `dacti`(1) to launch the application in a terminal:

```bash
:t ranger
```

```bash
:c ls -l
```

We can block an application and its launch with `:b`:

```bash
:cb rm
:b spacefm
```

To ignore a window raising and only allow executions of new instances:

```bash
:it elinks
:i firefox
```

And to declare, that an application should start in a new terminal instance `:n` (`new`):

```bash
:tn elinks
```

### Handling multiple entries in a desktop file  ###

Once an application has been indexed, `dacti`(1) always launches it with the settings in the desktop file. When the desktop entry has more than one section and you try to launch the application, then yet anthoher selection menu appears. It is a list of all entries with some information about the settings. You can select an entry or abort it with `Escape`. By aport, you finally end up in a third selection menu with these entries:

```bash
[1] return
[2] Exec: $ spacefm
[3] Set options and exec: $ spacefm
[4] Edit command and set options.
```

The choices `3` and `4` allow you to use `:b`, `:c`, `:i`, `:n`, `:t` and `:u`. With the last command `:u` (`build`) you can create a new execution section in the desktop file. You may also work with `:u` in the first place, if you know, that some entries per application exist. This behavior avoids the menu with the listing of specific entries of one application by skipping the index file.

```bash
:uti elinks
```

Moreover, you can use the command `:p` (`pretend`) or invocation of `dacti`(1) with option `--pretend`. With it, an application will be started without reading the index file and without creating a new entry. That is quite useful to start an application as you like without tracking:

```bash
:cpi task newest
```

###  Index all desktop entries  ###

Up to this point, `dacti`(1) only indexes applications after their launches (not using `:p`). Besides, `dacti`(1) only reads and writes files in `<DACTI_APPS_DIR_HOME>` (usually `${HOME}/.local/share/applications`). When you invoke `dacti`(1) with its options all desktop entries in `<DACTI_APPS_DIRS>` will be used; you can configure this enviroment variable, by default it references `/usr/local/share` and `/usr/share`. To scan all desktop entries and index them in the index application file, you need to use:

```bash
$ dacti -a
# or
$ dacti --update-applications
```

To quit after indexing without executing the selection menu:

```bash
$ dacti -aq
```

After that, you may have more than one desktop file of an application, for example `/usr/share/applications/spacefm.desktop` and `${HOME}/.local/share/applications/spacefm.desktop`. Since `dacti`(1) has only wright access of the local user, global desktop files can only be read. But their entries may be listed in the selection menu.

Same proceeding with categories and keywords. Index them with:

```bash
$ dacti -ck
```

To update them on the fly, select `[CATEGORIES]` or `[KEYWORDS]` and prefix it with `:u` (`update`):

```bash
:u [CATEGORIES]
```

You may also query keywords with the command `:q`. Prefix the selection and then type your query (regextype: posix-egrep). Your regex `$i` needs to fit in following expression:

```bash
"^(.*):Keywords=.*${i};.*$"
```

```bash
:uk [KEYWORDS]
tar
```

Furthermore, you can use simple search operators: `and`, `or` and `not`.

```bash
:uk [KEYWORDS]
tar and zip
zip not tar
```

### Result ###

`dacti`(1) is a simple `menu` driven bash shell script with interactive usage. You can use it in different ways:

* index all desktop files on your system, create new one or modify the existing
* only use local desktop files
* always use the `:p` or `--pretend` command and do not use desktop files at all; use `dacti`(1) as simple launcher without managing

Since all desktop files are plain text files, you can modify all keys and launching options like you want.

