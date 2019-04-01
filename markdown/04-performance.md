<!-- .slide: class="col-container" data-state="normal" id="perf-intro" data-menu-title="Performance" -->
## Performance

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

### Raw device performance
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

Note:
<h3>Tuning</h3>
<ul>
<li>Enable `blk-mq` IO scheduler</li>
<li>Disable Spectre/Metldown mitigations</li>
<li>Alter a number of kernel level networking parameters</li>
</ul>

* 6 SSDs and 2 NVMes per node


<!-- .slide: class="col-container" data-state="normal" id="perf-experiment" data-menu-title="Experiment description" -->
## Work loads
