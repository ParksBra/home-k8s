## Kubernetes Home Lab (home-k8s)

In my most recent knowledge ventures, I've been working towards rounding-off my skillset with Kubernetes while strengthening my CI/CD and DevOps concepts.

This lab is hosted on three separate Raspberry Pi 5's running Raspberry Pi OS Lite; One control-plane and two worker nodes.

### Relevant Repositories
| Repository  | Description |
| - | - |
| <u><i>Platform Repos</u></i> |
| [Cluster Base](https://github.com/ParksBra/home-k8s-cluster-base) | Ansible roles to provision the Kubernetes cluster and configure the underlying hosts |
| [Platform Network](https://github.com/ParksBra/home-k8s-tf-platform-network) | Terraform to manage the platform's network manifests and Helm charts:<br>&emsp;&bull; Calico/Tigera Operator - Cluster Network Interface<br>&emsp;&bull; Tailscale - Secure external ingress for hosted services<br>&emsp;&bull; Ingress-Nginx - Nginx level customization, access enabled through Tailscale<br>&emsp;&bull; Cert-Manager - Seamless auto-generated and auto-rotated web certificates |
| [Platform Storage](https://github.com/ParksBra/home-k8s-tf-platform-storage) | Terraform to manage the platform's storage manifests and Helm charts:<br>&emsp;&bull; Longhorn - Primary persistant storage<br>&emsp;&bull; Minio - S3-like storage for Velero backups<br>&emsp;&bull; Velero - Cluster state backups |
| <u><i>Service Repos</u></i> |
| [Home Assistant](https://github.com/ParksBra/home-k8s-tf-service-haenv) | Terraform to manage my Home Assistant environment's manifests and Helm charts:<br>&emsp;&bull; Home Assistant - Home automation provider<br>&emsp;&bull; Mosquitto - MQTT Broker between Zigbee2mqtt and Home Assistant<br>&emsp;&bull; Zigbee2Mqtt - More functionality versus native HA integration<br>&emsp;&bull; Akri - Provides Zigbee2Mqtt's USB radio connection |
| [Kubernetes Dashboard](https://github.com/ParksBra/home-k8s-tf-service-k8sdash) | Terraform to manage my Kubernetes Dashboard's manifests and Helm charts:<br>&emsp;&bull; Kubernetes Dashboard|
| <i><u>Azure Devops Repos</u></i> |
| [ADO Templates](https://github.com/ParksBra/home-k8s-ado-templates) | Templates for use across my Azure DevOps CI/CD pipelines |
| [Local ADO Agents](https://github.com/ParksBra/local-ado-agents) | Docker Compose file for local Azure DevOps agents |

### Project Goals
| Goal | Status | Notes |
| - | - | - |
| <u><i>Project-wide Goals</u></i> |
| Fully IaC defined environment | Achieved | All resources and tasks are defined using:<br>&emsp;&bull; Ansible - Configures all host-level resources<br>&emsp;&bull; Terraform - Defines all Kubernetes resources<br>&emsp;&bull; Azure DevOps - Defines deployment processes|
| Full CI/CD automation for changes and development | Achieved | Streamlined and reusable pipeline templates for deploying hosted services. Initially had built ontop of Jenkins, though switched to Azure DevOps for the wider feature set, allowing for cross-pipeline triggers. Azure DevOps requires local agents that can access the cluster nodes. |
| Automated Kubernetes cluster creation | Achieved | Developed several Ansible roles to orchistrate creating and maintaining a Kubernetes Cluster. |
| Automated node patching and upgrades | Achieved | To further harden security, all of my nodes are on a weekly patching interval, designed to minimize cluster impact. |
| Disaster recovery implementation | In-progress | A full recovery process in the event of a worse-case failure. Services should be available and restored to their latest state proceeding process completion. |
| Scalable and modular development platform | Achieved | A platform that allows full separation, if desired, across different hosted services / solutions. |
| Redundant backup methods | Achieved | Aside from application-made backups, I want to create snapshots of relevant persistent volumes and cluster state backups. This is achieved through Longhorn's snapshot feature and Velero's cluster backup solution. |
| Rollback capability | In-progress | The ability to quickly rollback changes that have unintended impacts. This will be dependent on good Git practices and versioning. |
| Service and infrasturcture monitoring | In-progress | The ability to monitor service and infrastructure health, while also gathering useful insights from service-related metrics. My plan is to primarily use Prometheus and ingest the data into a visualization tool such as Grafana or Splunk. |
| <u><i>Solution-specific Goals</u></i> |
| Home Assistant | Achieved | The primary backend supporing all of my home automation solutions. My goal with this is to minimize downtime during patching and upgrades via a multi-node cluster. |
| Kubernetes Zigbee and MQTT broker | Achieved | Services are deployed and auto-configured to connect. Allows for better granular control of IoT devices than Home Assistant's Zigbee integration. |
| Persistent cluster storage (local) | Achieved | I was originally using OpenEBS, though moved to Longhorn for better cross-node replication.  |
| Secure WAN ingress (local) | Achieved | Allow non-local connections to access hosted services without exposing them to the public WAN. Tailscale is my current solution for this, allowing access to the Ingress-Nginx controller. |
| Cluster-wide USB device availability | In-progress | Allow for single USB devices to be avaialble to pods, independent of which node the pod is on. Akri is my current solution for this. |

### Growth Goals
| Goal | Status | Notes |
| - | - | - |
| <u><i>Technologies to Initially Learn</u></i> |
| Kubernetes usage | Achieved | Troubleshooting processes<br>Core resources and their usage<br>Customizable / parameterized manifests<br>Disater recovery methods<br> |
| Kubernetes RBAC | In-progress | General notation<br>Where and when to use |
| Helm charts  | Achieved | Usage of pre-made charts<br>Chart creation<br>Helper templates|
| Prometheus | In-progress | Integration methods<br>Base monitoring usage<br>Bridge knowledge of other, familiar o11y solutions |
| <u><i>Technologies to Refine Usage Of</u></i> |
| Azure DevOps | In-progress | Pipeline, job, stage, and task templates<br>Deployment architecture |
| Ansible | Achieved | Kubernetes modules<br>Cleaner implementations of role meta, defaults, and handlers<br>Push towards module usage rather than shell/command tasks if applicable<br>Further align with standard structure and naming practices<br>Design around 'check' (dry-run) mode |
| Terraform | Achieved | Cross-state connection methods<br>Module versioning<br>Non-s3-based state methods<br>Kubernetes and Helm providers |
| <u><i>Methodologies to Stengthen</u></i> |
| Dependency-based CI/CD | In-progress | Architecting CI/CD pipeline dependencies and triggers<br>Pre-deployment testing methods |
| Kubernetes platform architecture  | In-progress | Separation of foundational resources from service manifests<br>Access control methods and best practices |
