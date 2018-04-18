# Filebeat

Setup a filebeat instance.


## Requirements

An apt based linux system

## Role Variables


| Variable           | Default / Mandatory                                                                                                                                  | Description                                                                                                                                                                                                                                              |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `filebeat_config`  | `{ output.elasticsearch: { hosts: ["localhost:9200"] }, filebeat.config.modules: { path: ${path.config}/modules.d/*.yml , reload.enabled: false } }` | Since the filebeat settings file is a yaml file we write the whole object to the settings file. For more Information please see the [filebeat settings file documentation](https://www.elastic.co/guide/en/filebeat/current/filebeat-settings-file.html) |
| `filebeat_modules` | `{}`                                                                                                                                                 | Dict of config files to write to modules.d/. More information below.                                                                                                                                                                                     |

### `filebeat_modules`
Each entry in the `filebeat_modules` consists out of the following entries.
The key of each entry is used to determine the name of the config file and the content of the entry is writen to the config file

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
      nginx:
        access:
          enabled: true
        error:
          enabled: true
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).


## Author Information

- [Fritz Otlinghaus (Scriptkiddi)](https://github.com/scriptkiddi) _fritz.otlinghaus@stuvus.uni-stuttgart.de_
