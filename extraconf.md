
vagrant ssh node-X
sudo -s

nano /etc/systemd/system/kubelet.service.d/10-kubeadm.conf

Environment="KUBELET_EXTRA_ARGS=--node-ip=192.168.77.21"
systemctl daemon-reload && systemctl restart kubelet
