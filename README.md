heartbleed-docker-container
===========================

Dockerfile to create a Heartbleed-able interactive container

Why?
=======

I didn't want to mess with Go in my system so I made a Heartbleed-able container with the tool precompiled and ready to check for the vuln.

Usage
=====

Pull the trusted build:

```
docker pull rcmorano/heartbleed 
```

Or build an image from source Dockerfile:

```
wget -O /tmp/Dockerfile.heartbleed https://raw.githubusercontent.com/rcmorano/heartbleed-docker-container/master/Dockerfile
cat /tmp/Dockerfile.heartbleed | docker build -t rcmorano/heartbleed -
```

Then spawn an interactive shell and run Heartbleed:

```
docker run -t -i rcmorano/heartbleed /bin/bash --login
root@f3a2fa2eef5b:/# Heartbleed 
This is a tool for detecting OpenSSL Heartbleed vulnerability (CVE-2014-0160).

Usage:

	Heartbleed server_name(:port)
	
	The default port is 443 (HTTPS).
root@f3a2fa2eef5b:/# 
```

Or just run Heartbleed directly:

```
localhost:~$ HEARTBLEED_MYNETWORK=$(docker run -d rcmorano/heartbleed /bin/bash -c 'for host in $(seq 1 254); do Heartbleed 192.168.1.$host; done')
localhost:~$ docker logs $HEARTBLEED_MYNETWORK
2014/04/10 17:02:02 192.168.1.1 - ERROR: dial tcp 192.168.1.1:443: network is unreachable
2014/04/10 17:02:05 192.168.1.2 - ERROR: dial tcp 192.168.1.2:443: i/o timeout
...
localhost:~$ docker kill $HEARTBLEED_MYNETWORK
02463beb56161548636452b517e04b7e18237aa9c3986db6cae0e1443ee96a88
localhost:~$
```

Notes
=====

Base image used is [jayofdoom/docker-ubuntu-14.04](https://github.com/jayofdoom/docker-ubuntu-14.04), the first ubuntu-14.04 trusted image I found doing 'docker search'.
