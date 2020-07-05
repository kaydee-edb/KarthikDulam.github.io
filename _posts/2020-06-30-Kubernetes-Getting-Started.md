---
layout: post
title: "Kubernetes - Getting Started"
date: 2020-06-30
---

# 
This my repository for learnings related to Kubernetes. This post would include how to create a YAML definition files for kubernetes and also some basic commands which can be used to deploy the YAML and get the status on the pods.

###### YAML:

The Yaml file should consist of the following four required components:

- apiVersion
- kind
- metadata
- spec

Here is how a basic version of the yml file should look like -

>apiVersion: v1
>
>kind: Pods
>
>metadata:
>
>​	name: gninx
>
>​	labels: 
>
>​		name: gninx
>
>​		type: backend_app
>
>spec:
>
>​	containers:
>
>​		-  name: gninx 
>
>​		   image: gninx

We will have to update the values of the parameters based on the container names which we plan to deploy. Also, as a rule of good practice there should only be one application container per Pod. 

The pod can have multiple containers if the second container consists of any helper functions required by the application. This will enable the containers to be created/destroyed at the same time.

The below are the basic commands used to deploy and run the pods. 

> kubectl get pods
>
> kubectl run nginx --image nginx
>
> kubectl describe pods nginx
>
> kubectl edit pod nginx

In the next posts, we will talk about more in detail about maintaining and running pods on kurbernetes. 



