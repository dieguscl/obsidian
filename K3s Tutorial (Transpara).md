## Install Helm

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```
## Requirements

https://docs.k3s.io/installation/requirements

## Installation

Run the following command to install `kubectl`, `k3s`, and a couple of scripts
```bash
curl -sfL https://get.k3s.io | sh -
```
Now set up permissions to be able to run `kubectl` without `sudo`
```bash
sudo groupadd k3s
sudo usermod -aG k3s transpara
sudo chgrp k3s /etc/rancher/k3s/k3s.yaml
sudo chmod 660 /etc/rancher/k3s/k3s.yaml
newgrp k3s
```


## Uninstall

```bash
/usr/local/bin/k3s-killall.sh
sudo /usr/local/bin/k3s-uninstall.sh
```

## Autocomplete

```bash
echo "source <(kubectl completion bash)" >> ~/.bashrc
source ~/.bashrc
```