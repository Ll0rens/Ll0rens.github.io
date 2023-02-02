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
sudo apt-get install -y php apache2
sudo git clone http//DOMAIN_NAME
sudo service apache2 start
```

## Configuration Management Tools

## Server Templating Tools

## Orchestation Tools

## Provisioning Tools

## The Benefits of Infrastructure as Code

## How Terraform Compares to Other IaC Tools

## Configuration Management VS Provisioning

## Using Multiple Tools Together
