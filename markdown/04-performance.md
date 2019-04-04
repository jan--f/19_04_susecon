<!-- .slide: data-state="section-break-2" id="Performance" data-timing="10s" -->
# Performance


<!-- .slide: class="col-container" data-state="normal" id="perf-intro" data-menu-title="Performance" -->
## Basic hardware performance

<div class="col-container">

<div class="col">
<h3>Cluster hardware</h3>
<ul>
<li>Ceph on 8 node
  <ul>
  <li>5 OSD nodes – 24 cores – 128 GB RAM</li>
  <li>16 OSD daemons per node – 1 per SSD, 5 per NVME</li>
  <li>3 MON/MDS nodes – 24 cores – 128 GB RAM</li>
  </ul></li>
<li>9 client nodes
  <ul>
  <li>16 cores – 64 GB RAM</li>
  </ul></li>
</ul>
</div>

<div class="col">
<h3>Basic networking performance</h3>
<ul>
<li>25G networking, 25G to 100G interfaces</li>
<li>Client node -> OSD node 25Gbit/s</li>
<li>Multiple client nodes -> OSD node 72 Mbit/s</li>
<li>OSD Node -> OSD Node 68 Mbit/s</li>
</ul>
</div>

</div>

### OSD devices
* 2 x Intel® SSD DC P3700 Series 800GB, 1/2 Height PCIe 3.0, 20nm, MLC
* 5 x Intel® SSD DC S3700 Series 400GB, 2.5in SATA 6Gb/s, 25nm, MLC

Note:
* 5 SSDs and 2 NVMes per node
* Total of 80 OSDs

<table>
<tr>
<td></td><td>4k Random Read/Write</td><td>4k Sequential Read/Write</td><td>4m Sequential
Read/Write</td>
</tr>
<tr>
<td>SSD</td><td></td><td></td><td></td>
</tr>
<tr>
<td>NVMe</td><td></td><td></td><td></td>
</tr>
</table>

<h3>Tuning</h3>
<ul>
<li>Enable `blk-mq` IO scheduler</li>
<li>Disable Spectre/Metldown mitigations</li>
<li>Alter a number of kernel level networking parameters</li>
</ul>


<!-- .slide: class="col-container" data-state="normal" id="perf-experiment" data-menu-title="Experiment description" -->
## Work loads

### Experiments

* Each client (thread) operates on 100 4MB files
* Sequential IO in 4k and 4M blocksizes
* `fsync` every 64 IO operations
* 10 minutes runtime with 2 minutes ramp time
* 7 clients, various process counts per client


<!-- .slide: data-state="normal" class="full-screen" id="cephs-bandwidth" data-menu-title="CephFS Bandwidth" data-timing="10s" -->
<img alt="CephFS bandwidth" src="images/cephfs_bw.png"/>


<!-- .slide: data-state="normal" class="full-screen" id="cephfs-iops" data-menu-title="CephFS IOps" data-timing="10s" -->
<img alt="CephFS IOps" src="images/cephfs_iops.png"/>


<!-- .slide: data-state="normal" class="full-screen" id="cephfs-lats" data-menu-title="CephFS latencies" data-timing="10s" -->
<img alt="CephFS latencies" src="images/cephfs_lats.png"/>


<!-- .slide: data-state="normal" class="full-screen" id="osd-load" data-menu-title="OSD Load" data-timing="10s" -->
<img alt="OSD load" src="images/osd_host_load.png"/>


<!-- .slide: data-state="normal" class="full-screen" id="client-cpu" data-menu-title="Client CPU" data-timing="10s" -->
<img alt="Client cpu utilisation" src="images/cephfs_client_cpu.png"/>


<!-- .slide: data-state="normal" class="full-screen" id="client-ram" data-menu-title="Client memory utilisation" data-timing="10s" -->
<img alt="Client memory utilisation" src="images/cephfs_client_mem.png"/>


<!-- .slide: data-state="section-break" id="fin" data-timing="60s" -->
# Thank you - Questions?

<div style="color: #02d35f; padding-top: 300px;">
<span style="font-weight: bold;">
Many Thanks to
<a style="color: #02d35f !important;" href="https://github.com/aspiers/presentation-template">Adam Spiers</a> ,
<a style="color: #02d35f !important;" href="https://github.com/fghaas/presentation-template/">Florian Haas</a> and 
<a style="color: #02d35f !important;" href="https://github.com/hakimel/reveal.js/">Hakim El-Hattab and contributors</a>
</span>
</div>


<!-- .slide: data-state="normal" id="aux-fio" data-menu-title="fio example job" data-timing="10s" -->
# fio example job

```
[global]
directory=/run/ceph_bench/1:/run/ceph_bench/2:/run/ceph_bench/3:/run/ceph_bench/4:/run/ceph_bench/5:/run/ceph_bench/6:/run/ceph_bench/7
unlink=1
wait_for_previous=1
filesize=4m
nrfiles=100
ramp_time=2m
time_based=1
runtime=10m
#size shouldn't be reached due to runtime
size=100G
fsync=64
numjobs=64

[64rw_4k_rw]
rw=rw
blocksize=4k
```
