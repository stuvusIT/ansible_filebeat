# Filebeat

Setup a filebeat instance.


## Requirements

An apt based linux system

## Role Variables


| Variable           | Default / Mandatory                                             | Description                                                                                                                                                                                                                                              |
|--------------------|-----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `filebeat_config`  | `{ path: { logs: /var/log/filebeat, data: /var/lib/filebeat }}` | Since the filebeat settings file is a yaml file we write the whole object to the settings file. For more Information please see the [filebeat settings file documentation](https://www.elastic.co/guide/en/filebeat/current/filebeat-settings-file.html) |
| `filebeat_modules` | `{}`                                                            | Dictionary of config files to write to modules.d/. More information below.                                                                                                                                                                               |

### `filebeat_modules`
Each entry in the `filebeat_modules` consits out of the following entries.
| Variable | Default / Mandatory | Description                                                                              |
|----------|---------------------|------------------------------------------------------------------------------------------|
| `name`   | :heavy_check_mark:  | Name of the module config file. This value has to be the same as the name of the module. |
| `config` | :heavy_check_mark:  | Yaml config for the module name .                                                        |

## Example Playbook

```yml
- hosts: all
  become: true
  vars:
    filebeat_config:
      filebeat.config.modules:
        path: ${path.config}/modules.d/*.yml
        reload.enabled: false
      output.logstash:
        hosts: ["localhost:5044"]
    filebeat_modules:
      - name: nginx
        config: 
          access:
            enabled: true
          error:
            enabled: true
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).


## Author Information

- [Fritz Otlinghaus (Scriptkiddi)](https://github.com/scriptkiddi) _fritz.otlinghaus@stuvus.uni-stuttgart.de_
