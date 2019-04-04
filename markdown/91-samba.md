<!-- .slide: data-state="normal" id="samba-intro" data-menu-title="Samba Introduction" -->
## Samba Introduction
* File and print server
  * SMB / CIFS, SMB2 and SMB3+ dialects
* Authentication
  * NTLMv2 and Kerberos
* Identity mapping
  * Windows SIDs to uids and gids
  * Active Directory domain member

Note:
* First released in 1992 by Tridge of rsync + ccache fame
* if you own a router then you probably have a Samba deployment


<!-- .slide: data-state="normal" id="samba-gw-intro" data-menu-title="Samba Gateway for CephFS" -->
## Samba Gateway for CephFS
* Samba VFS layer for filesystem abstraction
  * Ceph VFS module provides libcephfs callouts
* One or more nodes "proxy" SMB traffic through to CephFS
* Samba performs authentication and ID mapping
  * static CephX credentials per Samba gateway

Note:
* Similar to VFS modules already supported with SLES
  * vfs\_btrfs, vfs\_snapper, etc.
* vfs\_default or vfs\_ceph?
  * both supported with SES6
  * kernel provides (much) better performance but less flexibility
    * upgrades and future lease/oplock support


<!-- .slide: data-state="normal" id="samba-gw-intro-arch" data-menu-title="Samba Gateway for CephFS" -->
## Samba Gateway for CephFS
<img alt="Samba Gateway for CephFS" src="images/ceph-samba/samba-intro-arch.png"\>

Note:
* diag should also show ceph\_snapshots and winbind?


<!-- .slide: data-state="normal" id="ctdb-intro" data-menu-title="Samba Clustering with CTDB" -->
## Samba Clustering with CTDB
* Clustered Trivial Database (CTDB)
* Share state across multiple Samba nodes
  * Key-value store
  * Reliable messaging
* Active / Active
* HA features
* Monitoring and failover

Note:


<!-- .slide: data-state="normal" id="ctdb-further" data-menu-title="Clustering with CTDB" -->
## Clustering with CTDB
* Record location master and data master
* Elected recovery master monitors state of cluster
  * Performs database recovery if necessary
* Cluster-wide mutex used to prevent split brain
  * Uses Ceph RADOS object lock
* connections to public IPs are tracked
  * reset on IP failover
  * gratuitous ARP and "Tickle" clients

Note:
* Location determined by hash of key and active node map
* data master moves around based on use
* future: Witness protocol + Persistent handles for seamless failover


<!-- .slide: data-state="normal" id="gw-limitations" data-menu-title="Gateway Limitations" -->
## Gateway limitations
* Cross protocol access
* Performance
* Leases / oplocks
* Clustered node failover
* Load balancing

Note:
* Witness protocol with persistent handles for transparent failover


<!-- .slide: data-state="section-break" data-menu-title="Demonstration" id="Demonstration" -->
# Demonstration
