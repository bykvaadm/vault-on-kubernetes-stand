vagrant ssh master

cd /opt
wget https://get.helm.sh/helm-v3.5.2-linux-amd64.tar.gz
tar zxvf helm-v3.5.2-linux-amd64.tar.gz
mv linux-amd64/helm  /usr/local/bin/

kubectl create ns vault

cd /vagrant/helm/
helm repo add hashicorp https://helm.releases.hashicorp.com
helm upgrade --install vault hashicorp/vault -n vault -f values-vault.yaml


helm repo add bitnami https://charts.bitnami.com/bitnami
helm upgrade --install etcd-vault bitnami/etcd -n vault -f values-etcd.yaml

helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
kubectl create ns ingress
helm install ingress-nginx ingress-nginx/ingress-nginx -n ingress
