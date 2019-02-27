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


<!-- .slide: data-state="normal" id="intro-ceph" data-menu-title="Ceph Introduction" -->
## Ceph Introduction
* Distributed storage system based on RADOS
  * Scalable
  * Fault tolerant
  * Self-healing and self-managing
* Various client access modes
  * Object storage
  * remote block device
  * POSIX compatible file system
  * _Your applicaton_


<!-- .slide: data-state="normal" id="intro-arch" data-menu-title="Ceph Introduction" -->
## Ceph Architecture
<img alt="Ceph Architecture" src="images/ceph-architecture.png" height="80%"/>


<!-- .slide: data-state="normal" id="intro-arch" data-menu-title="Ceph Introduction" -->
## CephFS Introduction

<h3>
POSIX compatible clustered file system atop Ceph
</h3>

* File access is important in storage
  * Allows existing applications to utilize Ceph storage
  * Interoperability with existing infrastructure
  * Directories and permissions
  * Elastic capacity

