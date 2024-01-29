1. Install kubectl
2. Kind or Minikube for running clusters
3. kube config (only when running on cloud)
4. Lens for visualizing
5. Servicess

## Running windows on k8s

The Windows operating system plays a key role in running and managing enterprise applications and services. With that in mind, the Kubernetes community worked very hard to bring Windows support to Kubernetes.

With the release of Kubernetes v1.14, Windows was successfully introduced as a [supported](https://kubernetes.io/docs/setup/production-environment/windows/intro-windows-in-kubernetes/ "https://kubernetes.io/docs/setup/production-environment/windows/intro-windows-in-kubernetes/") production ready operating system only for worker nodes of a Kubernetes cluster. This enabled Kubernetes to support the deployment of Windows containers in the cluster, either as a dedicated Windows cluster, or a hybrid cluster with Windows nodes running alongside Linux nodes. Keep in mind, however, that the control plane nodes are limited to running on Linux only, with no plans to extend the support to Windows control plane nodes.

With Windows Server 2019 being the only Windows OS supported by Kubernetes, the same container workload orchestration tool can [schedule](https://kubernetes.io/docs/setup/production-environment/windows/user-guide-windows-containers/ "https://kubernetes.io/docs/setup/production-environment/windows/user-guide-windows-containers/") and deploy both Linux and Windows containers in the same cluster. The user is responsible to configure the workload scheduling according to the expected OS, that is to schedule Linux and Windows containers on nodes with their respective operating systems when nodes of each OS are found in the same Kubernetes cluster.

> Source: edX "Introduction to Kubernetes" course

https://pisquare.osisoft.com/s/question/0D51I00004UHk7sSAD/is-there-a-way-to-create-an-afsdk-docker-container

