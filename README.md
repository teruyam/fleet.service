# my fleet service files
=============

## Prerequisite
TODO: write system requirements here

## Getting Started

[fleet](https://github.com/coreos/fleet) is a distributed init system and is a cluster management tool.
fleet service files here launch container with discovery sidekick container.

Get repo
```
git clone https://github.com/MasashiTeruya/fleet.service.git && cd fleet.service
```
Launch nginx anyway!

```
$ cd nginx
$ fleetctl start nginx@{1..3} nginx-discovery@{1..3}.service
Job nginx@1.service launched on 367bcc23.../10.0.0.86
Job nginx-discovery@1.service launched on 367bcc23.../10.0.0.86
Job nginx@2.service launched on ca37dc8e.../10.0.0.84
Job nginx@3.service launched on ff566c92.../10.0.0.85
Job nginx-discovery@2.service launched on ca37dc8e.../10.0.0.84
Job nginx-discovery@3.service launched on ff566c92.../10.0.0.85
```

Show units running in your cluster

```
$ fleetctl list-units
UNIT                            DSTATE          TMACHINE                STATE           MACHINE                 ACTIVE
nginx-discovery@1.service       launched        ff566c92.../10.0.0.85   launched        ff566c92.../10.0.0.85   active
nginx-discovery@2.service       launched        ca37dc8e.../10.0.0.84   launched        ca37dc8e.../10.0.0.84   active
nginx-discovery@3.service       launched        367bcc23.../10.0.0.86   launched        367bcc23.../10.0.0.86   active
nginx@1.service                 launched        ff566c92.../10.0.0.85   launched        ff566c92.../10.0.0.85   active
nginx@2.service                 launched        ca37dc8e.../10.0.0.84   launched        ca37dc8e.../10.0.0.84   active
nginx@3.service                 launched        367bcc23.../10.0.0.86   launched        367bcc23.../10.0.0.86   active
```

Find host & port to access using etcd(https://github.com/coreos/etcd)

```
$ etcdctl ls /services --recursive
/services/http
/services/http/nginx
/services/http/nginx/nginx-1
/services/http/nginx/nginx-2
/services/http/nginx/nginx-3

$ etcdctl get /services/http/nginx/nginx-1
{ "host": "10.0.0.85", "port": 49157 }
```
