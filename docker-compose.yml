---
version: '3.7'
services:
  telegraf:
    image: telegraf:1.12.3
    hostname: "{{.Node.ID}}"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    configs:
      - source: telegraf.conf
        target: /etc/telegraf/telegraf.conf
    deploy:
      mode: global
  influxdb:
    image: influxdb:1.7.8
    configs:
      - source: influxdb.conf
        target: /etc/influxdb/influxdb.conf
    volumes:
      - telegraf-volume:/var/lib/influxdb
  grafana:
    image: grafana/grafana:6.4.2
    configs:
      - source: telegraf-datasources.conf
        target: /etc/grafana/provisioning/datasources/all.yml
    depends_on:
      - influxdb
    ports:
      - 3000:3000
    volumes:
      - influxdb-volume:/var/lib/grafana

configs:
  telegraf.conf:
    file: ./telegraf/telegraf.conf
  influxdb.conf:
    file: ./influxdb/influxdb.conf
  telegraf-datasources.conf:
    file: ./grafana/provisioning/datasources/all.yml

volumes:
    telegraf-volume:
        external: false
    influxdb-volume:
        external: false
