<!-- .slide: data-state="section-break-2" id="CephFS features" data-timing="10s" -->
# CephFS features (a selection)


<!-- .slide: data-state="normal" id="multi-mds" data-menu-title="Scale and HA" -->
## Multiple MDS daemons
### High availability and scalability

* A failed MDS will bring service down
* Many clients and many files can overwhelm MDS cache
* Directory tree is partitioned into ranks - `max_mds` defaults to 1
* Additional MDS daemons will join the cluster as standby's <!-- .element: class="fragment" data-fragment-index="1" -->

```bash
systemctl start ceph-mds@your.mds-host.ceph # start an additional mds
```
<!-- .element: class="fragment" data-fragment-index="1" -->

* increase MDS count <!-- .element: class="fragment" data-fragment-index="2" -->

```sh
ceph fs set <cephfs> max_mds 2
```
<!-- .element: class="fragment" data-fragment-index="2" -->

Note:
* limiting the rank an MDS can standby for usually calls for more standby
  daemons


<!-- .slide: data-state="normal" id="multi-mds-config" data-menu-title="HA config" -->
## Multi MDS configuration
### Failover handling parameters
* *mds_beacon_grace*
* *mds_standby_replay*
* *mds_replay_interval*
* *mds_standby_for_rank*
* *mds_standby_for_name*

### Control rank partitioning
* Automatic partitioning based on load - hard to beat
* Pin directories (and its sub-directories) to a certain rank
  * Spread periodic loads
  * Prevent particular load from impacting others


<!-- .slide: data-state="normal" id="xattr" data-menu-title="Extended Attrobutes" -->
## Extended attributes
### Many options can be controlled at runtime via `setxattr`

```bash
setfattr -n <attribute.name> -v 1000000 /some/dir # set to 1 million
getfattr -n <attribute.name> /some/dir            # read xattr
setfattr -x <attribute.name> /some/dir            # remove xattr
```

```
ceph.dir.pin
ceph.quota.[max_bytes|max_files]
ceph.[file|dir].layout.[pool|pool_namespace|stripe_unit|stripe_count|object_size]
```

### Caveats
* File and dir layout are inherited at creation time
* Clients need the `p` flag in their cephx key to set quota and layout
  restrictions


<!-- .slide: data-state="normal" id="quotas-features" data-menu-title="Quotas" -->
## Quotas
* Directory based
* Set with xattrs

### Limitation
* Cooperative - needs client cooperation
* Imprecise - rule of thumb: Clients will be stopped within 10s of reaching a
  quota
* Kernel support require >=4.17 kernel and mimic+ cluster
* Path restrictions can interner - Clients need read permission on quota
  directory
* Snapshots of since deleted data does not count - [see bug #24284](http://tracker.ceph.com/issues/24284)


<!-- .slide: data-state="normal" id="intro-features" data-menu-title="Agenda" -->
## Snapshots
* snapshot a directory tree
* Magic `.snap` directory (name can be configured)
* Take a snapshot: `mkdir .snap/my_snapshots`
* List snapshots: `ls .snap/`
* Delete a snapshot: `rmdir .snap/my_snapshots`
