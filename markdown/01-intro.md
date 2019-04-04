<!-- .slide: data-state="cover" id="intro-cover" data-timing="20" data-menu-title="Introduction" -->
<div class="title">
    <h1>CephFS and Samba</h1>
    <h2>Scale-out file serving for the Masses</h2>
</div>

<div class="row presenters">
    <div class="presenter presenter-1">
        <h3 class="name">David Disseldorp</h3>
        <h3 class="job-title">Senior Software Engineer</h3>
        <h3 class="email"><a href="mailto:david.disseldorp@suse.com">david.disseldorp@suse.com</a></h3>
    </div>
    <div class="presenter presenter-2">
        <h3 class="name">Jan Fajerski</h3>
        <h3 class="job-title">Senior Software Engineer</h3>
        <h3 class="email"><a href="mailto:jan.fajerski@suse.com">jan.fajerski@suse.com</a></h3>
    </div>
</div>


<!-- .slide: data-state="normal" id="qrcode-intro" data-menu-title="QR code" data-timing="0" -->

<div class="qrcode" id="qrcode-talk-intro"/>
<h2 style="text-align: center;"><a href="https://jan--f.github.io/19_04_susecon/" target="_blank"
       id="talk-intro">https://jan--f.github.io/19_04_susecon/</a></h2>


<!-- .slide: data-state="normal" id="intro-agenda" data-menu-title="Agenda" -->
## Agenda

* Quick intro
* Spotlight on a few (new) features
* Samba Gateway
* Performance numbers


<!-- .slide: data-state="normal" id="intro-ceph" data-menu-title="Ceph Introduction" -->
## Ceph Introduction
* **Distributed storage system based on RADOS**
  * Scalability by design
  * Fault tolerant
  * Self-healing and self-managing
* **Unified storage cluster**
  * Object storage
  * Block Storage
  * File system (POSIX compatible)
  * _Your applicaton_

Note:
* Originates from a research project at UC Santa Cruz Storage Research Systems Center
* POSIX compatible means not fully compliant but in reality no impact (ext is
  alos not fully compliant)


<!-- .slide: data-state="normal" id="intro-arch" data-menu-title="Ceph Introduction" -->
## Ceph Architecture
<img alt="Ceph Architecture" src="images/ceph-architecture.png"/>

Note:
* Rados is a K/V store based on the CRUSH algorithm
* Implements a form of rendezvous hashing to place data
* Implemented by two daemons MONs and OSDs
* MONs keep consensus on where data is/belongs
* OSDs store data


<!-- .slide: data-state="normal" id="cephfs-arch" data-menu-title="Ceph Introduction" -->
## CephFS Architecture
<img style="max-width: 85%;" alt="CephFS Architecture" src="images/cephfs_arch.png"/>

Note:
* MDS - daemon that manages metadata
* data and metadata is still stored in ceph
* clients talk to OSDs directly
