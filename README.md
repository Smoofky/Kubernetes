# 1. Utwórz przestrzeń nazw o nazwie lab4, w której można uruchomić 5 Podów i dostępna jest całkowita ilość 1000 millicore i 1 GiB RAM 
```
kubectl create namespace lab4
kubectl create quota lab4-quota --namespace=lab4 --hard=limits.cpu=1000m,limits.memory=1Gi,pods=5
```

# 2. Uruchom Deployment o nazwie restrictednginx w przestrzeni nazw lab4 z 3 pod-ami gdzie każdy Pod początkowo żąda: 64 MiB RAM oraz 125m CPU , a górny limit zasobów to 256 MiB RAM oraz 250m CPU. 
```
kubectl create deploy restrictednginx --image=nginx -n lab4 --replicas=3
kubectl set resources deployment restrictednginx -n lab4 --limits=cpu=250m,memory=256Mi --requests=cpu=125m,memory=64Mi
```
# 3. Potwierdź poprawność uruchomienia tych pod-ów za pomocą wybranych samodzielnie poleceń.
```
kubectl describe deployment restrictednginx -n lab4
```
![lab4_chmury](https://github.com/Smoofky/Kubernetes/assets/141446663/ee5b8709-64f6-4cb1-a950-651a32f1e989)
