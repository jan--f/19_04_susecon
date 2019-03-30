<!-- .slide: data-state="section-break-2" id="CephFS features" data-timing="10s" -->
# CephFS features (a selection)


<!-- .slide: data-state="normal" id="multi-mds" data-menu-title="Scale and HA" -->
## Multiple active MDS daemons
### High availability and scalability

* A failed MDS will bring service down
* Many clients and many files can overwhelm MDS cache

* dir tree is partitioned into ranks (*better explanation*)
* additional MDS daemons will join the cluster as standby's

```bash
systemctl start ceph-mds@your.mds-host.ceph # start an additional mds
```

* increase MDS count

```sh
ceph fs set <cephfs> max_mds 2
```


<!-- .slide: data-state="normal" id="multi-mds-config" data-menu-title="HA config" -->
## Multi MDS configuration
### Failover handling parameters
* *mds_standby_replay*
* *mds_replay_interval*
* *mds_standby_for_X*
* *mds_beacon_grace*

### Control rank partitioning
* automatic partitioning based on load
* pin directories to certain ranks


<!-- .slide: data-state="normal" id="intro-features" data-menu-title="Agenda" -->
## Extended attributes
* customize data placement
* list some attributes to talk about as code


<!-- .slide: data-state="normal" id="intro-features" data-menu-title="Agenda" -->
## Quotas
* Directory based


<!-- .slide: data-state="normal" id="intro-features" data-menu-title="Agenda" -->
## Snapshots
* snapshot a directory tree
* Magic `.snap` directory (name can be configured)
* Take a snapshot: `mkdir .snap/my_snapshots`
* List snapshots: `ls .snap/`
* Delete a snapshot: `rmdir .snap/my_snapshots`
