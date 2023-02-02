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
  - Terraform
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
- Coding conventions:
- Idempotence: Writing an Ad hoc script that works once is not too difficult. Writing and ad hoc script that works correctly even if you run it over and over again is a lot more difficult. Code that works correctly no matter how many times you run it is called idempotent code. To make the above Bash script idempotent you would need to add many lines of code, including lots of if-statements. On the other hand, most Ansible functions are idempotent by default.
- Distribution: Ad hoc scripts are designed to run on a single server. Ansible and other configuration management tools are designed specifically for managing large numbers of remote servers.

## Server Templating Tools

## Orchestation Tools

## Provisioning Tools

## The Benefits of Infrastructure as Code

## How Terraform Compares to Other IaC Tools

## Configuration Management VS Provisioning

## Using Multiple Tools Together
