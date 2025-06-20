# dired-sort

`dired-sort` is an Emacs package that enhances the Dired file manager with flexible sorting options and control over hidden file visibility. It provides a global minor mode, `dired-sort-mode`, to streamline file navigation with a clean, aligned menu or completion interface for sorting commands.

## Features

- **Toggle Hidden Files**: Show or hide dotfiles (e.g., `.gitignore`) with a single keybinding, preserving the `..` entry when hidden files are disabled.
- **Flexible Sorting Options**:
  - Sort by name (alphabetically, normal or reverse).
  - Sort by modification date (newest or oldest first).
  - Sort by file extension (normal or reverse).
- **Directory Priority**: Directories always appear at the top, regardless of the sorting method.
- **Live Updates**: Sorting and visibility changes apply instantly without restarting Emacs.
- **Interactive Menu**: Choose sorting options via a numbered menu or `completing-read` interface, with the current sort mode highlighted by an asterisk.
- **Automatic Buffer Updates**: Sorting updates automatically when switching Dired buffers or windows.
- **Customizable Keybindings**: Easily bind commands to preferred keys.

## Installation

### Manual Installation

1. Download `dired-sort.el` and place it in your Emacs load path (e.g., `~/.emacs.d/lisp/`).
2. Add the following to your Emacs configuration (`init.el`):

```emacs-lisp
(require 'dired-sort)
(dired-sort-mode 1)  ; Enable the global minor mode
```

### Via Package Manager (e.g., `use-package`)

If using `use-package`, add:

```emacs-lisp
(use-package dired-sort
  :ensure nil  ; Set to t if installed via a package repository
  :config
  (dired-sort-mode 1))
```

### Dependencies

- Emacs 24.4 or higher.
- `cl-lib` (included in Emacs 24.4+ for `cl-loop` and `cl-find`).

## Usage

1. **Enable the Mode**:
   ```emacs-lisp
   (require 'dired-sort)
   (dired-sort-mode 1)
   ```

2. **Set Up Keybindings**:
   Automatically bind default keys by adding:
   ```emacs-lisp
   (with-eval-after-load 'dired
     (dired-sort-setup-keys))
   ```

   Default keybindings:
   - `M-g h`: Toggle hidden files visibility.
   - `M-g n`: Sort by name (alphabetically).
   - `M-g r n`: Sort by name (reverse).
   - `M-g d`: Sort by date (oldest first).
   - `M-g r d`: Sort by date (newest first).
   - `M-g x`: Sort by extension.
   - `M-g r x`: Sort by extension (reverse).
   - `C-c m`: Show numbered sort menu.
   - `C-c c`: Show completion-based sort interface.

3. **Custom Keybindings**:
   Override defaults by defining your own keys:
   ```emacs-lisp
   (with-eval-after-load 'dired
     (dired-sort-setup-keys)
     (define-key dired-mode-map (kbd "C-c m") #'dired-sort-show-menu)
     (define-key dired-mode-map (kbd "C-c c") #'dired-sort-show-completion))
   ```

4. **Commands**:
   - `M-x dired-sort-toggle-hidden`: Toggle visibility of hidden files.
   - `M-x dired-sort-by-name`: Sort alphabetically.
   - `M-x dired-sort-by-name-reverse`: Sort alphabetically in reverse.
   - `M-x dired-sort-by-date`: Sort by modification time (oldest first).
   - `M-x dired-sort-by-date-reverse`: Sort by modification time (newest first).
   - `M-x dired-sort-by-extension`: Sort by file extension.
   - `M-x dired-sort-by-extension-reverse`: Sort by file extension in reverse.
   - `M-x dired-sort-show-menu`: Display a numbered menu of sort options.
   - `M-x dired-sort-show-completion`: Display a completion-based sort interface.

## Example Menu

When you press `C-c m` (`dired-sort-show-menu`), you’ll see:

```
Choose sort option:
1  [*] Sort by name           (\[dired-sort-by-name])
2  [ ] Sort by name (reverse) (\[dired-sort-by-name-reverse])
3  [ ] Sort by date           (\[dired-sort-by-date])
4  [ ] Sort by date (reverse) (\[dired-sort-by-date-reverse])
5  [ ] Sort by extension      (\[dired-sort-by-extension])
6  [ ] Sort by extension (reverse) (\[dired-sort-by-extension-reverse])
7  [ ] Toggle hidden files    (\[dired-sort-toggle-hidden])
8  [ ] Show sort command menu (\[dired-sort-show-menu])
Enter number:
```

- The asterisk `[*]` indicates the current sort mode.
- Enter a number (e.g., `1`) to apply the corresponding sort option.
- Alternatively, use `C-c c` for a completion-based interface.

## Configuration

Customize the behavior via `M-x customize-group RET dired-sort`:

- `dired-sort-show-hidden`: Enable/disable hidden files by default (boolean).

To change the default sort switches or add custom options, modify `dired-sort-extra-switches` in your functions or advise `dired-sort--setup`.

## Notes

- The package uses GNU `ls` with `--group-directories-first` for sorting. Ensure your system’s `ls` (GNU coreutils) supports this option. If not, install `coreutils` or use `ls-lisp`:
  ```emacs-lisp
  (require 'ls-lisp)
  (setq ls-lisp-use-insert-directory-program nil)
  (setq ls-lisp-dirs-first t)
  ```
- The `..` entry is manually inserted when hidden files are disabled to maintain navigation convenience.
- Requires `cl-lib` for menu construction. If you prefer pure Lisp, contact the author for an alternative implementation.

## License

`dired-sort` is licensed under the [GNU General Public License v3.0](LICENSE).

## Contributing

Contributions are welcome! Please submit issues or pull requests to [the repository](https://your.repo.url/here).

## Author

- Mykhailo Kazarian <michael.kazarian@gmail.com>