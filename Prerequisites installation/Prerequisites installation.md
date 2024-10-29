# Prerequisites

## Gnome
Install gnome-terminal :

```bash
sudo apt install gnome-terminal
```

## Docker
Set up Docker's `apt` repository :

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

Download the DEB package : [Docker DEB](https://desktop.docker.com/linux/main/amd64/docker-desktop-amd64.deb?utm_source=docker&utm_medium=webreferral&utm_campaign=docs-driven-download-linux-amd64)

Install the package with apt as follows :

```bash
# Fix the path of installtion to match with the location of downloaded Docker DEB package
sudo apt-get update
sudo apt-get install ./docker-desktop-<arch>.deb
```

Ensure the version is well installed and up-to-date

```bash
docker --version
```

## Kubectl

Kubectl allows the management of Kubernetes with CLI.

Download the latest release

```bash
  curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

Validate the binary

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
```

If it's valid, the output shall be the following :

```console
kubectl: OK
```

Install kubectl

```bash
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

Ensure the version is well installed and up-to-date

```bash
kubectl version --client
```

## Helm

Helm is a package manager for Kubernetes.

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

## Make

Make is maybe already installed.

```bash
make --version
```

If it not the case, install it.

```bash
sudo apt-get update
sudo apt-get install make
make --version
```

## Python3

Python is maybe already installed.

```bash
python3 --version
```

If it not the case, install it.

```bash
sudo apt-get update
sudo apt-get install python3
sudo apt-get install python3-pip
python3 --version
pip3 --version
```

The following command allows to call `python3` command even if `python` is called.  
```bash
sudo ln -s /usr/bin/python3 /usr/bin/python
```

## K3d

K3d ease the execution of Kubernetes lights clusters for local developement, by using k3s in Docker clusters.
`k3d` facilite l'exécution de clusters Kubernetes légers en utilisant `k3s` dans des conteneurs Docker.
```bash
curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
k3d --version
```
## Check installations and permissions

### Check installation
```bash
docker --version
kubectl version
helm version
make --version
python3 --version
k3d --version
```

### Check permission
```bash
	ls -l /usr/local/bin/<location>
OR
	ls -l $(which k3d)

```


### Modify permission
If there is a permission denied, then set it to 755 (-rwx r-x r-x 1 root root)
```bash
sudo chmod 755 /usr/local/bin/<location>
```