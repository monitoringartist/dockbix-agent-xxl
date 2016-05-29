# Zabbix Agent 3.0 XXL with Docker/systemd monitoring

[![Deploy to Docker Cloud](https://files.cloud.docker.com/images/deploy-to-dockercloud.svg)](https://cloud.docker.com/stack/deploy/?repo=https://github.com/monitoringartist/zabbix-agent-xxl) [![](https://badge.imagelayers.io/monitoringartist/zabbix-agent-xxl-limited:latest.svg)](https://imagelayers.io/?images=monitoringartist/zabbix-agent-xxl-limited:latest)

If you like or use this project, please provide feedback to author - Star it ★.

Start one container and monitor all Docker containers/systemd on your Docker host. [Zabbix Docker monitoring](https://github.com/monitoringartist/zabbix-docker-monitoring) and [Zabbix systemd monitoring](https://github.com/monitoringartist/zabbix-systemd-monitoring) are used - all [docker module container metrics](https://github.com/monitoringartist/Zabbix-Docker-Monitoring) are available except `docker.xnet`. Custom [template Zabbix Agent XXL](https://github.com/monitoringartist/zabbix-agent-xxl/tree/master/template) is provided for Docker metrics. Zabbix agent stress testing is supported as well. Quick start:

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

# Paid Zabbix Agent 3.0 XXL Docker image

**[Subcribe for Paid Zabbix Agent XXL 3.0 updates](https://docs.google.com/forms/d/15TAGdkusa2r1TNVxf0ZeZtYaCCXPiubao1IYSbg1Z3Y/viewform)** right now.

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

- zabbix agent provides only docker metrics, TLS fearures and Zabbix agent server IP check are disabled
- zabbix-agent-xxl-limited container publish statistic information

Source code of limited zabbix-agent is published in src directory.

# Integrations

* [Puppet for dockerized zabbix-agent-xxl-limited](https://github.com/monitoringartist/zabbix-agent-xxl/blob/master/puppet.md)
* [Ansible for dockerized zabbix-agent-xxl-limited](https://github.com/monitoringartist/zabbix-agent-xxl/blob/master/ansible.md)
* [docker-compose for dockerized zabbix-agent-xxl-limited](https://github.com/monitoringartist/zabbix-agent-xxl/blob/master/docker-compose.yml)

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

[Devops Monitoring Expert](http://www.jangaraj.com 'DevOps / Docker / Kubernetes / AWS ECS / Zabbix / Zenoss / Terraform / Monitoring'),
who loves monitoring systems, which start with letter Z. Those are Zabbix and Zenoss.

Professional devops / monitoring services:

[![Monitoring Artist](http://monitoringartist.com/img/github-monitoring-artist-logo.jpg)]
(http://www.monitoringartist.com 'DevOps / Docker / Kubernetes / AWS ECS / Zabbix / Zenoss / Terraform / Monitoring')
