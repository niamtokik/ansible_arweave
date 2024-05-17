# Arweave Ansible Role

This ansible role has been created to offer an easy way to deploy
ansible on any kind of operating system, from source, and without
using any kind of package. By default, it clones the latest branch and
install all dependencies.

Warning: at this time this role is mainly used for test and
development purpose

## Requirement

Here nodes requirement:

 - More than 4GB of RAM (for mining)
 - At least 4 CPU
 - More than 200GB of dedicated space (for mining)

## Usage

Defaut variables are defined in
[`defaults/main.yml`](defaults/main.yml) where `__arweave` is a
special variable containing default values for each of them. Then,
instead of modifying directly `tasks`, `files`, `templates` or
`handlers`, everything can be done there.

To work, `aeweave` variable MUST BE defined. Here a custom json as
example.

```json
{
  "arweave": {
    "installation_path": "/mnt/custom_volume"
  }
}
```

And the ansible command to deploy it.

```sh
ansible-playbook playbook_arweave.yml --diff --extra-vars '@arweave.json'
```

Where `playbook_arweave.yml` contains tasks to install arweave.

```yml
- hosts: arweave.host
  become_method: sudo
  roles:
    - arweave
```

## Support

| tasks    | ubuntu 20.04 | ubuntu 22.04 | ubuntu 24.04 | debian 12.0 | fedora |
|----------|--------------|--------------|--------------|-------------|--------|
| limits   | -            | yes          | -
| packages | -            | yes          | -
| clone    | -            | yes          | -
| compile  | -            | yes          | -

## TODO

 - [ ] Common
   - [x] user creation
   - [x] group creation
   - [ ] custom data store
 - [ ] Linux Common Configuration
   - [x] file limits
 - [x] Deployment from source with git
   - [x] custom branch
   - [x] custom directory
 - [ ] Ubuntu support
   - [ ] 24.04
   - [x] 22.04
   - [ ] 20.04
 - [ ] Windows Support
   - [ ] Windows 11 
   - [ ] Windows server 2022
   - [ ] Windows server 2019
   - [ ] Windows server 2016
 - [ ] MacOS support
   - [ ] MacOS server
 - [ ] Debian support
   - [x] 12
   - [ ] 11
   - [ ] 10
 - [ ] Fedora support
   - [ ] 40
   - [ ] 39 (can't compile)
 - [ ] AlmaOS support
   - [ ] 9
   - [ ] 8
 - [ ] CentOS support
   - [ ] 9
   - [ ] 8
 - [ ] Rocky support
   - [ ] 9
   - [ ] 8
 - [ ] ArchLinux
 - [ ] AlpineLinux
 - [ ] Gentoo
 - [ ] FreeBSD
 - [ ] OpenBSD
 - [ ] NetBSD
 - [ ] DragonFlyBSD
 - [ ] Promtail logs support

The next step is to create packages infrastructure for all these
systems.

## Tested Deployment

| cat | hosting company | cpu | ram  | type    | os           | note |
|-----|-----------------|-----|------|---------|--------------|------|
|  vm | hetzner         | 2   |  2GB |   cpx11 | ubuntu 22.04 | crash (oom kill)
|  vm | hetzner         | 3   |  4GB |   cpx21 | ubuntu 22.04 | crash (oom kill)
|  vm | hetzner         | 4   |  8GB |   cpx31 | ubuntu 22.04 | no problem so far
|  vm | scaleway        | 2   |  2GB |  dev1-s | -
|  vm | scaleway        | 3   |  4GG |  dev1-m | -
|  vm | scaleway        | 4   |  8GB |  dev1-l | -
|  vm | scaleway        | 4   | 12GB | dev1-xl | -

## Contributing

All roles are set by OS version and release. Please tests these tasks
before deploying.

## FAQ

### How to execute ansible-playblook without ansible host file?

```sh
ansible-playbook -i "${ip_address},"  -u root playbook_arweave.yml -C
```

### On Debian, python interpreter can't be found.

On Debian, `python` does not exist and one should use
`/usr/bin/python3` instead. The following environment variable can be
added:

```
-e 'ansible_python_interpreter=/usr/bin/python3'
```

see https://docs.ansible.com/ansible/latest/reference_appendices/python_3_support.html

## References and Resources

[Arweave Official Website](https://www.arweave.org/)

[Arweave Official Github](https://github.com/ArweaveTeam/arweave)

[Arweave Official Documentation](https://docs.arweave.org/developers)
