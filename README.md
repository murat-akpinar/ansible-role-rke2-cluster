# ansible-role-rke2-cluster
Ansible ile 1 Master 2 Worker Cluster ve üstüne metallb, longhorn

## To Do

- [x] System Gereksinimlerini Sorgulama
- [X] install rke2
- [X] Normal kullanıcı için kubectl komutlarını sudo eki olmadan çalıştırma.
- [X] Worker nodelara role verme
- [X] Worker nodlar master node bağlanması
- [ ] install metallb
- [ ] install longhorn

````bash
  _____  _        ___     _____ _           _            
 |  __ \| |      |__ \   / ____| |         | |           
 | |__) | | _____   ) | | |    | |_   _ ___| |_ ___ _ __ 
 |  _  /| |/ / _ \ / /  | |    | | | | / __| __/ _ \ '__|
 | | \ \|   <  __// /_  | |____| | |_| \__ \ ||  __/ |   
 |_|  \_\_|\_\___|____|  \_____|_|\__,_|___/\__\___|_|   
                                                         
Rke2 Cluster / Ver: "1.0-ubuntu"  / Developped by: Murat Akpınar

Versions:
  - rke2 v1.27.11+rke2r1
  - metallb
  - longhorn
  - grafana

### 

kubectl get nodes
NAME           STATUS   ROLES                       AGE     VERSION
rke2-master    Ready    control-plane,etcd,master   4m31s   v1.27.11+rke2r1
rke2-worker    Ready    worker-1                    2m40s   v1.27.11+rke2r1
rke2-worker2   Ready    worker-2                    2m30s   v1.27.11+rke2r1
````

````Bash
Thursday 14 March 2024  00:35:44 +0300 (0:00:04.325)       0:04:14.554 ******** 
=============================================================================== 
Gathering Facts -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- 1.21s
rke2_setup : Check minimum CPU requirements ---------------------------------------------------------------------------------------------------------------------------------------------- 0.39s
rke2_setup : Verify CPU count ------------------------------------------------------------------------------------------------------------------------------------------------------------ 0.07s
rke2_setup : Check minimum RAM requirements ---------------------------------------------------------------------------------------------------------------------------------------------- 0.26s
rke2_setup : Check minimum RAM requirements ---------------------------------------------------------------------------------------------------------------------------------------------- 0.29s
rke2_setup : Install RKE2 on master node ------------------------------------------------------------------------------------------------------------------------------------------------ 12.47s
rke2_setup : Ensure RKE2 server is enabled and running ---------------------------------------------------------------------------------------------------------------------------------- 83.54s
rke2_setup : Wait for RKE2 server to become ready ---------------------------------------------------------------------------------------------------------------------------------------- 0.35s
rke2_setup : Check if kubectl symbolic link already exists ------------------------------------------------------------------------------------------------------------------------------- 0.86s
rke2_setup : Find kubectl binary path ---------------------------------------------------------------------------------------------------------------------------------------------------- 0.30s
rke2_setup : Create symbolic link for kubectl -------------------------------------------------------------------------------------------------------------------------------------------- 0.23s
rke2_setup : Set KUBECONFIG environment variable globally -------------------------------------------------------------------------------------------------------------------------------- 0.41s
rke2_setup : Ensure RKE2 directory exists on worker nodes -------------------------------------------------------------------------------------------------------------------------------- 0.40s
rke2_setup : Check if RKE2 server is running --------------------------------------------------------------------------------------------------------------------------------------------- 0.24s
rke2_setup : Fetch RKE2 node token from master ------------------------------------------------------------------------------------------------------------------------------------------- 0.33s
rke2_setup : Install RKE2 on worker nodes ----------------------------------------------------------------------------------------------------------------------------------------------- 63.74s
rke2_setup : Set up RKE2 agent environment file on worker nodes -------------------------------------------------------------------------------------------------------------------------- 0.64s
rke2_setup : Ensure RKE2 agent is enabled and running ----------------------------------------------------------------------------------------------------------------------------------- 49.70s
rke2_setup : Define the user name with UID 1000 ------------------------------------------------------------------------------------------------------------------------------------------ 1.02s
rke2_setup : Set user name variable from getent passwd output ---------------------------------------------------------------------------------------------------------------------------- 0.05s
Playbook run took 0 days, 0 hours, 4 minutes, 14 seconds
````



## Forest

```bash
DevOps-EHKKKS-PROXMOX-ANSIBLE
├── collections
│   └── requirements.yml
├── inventory
│   ├── cluster_inventory.yml
├── playbooks
│   └── roles
│       └── rke2_setup
│           ├── defaults
│           │   └── main.yml
│           ├── handlers
│           │   └── main.yml
│           ├── meta
│           │   └── main.yml
│           ├── tasks
│           │   ├── 00_system_requirements.yml
│           │   ├── 01_install_rke2.yml
│           │   ├── 02_install_metallb.yml
│           │   ├── 03_install_longhorn.yml
│           │   ├── 04_wellcome.yml
│           │   └── main.yml
│           ├── templates
│           │   └── rke2_agent_config.j2
│           │   └── wellcome.j2
│           └── vars
│               ├── inventory
│               └── test.yml
│ 
│
├── .gitignore
├── ansible.cfg
├── hosts
├── LICENSE
├── README.md
└── site.yml
```
