heartbleed-docker-container
===========================

Dockerfile to create a Heartbleed-able interactive container

Usage
=====

Build image and spawn an interactive shell:

```
wget -O /tmp/Dockerfile.heartbleed https://raw.githubusercontent.com/rcmorano/heartbleed-docker-container/master/Dockerfile
cat /tmp/Dockerfile.heartbleed | docker build -t rcmorano/heartbleed -
docker run -t -i rcmorano/heartbleed
```

Run 'Heartbleed':

```
root@f3a2fa2eef5b:/# Heartbleed 
This is a tool for detecting OpenSSL Heartbleed vulnerability (CVE-2014-0160).

Usage:

	Heartbleed server_name(:port)
	
	The default port is 443 (HTTPS).
root@f3a2fa2eef5b:/# 
```

Notes
=====

Base image used is [jayofdoom/docker-ubuntu-14.04](https://github.com/jayofdoom/docker-ubuntu-14.04), the first ubuntu-14.04 trusted image I found doing 'docker search'.
