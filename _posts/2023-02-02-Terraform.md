---
layout: single
title: Why Terraform in Infrastructure as Code (IaC) ?
excerpt: "There are many tools for Infrastructure as Code (IaC) out there such as Chef, Puppet, Ansible, SaltStack, CloudFormation, Heat... In this article it is going to be explained how to go for the best tools for your Infrastructure and why Terraform is a tool you must, at least, take into consideration."
date: 2023-02-02
classes: wide
header:
  teaser: /assets/images/terraform-logo.png
  teaser_home_page: true
  icon: /assets/images/terraform-logo.png
categories:
  - DevOps
tags:  
  - terraform
  - devops
  - iaac
  - Cloud Computing
---

## What is Infrastructure as Code (IaC)

The main aim of Infrastructure as code is to write and execute code to define, deploy, update and destroy the infrastructure.

There are five broad categories of IAC tools:
- Ad hoc Scripts
- Configuration management Tools
- Server templating tools
- Orchestration tools
- Provisioning tools

## Ad Hoc Scripts

The most common way to automating anything is to write an `ad hoc script`. Basically, it means breaking a task in different steps using a scripting language (Bash, Ruby, Python) to define each of those steps and execute that script on your server.

For example:
```bash
# Update the apt-get cache
sudo apt-get update

# Install PHP and Apache
sudo apt-get install -y php apache2

# Copy the code from the repo
sudo git clone http//DOMAIN_NAME

# Start the Apache service
sudo service apache2 start
```

This is not a big deal for an eight-line script that installs Apache, but it gets messy if you try to use ad hoc scripts to manage dozens of servers, databases, load balancers, network configurations and so on. Ad hoc scripts are great for small, one-off tasks, but if you are going to be managing all of your infrastructure as code, then you should use and IaC tool that is purpose-build for that job, in other words, a configuration management tool.

## Configuration Management Tools

Chef, Puppet, Ansible and SaltStack are all `configuration management tools`, which means that they are defined to install and manage software on existing serves.
For example, using Ansible instead of a Bash script offers a number of advantages:
- Coding conventions: Ansible enforces a consistent, predictable structure, including documentation, file layout, clearly named parameters, secrets management, and so on. While every developer organizes their ad hoc scripts in a different way, most configuration management tools come with a set of conventions that makes it easier to navigate the code.
- Idempotence: Writing an Ad hoc script that works once is not too difficult. Writing and ad hoc script that works correctly even if you run it over and over again is a lot more difficult. Code that works correctly no matter how many times you run it is called idempotent code. To make the above Bash script idempotent you would need to add many lines of code, including lots of if-statements. On the other hand, most Ansible functions are idempotent by default.
- Distribution: Ad hoc scripts are designed to run on a single server. Ansible and other configuration management tools are designed specifically for managing large numbers of remote servers.

## Server Templating Tools

An alternative to configuration management that has been growing in popularity recently are server templating tools such as Docker, Packer, and Vagrant. The idea behind these tools is to create an `image` of a server that captures fully self-contained `snapshot` of the Operating System (OS), the software, the files and all other relevant details. There are two main technologies for working with images: Virtual Machines and Containers.

## Orchestation Tools

Orchestation tools such as Kubernetes, Marathon/Mesos, Amazon Elastic Container Service (Amazon ECS), Docker Swarm and Nomad. For example, Kubernetes allows you to define how to manage your Docker containers as code. You first deploy a Kubernetes cluster, which is a group of servers that Kubernetes will manage and use to run you Docker containers.

## Provisioning Tools

Configuration management, server templating and orchestation tools define the code that runs on each server, provisioning tools such as Terraform, CloudFormation and OpenStack Heat are responsible for creating the servers themselves.


## How Terraform Compares to Other IaC Tools

Infrastructure as code is great, but it is quite difficult to opt for the correct IaC tool. Many of the IaC tools are similar for some use cases and it is not clear how you should pick one or another. There are different criterias to consider, but one of the most important ones is: Configuration management vs Provisioning

## Configuration Management VS Provisioning

Chef, Puppet, Ansible and SaltStack are all configuration management tools, whereas CloudFormation, Terraform and OpenStack Heat are all provisioning tools.

If you are using server templating tools such as Docker or Packer, the vast majority of your configuration management needs are already taken care of. Once you have an image created form a Dockerfile of Packer template, all that´s left to do is provisioning the infrastructure running those images. And when it comes to provisioning, a provisioning tool is going to be your best choice. With that being said, if you are not using server templating tools, a good alternative is to use a configuration management and provisioning tool together. For example, you might use Terraform to provision your servers and run Chef to configure each one.

## Using Multiple Tools Together

The reality is that you will  likely need to use multiple tools to build your infrastructure.

- `Provisioning + Configuration Management:` Terraform and Ansible. You use Terraform to deploy all the underlying infrastructure, including the network topology and you use Ansible to deploy your apps on the top of those servers.

- `Provisioning + Server Templating:` Terraform and Packer. Use Packer to package your apps as VM images and then use Terraform to deploy servers with these images and the rest of the infrastructure.

- `Provisioning + Server Templating + Orchestation:` Terraform, Packer, Docker and Kubernetes. You use Packer to create a VM image that has Docker and Kubernetes installed. You then use Terraform to deploy a cluster of servers (each one using this VM image) and the rest of the infrastructure. Finally, when the cluster of servers boots up, it forms a Kubernetes cluster that you use to run and manage your Dockerized applications.
