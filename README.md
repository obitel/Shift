Shift is a minimalistic approach to maximum control of your Transmission.
=====

*Shift is targeted at Mozilla Firefox 4+ with degraded and untested functionality for other or older browsers.*

![shift_torrents](https://cloud.githubusercontent.com/assets/932370/12071321/fa568a5a-b0a5-11e5-919c-28adadfe0852.png)
![shift_session](https://cloud.githubusercontent.com/assets/932370/12071322/ff3b78fa-b0a5-11e5-9ee8-195593a59364.png)

## Column based sorting and filtering.

* General:
Click on the name in a column header and the table will be sorted by that column. Click on it again and the sorting order is reversed.

* Torrents:
Click on the LED in the column header, next to the name and filtering input options are shown. By default only torrents currently downloading are shown and are sorted by percentDone in descendent order. When you change the value of the "Status" filter the column view changes also to better suit the context of the filtered torrents.

* Files:
The sorting of files contained in the torrent works similarly but with a twist or two. The first twist is that files are sorted by the given column and then the tree structure is changed to match the new sort order. The other twist is in the name column. By default it is sorted by torrent order in the exact sequence of files contained in the torrent. Click on the name column header and it is sorted by tree order, alphabetically and nested. If the files were added to the torrent in proper tree order then the view will not change.

## Improved files management.

Double-click on a torrent row or select Details from the torrent context menu, the LED on the left\*, to view the files contained in the torrent. The files are shown in a tree-like structure, with the important addition that this structure is fully functional. Change the download priority (high, normal, low, none) on a node, again from the context menu, and all subnodes are assigned the same priority. Oh, and you CAN change the priority of already downloaded files.

<sup>\* The LED also doubles as a selection indicator for batch commands, except Announce, Detail and Select.</sup>

## Files in torrents can be linked. (Even if they are not 100% complete.)

Click on a file in a torrent and you will get a link to it. You do need to configure some base URLs first, but then the possibilities are ginormous. ( example: ftp://myname@myserver/mydownloads/... ). And even though the Transmission daemon is not meant to be used as a webserver, it IS possible to have it serve the linked file! You do need some clever file placement and/or symbolic linking for that to work, though. I recommend using a reverse proxy for serving the files.

## Improved drag & drop interface.

You can drop files and links anywhere on the Shift page. Currently supported are torrent files and text files containing links. (Yes, magnets are also links.)

## Change less means more.

Why reload semi-static data each and every AJAX call? Shift tries to minimize the data consumption from Transmission. This means using less bandwidth and less processing for Transmission. Because of this saving the smaller requests can be made more often. Shift also works hard to not update cell data when it doesn't need to.

## Open for mutilation.

* "I really loved your old-skool green-on-black theme, just loved it!" No problemo, it is still around but has been renamed to terminal.css.
* "I really need to have a column to show the eta of the torrents." Then you can add a "doneDate" entry in the torrentColumns object. To make it visible and have it regularly updated for status "Downloading" also add the entry to the columns and field arrays:

```javascript
var globals = {
  torrentStatus: {
    ...
    4: {
      label: "Downloading",
      columns: [... , "doneDate", ...],
      fields: [... , "doneDate", ...]
    },
    ...
  }
}

var torrentColumns = {
  ...
  "doneDate": {
    label: "ETA", render: function( date ) {
      return date ? renderDateTime( date ) : "";
    }
  },
  ...
}
```
* "This functionality doesn't work on Google Chrome\*." Ah, then you(!) have some 'splaining to do... and probably some work as well.

<sup>\* Swap in your favorite browser here.</sup>

## Keyboard navigation.

* General:

| Key                        | Action                    |
| -------------------------: | :------------------------ |
| <kbd>**Up**</kbd>          | Activate row up           |
| <kbd>**Down**</kbd>        | Activate row down         |
| <kbd>**Esc**</kbd>         | Close popup / dialog      |
| <kbd>**Space**</kbd>       | Select / Deselect         |
| <kbd>**?**</kbd>           | About                     |

* Torrent view:

| Key                                | Action                               |
| ---------------------------------: | :----------------------------------- |
| <kbd>**a**</kbd>                   | Show all torrents                    |
| <kbd>**c**</kbd>                   | Show checking (/waiting) torrents    |
| <kbd>**d**</kbd>                   | Show downloading (/waiting) torrents |
| <kbd>**s**</kbd>                   | Show stopped torrents                |
| <kbd>**u**</kbd>                   | Show uploading (/waiting) torrents   |
| <kbd>**1**</kbd>..<kbd>**0**</kbd> | Sort torrents                        |
| <kbd>**Del**</kbd>                 | Remove torrent                       |
| <kbd>**Shift + Del**</kbd>         | Trash torrent                        |
