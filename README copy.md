# Virtualizacion
* # Parcial 2

Procesos:
Instalar herramientas
    docker version
    minikube version
    kubectl version --client
    helm version
    git --version

iniciar minikube y obtener ip
ip: 192.168.49.2

instalar metalLB
curl.exe -L -o metallb\metallb-native.yaml https://raw.githubusercontent.com/metallb/metallb/v0.14.9/config/manifests/metallb-native.yaml
kubectl apply -f metallb\metallb-native.yaml
kubectl wait -n metallb-system --for=condition=ready pod --all --timeout=120s
Cree metallb/ipaddresspool.yaml (una sola IP):

aplicar la instancia
kubectl apply -f metallb\ipaddresspool.yaml

paso 4
instalar traefic
crear Cree traefik/values.yaml:

instalar traefik
helm install traefik traefik/traefik -n traefik --create-namespace -f traefik\values.yaml
ver los servicios creados por traefik
kubectl get svc -n traefik
el servicio de Traefik está expuesto y qué IP le asignó MetalLB.


paso 5 namespace y 4 apps
 apps/namespace.yaml:
 apps/apps.yaml:
 apps/ingress.yaml (esto hace que Traefik maneje los servicios por dominio):
 Aplique y verifique:
 kubectl apply -f apps\namespace.yaml
kubectl apply -f apps\apps.yaml
kubectl apply -f apps\ingress.yaml
kubectl get all,ingress -n parcial-dryca


paso 6 ver metallb y traefik
Desde dentro del nodo de Minikube (evidencia para el README):
minikube ssh -- curl -s -H "Host: whoami.dryca.test" http://192.168.49.240
o
minikube ssh "curl -s -H 'Host: whoami.dryca.test' http://192.168.49.240"
minikube ssh "curl -s -H 'Host: nginx.dryca.test' http://192.168.49.240"

Paso 7: DNS local (archivo hosts)
Con el driver Docker en Windows, la IP 192.168.49.240 no es alcanzable desde el navegador.
port-forward y hosts apuntando a 127.0.0.1

Add-Content C:\Windows\System32\drivers\etc\hosts "127.0.0.1 nginx.dryca.test 
httpd.dryca.test 
whoami.dryca.test 
hello.dryca.test"

En otra terminal, déjelo corriendo mientras prueba:
kubectl port-forward -n traefik svc/traefik 80:80
entrar a http://nginx.dryca.test:8080