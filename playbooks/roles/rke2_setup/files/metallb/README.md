### Çalıştırmak için
* MetalLB Çalıştırmak için
````bash
kubectl apply -f metallb.yaml
````

* IP Aralğını belirtiğiniz config dosyası
````bash
kubectl apply -f metallb-config.yaml
`````
* Pod Kontrolü
````bash
kubectl get pods -n metallb-system
````
