# https://grafana.com/docs/loki/latest/setup/install/docker/

Download Loki config files

	
	```bash
wget https://raw.githubusercontent.com/grafana/loki/v3.0.0/cmd/loki/loki-local-config.yaml -O loki-config.yaml
```


wget https://raw.githubusercontent.com/grafana/loki/v3.0.0/clients/cmd/promtail/promtail-docker-config.yaml -O promtail-config.yaml

Run Docker

docker run --name loki -d -v $(pwd):/mnt/config -p 3100:3100 grafana/loki:3.0.0 -config.file=/mnt/config/loki-config.yaml
docker run --name promtail -d -v $(pwd):/mnt/config -v /var/log:/var/log --link loki grafana/promtail:3.0.0 -config.file=/mnt/config/promtail-config.yaml

Verify

http://localhost:3100/ready
http://localhost:3100/metrics

Install Grafana

docker run -d -p 3000:3000 --name=grafana grafana/grafana-enterprise

Visit
http://localhost:3000/login

Default username is admin and password is admin

Grafana Add Datasource

Click on Menu
Click on connections->datasource

Type loki in filter and select
In URL enter http://host.docker.internal:3100

Go to label filters and select value and search

Youtube video here
