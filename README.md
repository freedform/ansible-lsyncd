# lsyncd

lsyncd role

## Table of contents

- [Requirements](#requirements)
- [Default Variables](#default-variables)
  - [lsyncd_actions](#lsyncd_actions)
  - [lsyncd_config](#lsyncd_config)
  - [lsyncd_config_base](#lsyncd_config_base)
  - [lsyncd_config_file](#lsyncd_config_file)
  - [lsyncd_inotify_mode](#lsyncd_inotify_mode)
  - [lsyncd_insist](#lsyncd_insist)
  - [lsyncd_log_base](#lsyncd_log_base)
  - [lsyncd_log_file](#lsyncd_log_file)
  - [lsyncd_max_processes](#lsyncd_max_processes)
  - [lsyncd_nodaemon](#lsyncd_nodaemon)
  - [lsyncd_state_action](#lsyncd_state_action)
  - [lsyncd_status_file](#lsyncd_status_file)
  - [lsyncd_status_interval](#lsyncd_status_interval)
  - [lsyncd_version](#lsyncd_version)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Requirements

- Minimum Ansible version: `2.20`

## Default Variables

### lsyncd_actions

List of actions the role does, accepts one or more actions.
Use comma without spaces as a delimiter for multiple actions.

**_Required:_** `true`<br />
**_Type:_** String<br />

#### Example usage

```YAML
  lsyncd_actions: install
  lsyncd_actions: install,deploy_config
```

### lsyncd_config

Maps local source directories to a list of remote rsync targets, allowing
a single source to be synced to more than one remote host.
Each target accepts an optional `host_verification` key ("yes" by default),
passed to ssh as StrictHostKeyChecking. Only set it to "no" if you
understand this disables verification of the remote host's identity.

**_Required:_** `true`, only when action is deploy_config<br />
**_Type:_** Dict of Lists<br />

#### Example usage

```YAML
lsyncd_config:
  /var/www/html:
    - rsync_user_name: rsync_user
      rsync_host_ip: 192.168.1.10
      rsync_host_port: '22'
      rsync_user_key: /home/rsync_user/.ssh/id_ed25519
      destination_dir: /var/www/html
      delete: 'true'
      delay: 5
      host_verification: yes
    - rsync_user_name: rsync_user
      rsync_host_ip: 192.168.1.11
      rsync_host_port: '22'
      rsync_user_key: /home/rsync_user/.ssh/id_ed25519
      destination_dir: /var/www/html
      delete: 'true'
      delay: 5
```

### lsyncd_config_base

Base directory for lsyncd configuration files

**_Type:_** String<br />

#### Default value

```YAML
lsyncd_config_base: /etc/lsyncd
```

### lsyncd_config_file

Path to the main lsyncd configuration file

**_Type:_** String<br />

#### Default value

```YAML
lsyncd_config_file: '{{ lsyncd_config_base }}/lsyncd.conf.lua'
```

### lsyncd_inotify_mode

inotify event type that triggers a sync (CloseWrite, Modify, or CloseWrite or Modify)

**_Type:_** String<br />

#### Default value

```YAML
lsyncd_inotify_mode: CloseWrite
```

### lsyncd_insist

Keep retrying on startup errors when true

**_Type:_** String<br />

#### Default value

```YAML
lsyncd_insist: 'true'
```

### lsyncd_log_base

Base directory for lsyncd log files

**_Type:_** String<br />

#### Default value

```YAML
lsyncd_log_base: /var/log/lsyncd
```

### lsyncd_log_file

Path to the lsyncd log file

**_Type:_** String<br />

#### Default value

```YAML
lsyncd_log_file: '{{ lsyncd_log_base }}/lsyncd.log'
```

### lsyncd_max_processes

Maximum number of rsync processes running simultaneously

**_Type:_** Integer<br />

#### Default value

```YAML
lsyncd_max_processes: 1
```

### lsyncd_nodaemon

Run lsyncd in foreground instead of as a daemon when true

**_Type:_** String<br />

#### Default value

```YAML
lsyncd_nodaemon: 'false'
```

### lsyncd_state_action

Target state for the lsyncd daemon

**_Required:_** `true`, only when action is state_control<br />
**_Type:_** String<br />

#### Example usage

```YAML
  lsyncd_state_action: restarted
```

### lsyncd_status_file

Path to the lsyncd status file

**_Type:_** String<br />

#### Default value

```YAML
lsyncd_status_file: '{{ lsyncd_log_base }}/lsyncd.status'
```

### lsyncd_status_interval

Interval in seconds for writing the status file

**_Type:_** Integer<br />

#### Default value

```YAML
lsyncd_status_interval: 20
```

### lsyncd_version

Lsyncd package version to install

**_Type:_** String<br />

#### Default value

```YAML
lsyncd_version: 2.2.3-1
```

## Dependencies

None.

## License

MIT

## Author

freedform
