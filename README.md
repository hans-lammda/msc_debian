# msc_debian
Getting started with MSC  
<ul>  
  <li>Install Debian 12 on Virtualbox</li>
  <li>Add Crosscompiler on Debian </li>
  <ul>
    <li>Compile hello.c as static binary </li>
    <li>Compile hello.c as dynamic binary</li>
    
  </ul>
<li>Pull and run Container on target</li>
</ul>

# Setup 
## Prepare Debian
<pre>
 # apt-get install git make 
 # Add your username to /etc/sudoers 
 # %hans   ALL=(ALL:ALL) ALL
</pre>
## Clone msc_debian repository 
<pre>
  $ git clone https://github.com/hans-lammda/msc_debian.git
  $ cd msc_debian 
</pre>
## Install cross compiler 
<pre>
  $ make -C tools all
</pre>

# Build 
## Static binary 
<pre>
  $ make -C example static
</pre>
## Dynamic binary 
<pre>
  $ make -C example dynamic
</pre> 

# Deploy 
Find out the IP-address of the target 
<pre>
  make -C example deploy TARGET=172.17.10.244
</pre>
# Test 
Log in with ssh to TARGET and execute /tmp/hello and /tmp/hello.static
<pre>
$ ssh root@172.17.10.244
root@172.17.10.244's password: 
# cd /tmp
# ./hello.static 
Hello 
</pre>


