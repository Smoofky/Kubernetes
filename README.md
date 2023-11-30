# 1. Należy uruchomić serwer WWW o nazwie lab8server w przestrzeni nazw restricted, używając obraz nginx oraz utworzyć dla niego Service typu ClusterIP.
Plik **nginx_deployment.yaml** zawiera deklaracje serwera WWW w przestrzeni nazw restricted wraz z serwisem typu clusterIP. Poniżej przedstawiam polecenia.
```
kubectl create namespace restricted # Tworzenie przestrzeni nazw 'restricted'
kubectl apply -f nginx_deployment.yaml # Tworzenie serwera WWW poprzez gotowy plik yaml
```
# 2. W domyślnej przestrzeni nazw należy uruchomić dwa Pod-y: Sleepybox1 i Sleepybox2, każdy oparty na obrazie busybox i wykonujący przy polecenie: sleep 3600
Wykorzystałem plik **sleepybox_deployment.yaml** do utworzenia dwóch podów, gdzie Sleepybox1 ma również ustawiony label app:sleepybox1.
```
kubectl apply -f sleepybox_deployment.yaml # Tworzenie dwóch podów
```
# 3. Należy utworzyć NetworkPolicy, który ogranicza ruch przychodzący do przestrzeni nazw restricted w taki sposób, że dostęp do lab8server ma tylko pod Sleepybox1 z domyślnej przestrzeni nazw a każdy inny dostęp do przestrzeni restricted jest zabroniony
Stworzyłem plik **network_policy.yaml**, który definiuje ruch przychodzący (ingress) w przestrzeni nazw z labelem default oraz określa, których podów to dotyczy (podSelector - matchLabel). Więc efekt powinien być taki, że pod z przestrzeni default z labelem sleepybox1 powinien móc dostać się do servera WWW, natomiast inne pody z tej przestrzeni nie będą mogły się dostać bez odpowiedniego labela.
```
kubectl apply -f network-policy.yaml
```

# Weryfikacja

![chmury](https://github.com/Smoofky/Kubernetes/assets/141446663/b1bca9ce-a22a-452c-8a6a-ac85eff351d4)
