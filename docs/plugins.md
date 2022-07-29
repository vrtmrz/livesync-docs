# Plugin and setting synchronisation.

## Sync hidden files

*This feature is still experimental. I'm using this every day and getting better, less fragile. But still sometimes works ridiculous. Be sure to back your vault up to some rigid place.*

### Sync hidden files
If we enable this. LiveSync scans changes on hidden files.
Changes in hidden files make no notification to LiveSync. So LiveSync must scan them in periodic or before replication once.

### Scan hidden files before replication

If enabled, LiveSync scans for changes before each replication; Only works for non-LiveSync.

### Scan hidden files periodicaly.
If set to non-zero value, LiveSync scans for changes each configured seconds.

### Skip patterns.

List of regular expressions to skip files during scan and synchronisation.
For synchronisation across platforms, `.workspace$` must be added in addition to the default.


## What will happen?

When new hidden files are incoming, popups will be shown.

1. Enabled plug-in's files notification.
   ![[Pasted image 20220727162827.png]]
   If we press `HERE`, the plugin will be reloaded.
2. Disabled plug-in's files or Obsidian's files file notification.
   ![[Pasted image 20220727162812.png]]
   If you press `HERE`, Obsidian will be reloaded.

## What can we do when we have applied the wrong changeset?

Take it easy, chill down and open `Pick file to show history`. and type `.obsidian/` or names that you have seen on the dialog. If you choose one of the files, open it.
If the file had history of recently modified, we can roll the file back by `Back to this revision`. We should restart obsidian after roll it back.


## Plugins and their settings

The older feature of the LiveSync. but works well if you want to pick and apply the plugins and their configuration.

