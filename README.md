# sbt

Ansible role to install and configure SBT (Scala Build Tool).

## Requirements

- Ubuntu 22.04 or later

## Role Variables

### `sbt_users` (list)

List of users to configure with SBT. Each user can optionally have Sonatype credentials configured.

```yaml
sbt_users:
  - username: fabrizio
    sbt_sonatype:
      username: sona_fabrizio
      password: Passw0rd
```

### `sbt_global_opts` (dict)

System-wide SBT options deployed to `/etc/sbt/sbtopts`. Supports all standard SBT options including `allow_empty`, `mem`, `no_share`, `coursier`, `ivy`, `global`, `supershell`, `task.timings`, `jvm_properties`, and more.

See `defaults/main.yml` for the full list of supported options and their descriptions.

### `sbt_global_config` (string)

User-global SBT configuration appended to each user's `~/.sbt/global.sbt`. Use this to add custom SBT settings that apply per-user.

## Example Playbook

### Basic installation

```yaml
- hosts: servers
  roles:
    - role: sbt
```

### With Sonatype credentials and global options

```yaml
- hosts: servers
  roles:
    - role: sbt
      sbt_users:
        - username: fabrizio
          sbt_sonatype:
            username: ColOfAbRiX
            password: Passw0rd
      sbt_global_opts:
        allow_empty: true
        no_share: true
        coursier:
          enabled: "true"
        ivy:
          enabled: "true"
          home: "~/.ivy2"
```

## Files Deployed

| File | Purpose |
|------|---------|
| `/etc/sbt/sbtopts` | System-wide SBT options |
| `~/.sbt/global.sbt` | Per-user global configuration |
| `~/.sbt/sonatype_central_credentials` | Per-user Sonatype credentials |

## License

MIT

## Author Information

Fabrizio Colonna <colofabrix@tin.it>

## Contributors

Pull requests are also welcome. Please create a topic branch for your proposed changes.
