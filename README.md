# extify

Extify is a Linux tool used to instantly map file extensions to programs.

Simply open a terminal and type `extify program extension [extensions...]`. You can pass in multiple extensions to assign them to the same program.

* `program` must be in PATH (this will be fixed in the future).

**Note:** extify is still under development and may not work as expected.

## Requirements

* Python 3
* xdg-utils

## Inspiration

Under Windows, you can create new file extension mappings, simply by renaming the file, right-clicking in Explorer, and selecting "Open with...". I sadly discovered that Linux file extensions require a complex process of creating a .desktop file in `~/.local/share/applications/app.desktop`, creating a XML file in `~/.local/share/mime/packages/mime.xml` with the desired file extension, and finally linking them together by ~~editing `~/.config/mimeapps.list`~~ `xdg-mime default app.desktop mimetype` .

## Technical Details

* Program - .desktop file
    * `~/.local/share/applications/program.desktop`
* Extension - MIME type
    * `~/.local/share/mime/packages/extension.xml`
    * `text/x-extension`
* File association
    * Runs: `xdg-mime default program.desktop text/x-extension`
    * This program edits `~/.config/mimeapps.list`
