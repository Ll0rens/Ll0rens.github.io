---
layout: single
title: AWS - Identity and Federation
excerpt: "Deep dive into AWS Identity and Federation services. In this article we will deepen in the Identity mechanism offered by Amazon Web Services (AWS)."
date: 2023-01-31
classes: wide
header:
  teaser: /assets/images/aws-logo.png
  teaser_home_page: true
  icon: /assets/images/aws-logo.png
categories:
  - Amazon Web Services
tags:  
  - Amazon Web Services
  - Cloud Computing
---

## IAM

## IAM Access Analyzer

## STS

## Identity Federation and Cognito

## AWS Directory Services

- Managed Microsoft AD: Standalone or setup trust AD with on-premises, has MFA, seamless join, RDS integration...
- AD Connector: Proxy requests to on-premises AD.
- Simple AD: Standalone and cheap AD-compatible with no MFA, no advanced capabilities.

## AWS Organizations

## AWS Organizations Policies

## AWS IAM Identity Center

## AWS Control Tower

Easy way to set up and govern a secure and compliant `multi-account AWS environment` based on best practices. It runs on top of AWS Organizations. It automatically sets up AWS Organizations to organize accounts and implement SCP (Service Control Policies).

Guardrail: Provides ongoing governance for your Control Tower environment (AWS accounts). Guardrails levels:
- Mandatory
- Strongly Recommended
- Elective

## Resource Access Manager (RAM)

Share AWS resources that you own with other AWS accounts.
- VPC Subnets and CIDR blocks.
