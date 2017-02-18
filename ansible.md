# Ansible for dockerized dockbix-agent-xxl-limited

This for your Ansible inspiration. Final implementation is up to you:

```
# Jan Garaj - www.monitoringartist.com
# Used Core Docker module - http://docs.ansible.com/ansible/docker_module.html
- name: dockbix-agent-xxl container
  docker:
    name: dockbix-agent-xxl
    image: monitoringartist/dockbix-agent-xxl-limited:latest
    restart_policy: unless-stopped
    state: started
    pull: always
    net: host
    privileged: true
    volumes:
      - /:/rootfs    
    env:
        ZA_Server: <ZABBIX SERVER IP/DNS NAME>     
```

# Author

[Devops Monitoring Expert](http://www.jangaraj.com 'DevOps / Docker / Kubernetes / AWS ECS / Google GCP / Zabbix / Zenoss / Terraform / Monitoring'),
who loves monitoring systems and cutting/bleeding edge technologies: Docker,
Kubernetes, ECS, AWS, Google GCP, Terraform, Lambda, Zabbix, Grafana, Elasticsearch,
Kibana, Prometheus, Sysdig, ...

Summary:
* 1000+ [GitHub](https://github.com/monitoringartist/) stars
* 6000+ [Grafana dashboard](https://grafana.net/monitoringartist) downloads
* 800 000+ [Docker image](https://hub.docker.com/u/monitoringartist/) pulls

Professional devops / monitoring / consulting services:

[![Monitoring Artist](http://monitoringartist.com/img/github-monitoring-artist-logo.jpg)](http://www.monitoringartist.com 'DevOps / Docker / Kubernetes / AWS ECS / Google GCP / Zabbix / Zenoss / Terraform / Monitoring')
