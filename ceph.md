# Operating

ceph status
```
ceph -s
```

Pool ops (http://docs.ceph.com/docs/master/rados/operations/pools/)

```
ceph osd lspools
rados df
ceph osd pool get <pool name> all
```

rbd list images

```
rbd ls <poolname>
```

Create pool

```
ceph osd pool create {pool-name} {pg-num} [{pgp-num}]
```

Pool sizes

```
ceph df
```

Pool stats

```
ceph osd pool stats
```

Result:
```
pool docker_swarm_ace_test id 1
  client io 100516 B/s rd, 3850 B/s wr, 37 op/s rd, 7 op/s wr

pool k8s_ace_test id 2
  nothing is going on

pool benchmark id 3
  nothing is going on
```

## Check

check bluestore (http://docs.ceph.com/docs/master/rados/operations/bluestore-migration/)
```
ceph osd metadata | grep osd_objectstore
ceph osd count-metadata osd_objectstore
```

# Authentication

List users

```
ceph auth list
```

Auth as user

```
ceph -n client.admin --keyring=/etc/ceph/ceph.client.admin.keyring health
ceph -n client.k8s --keyring=/etc/ceph/ceph.client.k8s.keyring -s
```

Create user

```
ceph auth add client.john mon 'allow r' osd 'allow rw pool=liverpool'
ceph auth get-or-create client.k8s mon 'profile rbd' osd 'profile rbd pool=k8s_ace_test'
```

# Maintenance

## Boot OSD

Before reboot OSD node

```
ceph osd set noout
```

After reboot

```
ceph osd unset noout
```

## Upgrade cluster

http://docs.ceph.com/docs/luminous/install/upgrading-ceph/

Sequence:
  * Monitors
  * OSD Daemons
  * Metadata Servers
  * Object Gateways

Upgrade monitors first

```
ceph-deploy install --release luminous mon1 mon2 mon3
```
> Restart services on mons!!!

Upgrade OSDs

```
ceph osd set noout
ceph-deploy install --release luminous osd1 osd2 osd3
ceph osd unset noout
```
> Restart services on osds!!!


Monitor upgrade of OSDs

```
ceph osd tree
```

See version of local components

```
ceph version
```

See versions of all components

```
ceph versions
```

Upgrade osd features from jewel to luminous. After all osds are migrated
https://www.virtualtothecore.com/en/upgrade-ceph-cluster-luminous/

```
ceph osd require-osd-release luminous
```



# Install ceph

Become ceph-deploy user
```
su - ceph-deploy
```

Install ceph on all nodes
```
ceph-deploy install frvpfsl007-ceph frvpfsl008-ceph frvpfsl009-ceph frvpfsl010-ceph frvpfsl011-ceph frvpfsl012-ceph
# Luminous
ceph-deploy install --release luminous ceph1 ceph2 ceph3
```

Init new cluster
```
ceph-deploy new frvpfsl007-ceph
```

Add public_network to ceph.conf
```
echo "public network = 10.16.34.0/24" > ceph.conf
```

Create initial mon
```
ceph-deploy mon create-initial
```

Copy admin keys
```
ceph-deploy admin frvpfsl007-ceph frvpfsl008-ceph frvpfsl009-ceph frvpfsl010-ceph frvpfsl011-ceph frvpfsl012-ceph

```

Add other mon

> http://tracker.ceph.com/issues/8861
```
ceph-deploy --overwrite-conf mon create frvpfsl008-ceph frvpfsl009-ceph
```

Create all osd
```
ceph-deploy osd create frvpfsl010-ceph:vdb frvpfsl011-ceph:vdb frvpfsl012-ceph:vdb
# Luminous
ceph-deploy osd create --bluestore ceph1:vdb ceph2:vdb ceph3:vdb
```

## Add mds & mgr (Luminous)
```
ceph-deploy mds create ceph1
ceph-deploy mgr create ceph1
ceph mgr module enable dashboard
```

## Create Object Gateway (radosgw)

http://docs.ceph.com/docs/master/install/install-ceph-gateway/

```
ceph-deploy rgw create ceph1
```

Change default port 7480 to 80 in ceph.conf

```
[client.rgw.<rgw-nodename>]
rgw_frontends = "civetweb port=80"
```

Create realm

```
radosgw-admin realm create --rgw-realm={realm-name} [--default]
```

Create User

```
radosgw-admin user create --uid="testuser" --display-name="First User"
```

Result:

```json
{
    "user_id": "testuser",
    "display_name": "First User",
    "email": "",
    "suspended": 0,
    "max_buckets": 1000,
    "auid": 0,
    "subusers": [],
    "keys": [
        {
            "user": "testuser",
            "access_key": "TZPYZ3E2XI4F3CSWGW26",
            "secret_key": "SuwRVFOAOClFWaUjmryfwPX7JRkNOR3AoOehEGwX"
        }
    ],
    "swift_keys": [],
    "caps": [],
    "op_mask": "read, write, delete",
    "default_placement": "",
    "placement_tags": [],
    "bucket_quota": {
        "enabled": false,
        "check_on_raw": false,
        "max_size": -1,
        "max_size_kb": 0,
        "max_objects": -1
    },
    "user_quota": {
        "enabled": false,
        "check_on_raw": false,
        "max_size": -1,
        "max_size_kb": 0,
        "max_objects": -1
    },
    "temp_url_keys": [],
    "type": "rgw"
}
```

Add capabilities to user

```
radosgw-admin caps add --uid=testuser --caps="users=*;buckets=*
```

Result:

```json
{
    "user_id": "testuser",
    "display_name": "First User",
    "email": "",
    "suspended": 0,
    "max_buckets": 1000,
    "auid": 0,
    "subusers": [],
    "keys": [
        {
            "user": "testuser",
            "access_key": "TZPYZ3E2XI4F3CSWGW26",
            "secret_key": "SuwRVFOAOClFWaUjmryfwPX7JRkNOR3AoOehEGwX"
        }
    ],
    "swift_keys": [],
    "caps": [
        {
            "type": "buckets",
            "perm": "*"
        },
        {
            "type": "users",
            "perm": "*"
        }
    ],
    "op_mask": "read, write, delete",
    "default_placement": "",
    "placement_tags": [],
    "bucket_quota": {
        "enabled": false,
        "check_on_raw": false,
        "max_size": -1,
        "max_size_kb": 0,
        "max_objects": -1
    },
    "user_quota": {
        "enabled": false,
        "check_on_raw": false,
        "max_size": -1,
        "max_size_kb": 0,
        "max_objects": -1
    },
    "temp_url_keys": [],
    "type": "rgw"
}
```

Get user info

```
radosgw-admin user info --uid backup
```

ceph.conf:

```
[client.rgw.ceph1]
rgw_frontends = "civetweb port=80"
```

Copy config to node

```
ceph-deploy --overwrite-conf config push ceph1
```

Restart service

```
systemctl restart ceph-radosgw@rgw.ceph1.service
```

Test S3 in python

```python
import boto
import boto.s3.connection
access_key = 'TZPYZ3E2XI4F3CSWGW26'
secret_key = 'SuwRVFOAOClFWaUjmryfwPX7JRkNOR3AoOehEGwX'

conn = boto.connect_s3(
        aws_access_key_id = access_key,
        aws_secret_access_key = secret_key,
        host = 'gw.psynet.lan',
        is_secure=False,
        calling_format = boto.s3.connection.OrdinaryCallingFormat(),
        )

bucket = conn.create_bucket('alex-test')

for bucket in conn.get_all_buckets():
        print "{name}\t{created}".format(
                name = bucket.name,
                created = bucket.creation_date,
        )
```

# Playing
```
ceph osd pool create mypool 8
ceph quorum_status --format json-pretty
ceph --show-config
```

# Influx plugin

http://docs.ceph.com/docs/master/mgr/influx/

```
ceph mgr module enable influx
ceph config-key set mgr/influx/hostname 192.168.2.55
ceph config-key set mgr/influx/port 8086
ceph config-key set mgr/influx/database ceph
```

Install python influxdb

```
apt install python3-influxdb python-influxdb
```

# benchmark

http://tracker.ceph.com/projects/ceph/wiki/Benchmark_Ceph_Cluster_Performance
https://github.com/fghaas/chosug-march-2015/blob/master/markdown/benchmark.md

# Only for testing!!
## Purge all configuration
```
ceph-deploy purge frvpfsl007-ceph frvpfsl008-ceph frvpfsl009-ceph
ceph-deploy purgedata frvpfsl007-ceph frvpfsl008-ceph frvpfsl009-ceph
ceph-deploy forgetkeys
```

# Troubleshooting

## Pools

### applicatins on pools

http://tracker.ceph.com/issues/20891
https://ceph.com/community/new-luminous-pool-tags/

```
application not enabled on 3 pool(s)
```

Enable applications for pools

```
ceph osd pool application enable <pool> <rbd|rgw|cephfs>
```

## RadosGW

### Common

```
ceph daemon /var/run/ceph/ceph-client.rgw.kavtfsl012-rgw.asok help
```

### RadosGW error reshard

http://tracker.ceph.com/issues/20289
http://docs.ceph.com/docs/master/radosgw/dynamicresharding/

```
Mar 20 10:44:58 kavtfsl012-rgw radosgw[68275]: 2018-03-20 10:44:58.412325 7f1567cec700 -1 ERROR: failed to list reshard log entries, oid=reshard.0000000000
```

Upgrade all mons and osds to luminous!!!
