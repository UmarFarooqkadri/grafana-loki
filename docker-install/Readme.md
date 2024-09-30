[Official Documentation](https://grafana.com/docs/loki/latest/setup/install/docker/ "Official Documentation")

[![Odyssey Cloud](https://www.odysseycloud.io/ "Odyssey Cloud")](https://www.odysseycloud.io/ "Odyssey Cloud")

Youtube video here

## Download Loki config files


```bash
wget https://raw.githubusercontent.com/grafana/loki/v3.0.0/cmd/loki/loki-local-config.yaml -O loki-config.yaml
```


## Download Promtail config files
```bash
wget https://raw.githubusercontent.com/grafana/loki/v3.0.0/clients/cmd/promtail/promtail-docker-config.yaml -O promtail-config.yaml
```

## Run Loki docker container

```bash
docker run --name loki -d -v $(pwd):/mnt/config -p 3100:3100 grafana/loki:3.0.0 -config.file=/mnt/config/loki-config.yaml
```

## Run Promtail docker container

```bash
docker run --name promtail -d -v $(pwd):/mnt/config -v /var/log:/var/log --link loki grafana/promtail:3.0.0 -config.file=/mnt/config/promtail-config.yaml
```

## Verify Loki

http://localhost:3100/ready
http://localhost:3100/metrics

## Install Grafana

```bash
docker run -d -p 3000:3000 --name=grafana grafana/grafana-enterprise
```

## Verify grafana

http://localhost:3000/login

:fa-exclamation-circle: Default username is admin and password is admin

## Grafana Add Datasource

Click on Menu
Click on connections->datasource

Type loki in filter and select
In URL enter http://host.docker.internal:3100

Go to label filters and select value and search


