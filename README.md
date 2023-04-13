# RKE2 (cli) Install
https://docs.rke2.io/install/quickstart

## Server install
```
curl -sfL https://get.rke2.io | INSTALL_RKE2_VERSION=v1.26.3+rke2r1 INSTALL_RKE2_TYPE=server sh -

# Enable the rke2-server service
systemctl enable rke2-server.service

# Start the service
systemctl start rke2-server.service

# <SERVER_TOKEN>
cat /var/lib/rancher/rke2/server/node-token
```

## Agent install
```
curl -sfL https://get.rke2.io | INSTALL_RKE2_VERSION=v1.26.3+rke2r1 INSTALL_RKE2_TYPE=agent sh -

# Enable the rke2-agent service
systemctl enable rke2-agent.service

# Configure the rke2-agent service
mkdir -p /etc/rancher/rke2/

# <SERVER_TOKEN> (server)
/var/lib/rancher/rke2/server/node-token

# Content for config.yaml:
cat << EOF > /etc/rancher/rke2/config.yaml
server: https://<SERVER_IP>:9345
token: <SERVER_TOKEN>
EOF

# Start the service
systemctl start rke2-agent.service


```

## Environment variables:
```
#   - INSTALL_RKE2_CHANNEL
#     Channel to use for fetching rke2 download URL.
#     Defaults to 'latest'.
#
#   - INSTALL_RKE2_METHOD
#     The installation method to use.
#     Default is on RPM-based systems is "rpm", all else "tar".
#
#   - INSTALL_RKE2_TYPE
#     Type of rke2 service. Can be either "server" or "agent".
#     Default is "server".
#
#   - INSTALL_RKE2_EXEC
#     This is an alias for INSTALL_RKE2_TYPE, included for compatibility with K3s.
#     If both are set, INSTALL_RKE2_TYPE is preferred.
#
#   - INSTALL_RKE2_VERSION
#     Version of rke2 to download from github.
#
#   - INSTALL_RKE2_RPM_RELEASE_VERSION
#     Version of the rke2 RPM release to install.
#     Format would be like "1.el7" or "2.el8"
#
#   - INSTALL_RKE2_TAR_PREFIX
#     Installation prefix when using the tar installation method.
#     Default is /usr/local, unless /usr/local is read-only or has a dedicated mount point,
#     in which case /opt/rke2 is used instead.
#
#   - INSTALL_RKE2_COMMIT
#     Commit of RKE2 to download from temporary cloud storage.
#     For developer & QA use only
#
#   - INSTALL_RKE2_AGENT_IMAGES_DIR
#     Installation path for airgap images when installing from CI commit
#     Default is /var/lib/rancher/rke2/agent/images
#
#   - INSTALL_RKE2_ARTIFACT_PATH
#     If set, the install script will use the local path for sourcing the rke2.linux-$SUFFIX and sha256sum-$ARCH.txt files
#     rather than the downloading the files from the internet.
#     Default is not set.
#
#   - INSTALL_RKE2_SKIP_RELOAD
#     If set, the install script will skip reloading systemctl daemon after the tar has been extracted and systemd units
#     have been moved.
#     Default is not set.
```


# RKE/RKE2 (access)
https://docs.rke2.io/cluster_access

```
export KUBECONFIG=/etc/rancher/rke2/rke2.yaml
kubectl get pods --all-namespaces
helm ls --all-namespaces
```


# RKE2 (cli) Uninstall
https://docs.rke2.io/install/uninstall
```
/usr/bin/rke2-uninstall.sh
/usr/local/bin/rke2-uninstall.sh
/usr/local/bin/k3s-uninstall.sh
/usr/local/bin/k3s-agent-uninstall.sh

kubeadm reset
sudo apt-get purge kubeadm kubectl kubelet kubernetes-cni kube*
sudo apt-get autoremove
sudo rm -rf ~/.kube
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
systemctl restart docker

sudo iptables -t filter -F
sudo iptables -t filter -X
sudo netstat -ntlp
```


# RKE/RKE2 (web ui)
https://www.rancher.com/quick-start
```
sudo docker run --privileged -d --restart=unless-stopped -p 80:80 -p 443:443 rancher/rancher
```


# RKE2 (system requirements)
https://docs.rke2.io/install/requirements
```
#
# Make sure your environment fulfills the requirements. If NetworkManager is installed and enabled on your hosts, ensure that it is configured to ignore CNI-managed interfaces.
# For RKE2 versions 1.21 and higher, if the host kernel supports AppArmor, the AppArmor tools (usually available via the apparmor-parser package) must also be present prior to installing RKE2.
# The RKE2 installation process must be run as the root user or through sudo.
```
