# Scaling-operator
This is a simple scaling operator based on operator-sdk, it can scale up or down to the number of replicas you want.

## Description
The detail of this scaling operator is described in both `scaler_types.go` and also `scaler_controller.go`, which contains the spec and also the scaling logic of the scaling operator.

## Getting Started
1. Make sure you have [Docker](https://www.docker.com/) installed, and also Kubernetes enabled.
2. You’ll need a Kubernetes cluster to run, You can use [KIND](https://sigs.k8s.io/kind) to get a local cluster for testing, or run against a remote cluster. You might need to install kind if it's not installed yet in your environment.
**Note:** Your controller will automatically use the current context in your kubeconfig file (i.e. whatever cluster `kubectl cluster-info` shows).

### Running on the cluster
1. Clone this project, direct to the folder.

2. Create a local cluster, here I use kind as an example. Make sure Docker is running in the background.
```sh
kind create cluster
```

3. Install Instances of Custom Resources:

```sh
kubectl apply -f config/crd/bases/api.nextfaas.com_scalers.yaml
```
You can check the CRD if it's correctly installed with this command:

```sh
kubectl get crd
```

4. Now you can deploy one function to test the scaling operator. Build and push your image to the location specified by `IMG`:

```sh
make docker-build docker-push IMG=<some-registry>/scaling-operator:tag
```

5. Deploy the controller to the cluster with the image specified by `IMG`:

```sh
make deploy IMG=<some-registry>/scaling-operator:tag
```

6. Run the Operator:
   
```sh
make run
```

7. Apply the scaling requirements:
```sh
kubectl apply -f config/samples/api_v1alpha1_scaler.yaml
```

8. See the result of the replicas:
```sh
kubectl get pods
```


### Uninstall CRDs
To delete the CRDs from the cluster:

```sh
make uninstall
```

### Undeploy controller
UnDeploy the controller from the cluster:

```sh
make undeploy
```

### How it works
This project aims to follow the Kubernetes [Operator pattern](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/).

It uses [Controllers](https://kubernetes.io/docs/concepts/architecture/controller/),
which provide a reconcile function responsible for synchronizing resources until the desired state is reached on the cluster.

### Test It Out
1. Install the CRDs into the cluster:

```sh
make install
```

2. Run your controller (this will run in the foreground, so switch to a new terminal if you want to leave it running):

```sh
make run
```

**NOTE:** Run `make --help` for more information on all potential `make` targets

More information can be found via the [Kubebuilder Documentation](https://book.kubebuilder.io/introduction.html)

## License

Copyright 2024.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

