Accessing Minikube

Any healthy running Kubernetes cluster can be accessed via any one of the following methods: Command Line Interface (CLI) tools and scripts, web-based User Interface (Web UI) from a web browser, APIs from CLI or programmatically.

These methods are applicable to all Kubernetes clusters.

Command Line Interface (CLI)

kubectl is the Kubernetes Command Line Interface (CLI) client to manage cluster resources and applications. It is very flexible and easy to integrate with other systems, therefore it can be used standalone, or part of scripts and automation tools. Once all required credentials and cluster access points have been configured for kubectl, it can be used remotely from anywhere to access a cluster.

We will be using kubectl extensively to deploy applications, manage and configure Kubernetes resources.

Web-based User Interface (Web UI)

The Kubernetes Dashboard provides a Web-based User Interface (Web UI) to interact with a Kubernetes cluster to manage resources and containerized applications. While not as flexible as the kubectl CLI client tool, it is still a preferred tool to users who are not as proficient with the CLI.

APIs

The main component of the Kubernetes control plane is the API Server, responsible for exposing the Kubernetes APIs. The APIs allow operators and users to directly interact with the cluster. Using both CLI tools and the Dashboard UI, we can access the API server running on the control plane node to perform various operations to modify the cluster's state. The API Server is accessible through its endpoints by agents and users possessing the required credentials.

Below, we can see the representation of the HTTP API directory tree of Kubernetes:

![Http apis directory](images/httpdir.png)

HTTP API directory tree of Kubernetes can be divided into three independent group types:

    Core group (/api/v1)
    This group includes objects such as Pods, Services, Nodes, Namespaces, ConfigMaps, Secrets, etc.
    Named group
    This group includes objects in /apis/$NAME/$VERSION format. These different API versions imply different levels of stability and support:
    - Alpha level - it may be dropped at any point in time, without notice. For example, /apis/batch/v2alpha1.
    - Beta level - it is well-tested, but the semantics of objects may change in incompatible ways in a subsequent beta or stable release. For example, /apis/certificates.k8s.io/v1beta1.
    - Stable level - appears in released software for many subsequent versions. For example, /apis/networking.k8s.io/v1.
    System-wide
    This group consists of system-wide API endpoints, like /healthz, /logs, /metrics, /ui, etc.

We can access an API Server either directly by calling the respective API endpoints, using the CLI tools, or the Dashboard UI.

Next, we will see how we can access the Minikube Kubernetes cluster we set up in the previous chapter.



kubectl

kubectl allows us to manage local Kubernetes clusters like the Minikube cluster, or remote clusters deployed in the cloud. It is generally installed before installing and starting Minikube, but it can also be installed after the cluster bootstrapping step.

A Minikube installation has its own kubectl CLI installed and ready to use. However, it is somewhat inconvenient to use as the kubectl command becomes a subcommand of the minikube command. Users would be required to type longer commands, such as minikube kubectl -- <subcommand> <object-type> <object-name> -o --option, instead of just kubectl <subcommand> <object-type> <object-name> -o --option. While a simple solution would be to set up an alias, the recommendation is to run the kubectl CLI tool as a standalone installation.

Once separately installed, kubectl receives its configuration automatically for Minikube Kubernetes cluster access. However, in different Kubernetes cluster setups, we may need to manually configure the cluster access points and certificates required by kubectl to securely access the cluster.

There are different methods that can be used to install kubectl listed in the Kubernetes documentation. For best results, it is recommended to keep kubectl within one minor version of the desired Kubernetes release. Next, we will describe the kubectl CLI installation process.

Additional details about the kubectl command line client can be found in the kubectl book, the Kubernetes official documentation, or its GitHub repository.

Installing kubectl on Linux

To install kubectl on Linux, follow the instructions below extracted from the official installation guide.

Download and install the latest stable kubectl binary:

$ curl -LO "htt‌‌ps://dl.k8s.io/release/$(curl -L -s \
htt‌‌ps://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

$ sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

Where ht‌tps://dl.k8s.io/release/stable.txt aims to display the latest Kubernetes stable release version.

NOTE: To download and set up a specific version of kubectl (such as v1.28.3) to be aligned with the Kubernetes version of the Minikube cluster, issue the following command instead:

$ curl -LO ht‌‌tps://dl.k8s.io/release/v1.28.3/bin/linux/amd64/kubectl

The installed version can be verified with:

$ kubectl version --client

A typical helpful post-installation configuration is to enable shell autocompletion for kubectl. For bash shell it can be achieved by running the following sequence of commands:

$ sudo apt update && sudo apt install -y bash-completion

$ source /usr/share/bash-completion/bash_completion

$ source <(kubectl completion bash)

$ echo 'source <(kubectl completion bash)' >> ~/.bashrc



