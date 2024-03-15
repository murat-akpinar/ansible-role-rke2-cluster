#  Ansible Role: RKE2 Cluster
![release](https://img.shields.io/badge/release-v1.0-blue)

<img src="https://camo.githubusercontent.com/e8b5779608fb6e9487657a97573e6658fa8ad24ac193c00c4424bd5d83b818a1/68747470733a2f2f646f63732e726b65322e696f2f696d672f6c6f676f2d686f72697a6f6e74616c2d726b65322e737667" alt="RKE2" data-canonical-src="https://docs.rke2.io/img/logo-horizontal-rke2.svg" style="max-width: 100%;">

# Ansible Role: RKE2 Cluster Kurulumu

Bu Ansible rolü, otomatik olarak **RKE2** tabanlı Kubernetes kümesi kurulumunu gerçekleştirir. Kurulum, bir adet master ve birden fazla worker düğümünden oluşan bir yapıyı destekler.

## Önkoşullar

- **Ansible** yüklü bir kontrol makinesi.
- **SSH** erişimi olan ve sudo yetkisine sahip Linux tabanlı hedef sunucular.
````bash
ssh-copy-id -i ~/.ssh/mykey root@192.168.1.152
ssh-copy-id -i ~/.ssh/mykey root@192.168.1.153
ssh-copy-id -i ~/.ssh/mykey root@192.168.1.156
````
- Master ve Worker nodların hostnameleri bir birinden farklı olmalı. Hostnamectl komutu ile değiştirmeniz mümkün.
````bash
hostnamectl set-hostname
````

## Hızlı Başlangıç

1. **Hosts Dosyasını Düzenle**: Projenin kök dizinindeki `hosts` dosyasını kendi ortamınıza göre ayarlayın. Örnek yapılandırma:

```
master1 ansible_host=192.168.1.152
worker1 ansible_host=192.168.1.153
worker2 ansible_host=192.168.1.156
```

2. **Envanter Dosyasını Düzenle**: Projenin kök dizinindeki `cluster_inventory.yml` dosyasını kendi ortamınıza göre ayarlayın. Örnek yapılandırma:

```
all:
  children:
    master:
      hosts:
        master1:
          ansible_host: 192.168.1.152
    worker:
      hosts:
        worker1:
          ansible_host: 192.168.1.153
        worker2:
          ansible_host: 192.168.1.156

```

3. **Playbook'u Çalıştır**: Aşağıdaki komut ile Ansible playbook'unu çalıştırın:

```bash
ansible-playbook -i inventory/cluster_inventory.yml site.yml
```

## Yapılandırma

`vars/main.yml` dosyasında bulunan değişkenleri kendi ihtiyaçlarınıza göre düzenleyebilirsiniz. Bu değişkenler, cluster kurulumu sırasında kullanılacak ayarları içerir.

## Yapılacaklar

### RKE Cluster Kurulumu
- [x] Sistem Gereksinimlerinin Kontrol Edilmesi
- [X] RKE2'nin Kurulumu
- [X] Kubectl Komutlarının Normal Kullanıcılar Tarafından Sudo İhtiyacı Olmadan Çalıştırılması
- [X] Worker Node'ların Master Node'a Bağlanması
- [X] Worker Node'ların Rollendirilmesi
- [ ] hostname değiştirilmesi
### Ön Tanımlı Gelecek Paketler
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


# Yapı

```bash
ansible-role-rke2-cluster
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
