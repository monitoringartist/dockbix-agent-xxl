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
who loves monitoring systems, which start with letter Z. Those are Zabbix and Zenoss.

Professional devops / monitoring services:

[![Monitoring Artist](http://monitoringartist.com/img/github-monitoring-artist-logo.jpg)](http://www.monitoringartist.com 'DevOps / Docker / Kubernetes / AWS ECS / Google GCP / Zabbix / Zenoss / Terraform / Monitoring')
