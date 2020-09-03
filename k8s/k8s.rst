.. _k8s:

.. title:: Introduction to Kubernetes

What is Kubernetes and why K8s as the acronym?
==============================================

From the official Kubernetes webpage (https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/):

"Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.
The name Kubernetes originates from Greek, meaning helmsman or pilot. Google open-sourced the Kubernetes project in 2014. Kubernetes combines over 15 years of Google's experience running production workloads at scale with best-of-breed ideas and practices from the community."

Kubernetes provides you with:

- Service discovery and load balancing
    Kubernetes can expose a container using the DNS name or using their own IP address. If traffic to a container is high, Kubernetes is able to load balance and distribute the network traffic so that the deployment is stable.
- Storage orchestration
    Kubernetes allows you to automatically mount a storage system of your choice, such as local storages, public cloud providers, and more.
- Automated rollouts and rollbacks
    You can describe the desired state for your deployed containers using Kubernetes, and it can change the actual state to the desired state at a controlled rate. For example, you can automate Kubernetes to create new containers for your deployment, remove existing containers and adopt all their resources to the new container.
- Automatic bin packing
    You provide Kubernetes with a cluster of nodes that it can use to run containerized tasks. You tell Kubernetes how much CPU and memory (RAM) each container needs. Kubernetes can fit containers onto your nodes to make the best use of your resources.
- Self-healing
    Kubernetes restarts containers that fail, replaces containers, kills containers that don’t respond to your user-defined health check, and doesn’t advertise them to clients until they are ready to serve.
- Secret and configuration management
    Kubernetes lets you store and manage sensitive information, such as passwords, OAuth tokens, and SSH keys. You can deploy and update secrets and application configuration without rebuilding your container images, and without exposing secrets in your stack configuration

Kubernetes is not a traditional, all-inclusive PaaS (Platform as a Service) system. Since Kubernetes operates at the container level rather than at the hardware level, it provides some generally applicable features common to PaaS offerings, such as deployment, scaling, load balancing, and lets users integrate their logging, monitoring, and alerting solutions. However, Kubernetes is not monolithic, and these default solutions are optional and pluggable. Kubernetes provides the building blocks for building developer platforms, but preserves user choice and flexibility where it is important.

Kubernetes:

- Does not limit the types of applications supported. Kubernetes aims to support an extremely diverse variety of workloads, including stateless, stateful, and data-processing workloads. If an application can run in a container, it should run great on Kubernetes.
- Does not deploy source code and does not build your application. Continuous Integration, Delivery, and Deployment (CI/CD) workflows are determined by organization cultures and preferences as well as technical requirements.
- Does not provide application-level services, such as middleware (for example, message buses), data-processing frameworks (for example, Spark), databases (for example, MySQL), caches, nor cluster storage systems (for example, Ceph) as built-in services. Such components can run on Kubernetes, and/or can be accessed by applications running on Kubernetes through portable mechanisms, such as the Open Service Broker.
- Does not dictate logging, monitoring, or alerting solutions. It provides some integrations as proof of concept, and mechanisms to collect and export metrics.
- Does not provide nor mandate a configuration language/system (for example, Jsonnet). It provides a declarative API that may be targeted by arbitrary forms of declarative specifications.
- Does not provide nor adopt any comprehensive machine configuration, maintenance, management, or self-healing systems.
- Additionally, Kubernetes is not a mere orchestration system. In fact, it eliminates the need for orchestration. The technical definition of orchestration is execution of a defined workflow: first do A, then B, then C. In contrast, Kubernetes comprises a set of independent, composable control processes that continuously drive the current state towards the provided desired state. It shouldn’t matter how you get from A to C. Centralized control is also not required. This results in a system that is easier to use and more powerful, robust, resilient, and extensible.

(https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/)

So why the k8s, well it seems to be related to laziness of developers back in the days (https://medium.com/@rothgar/why-kubernetes-is-abbreviated-k8s-905289405a3c). 
"Ok so from now on I’ll be using k8s instead of Kubernetes, saves a lot of typing ;)..."
  
What are pros and cons of k8s vs Docker Swarm
----------------------------------------------

John did some research on the internet and found this good comparison (https://phoenixnap.com/blog/kubernetes-vs-docker-swarm#:~:text=Docker%20Swarm%20can%20deploy%20containers,times%20for%20scaling%20on%20demand.&text=By%20utilizing%20its%20own%20YAML,be%20used%20to%20define%20containers.)
From that site the below figure gave him something that he liked very much: "Auto Scaling! That is something that my org wants to have as a requirement. Well not Automatic, but I like that. Saves me time at night to get scaling done. That’s gonna be on my agenda, how do I do that automatica scaling...", he thinks while reading the articles.

.. figure::images/01.png

After looking at other articles where he searches for Docker Swarm and k8s support, it seems to him that even though all support both solutions, the Docker Swarm are still VMs that need to be managed by the organisation whereas the k8s can be a native solution where the underlying VMs don’t have to be managed. So the k8s infra is a service that can be used. Saves the upgrading and keeping everything updated to a minimum for the underlying k8s cluster.
Another item that John is interested in is the support from other people. Using youtube, Google and other media is helping in understanding new information. He did some searches and found that there is more information to be found on k8s then there is in Docker Swarm. Secondly he noticed that because of the possibilities in APIs and extras, like different load balancers, monitoring and logging, he choice for k8s for his organisation makes sense.

Downside of the k8s is that it can be seen as very complex if you have to do this by hand, not even speaking of the immense amount of possibilities it has... He found an article https://github.com/kelseyhightower/kubernetes-the-hard-way on setting up k8s manually. He got scared instantly... "That’ll be something to 'read and play with' on a rainy weekend... Not now please..."

Pros vs Cons in relation to the task at hand
--------------------------------------------
After reading the articles, looking at youtube movies, John created the below table where he looked at the tasks at head and if k8s can be the solution.

.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Task
     - k8s
   * - Can use Docker containers                         
     - Yes
   * - Config changes outside of container
     - Yes, using configMaps
   * - Rebooting container should not impact service
     - Yes
   * - Reboot host (master or worker) no impact on service
     - Yes, just make sure the cluster is big enough wrt “surviving nodes”
   * - Update config and/or image: Roll back
     - Not sure, need to investigate
   * - Update config and/or image: no impact on service
     - Not sure, need to investigate
   * - Scaling possibilities (out/in)
     - Yes, automatic on pod failure.
   * - Public cloud supported
     - Yes, natively and via VMs

Based on the outcome of the table, John concluded that the requirements can be made, but it’s going to take some time as he is interested in the difficulty to get a k8s cluster up and running. And what is needed to have his pre created images work in the "new" environment.

