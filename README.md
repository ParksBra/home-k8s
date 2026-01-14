## Kubernetes Home Lab (home-k8s)

In my most recent knowledge ventures, I've been working towards rounding-off my skillset with Kubernetes while strengthening my CI/CD and DevOps concepts.

This lab is hosted on three separate Raspberry Pi 5's running Raspberry Pi OS Lite; One control-plane and two worker nodes.

### Relevant Repositories
| Repository  | Description |
| - | - |
| <u><i>Platform Repos</u></i> |
| [Cluster Base](https://github.com/ParksBra/home-k8s-cluster-base) | Ansible roles to provision the Kubernetes cluster and configure the underlying hosts |
| [Platform Network](https://github.com/ParksBra/home-k8s-tf-platform-network) | Terraform to manage the platform's network manifests and Helm charts:<br>&emsp;&bull; Calico/Tigera Operator - Cluster Network Interface<br>&emsp;&bull; Tailscale - Secure external ingress for hosted services<br>&emsp;&bull; Ingress-Nginx - Nginx level customization, access enabled through Tailscale<br>&emsp;&bull; Cert-Manager - Seamless auto-generated and auto-rotated web certificates |
| [Platform Storage](https://github.com/ParksBra/home-k8s-tf-platform-storage) | Terraform to manage the platform's storage manifests and Helm charts:<br>&emsp;&bull; Longhorn - Primary persistant storage<br>&emsp;&bull; Minio - Velero backup storage<br>&emsp;&bull; Velero - Cluster state backups |
| <u><i>Service Repos</u></i> |
| [Home Assistant](https://github.com/ParksBra/home-k8s-tf-service-haenv) | Terraform to manage my Home Assistant environment's manifests and Helm charts:<br>&emsp;&bull; Home Assistant - Home automation provider<br>&emsp;&bull; Mosquitto - MQTT Broker between Zigbee2mqtt and Home Assistant<br>&emsp;&bull; Zigbee2Mqtt - More functionality versus native HA integration<br>&emsp;&bull; Akri - Provides Zigbee2Mqtt's USB radio connection |
| [Kubernetes Dashboard](https://github.com/ParksBra/home-k8s-tf-service-k8sdash) | Terraform to manage my Kubernetes Dashboard's manifests and Helm charts:<br>&emsp;&bull; Kubernetes Dashboard|
| <i><u>Azure Devops Repos</u></i> |
| [ADO Templates](https://github.com/ParksBra/home-k8s-ado-templates) | Templates for use across my Azure DevOps CI/CD pipelines |
| [Local ADO Agents](https://github.com/ParksBra/local-ado-agents) | Docker Compose file for local Azure DevOps agents |
