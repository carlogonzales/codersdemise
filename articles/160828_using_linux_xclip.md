# Using Linux XCLIP

`xclip` is a command line utility for setting and getting values on the clipboard using other command's output or input. Instead of directly using shortcut keys on the terminal, `xclip` can be used likewise except you have to pipe the output and input from other commands.

In general here's the three(3) selection for `xclip`

- Primary - Used for the 3rd mouse button
- Secondary - Act's as an alternative to primary
- Clipboard - GUI or window-style clipboard using the shortcut keys (`ctrl+c`, `ctrl+shift+v`)

### Sample Usage

#### Copying directory listing to clipboard

```bash
ls | xclip -selection c
# Alternative
ls | xclip -selection clipboard
```

#### Outputing clipboard

```bash
xclip -o -selection c
```

### Aliasing xclip

Since **clipboard**'s the common selection for xclip we can just create an alias on our `~/.bashrc` file or system-wide `/etc/bashrc`, if you're using bash.

**USER**
```bash
echo "alias xclip='xclip -selection clipboard'" >> ~/.bashrc 
source ~/.bashrc
```

**SYSTEM-WIDE**
```bash
echo "alias xclip='xclip -selection clipboard'" >> /etc/bashrc
source /etc/bashrc
```


#### References

- [xclip manpage](http://linux.die.net/man/1/xclip)
- [ixsel manpage](http://linux.die.net/man/1/xsel)
- [ArchLinux Clipboard](https://wiki.archlinux.org/index.php/clipboard)
