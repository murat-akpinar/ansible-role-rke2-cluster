# ansible-role-rke2-cluster
Ansible ile 1 Master 2 Worker Cluster ve üstüne metallb, longhorn

## To Do

- [x] System Gereksinimlerini Sorgulama
- [X] install rke2
- [X] cluster connection
- [ ] install metallb
- [ ] install longhorn

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