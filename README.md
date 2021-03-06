# Ansible-Alex
<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Ansible Alex](#ansible-alex)
	- [Purpose](#purpose)
	- [Usage](#usage)
		- [Examples](#examples)
		- [Only on one host](#only-on-one-host)
		- [Specifying a tag](#specifying-a-tag)
		- [Specifying multiple tags](#specifying-multiple-tags)
		- [Skip specifying a tag](#skip-specifying-a-tag)
		- [Skip specifying multiple tags](#skip-specifying-multiple-tags)
		- [Both](#both)
	- [Notes](#notes)
		- [Failed to set permissions on the temporary files Ansible needs to create when becoming an unprivileged user](#failed-to-set-permissions-on-the-temporary-files-ansible-needs-to-create-when-becoming-an-unprivileged-user)
	- [Available tags](#available-tags)
		- [Docker](#docker)
		- [Services](#services)

<!-- /TOC -->
## Purpose
This repository's purpose is to learn how to use ansible, it is made to deploy docker and services as well as some apt repositories on 3 distant server. So this repo has a teaching purpose and not a practical one !

## Usage

```
./alexsible -i inventory/hosts.yml playbook.yml
```


### Examples

### Only on one host
```
./alexsible -i inventory/hosts.yml playbook.yml -l hostentry
```

### Specifying a tag
```
./alexsible -i inventory/hosts.yml playbook.yml -t "test"
```

### Specifying multiple tags
```
./alexsible -i inventory/hosts.yml playbook.yml -t "test" -t "test2"
```

### Skip specifying a tag
```
./alexsible -i inventory/hosts.yml playbook.yml --skip-tags "github_key_import"
```

### Skip specifying multiple tags
```
./alexsible -i inventory/hosts.yml playbook.yml --skip-tags "tag1,tag2,tag3"
```

### Both
```
./alexsible -i inventory/hosts.yml playbook.yml -l hostentry -t "test"
```

### Reboot only designated machines
```
./alexsible -i inventory/hosts.yml playbook.yml -l "host1, host2, ..." -t "reboot"
```

## Notes

### Failed to set permissions on the temporary files Ansible needs to create when becoming an unprivileged user

If you get an error similar to:  
```
fatal: [ponsfrilus]: FAILED! => {"msg": "Failed to set permissions on the temporary files Ansible needs to create when becoming an unprivileged user (rc: 1, err: chown: changing ownership of '/var/tmp/ansible-tmp-1586959025.216097-122038295697183/': Operation not permitted\nchown: changing ownership of '/var/tmp/ansible-tmp-1586959025.216097-122038295697183/AnsiballZ_stat.py': Operation not permitted\n}). For information on working around this, see https://docs.ansible.com/ansible/become.html#becoming-an-unprivileged-user"}
```
be sure that the `acl` package is installed on the host.

It's also can be workarounded with an `ansible.cfg` file in the project's root, with:  
```
[defaults]
allow_world_readable_tmpfiles=true
```

## Available tags

### Docker
```
./alexsible -i inventory/hosts.yml playbook.yml -t docker
```

### Services
```
./alexsible -i inventory/hosts.yml playbook.yml -t services
```
