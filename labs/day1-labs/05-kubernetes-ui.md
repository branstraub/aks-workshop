# Kubernetes Dashboard

The Kubernetes dashboard is a web ui that lets you view, monitor, and troubleshoot Kubernetes resources. 

> Note: The Kubernetes dashboard is a secured endpoint and can only be accessed using the SSH keys for the cluster. Since cloud shell runs in the browser, it is not possible to tunnel to the dashboard using the steps below.

### Accessing The Dashboard UI

There are multiple ways of accessing Kubernetes dashboard. You can access through kubectl command-line interface or through the master server API. We'll be using kubectl, as it provides a secure connection, that doesn't expose the UI to the internet.

1. Command-Line Proxy

* On the terminal VM:
* Run ```cd /home/<user>``` 
* Run ```curl https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip > ngrok.zip``` to download ngrok in the Linux VM.
* Run ```sudo apt-get install unzip``` to install unzip.
* Run ``` unzip ngrok.zip ``` to unzip ngrok.
* Run ```kubectl proxy``` this creates a local proxy to 127.0.0.1:8001
* In other terminal with SSH to the same VM run  ```./ngrok http 8001 -host-header="localhost:8001"```
* Then browse: <https://***.ngrok.io/api/v1/proxy/namespaces/kube-system/services/kubernetes-dashboard/#!/cluster?namespace=default> Replace *** with the address shown on the terminal.

### Explore Kubernetes Dashboard

1. In the Kubernetes Dashboard select nodes to view
![](img/ui_nodes.png)
2. Explore the different node properties available through the dashboard
3. Explore the different pod properties available through the dashboard ![](img/ui_pods.png)
4. In this lab feel free to take a look around other at  other resources Kubernetes provides through the dashboard

> To learn more about Kubernetes objects and resources, browse the documentation: <https://kubernetes.io/docs/user-journeys/users/application-developer/foundational/#section-3>
