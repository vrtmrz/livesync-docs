# Synchronise files between devices

## LiveSync

By using [[What is the database|Differential replication]], we can synchronise files in the near-real-time.
Only we have to enable is `LiveSync`, we can synchronise in live.
Due to its nature, `Batch database update` cannot be used.
This feature will consume more traffic and battery. In mobile device or laptop, we can use `Periodic sync` alternatively.

## Periodic sync

Enable this option we you want to synchronise regularly. If enabled this option, replication will been started in each configured seconds.

## What will happen if we don't enable both options?

Replication will not run except our interaction or any other synchronise option.

## Some devices are set to LiveSync, other devices are set to Periodic, and another is set to manual, does it make any trouble?

No. This is the ideal configuration.

## Any other synchronise options

### Sync on save
Synchronise when note has been changed.
Changes in other devices will be reflected when we have modified notes. It maybe make us frustrated.

### Sync on FIle Open
Synchronise when note has been changed.
Changes in other devices will be reflected when we have opened the note, if we have kept the note be opened, also we be frustrated.

### Sync on Start
Synchronise when Obsidian has been started.
Totally fine, when we had enabled all of `Any other synchronise options` and make sure to shutdown Obsidian after editing on each device.

These three options are only recommended in certain situations (i.e., on limited network on a workplace.)
