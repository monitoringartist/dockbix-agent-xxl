# Puppet for dockerized zabbix-agent-xxl-limited

This for your Puppet inspiration. Final implementation is up to you:

```
# Jan Garaj - www.monitoringartist.com
# Used Puppet module - https://github.com/garethr/garethr-docker

class { 'docker':
  version => 'latest',
}->
docker::image { 'monitoringartist/zabbix-agent-xxl-limited':
  image_tag => 'latest',
}->
docker::run { 'zabbix-agent-xxl':
  image            => 'monitoringartist/zabbix-agent-xxl-limited',
  extra_parameters => ['--restart=unless-stopped'],
  ports            => ['10050'],
  volumes          => ['/:/rootfs'],
  env              => [
    'ZA_Server=<ZABBIX SERVER IP/DNS NAME>',
  ],
}
```

# Author

[Devops Monitoring Expert](http://www.jangaraj.com 'DevOps / Docker / Kubernetes / AWS ECS / Google GCP / Zabbix / Zenoss / Terraform / Monitoring'),
who loves monitoring systems, which start with letter Z. Those are Zabbix and Zenoss.

Professional devops / monitoring services:

[![Monitoring Artist](http://monitoringartist.com/img/github-monitoring-artist-logo.jpg)](http://www.monitoringartist.com 'DevOps / Docker / Kubernetes / AWS ECS / Google GCP / Zabbix / Zenoss / Terraform / Monitoring')
