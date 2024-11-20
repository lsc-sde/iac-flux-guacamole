---
title: FluxCD
layout: page
parent: Apache Guacamole
grand_parent: Virtual Desktop Infrastructure
---

The repository that defines the flux configuration for Apache Guacamole is located at https://github.com/lsc-sde/iac-flux-guacamole


## Network Policies

```mermaid
flowchart LR
    all([all services]) -->|Ingress ALL| svc[JupyterHub] 
    svc -->|Egress ALL|all
    svc -->|Egress TCP 3389,5900|all
    svc -->|Egress HTTPS| kubernetes[[Kubernetes API]]
    svc -->|Egress DNS| coredns
```

| Direction | Ports/Type | Description |
| --- | --- | --- |
| Ingress | All | Allows all traffic inbound. TODO: This needs to be refined |
| Egress | All | Allows all traffic to egress. TODO: This needs to be refined |
| Egress | TCP/UDP 53 | Allows traffic for DNS ports |
| Egress | HTTPS | Allows access to the kubernetes service to allow Kubernetes API Access |
| Egress | TCP 3389,5900 | Allows traffic for RDP and VNC |