# Helm
* Helm is a tool for kubernetes that helps to install and manage applications.
* Helm is package manager like `yum` in linux.
* It is specifically designed for deploying the applications into kubernetes cluster
* Basically we use Helm for the repetitive tasks, and we can do application deployment easily
* It can be reusable

**Example:**
* If we want to deploy an application, we need many components like, pod, secrets, volumes, configMaps, etc.. 
* If we don't have Helm, then we need to create each individual yaml file for each resource and we need to execute them with `kubectl` command. 
* Managing these resources with `kubectl` is very tough.
* Instead of `kubectl` command we can use Helm to package all the together and create it as a Helm chart, so that deployment is very easy.
* Also we can maintain version of the Charts and many things we can perform.
