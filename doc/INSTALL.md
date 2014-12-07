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
