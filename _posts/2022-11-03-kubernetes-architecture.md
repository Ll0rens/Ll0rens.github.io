---
layout: single
title: Introduction to Kubernetes - Kubernetes
excerpt: "Kubernetes provides a container based management environment. Kubernetes orchestrates the compute capacity, the networking and the storage infrastructure so that user don't have to. It offers the simplicity of Platform-as-a-Service (PaaS) with the flexibility of Infrastructure-as-a-Service (IaaS) and enables portability between infrastructure providers. In this article I am going to present the basic components of a Kubernetes cluster and its architecture."
date: 2022-11-03
classes: wide
header:
  teaser: /assets/images/kubernetes-logo.png
  teaser_home_page: true
  icon: /assets/images/kubernetes-logo.png
categories:
  - DevOps
tags:  
  - kubernetes
  - DevOps
---

![](/assets/images/kubernetes-logo.png.png)

As in any traditional cluster, Kubernetes is composed of nodes that control the cluster, these are known as `Control Plane`, and nodes that are in charge of performing the work, known as workers or minions. Depending on the function of a node in the cluster, a series of components are installed on it. Below you can see the typical architecture of how these components are installed in the different nodes of the cluster.
## History
In 2013 three google engineers (at that time) Craig McLuckie, Joe Beda and Brendan Burns started working in a project about public infrastructure in the cloud. Google had plenty of experience building distributed applications and internally they were using a cluster administrator called `Borg`, born in 2003.

In 2013, at that same year, Docker was released as open source project. Joe Beda proposed to start using docker in their internal platform because he thought that it could be a key component in their architecture (In fact, Docker ended up being a fundamental part of the platform).

In 2015, Kubernetes version 1.0 was released. Google partnered with the Linux Foundation to create a new non-profit organization, `Cloud Native Computing Foundation (CNCF)`, and donated the Kubernetes project to this.
## Kubernetes architecture

![](/assets/images/Intro-Kubernetes/Kubernetes-architecture.png)

## Control Plane

These are the nodes that control the cluster. In the diagram above it can bee seen that all of the components are in the same 'box'. The reality is that all these components do not need to live in the same node. It is perfectly possible to deploy these components across different nodes, commonly they are deployed in the same node.

- Kube-apiserver: Represented as API in the above diagram. This component is the interaction point with the cluster, not only externally, but also internally. The internal components of the cluster do not interact each other directly, everything passes through `kube-apiserver`. It is basically an API REST.
- etcd: This is a key-value high availability database and it is used by kube-apiserver to keep track of the cluster state.
- Kube-scheduler: This component is the one in charge of decide where are the pods going to be deployed in the cluster.
- Kube-controller-manager: This component is in charge of executing the controllers. In Kubernetes, the controllers are processes that are constantly listening for the cluster events. When an event happens, the controller takes notes and decide if it has to make an action or not.
- Cloud-controller-manager: This is an optional component in case that the Kubernetes cluster is integrated and configured by a cloud provider. As the kube-controller-manager, the cloud-controller-manager is in charge of executing the cloud controllers, many of which are processes that interacts with the cloud provider to create resource in it.

## Nodes
- Container engine: The aim of this component is to deploy the containers, so this component needs to be installed in every node of the cluster that a Pod can be deployed.
- Kubelet: This components is in charge of deploying the containers in the Pod. In other words, when the `kube-scheduler` decides in which node the Pod has to be deployed, `kubelet` interacts with `kube-apiserver`, receives that information and thanks to the `container engine` it deploys the containers in the Pod.
- Kube-proxy: This component is in charge of controlling the internal network traffic inside the cluster. Any kind of network traffic of a Pod passes through this component and it routes that traffic to its destination.

## Namespaces

Linux namespaces make it possible to run a whole range of applications on a single real machine and ensure no two of them can interfere with each other, without having to resort to using virtual machines.

In **Kubernetes**, namespaces are virtual clusters backed by the same physical cluster. Kubernetes objects, such as pods and containers, live in namespaces. Namespaces are a way to separate and organize objects in your cluster.

List namepaces:

`kubectl get namespaces`

All clusters have a **default** namespace

It is possible to specify a namespace for each command:

`kubectl get pods --namespace my-namespace`
`kubectl get pods -n my-namespace`
`kubectl get pods --all-namespaces`

Create a namespace:
`kubectl create namespace my-namespace`
