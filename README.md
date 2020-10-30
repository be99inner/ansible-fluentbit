# Role Name

Ansible role to install and configure Fluentbit.

## Requirements

- Ansible version >= 2.9

## Role Variables

| variables                                   | require | description                                                               | type       | default                 |
| ------------------------------------------- | ------- | ------------------------------------------------------------------------- | ---------- | ----------------------- |
| fluentbit_inputs                            | true    | fluentbit input configuration                                             | list(dict) | []                      |
| fluentbit_outputs                           | true    | fluentbit output configuration                                            | list(dict) | []                      |
| fluentbit_service_flush                     | false   | set an interval of seconds before to flush records to a destination       | number     | 5                       |
| fluentbit_service_daemon                    | false   | instruct Fluent Bit to run in foreground or background mode.              | string     | Off                     |
| fluentbit_service_log_level                 | false   | set the verbosity level of the service                                    | string     | info                    |
| fluentbit_service_parsers_file              | false   | specify an optional 'Parsers' configuration file                          | string     | parsers.conf            |
| fluentbit_service_plugins_file              | false   | specify an optional 'Plugins' configuration file to load external plugins | string     | plugins.conf            |
| fluentbit_service_http_server               | false   | enable/Disable the built-in HTTP Server for metrics                       | string     | Off                     |
| fluentbit_service_http_listen               | false   | setup http server address                                                 | string     | 0.0.0.0                 |
| fluentbit_service_http_port                 | false   | set http server port                                                      | number     | 2020                    |
| fluentbit_service_storage_metrics           | false   | publish storage pipeline metrics in '/api/v1/storage'                     | string     | on                      |
| fluentbit_service_storage_path              | false   | absolute file system path to store filesystem data buffers (chunks)       | string     | "/var/lib/td-agent-bit" |
| fluentbit_service_storage_sync              | false   | configure the synchronization mode used to store the data into the        | string     | normal                  |
| fluentbit_service_storage_checksum          | false   | enable the data integrity check when writing and reading data from the    | string     | off                     |
| fluentbit_service_storage_backlog_mem_limit | false   | this option configure a hint of maximum value of memory                   | string     | 5M                      |
| fluentbit_service_storage_max_chunks_up     | false   | control memory usage                                                      | number     | 128                     |
| fluentbit_service_additional                | false   | additional configuration                                                  | list(dict) | []                      |
| fluentbit_custom_parsers                    | false   | fluentbit custom parser configuration                                     | list(dict) | []                      |
| fluentbit_plugins_paths                     | false   | fluentbit custom plugins configuration                                    | list(dict) | []                      |

more information on [defaults](https://github.com/be99inner/ansible-fluentbit/blob/master/defaults/main.yml)

## Dependencies

None

## Installation

You can install this role via `anslbie-galaxy`.

```sh
ansible-galaxy install be99inner.fluentbit
```

## Example Playbook

Example of playbook configuration, You need to specify
`fluentbit_inputs` and `fluentbit_outputs` to make it run perfectly.

NOTE: You can specify your own variables in `group_vars` or `host_vars`.

```yaml
- hosts: all
  become: true
  gather_facts: true
  vars:
    fluentbit_inputs:
      - {"name": "cpu", "tags": "cpu.local", "interval_sec": 5}
    fluentbit_outputs:
      - {"name: "stdout", "match": "*"}
  roles:
    - be99inner.fluentbit
```

## License

MIT

## Author Information

Anurak Jannawan (be99inner)
