# RKE2 (cli) Install
https://docs.rke2.io/install/quickstart
```
# curl -sfL https://get.rke2.io | INSTALL_RKE2_VERSION=v1.26.3+rke2r1 sh -
#
# Environment variables:
#
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
# export KUBECONFIG=/etc/rancher/rke2/rke2.yaml
# kubectl get pods --all-namespaces
# helm ls --all-namespaces
```


# RKE2 (cli) Uninstall
https://docs.rke2.io/install/uninstall
```
# /usr/local/bin/rke2-uninstall.sh
```


# RKE/RKE2 (web ui)
https://www.rancher.com/quick-start
```
# sudo docker run --privileged -d --restart=unless-stopped -p 80:80 -p 443:443 rancher/rancher
```


# RKE2 (system requirements)
https://docs.rke2.io/install/requirements
```
#
# Make sure your environment fulfills the requirements. If NetworkManager is installed and enabled on your hosts, ensure that it is configured to ignore CNI-managed interfaces.
# For RKE2 versions 1.21 and higher, if the host kernel supports AppArmor, the AppArmor tools (usually available via the apparmor-parser package) must also be present prior to installing RKE2.
# The RKE2 installation process must be run as the root user or through sudo.
```
