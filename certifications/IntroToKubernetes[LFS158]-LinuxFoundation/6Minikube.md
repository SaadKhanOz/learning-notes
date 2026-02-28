What Is Minikube?

Minikube is one of the easiest, most flexible and popular methods to run an all-in-one or a multi-node local Kubernetes cluster directly on our local workstations. It installs and runs on any native OS such as Linux, macOS, or Windows. However, in order to fully take advantage of all the features Minikube has to offer, a Type-2 Hypervisor or a Container Runtime should be installed on the local workstation, to run in conjunction with Minikube. The role of the hypervisor or container runtime is to offer an isolated infrastructure for the Minikube Kubernetes cluster components, that is easily reproducible, easy to use and tear down. This isolation of the cluster components from our daily environment ensures that once no longer needed, the Minikube components can be safely removed leaving behind no configuration changes to our workstation, thus no traces of their existence. This does not mean, however, that we are responsible for the provisioning of any VMs or containers with guest operating systems with the help of the hypervisor or container runtime. Minikube includes the necessary adapters to interact directly with the isolation software of choice to build all its infrastructure as long as the Type-2 Hypervisor or Container Runtime is installed on our workstation.

Minikube is built on the capabilities of the libmachine library originally designed by Docker to build Virtual Machine container hosts on any physical infrastructure. In time Minikube became very flexible, supporting several hypervisors and container runtimes, depending on the host workstation's native OS.

For those who feel more adventurous, Minikube can be installed without an isolation software, on bare-metal, which may result in permanent configuration changes to the host OS. To prevent such permanent configuration changes, a second form of isolation can be achieved by installing Minikube inside a Virtual Machine provisioned with a Type-2 Hypervisor of choice, and a desktop guest OS of choice (with enabled GUI). As a result, when installed inside a VM, Minikube will end up making configuration changes to the guest environment, still isolated from the host workstation. Therefore, now we have two distinct methods to isolate the Minikube environment from our host workstation.

The isolation software can be specified by the user with the --driver option, otherwise Minikube will try to find a preferred method for the host OS of the workstation.

Once decided on the isolation method, the next step is to determine the required number of Kubernetes cluster nodes, and their sizes in terms of CPU, memory, and disk space. Minikube invokes the hypervisor of choice to provision the infrastructure VM(s) which will host the Kubernetes cluster node(s), or the runtime of choice to run infrastructure container(s) that host the cluster node(s). Keep in mind that Minikube now supports all-in-one single-node and multi-node clusters. Regardless of the isolation method and the expected cluster and node sizes, a local Minikube Kubernetes cluster will ultimately be impacted and/or limited by the physical resources of the host workstation. We have to be mindful of the needs of the host OS and any utilities it may be running, then the needs of the hypervisor or the container runtime, and finally the remaining resources that can be allocated to our Kubernetes cluster. For a learning environment the recommendations are that a Kubernetes node has 2 CPU cores (or virtual CPUs) at a minimum, at least 2 GB of RAM memory (with 4 - 8 GB of RAM recommended for optimal usage), and 20+ GB of disk storage space. When migrating towards a larger, more dynamic, production grade cluster, these resource values should be adjusted accordingly. The Kubernetes nodes are expected to access the internet as well, for software updates, container image downloads, and for client accessibility.

Following the node(s)' provisioning phase, Minikube invokes kubeadm, to bootstrap the Kubernetes cluster components inside the previously provisioned node(s). We need to ensure that we have the necessary hardware and software required by Minikube to build our environment.


Requirements for Running Minikube
VT-x/AMD-v virtualization

VT-x/AMD-v virtualization may need to be enabled on the local workstation for certain hypervisors.

kubectl

kubectl command line client (CLI) is a binary used to access and manage any Kubernetes cluster. It is installed through Minikube and accessed through the minikube kubectl command, or it can be installed separately and run as a standalone tool. We will explore kubectl installation and usage in future chapters.

Type-2 hypervisor or container runtime

Without a specified driver, Minikube will try to find an installed hypervisor or a runtime, in the following order of preference (on a Linux host): docker, kvm2, podman, vmware, and virtualbox. If multiple isolation software installations are found, such as docker and virtualbox, Minikube will pick docker over virtualbox if no desired driver is specified by the user. Hypervisors and Container Runtimes supported by various native workstation OSes:

    On Linux VirtualBox, KVM2, and QEMU hypervisors, or Docker and Podman runtimes.
    On macOS VirtualBox, HyperKit, VMware Fusion, Parallels, and QEMU hypervisors, or Docker and Podman runtimes.
    On Windows VirtualBox, Hyper-V, VMware Workstation, and QEMU hypervisors, or Docker and Podman runtimes.

NOTE: Minikube supports a --driver=none (on Linux) option that runs the Kubernetes components bare-metal, directly on the host OS and not inside a VM. With this option a Docker installation is required and a Linux OS on the local workstation, but no hypervisor installation. This driver is recommended for advanced users.

Internet connection on the first Minikube run

This is needed to download packages, dependencies, updates and pull images needed to initialize the Minikube Kubernetes cluster components. Subsequent Minikube runs will require an Internet connection only when new container images need to be pulled from a public container registry or when deployed containerized applications need it for client accessibility. Once a container image has been pulled, it can be reused from the local container runtime image cache without an Internet connection.


Installing Minikube on Linux

Let's learn how to install the latest Minikube release on Ubuntu Linux 22.04 LTS with VirtualBox v7.0 specifically. This installation assumes no other isolation software is installed on our Linux workstation, such as KVM2, QEMU, Docker Engine or Podman, that Minikube can use as a driver.

NOTE: For other Linux OS distributions or releases, VirtualBox and Minikube versions, the installation steps may vary! Check the Minikube installation for specific installation instructions!

Verify the virtualization support on your Linux OS in a terminal (a non-empty output indicates supported virtualization):

$ grep -E --color 'vmx|svm' /proc/cpuinfo

The easiest way to download and install the VirtualBox hypervisor for Linux is from its official download site. VirtualBox is available for many Linux distributions such as Oracle Linux, RHEL, CentOS 7, Ubuntu, Debian, openSUSE, and Fedora.

Minikube can be easily downloaded and installed in a terminal. Either the latest release or a specific release available from the Minikube release page can be installed by running the following commands. While these installation commands reflect the official installation guide at the time of this course content update, they may change in the near future as part of the continuous growth of Kubernetes. It is strongly recommended to inspect the official installation guide for Linux > x86-64 > Stable when attempting the installation, to ensure the most up-to-date package repositories are used in the process. Below we are presenting the Binary download option, a distribution neutral installation approach:

$ curl -LO \
https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64

$ sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64

NOTE: Replacing /latest/ with a particular version, such as /v1.31.2/ will download that specified Minikube version.

Start Minikube. In a terminal we can start Minikube with the minikube start command, which bootstraps a single-node cluster with the latest supported stable Kubernetes version release. For a specific Kubernetes version the --kubernetes-version option can be used as such minikube start --kubernetes-version=v1.27.1 (where latest is default and acceptable version value, and stable is also acceptable). In case there are other virtualization driver candidates for Minikube on the workstation, it is good practice to supply the desired driver with the --driver=virtualbox option. More advanced start options will be explored later in this chapter:

$ minikube start --driver=virtualbox

😄 minikube v1.32.0 on Ubuntu 22.04
✨ Using the virtualbox driver based on user configuration
💿 Downloading VM boot image ...
   > minikube-v1.32.1-amd64.iso....: 65 B / 65 B [---------] 100.00% ? p/s 0s
   > minikube-v1.32.1-amd64.iso: 292.96 MiB / 292.96 MiB 100.00% 31.34 MiB p
👍 Starting control plane node minikube in cluster minikube
💾 Downloading Kubernetes v1.28.3 preload ...
   > preloaded-images-k8s-v18-v1...: 403.35 MiB / 403.35 MiB 100.00% 32.19 M
🔥 Creating virtualbox VM (CPUs=2, Memory=6000MB, Disk=20000MB) ...
🐳 Preparing Kubernetes v1.28.3 on Docker 24.0.7 ...
   ▪ Generating certificates and keys ...
   ▪ Booting up control plane ...
   ▪ Configuring RBAC rules ...
🔗 Configuring bridge CNI (Container Networking Interface) ...
🔎 Verifying Kubernetes components...
   ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟 Enabled addons: storage-provisioner, default-storageclass
💡 kubectl not found. If you need it, try: 'minikube kubectl -- get pods -A'
🏄 Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default

NOTE: An error message that reads "Unable to pick a default driver..." means that Minikube was not able to locate any one of the supported hypervisors or runtimes. The recommendation is to install or re-install a desired isolation tool, and ensure its executable is found in the default PATH of your OS distribution.

NOTE: An error message that reads “The vboxdrv kernel module is not loaded” means that a critical VirtualBox kernel module may not be available. First, try to re-install VirtualBox on the workstation. Second, try installing a C compiler that may be missing from your workstation and then build the kernel module. For the Ubuntu 22.04 LTS OS the required gcc compiler can be downloaded and installed from https://packages.ubuntu.com/jammy/amd64/gcc-12/download. The kernel module can be built with the sudo /sbin/vboxconfig command. After a successful rebuild, attempt to start minikube again with virtualbox using the command above.

Check the status. With the minikube status command, we display the status of the Minikube cluster:

$ minikube status

minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

Stop Minikube. With the minikube stop command, we can stop Minikube. This command stops all applications running in Minikube, safely stops the cluster and the VirtualBox VM, preserving our work until we decide to start the Minikube cluster once again, while preserving the Minikube VM:

$ minikube stop

✋  Stopping node "minikube"  ...
🛑  1 node stopped.

When it is time to run the cluster again, simply run the minikube start command (driver option is not required), and it will restart the earlier bootstrapped Minikube cluster.

Remove Minikube. The minikube delete command completely removes Minikube and the Minikube VM. This command should be attempted only when the Minikube cluster is to be decommissioned. All work will be lost after the completion of this command:

$ minikube delete

🔥 Deleting "minikube" in virtualbox ...
💀 Removed all traces of the "minikube" cluster.

NOTE:
if virtualbox is not working, then install docker and then use command:
minikube start --driver=docker

Advanced Minikube Features (1)

Now that we have familiarized ourselves with the default minikube start command, let's dive deeper into Minikube to understand some of its more advanced features.

The minikube start by default selects a driver isolation software, such as a hypervisor or a container runtime, if one (VitualBox) or multiple are installed on the host workstation. In addition it downloads the latest Kubernetes version components. With the selected driver software it provisions a single VM named minikube (with hardware profile of CPUs=2, Memory=6GB, Disk=20GB) or container (Docker) to host the default single-node all-in-one Kubernetes cluster. Once the node is provisioned, it bootstraps the Kubernetes control plane (with the default kubeadm tool), and it installs the latest version of the default container runtime, Docker, that will serve as a running environment for the containerized applications we will deploy to the Kubernetes cluster. The minikube start command generates a default minikube cluster with the specifications described above and it will store these specs so that we can restart the default cluster whenever desired. The object that stores the specifications of our cluster is called a profile.

As Minikube matures, so do its features and capabilities. With the introduction of profiles, Minikube allows users to create custom reusable clusters that can all be managed from a single command line client.

The minikube profile command allows us to view the status of all our clusters in a table formatted output. Assuming we have created only the default minikube cluster, we could list the properties that define the default profile with:

$ minikube profile list

|----------|------------|---------|----------------|------|---------|---------|-------|--------|
| Profile  | VM Driver  | Runtime |       IP       | Port | Version | Status  | Nodes | Active |
|----------|------------|---------|----------------|------|---------|---------|-------|--------|
| minikube | virtualbox | docker  | 192.168.59.100 | 8443 | v1.28.3 | Running |     1 | *      |
|----------|------------|---------|----------------|------|---------|---------|-------|--------|

This table presents the columns associated with the default properties such as the profile name: minikube, the isolation driver: VirtualBox, the container runtime: Docker, the Kubernetes version: v1.28.3, the status of the cluster - running or stopped. The table also displays the number of nodes: 1 by default, the private IP address of the minikube cluster's control plane VirtualBox VM, and the secure port that exposes the API Server to cluster control plane components, agents and clients: 8443. 

What if we desire to create several reusable clusters instead, with other drivers (Docker or Podman - still experimental on Linux) for node isolation, or different Kubernetes versions (v1.27.10 or v1.28.1), another runtime (cri-o or containerd), and possibly 2, 3, or more nodes (if permitted by the resources of our host system)? What if we desire to further customize the cluster with a specific networking option or plugin? The minikube start command allows us to create such custom profiles with the --profile or -p flags. Several of the isolation drivers support creation of node VMs or node containers of custom sizes as well, features that we will not explore in this course as not all are very stable at the time of this writing.

Below are a few examples of more complex start commands that allow custom clusters to be created with Minikube. They assume that the desired driver software (Docker and/or Podman) has been installed on the host workstation. There is no need to download the desired CNI (network plugin) or the container runtime, they will be set up and enabled by Minikube on our behalf:

$ minikube start --kubernetes-version=v1.27.10 \
  --driver=podman --profile minipod

$ minikube start --nodes=2 --kubernetes-version=v1.28.1 \
  --driver=docker --profile doubledocker

$ minikube start --driver=virtualbox --nodes=3 --disk-size=10g \
  --cpus=2 --memory=6g --kubernetes-version=v1.27.12 --cni=calico \
  --container-runtime=cri-o -p multivbox

$ minikube start --driver=docker --cpus=6 --memory=8g \
  --kubernetes-version="1.27.12" -p largedock

$ minikube start --driver=virtualbox -n 3 --container-runtime=containerd \
  --cni=calico -p minibox

Once multiple cluster profiles are available (the default minikube and custom minibox), the profiles table will look like this:

$ minikube profile list

|----------|------------|---------|----------------|------|---------|---------|-------|--------|
| Profile  | VM Driver  | Runtime |       IP       | Port | Version | Status  | Nodes | Active |
|----------|------------|---------|----------------|------|---------|---------|-------|--------|
| minibox  | virtualbox | crio    | 192.168.59.101 | 8443 | v1.25.3 | Running |     3 |        |
| minikube | virtualbox | docker  | 192.168.59.100 | 8443 | v1.25.3 | Running |     1 | *      |
|----------|------------|---------|----------------|------|---------|---------|-------|--------|

The active marker indicates the target cluster profile of the minikube command line tool, also known as its context. The target cluster can be set to minibox with the following command:

$ minikube profile minibox

The target cluster can be set to the default minikube with one of the following commands:

$ minikube profile minikube

$ minikube profile default



Advanced Minikube Features (2)

Most minikube commands, such as start, stop, node, etc. are profile aware, meaning that the user is required to explicitly specify the target cluster of the command, through its profile name. The default minikube cluster, however, can be managed implicitly without specifying its profile name. Stopping and re-starting the two clusters listed above, the minibox cluster (explicitly) and the default minikube cluster (implicitly):

$ minikube stop -p minibox

$ minikube start -p minibox

$ minikube stop

$ minikube start

Additional helpful minikube commands:

To display the version of the current Minikube installation:

$ minikube version

minikube version: v1.32.0
commit: 8220a6eb95f0a4d75f7f2d7b14cef975f050512d

Completion is a helpful post installation configuration to enable the minikube command to respond to typical auto-completion mechanisms, such as completing a command in the terminal by pressing the TAB key. To enable completion for the bash shell on Ubuntu:

$ sudo apt install bash-completion

$ source /etc/bash_completion

$ source <(minikube completion bash)

If needed, also run the following command:

$ minikube completion bash

A command that allows users to list the nodes of a cluster, add new control plane or worker nodes, delete existing cluster nodes, start or stop individual nodes of a cluster:

$ minikube node list

minikube 192.168.59.100

$ minikube node list -p minibox

minibox   192.168.59.101
minibox-m02   192.168.59.102
minibox-m03   192.168.59.103

To display the cluster control plane node's IP address, or another node's IP with the --node or -n flags:

$ minikube ip

192.168.59.100

$ minikube -p minibox ip

192.168.59.101

$ minikube -p minibox ip -n minibox-m02

192.168.59.102

When a cluster configuration is no longer of use, the cluster's profile can be deleted. It is also a profile aware command - it deletes the default minikube cluster if no profile is specified, or a custom cluster if its profile is specified:

$ minikube delete

🔥  Deleting "minikube" in virtualbox ...
💀  Removed all traces of the "minikube" cluster.

$ minikube delete -p minibox

🔥  Deleting "minibox" in virtualbox ...
🔥  Deleting "minibox-m02" in virtualbox ...
🔥  Deleting "minibox-m03" in virtualbox ...
💀  Removed all traces of the "minibox" cluster.

For additional commands and usage options please visit the Minikube command line reference. 


