# Role Name

This role sets up fail2ban.

## Requirements

An apt-based system with `fail2ban` in a configured repository.
The role can be used in combination with the [nginx](https://github.com/stuvusIT/nginx) role. 

## Role Variables

### General

| Name | Required/Default | Description |
|------|------------------|-------------|
| `fail2ban_bantime` | `3600` | Time to ban hosts. Can be overwritten for individual jails. |
| `fail2ban_findtime` | `600` | If a hosts exceeds `fail2ban_maxretry` violations within this timeframe it will get banned. Can be overwritten for individual jails. |
| `fail2ban_maxretry` | `3` | Maximum violations until ban. Can be overwritten for individual jails. |
| `fail2ban_enabled` | `False` | Whether to enable all jails by default. |
| `fail2ban_backend` | `systemd` | Default backend used to read logs and detect violations. |
| `fail2ban_logencoding` | `auto` ||
| `fail2ban_ignoreip` | `["127.0.0.1/8"]` | List of IPs that must not get banned. |

### Jails

`fail2ban_jails` is a list of objects with the following attributes:

| Name | Required/Default | Description |
|------|------------------|-------------|
| `name` | :heavy_check_mark: | Name of the jail. |
| `port` | :heavy_check_mark: | Portnumber to check. Is only considered by certain filters. |
| `logpath` | :heavy_check_mark: | Logfile to check. |
| `backend` | :heavy_multiplication_x: | Backend e.g. `systemd` or `auto` |
| `enabled` | `False` | Enables/Disables the jail. |
| `maxretry` | :heavy_multiplication_x: | Maximum violations until ban. |
| `bantime` | :heavy_multiplication_x: | Time to ban hosts. |
| `findtime` | :heavy_multiplication_x: | If a hosts exceeds `fail2ban_maxretry` or respectively `maxretry` violations within this timeframe it will get banned. |
| `filters` | :heavy_multiplication_x: | Name of the filter to be applied. |
| `action` | :heavy_multiplication_x: | Name of the action to be applied if a filter matches. |

## Example Playbook

```
fail2ban_jails:
  - name: wordpress
    port: http,https
    filter: wordpress
    action: nginx
    logpath: "%(nginx_error_log)s"
    backend: "%(default_backend)s"
    enabled: True
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).


## Author Information

- [Adriaan Nieß](https://github.com/AdriaanNiess)
