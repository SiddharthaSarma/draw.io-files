# Basic building blocks: Nodes and Pods

### Nodes
Node can be a physical computer or a virtual machine. The Node has the following requirements. Each Node must have a Kubelet running, container tooling, like Docker, a kube-proxy process running, and a process like Supervisord, so it can restart components.
**Note:** If you're using Kubernetes in a production like setting, it's recommended that you have at least a **three Node** cluster.

### Pods
In the Kubernetes model, a Pod is the simplest unit that you can interact with. You can create, deploy, and delete Pods, and it represents one running process in your cluster.

A Pod contains the following things. 
1) Docker application container, 
2) storage resources, 
3) a unique network IP, and 
4) options that govern how the container should run. 

In some scenarios, you can have multiple docker containers running in a Pod, but a Pod represents one single unit of deployment, a single instance of an application in Kubernetes that's tightly coupled and shares resources. Pods are designed to be ephemeral, disposable entities. 

**Note**: Never create Pods just by themselves in a production application. Do this when you need to test whether the underlying containers actually work. 

#### Cons of using Pods
1. They don't self-heal.
2. If a Pod dies, for some reason, it will not be rescheduled. 
3. If a Pod is exited from a Node because of lack of resources, it will not be restarted on different healthier Nodes. 
 
There are higher level constructs to manage and add stability to Pods, called **controllers**. 

**Tip**: Don't use a Pod directly. Use a controller instead, like a deployment.

#### Lifecycle states
- **Pending:** Pod has been accepted by Kubernetes, but a container has not been created yet.
- **Running:** Pod has been successfully scheduled on a Node, and all of its containers are created and atleast one is running.
- **Succeeded:** All the containers in the Pod have exited with an exit stat of zero, which indicates successful execution and will not be restarted.
- **Failed:** All the containers in the Pod have exited and atleast one container has failed and returned a non-zero exit status.
- **CrashLoopBackOff:** This is where container fails to start, for some reason, and then kubernetes module tries over and over again to restart the respective Pod.
