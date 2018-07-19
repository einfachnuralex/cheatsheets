##

## Bash completion

```
source <(openstack complete)
```

### Domain

https://github.com/AJNOURI/COA/issues/34

```
export OS_IDENTITY_API_VERSION=3 or
openstack --os-identity-api-version 3 domain ...
```

# Operating

## Cinder

https://ask.openstack.org/en/question/66918/how-to-delete-volume-with-available-status-and-attached-to/

### Fix inconsistent Openstack volumes and instances from Cinder and Nova via the database

https://raymii.org/s/articles/Fix_inconsistent_Openstack_volumes_and_instances_from_Cinder_and_Nova_via_the_database.html

```
$ mysql nova_db
> update instances set deleted='1', vm_state='deleted', deleted_at='now()'' where uuid='$vm_uuid' and project_id='$project_uuid';
```

#### Set a volume as detached in Cinder

```
$ mysql cinder_db
> update cinder.volumes set attach_status='detached',status='available' where id ='$volume_uuid';
```

#### Delete a volume from Cinder

```
$ mysql cinder_db
> update volumes set deleted=1,status='deleted',deleted_at=now(),updated_at=now() where deleted=0 and id='$volume_uuid';
```

## Neutron

#### Domains

https://ask.openstack.org/en/question/64458/search-domain-in-resolvconf-not-updating/
https://ask.openstack.org/en/question/26918/change-novalocal-suffix-in-hostname/

#### Neutron API behind SSL terminating haproxy returns http version URL's instead of https

https://bugs.launchpad.net/neutron/+bug/1620967
