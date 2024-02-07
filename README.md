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
# Standard Container 
A simple integration test involves ghcr.io/iotopen/edge-client:latest
## Docker bridge 
Sometimes the IP-address assigned by DHCP conflicts with the default ip for docker. 
If so modify daemon.json 
<pre>
cat /etc/docker/daemon.json 
{
	    "bip": "192.168.100.1/24"
}
</pre>
## Download and start container 
<pre>
  docker run -t -i  -p 8088:80 ghcr.io/iotopen/edge-client:latest
</pre>
Verify that container is running 
<pre>
  docker ps -a 
CONTAINER ID   IMAGE                                COMMAND                  CREATED      STATUS      PORTS                                   NAMES
51981b5a88f1   ghcr.io/iotopen/edge-client:latest   "/opt/iotopen/edge/s…"   3 days ago   Up 3 days   0.0.0.0:8088->80/tcp, :::8088->80/tcp   gracious_blackwell
</pre>
## Verify with browser 
The login page should be displayed 
<pre>
  $ firefox http://172.17.10.244:8088/
</pre>

# Wolfi Container 
<br>
<A HREF="https://edu.chainguard.dev/chainguard/chainguard-images/how-to-use-chainguard-images/">Howto</A>
<br>
<br>

<pre>
 echo "Hello Wolfi" > index.html
 docker run -d -p 8080:8080 -v $PWD/index.html:/usr/share/nginx/html/index.html cgr.dev/chainguard/nginx
</pre>
## Verify with browser 
Expect Hello Wolfi in the browser
<pre>
  $ firefox http://172.17.10.244:8080/
</pre>
# Roadmap 
## V1.0 
With the upcoming regulations CRA and NIS2, vulnerabilities must be handled for the entire lifecycle of the product. 
The <A HREF="https://github.com/hans-lammda/brconf">Cross compiler</A> is critical and must be provided as source code.
<br>
The current software must use the same compiler for all layers. 
<br>

| Layer    | Prototyping | Workshop 2024-01-30| April 2024-04-10|
|----------|----------|----------|----------|
| Container | N/A   | Chainguard <br> Debian <br> Static Golang |IO ports via /sys and /dev <br> portianer.io|
| Linux Kernel   | Kernel tree and toolchain provided by MSC   | N/A   |Linaro GCC |
| Hypervisor  | N/A   | N/A    |N/A|
| Bootloader  | N/A   | N/A   |Linaro GCC|
| Firmware   | N/A   | N/A   |Linaro GCC| 




