# Tidbits
Some random tidbits of information captured along the way per components in a Hadoop stack.

## Ambari/Cloudera Manager
* Make sure to follow recommendations from Ambari/Cloudera Manager except when there is justification for change.

## Hive
* Use `beeline` if you want authorization to take place via Ranger/Sentry
  * `hive` cli avoids all authorization checks

## HBase
* Region server failure can cause 10s of seconds of downtime when configured with the default settings.

## Ranger
* Adding/removing users/groups from Ranger doesn't change users/groups on the cluster.
* Users and groups synced via Ranger Usersync serve two purposes:
  * Policy auto-completion drop-downs
  * Policy edit authorization 

## Storm
* Always anchor tuples when emitting to get accurate counts
* Check that `topology.max.spout.pending` is set properly for your topology
* Make sure that `topology.users/groups` and/or `logs.users/groups` are set per topology
* Make execute code as efficient as possible

## ZooKeeper
* Make sure `autopurge.purgeInterval` and `autopurge.snapRetainCount` are set to avoid ZooKeeper taking up lots of disk space