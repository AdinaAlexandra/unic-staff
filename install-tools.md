
Commands to install tools on github workspaces or jump hosts vm's 

Install Argo CD CLI To interact with the API Server we need to deploy the CLI:

sudo curl --silent --location -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/download/v2.4.7/argocd-linux-amd64

sudo chmod +x /usr/local/bin/argocd



#sudo apt-get update
#sudo apt-get install -y kubectl


VERSION="latest"  # You can specify a specific version if needed
wget https://mirror.openshift.com/pub/openshift-v4/clients/oc/$VERSION/linux/oc.tar.gz
tar -xvf oc.tar.gz
sudo mv oc /usr/local/bin/
rm oc.tar.gz


curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh


KUSTOMIZE_VERSION="v4.2.0"  # Replace with the desired version
wget https://github.com/kubernetes-sigs/kustomize/releases/download/kustomize%2F${KUSTOMIZE_VERSION}/kustomize_${KUSTOMIZE_VERSION}_linux_amd64.tar.gz
tar -xvf kustomize_${KUSTOMIZE_VERSION}_linux_amd64.tar.gz
sudo mv kustomize /usr/local/bin/
rm kustomize_${KUSTOMIZE_VERSION}_linux_amd64.tar.gz



sudo apt-get update
sudo apt-get install -y maven


TKN_VERSION="0.26.0"  # Replace with the desired version
wget https://github.com/tektoncd/cli/releases/download/v${TKN_VERSION}/tkn_${TKN_VERSION}_Linux_x86_64.tar.gz
tar -xvf tkn_${TKN_VERSION}_Linux_x86_64.tar.gz


sudo mv tkn /usr/local/bin/



echo "deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_20.04/ /" | sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list

curl -L "https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_20.04/Release.key" | sudo apt-key add -

sudo apt update


sudo apt-get install -y podman skopeo buildah



##end
at the gitops labs:
argocd login gitops url 

replace gitops url with right hostname 

use admin and password from oc cli command :

oc extract secret/openshift-gitops-cluster -n openshift-gitops --to=-

argocd login openshift-gitops-server-openshift-gitops.apps.training1.openshift.labs.sass.ro WARNING: server certificate had error: x509: certificate signed by unknown authority. Proceed insecurely (y/n)? y WARN[0003] Failed to invoke grpc call. Use flag --grpc-web in grpc calls. To avoid this warning message, use flag --grpc-web. Username: admin Password: 'admin:login' logged in successfully Context 'openshift-gitops-server-openshift-gitops.apps.training1.openshift.labs.sass.ro' updated


