# staticroute-operator
Static IP route operator for Kubernetes clusters

# Prerequisites
The following components are needed to be installed on your environment:
  * git
  * go 1.13+
  * docker
  * kubectl v1.12.0 or newer
  * golangci-lint v1.23.6
  * Operator SDK CLI (more information: https://github.com/operator-framework/operator-sdk/blob/master/doc/user/install-operator-sdk.md)
  * and access to a Kubernetes cluster on a version v1.12.0 or newer
  * before you run any of the make target below, make sure the following are done:
    - export `REGISTRY_REPO` environment variable to your docker registry repo url (ie.: quay.io/example/staticroute-operator:v0.0.1)
    - export `KUBECONFIG` environment variable to the path of kubeconfig file (if not set, default $$HOME/.kube/config will be used)
    - login to your docker registry using your credentials (ie.: docker login... , ibmcloud cr login etc.)

# Updating the Custom Resource Definitions (CRDs)
Make sure, that every time you modify anything in `*_types.go` file, run the `make update-operator-resource` to update generated code for `k8s` and `CRDs`.

# Building the static route operator
`make dev-publish-image` target can be used for updating, building and publishing the operator image into your Docker repository

# Testing the changes
Once you have made changes in the source, you have two option to run and test your operator:
- as a `deployment` inside a Kubernetes cluster
- as a binary program running locally on your development environment
  1. Run as a deployment inside your cluster
     - run the `make dev-run-operator-remote` target which updates your operator resources, builds the operator, pushes the built operator docker image to the `REGISTRY_REPO`, changes the operator manifest file and creates the Kubernetes resources (CRDs, operator, role, rolebinding and service account) inside the cluster
     - you can remove the operator resources using `make dev-cleanup-operator` target
  2. Run as a Go program on your local development environment
     - run `make dev-run-operator-local`