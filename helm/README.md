vagrant ssh master

cd /opt
wget https://get.helm.sh/helm-v3.5.2-linux-amd64.tar.gz
tar zxvf helm-v3.5.2-linux-amd64.tar.gz
mv linux-amd64/helm  /usr/local/bin/

kubectl create ns vault
helm repo add hashicorp https://helm.releases.hashicorp.com
helm upgrade --install vault hashicorp/vault -n vault -f values.yaml 


helm repo add bitnami https://charts.bitnami.com/bitnami
helm upgrade --install etcd-vault bitnami/etcd -n vault -f values-etcd.yaml