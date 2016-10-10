# telegraf-sample

sample code to collect metrics by using telegraf, store and visualize

# setup

```
$ vagrant up
``` 

# provision

```
$ ansible-playbook site.yml -i hosts -k -c paramiko
SSH password: 
```

please type password for vagrant user : vagrant

# Log server administration

## Node deployment

* 192.168.33.3: log-server
    * [InfluxDB administration](http://192.168.33.3:8083)
        * user: root
        * password: root
        * database: influxdb
    * [Grafana](http://192.168.33.3:3000)
        * user: admin
        * password: admin

## InfluxDB administration

* example of show tables like querying

```sql
SHOW SERIES
```    

please see also the [manual](https://docs.influxdata.com/influxdb/v1.0/query_language/schema_exploration/) for detail

* example of showing points of series

```sql 
SELECT * FROM cpu LIMIT 10;
```

please see also the [manual](https://docs.influxdata.com/influxdb/v1.0/query_language/data_exploration/)) for detail

## Grafana dashboard administration

http://docs.grafana.org/datasources/influxdb/

### Setup Data Sources

Data Sources > add data source

* Name: influxdb
* Type: InfluxDB
* Http settings:
    * Url: http://192.168.33.3:8086
    * Access: direct
* InfluxDB Details
    * Database: influxdb
    * User: root
    * Password: root

### Import Dashboard sample

[open dashboard import](http://192.168.33.3:3000/dashboard/new?editview=import) and select roles/grafana/files/sample.json

# Metric collector administration

## Node deployment

* 192.168.33.2: client-node
    * telegraf (/opt/telegraf)

please see [README.md](https://github.com/influxdb/telegraf/blob/master/README.md) for detail

distributed config by this repository is [here](https://github.com/takaidohigasi/telegraf-sample/blob/master/roles/telegraf/templates/telegraf.conf.j2)

# Notes

* please be sure to confirm timezones of virtualmachines/host are identical.
* see also [Japanese related document](https://slack-redir.net/link?url=http%3A%2F%2Fqiita.com%2Ftakaidohigasi%2Fitems%2Ffdc81db8336aa7601fc9&v=3)
