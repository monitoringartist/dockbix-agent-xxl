# Zabbix Agent 3.0 XXL with Docker monitoring

[![Deploy to Docker Cloud](https://files.cloud.docker.com/images/deploy-to-dockercloud.svg)](https://cloud.docker.com/stack/deploy/?repo=https://github.com/monitoringartist/zabbix-agent-xxl)

If you like or use this project, please provide feedback to author - Star it ★.

Start one container and monitor all Docker containers on your hosts. [Zabbix Docker monitoring](https://github.com/monitoringartist/Zabbix-Docker-Monitoring) is used - all [docker module container metrics](https://github.com/monitoringartist/Zabbix-Docker-Monitoring) are available except `docker.xnet`. Custom [template Zabbix Agent XXL](https://github.com/monitoringartist/zabbix-agent-xxl/tree/master/template) is provided as well. Quick start:

```
docker run \
  --name=zabbix-agent-xxl \
  -h `hostname` \
  -p 10050:10050 \
  -v /:/rootfs \
  -e "ZA_Server=<ZABBIX SERVER IP/DNS NAME>" \
  -d monitoringartist/zabbix-agent-xxl-limited:latest
```

Ubuntu users need also `-v /var/run:/var/run`.

Tested on CoreOS, RHEL, CentOS, Ubuntu, Debian, Boot2docker, Photon OS.

Please donate to author, so he can continue to publish other awesome projects 
for free:

[![Paypal donate button](http://jangaraj.com/img/github-donate-button02.png)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=8LB6J222WRUZ4)

# Zabbix Agent 3.0 XXL without any limitations

**[Subcribe for Zabbix Agent XXL 3.0 updates](https://docs.google.com/forms/d/15TAGdkusa2r1TNVxf0ZeZtYaCCXPiubao1IYSbg1Z3Y/viewform)** right now.

We would like to publish full version as a Docker image `monitoringartist/zabbix-agent-xxl` soon. It won't have limitations of public limited image and some additional features will be added as well. Current roadmap:

- host metrics - see [example of Zabbix Agent XXL template](https://raw.githubusercontent.com/monitoringartist/zabbix-agent-xxl/master/doc/Template-Zabbix-Agent-XXL.png) with some host metrics 
- realtime docker.discovery
- Kubernetes monitoring - again realtime container discovery
- stress testing support
- tiny image size (~20MB)
  
It'll be supported commercially. It's available only for private beta testing at the moment.

# How it works

![Zabbix Agent XXL Docker container](https://raw.githubusercontent.com/monitoringartist/zabbix-agent-xxl/master/doc/zabbix-agent-xxl-schema.png) 

No classic rpm/deb package installation or Zabbix module compilation. Just start
zabbix-agent-xxl container and your Docker container metrics will be collected
from the Docker or cgroup layer.

# Environment configuration variables

You can use any [agent config variable](https://www.zabbix.com/documentation/3.0/manual/appendix/config/zabbix_agentd), just add prefix `ZA_`.
If you don't specify custom settings, then default Zabbix agent settings will be used.

Example:

```
docker run \
  --name=zabbix-agent-xxl \
  -h `hostname` \
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

Be aware of limited monitoringartist/zabbix-agent-xxl-limited functionalities:

- zabbix agent provides only docker metrics, TLS and agent's Zabbix server IP check are disabled
- zabbix-agent-xxl-limited container publish statistic information

Source code of limited zabbix-agent is published in src directory.

Integrations
============

* [Puppet for dockerized zabbix-agent-xxl-limited](https://github.com/monitoringartist/zabbix-agent-xxl/blob/master/puppet.md)
* [Ansible for dockerized zabbix-agent-xxl-limited](https://github.com/monitoringartist/zabbix-agent-xxl/blob/master/ansible.md)
* [docker-compose for dockerized zabbix-agent-xxl-limited](https://github.com/monitoringartist/zabbix-agent-xxl/blob/master/docker-compose.yml)

# Troubleshooting and bugs

Troubleshooting: check container logs `docker logs zabbix-agent-xxl`.  Development is driven by customer. You can still report bugs, however customer bugs/feature requests will be prioritized.  

# Author

[Devops Monitoring zExpert](http://www.jangaraj.com 'DevOps / Docker / Kubernetes / Zabbix / Zenoss / Monitoring'), who loves monitoring
systems, which start with letter Z. Those are Zabbix and Zenoss.

Professional monitoring services:

[![Monitoring Artist](http://monitoringartist.com/img/github-monitoring-artist-logo.jpg)](http://www.monitoringartist.com 'DevOps / Docker / Kubernetes / Zabbix / Zenoss / Monitoring')
