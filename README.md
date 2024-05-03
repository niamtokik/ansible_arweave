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

## Tested Deployment

| hosting company | cpu | ram | type  | os           | note |
|-----------------|-----|-----|-------|--------------|------|
| hetzner         | 2   | 2GB | cpx11 | ubuntu 22.04 | crash (oom kill)
| hetzner         | 3   | 4GB | cpx21 | ubuntu 22.04 | crash (oom kill)
| hetzner         | 4   | 8GB | cpx31 | ubuntu 22.04 | no problem so far

## Contributing

All roles are set by OS version and release. Please tests these tasks
before deploying.

## References and Resources

[Arweave Official Website](https://www.arweave.org/)

[Arweave Official Github](https://github.com/ArweaveTeam/arweave)

[Arweave Official Documentation](https://docs.arweave.org/developers)
