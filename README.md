# Local multi-node Kubernetes clusters using kind

#########
# Setup #
#########

# Install kind (https://kind.sigs.k8s.io/docs/user/quick-start/#installation)

# Install Docker Desktop if macOS or Windows, or Docker if Linux

# Disable Kubernetes in Docker Desktop

#################################
# Creating single-node clusters #
#################################

export KUBECONFIG=$PWD/kubeconfig.yaml

kind create cluster --name my-cluster

docker container ls

kubectl get nodes

##################
# Loading images #
##################

kind load --help

################################
# Creating additional clusters #
################################

kind create cluster \
    --name another-cluster

docker container ls

#####################
# Deleting clusters #
#####################

kind delete cluster --name my-cluster

kind delete cluster --name another-cluster

#####################################
# Creating clusters through configs #
#####################################

git clone https://github.com/vfarcic/kind-demo.git

cd kind-demo

cat multi-node.yaml

kind create cluster \
    --config multi-node.yaml

kubectl get nodes

docker container ls

kubectl apply --filename k8s/

# Open http://localhost in a browser

kubectl apply \
    --filename https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/kind/deploy.yaml

# Wait for a while and reload the browser

#####################
# Deleting clusters #
#####################

kind delete cluster --name kind
