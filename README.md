# Filebeat module for ProxySQL
Simple Filebeat module for parsing ProxySQL logs and ship them to ElasticSearch

How to use:
1. Copy module (`proxysql` folder from this repository) to the `/usr/share/filebeat/module` folder
2. Create a file `/etc/filebeat/modules.d/proxysql.yml` with content:
```
# Module: proxysql
# Docs: https://github.com/altuhovsu/filebeat-proxysql-module

- module: proxysql
  # Error logs
  error:
    enabled: true

    # Set custom paths for the log files. If left empty,
    # Filebeat will choose the paths depending on your OS.
    #var.paths:
```
3. systemctl restart filebeat
4. Check in the Kibana Discover for `event.module :"proxysql"`

Notes:
1. Lines like `[INFO]` and `Closing unhealthy client connection` will be ignored (`exclude_lines: ['.*\[INFO\].*', '.*Closing unhealthy client connection.*']`)
2. default log file path: `/var/lib/proxysql/proxysql.log`

To Do:
1. Create a proper module structure (like described in the guide https://www.elastic.co/guide/en/beats/devguide/current/filebeat-modules-devguide.html)
2. Create a Kibana dashboard
3. Submit everything to the main repository https://github.com/elastic/beats
