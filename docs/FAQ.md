# FAQ

## 1. `Ctrl-C` doesn’t stop the program

Yes, `Ctrl+C` will not stop guiscrcpy. This is because PyQt5’s renderer dos not handle `SIGINT` or `KeyboardInterrupt`. You can use a Task Manager to kill it or use the commanline `kill` / `killall`. If you try to use `Ctrl+C`, it can force guiscrcpy into an unresponsive state, and later hangs. Alternatively, use the close button to stop it.

## 2. `libQt*.so.*` is not found?

This is probably because you have two installations of `PyQt5` or `PySide2`, The `PySide2` and `PyQt5` are conflicting packages. Uninstalling one of them will not fix the error. This is because `pip` uninstalls the co-referenced file, which later becomes missing. The solution, is however to create a [`virtual environment`](https://google/search?q=python+virtual+environment) or to uninstall `PyQt5` (and `PySide2` if it exists) and reinstall them on local level. If the PyQt5 level matches the system level only, you can either uninstall all local level `PyQt5` or you can run `guiscrcpy` with

```bash
python -s $(which guiscrcpy)
```

## 3. Window panels are not draggable

Related to [#103 (comment)](https://github.com/srevinsaju/guiscrcpy/issues/103#issuecomment-619428461]), this is a problem with `PyQt5` and some desktop managers which do not support Frame less window dragging or windows that do not have permission to change their position on the screen. 

On some desktop managers like `LXDE`, `KDE Plasma`; it has been found that you can drag these windows using your `Alt` modifier key while dragging. 

If using `Alt` does not fix the problem, and until a solution for this is found; You can temporarily use

```bash
guiscrcpy --force_window_frame
```

or 

```bash
python3 -m guiscrcpy --force_window_frame
```

This enables the your desktop managers window decoration to be included inside the frame; so that you can at least drag it. Alternatively; if you feel its too distractive; you can permanently disable it. 

## 4. Desktop files not created

It is possible that `guiscrcpy` may give the message `Desktop file creation was successful` on Linux, but not created anywhere. `guiscrcpy` respects [**freedesktop’s**](https://en.wikipedia.org/wiki/Freedesktop.org) guidelines for creating shortcut on desktops. For every standard Linux installation, an environment variable `XDG_DESKTOP_DIR` and `XDG_CONFIG_HOME` is likely to be set. In the absence of such a variable, `guiscrcpy` might not know where to save the desktop icon.

A possible solution is to set your `XDG_DESKTOP_DIR` to the `PATH` wherever you would like to have your shortcuts

```bash
export XDG_DESKTOP_DIR="/path/to/dir"
```

You may also like to add it to your `.bashrc` or `.zshrc`

```bash
echo 'export XDG_DESKTOP_DIR="/path/to/dir"' >> ~/.bashrc
```

```bash
echo 'export XDG_DESKTOP_DIR="/path/to/dir"' >> ~/.zshrc
```



