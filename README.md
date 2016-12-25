# Zabbix Agent XXL with Docker/systemd monitoring

[![DockerHub pulls](https://img.shields.io/docker/pulls/monitoringartist/zabbix-agent-xxl-limited.svg?style=plastic&label=DockerHub%20Pulls)](https://img.shields.io/docker/pulls/monitoringartist/zabbix-agent-xxl-limited.svg)
[![GitHub stars](https://img.shields.io/github/stars/monitoringartist/zabbix-agent-xxl.svg?style=plastic&label=GitHub%20Stars)](https://github.com/monitoringartist/zabbix-agent-xxl)
[![DockerHub stars](https://img.shields.io/docker/stars/monitoringartist/zabbix-agent-xxl-limited.svg?style=plastic&label=DockerHub%20Stars)](https://img.shields.io/docker/pulls/monitoringartist/zabbix-agent-xxl-limited.svg)
[![Docker ready](https://img.shields.io/badge/Docker-ready-brightgreen.svg)](https://hub.docker.com/r/monitoringartist/zabbix-agent-xxl-limited/)
[![Commercial support ready](https://img.shields.io/badge/Commercial support-ready-brightgreen.svg)](http://www.monitoringartist.com 'DevOps / Docker / Kubernetes / AWS ECS / Google GCP / Zabbix / Zenoss / Terraform / Monitoring')

If you like or use this project, please provide feedback to author - Star it ★
and [write what's missing for you](https://docs.google.com/forms/d/e/1FAIpQLSdte1irviwtQzXU8_DMzboxf_qggE3qgjgpPHoBlE9RzLCXKA/viewform).

**Overview of Monitoring Artist (dockerized) monitoring ecosystem:**

- **[Zabbix XXL](https://hub.docker.com/r/monitoringartist/zabbix-xxl/)** - standard Zabbix server/proxy/UI/snmpd/java gateway with additional XXL extensions
- **[Zabbix agent XXL](https://hub.docker.com/r/monitoringartist/zabbix-agent-xxl-limited/)** - Zabbix agent with [Docker (Mesos/Chronos/Marathon) monitoring](https://github.com/monitoringartist/zabbix-docker-monitoring) and [systemd monitoring](https://github.com/monitoringartist/zabbix-systemd-monitoring)
- **[Zabbix templates](https://hub.docker.com/r/monitoringartist/zabbix-templates/)** - tiny (5MB) image for easy template deployment of selected Zabbix monitoring templates
- **[Zabbix extension - all templates](https://hub.docker.com/r/monitoringartist/zabbix-ext-all-templates/)** - storage image for Zabbix XXL with 200+ [community templates](https://github.com/monitoringartist/zabbix-community-repos)
- **[Kubernetized Zabbix](https://github.com/monitoringartist/kubernetes-zabbix)** - containerized Zabbix cluster based on Kubernetes
- **[Grafana XXL](https://hub.docker.com/r/monitoringartist/grafana-xxl/)** - dockerized Grafana with all community plugins
- **[Grafana dashboards](https://grafana.net/monitoringartist)** - Grafana dashboard collection for [AWS](https://github.com/monitoringartist/grafana-aws-cloudwatch-dashboards) and [Zabbix](https://github.com/monitoringartist/grafana-zabbix-dashboards)
- **[Monitoring Analytics](https://hub.docker.com/r/monitoringartist/monitoring-analytics/)** - R statistical computing and graphics for monitoring from data scientists
- **[Docker killer](https://hub.docker.com/r/monitoringartist/docker-killer/)** - Docker image for Docker stress and Docker orchestration testing

Start one container and monitor all Docker containers on your Docker host. [Zabbix Docker monitoring](https://github.com/monitoringartist/zabbix-docker-monitoring) and [Zabbix systemd monitoring](https://github.com/monitoringartist/zabbix-systemd-monitoring) are used - all [docker module container metrics](https://github.com/monitoringartist/Zabbix-Docker-Monitoring) are available except `docker.xnet`. Custom [template Zabbix Agent XXL](https://github.com/monitoringartist/zabbix-agent-xxl/tree/master/template) is provided for Docker metrics. Zabbix agent stress testing is supported as well. Quick start:

```
docker run \
  --name=zabbix-agent-xxl \
  -h $(hostname) \
  -p 10050:10050 \
  -v /:/rootfs \
  -v /var/run:/var/run \
  -e "ZA_Server=<ZABBIX SERVER IP/DNS NAME>" \
  -d monitoringartist/zabbix-agent-xxl-limited:latest
```

**Don't use `localhost` or `127.0.0.1` in `ZA_Server` setting!**

Tested on CoreOS, RHEL, CentOS, Ubuntu, Debian, Boot2docker, Photon OS.

Please donate to author, so he can continue to publish other awesome projects 
for free:

[![Paypal donate button](http://jangaraj.com/img/github-donate-button02.png)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=8LB6J222WRUZ4)

You can use Docker image [monitoringartist/zabbix-templates](https://hub.docker.com/r/monitoringartist/zabbix-templates/) for import of supported Zabbix App Docker monitoring template into your Zabbix. Example:

```
docker run --rm \
  -e XXL_apiurl=http://zabbix.org/zabbix \
  -e XXL_apiuser=Admin \
  -e XXL_apipass=zabbix \
  monitoringartist/zabbix-templates
```

# Paid Zabbix Agent XXL Docker image

**[Subcribe for Paid Zabbix Agent XXL updates](https://docs.google.com/forms/d/15TAGdkusa2r1TNVxf0ZeZtYaCCXPiubao1IYSbg1Z3Y/viewform)** right now.

We would like to publish paid version as a Docker image `monitoringartist/zabbix-agent-xxl` soon. It won't have any limitations of public limited image and some additional features will be included. Current roadmap:

- host metrics - see [example of Zabbix Agent XXL template](https://raw.githubusercontent.com/monitoringartist/zabbix-agent-xxl/master/doc/Template-Zabbix-Agent-XXL.png) with some host metrics 
- realtime docker.discovery
- Kubernetes monitoring - again realtime container discovery

# How it works

![Zabbix Agent XXL Docker container](https://raw.githubusercontent.com/monitoringartist/zabbix-agent-xxl/master/doc/zabbix-agent-xxl-schema.png) 

No classic rpm/deb package installation or Zabbix module compilation. Just start
zabbix-agent-xxl container and your Docker container metrics will be collected
from the Docker daemon or cgroup layer.

# Included projects
 
 * [zabbix_agent_bench](https://github.com/cavaliercoder/zabbix_agent_bench) - utility to test performance of Zabbix agent
 * [zabbix-server-stress-test](https://github.com/monitoringartist/zabbix-server-stress-test) - loadbable agent module for stress testing

Zabbix agent stress testing:

```
docker run \
  --name=zabbix-agent-xxl \
  -h $(hostname) \
  -p 10050:10050 \
  -v /:/rootfs \
  -v /var/run:/var/run \  
  -e "ZA_Server=<ZABBIX SERVER IP/DNS NAME>" \
  -d monitoringartist/zabbix-agent-xxl-limited:latest
  
# used HW - 8xCPU Intel(R) Xeon(R) CPU E31270 @ 3.40GHz:
docker exec -ti zabbix-agent-xxl zabbix_agent_bench -timelimit 30 -key stress.ping --threads 50
Testing 1 keys with 50 threads (press Ctrl-C to cancel)...
stress.ping :	1225787	0	0

=== Totals ===

Total values processed:		1225787
Total unsupported values:	0
Total transport errors:		0
Total key list iterations:	1225787

Finished! Processed 1225787 values across 50 threads in 30.002141605s (40856.650040 NVPS)
```

# Environment configuration variables

You can use any [agent config variable](https://www.zabbix.com/documentation/3.0/manual/appendix/config/zabbix_agentd), just add prefix `ZA_`.
If you don't specify custom settings, then default Zabbix agent settings will be used.

Example:

```
docker run \
  --name=zabbix-agent-xxl \
  -h $(hostname) \
  -p 10050:10050 \
  -v /:/rootfs \
  -e "ZA_Server=<ZABBIX SERVER IP/DNS NAME>" \
  -e "ZA_ServerActive=<ZABBIX SERVER IP/DNS NAME>" \
  -e "ZA_StartAgents=10" \
  -e "ZA_Timeout=30" \
  -d monitoringartist/zabbix-agent-xxl-limited:latest
```

Some settings are excluded and you can't override them: `AllowRoot, LoadModulePath, LoadModule, LogType`, because Docker monitoring module is used. 

# Limitations

Be aware of limited `monitoringartist/zabbix-agent-xxl-limited` functionalities:

- zabbix agent provides only docker metrics (no host metrics), TLS features and Zabbix agent server IP check are disabled
- zabbix-agent-xxl-limited container send statistic informations (Docker version, kernel version, execution driver, agent container start-up fatal errors, ...) to Google Analytics - data are used to improve Docker monitoring functionality and aggregated data might be published

Source code of limited zabbix-agent is published in src directory.

# Integrations

* [Puppet for dockerized zabbix-agent-xxl-limited](https://github.com/monitoringartist/zabbix-agent-xxl/blob/master/puppet.md)
* [Ansible for dockerized zabbix-agent-xxl-limited](https://github.com/monitoringartist/zabbix-agent-xxl/blob/master/ansible.md)
* [docker-compose for dockerized zabbix-agent-xxl-limited](https://github.com/monitoringartist/zabbix-agent-xxl/blob/master/docker-compose.yml)
* [systemd service unit file - see next section](https://github.com/monitoringartist/zabbix-agent-xxl/blob/master/systemd/docker-zabbix-agent-xxl.service)

# Dockerized Zabbix agent XXL service managed by systemd

Example of service unit file for Dockerized Zabbix agent XXL - don't forget to
edit environment variables. You can manage it as a standard OS service:

```
# wget -P /usr/lib/systemd/system/ https://raw.githubusercontent.com/monitoringartist/zabbix-agent-xxl/master/systemd/docker-zabbix-agent-xxl.service
## edit env variables: vi /usr/lib/systemd/system/docker-zabbix-agent-xxl.service
# systemctl enable docker-zabbix-agent-xxl.service
Created symlink from /etc/systemd/system/multi-user.target.wants/docker-zabbix-agent-xxl.service to /usr/lib/systemd/system/docker-zabbix-agent-xxl.service.
# systemctl start docker-zabbix-agent-xxl.service
# systemctl status docker-zabbix-agent-xxl.service
● docker-zabbix-agent-xxl.service - Dockerized Zabbix Agent XXL www.monitoringartist.com
   Loaded: loaded (/usr/lib/systemd/system/docker-zabbix-agent-xxl.service; enabled; vendor preset: disabled)
   Active: active (running) since Sat 2016-08-20 00:17:04 BST; 5s ago
  Process: 72712 ExecStartPre=/usr/bin/docker pull monitoringartist/zabbix-agent-xxl-limited:latest (code=exited, status=0/SUCCESS)
 Main PID: 72719 (docker)
   Memory: 8.6M
   CGroup: /system.slice/docker-zabbix-agent-xxl.service
           └─72719 /usr/bin/docker run --rm -e ZA_Server=<ZABBIX SERVER IP/DNS NAME> --name docker-zabbix-agent-xxl.service -h dockerhost -p 10050:10050 -v /:/rootfs...

Aug 20 00:17:05 dockerhost docker[72719]: 11:20160819:231705.575 IPv6 support:          YES
Aug 20 00:17:05 dockerhost docker[72719]: 11:20160819:231705.575 TLS support:           YES
Aug 20 00:17:05 dockerhost docker[72719]: 11:20160819:231705.575 **************************
Aug 20 00:17:05 dockerhost docker[72719]: 11:20160819:231705.575 using configuration file: /etc/zabbix/zabbix_agentd.conf
Aug 20 00:17:05 dockerhost docker[72719]: 11:20160819:231705.581 loaded modules: zabbix_module_docker.so, zabbix_module_stress.so
Aug 20 00:17:05 dockerhost docker[72719]: 11:20160819:231705.583 agent #0 started [main process]
Aug 20 00:17:05 dockerhost docker[72719]: 12:20160819:231705.583 agent #1 started [collector]
Aug 20 00:17:05 dockerhost docker[72719]: 14:20160819:231705.583 agent #3 started [listener #2]
Aug 20 00:17:05 dockerhost docker[72719]: 13:20160819:231705.584 agent #2 started [listener #1]
Aug 20 00:17:05 dockerhost docker[72719]: 15:20160819:231705.586 agent #4 started [listener #3]
# docker ps | grep zabbix-agent-xxl
b2ecbf3a7df0        monitoringartist/zabbix-agent-xxl-limited:latest   "/zocker-xxl"       25 seconds ago      Up 24 seconds       0.0.0.0:10050->10050/tcp   docker-zabbix-agent-xxl.service
```

# Troubleshooting

Check container logs `docker logs zabbix-agent-xxl`. Development is driven by customer. You can still report bugs, however customer bugs/feature requests will be prioritized. Please provide all details to replicate your issue (Docker/OS version, how was started zabbix-agent/monitored container, listing of you cgroup pseudofiles, ....). Keep in mind that limited Docker image doesn't provide all Zabbix agent features.

# Support

Free public Docker image `monitoringartist/zabbix-agent-xxl-limited` has best effort support. Paid private Docker image `monitoringartist/zabbix-agent-xxl` has a standard tech support and its issues are prioritized. Our typical response time is 1 working day.

# Security issues

Our zabbix-agent-xxl Docker images are security scanned regularly. All detected vulnerabilities are fixed*:

* Critical vulnerabilities - within 72 hours of notification
* Major vulnerabilities - within 7 days of notification
 
\*except Zabbix security issues, which will be reported directly to Zabbix vendor

Author
======

[Devops Monitoring Expert](http://www.jangaraj.com 'DevOps / Docker / Kubernetes / AWS ECS / Google GCP / Zabbix / Zenoss / Terraform / Monitoring'),
who loves monitoring systems, which start with letter Z. Those are Zabbix and Zenoss.

Professional devops / monitoring services:

[![Monitoring Artist](http://monitoringartist.com/img/github-monitoring-artist-logo.jpg)]
(http://www.monitoringartist.com 'DevOps / Docker / Kubernetes / AWS ECS / Google GCP / Zabbix / Zenoss / Terraform / Monitoring')
