#### Monitoramento do Proxmox Virtual Environment (PVE) com Prometheus ####

Crie a network ```public_network```.
```bash
docker network create public_network
```

No arquivo ```prometheus.yml``` adicione as configurações no nó PVE à ser monitorado.

```yaml
  - job_name: 'pve'
    metrics_path: /pve
    params:
      module: [default]
    static_configs:
      - targets: ['pve.meudominio.local:9221']
        labels:
          environment: 'desenvolvimento'
          hostname: 'pve.meudominio.local'
```

Inicialize a stack de monitoramento.
```bash
docker-compose up --detach
```