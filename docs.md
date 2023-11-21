# [Docs](https://developer.hashicorp.com/terraform/docs)

## Introduction

### What is Terraform?

- Terraform is an infrastructure as code tool that lets you build,
 change, and version cloud and on-prem resources safely and efficiently.
- Terraform can manage low-level components like compute, storage,
 and networking resources, as well as high-level components like DNS entries and SaaS features.

#### How does Terraform work?

- Terraform creates and manages resources on cloud platforms and other services through 
their application programming interfaces (APIs).
- Providers enable Terraform to work with virtually any platform or service with an accessible API.
- HashiCorp and the Terraform community have already written thousands of providers to manage
 many different types of resources and services.
- You can find all publicly available providers on the [Terraform Registry](https://registry.terraform.io/?product_intent=terraform).
- The core Terraform workflow consists of three stages:
    - **Write**: You define resources.
    - **Plan**: Terraform creates an execution plan.
    - **Apply**: On approval, Terraform performs the proposed operations in the correct order,
     respecting any resource dependencies.
- Terraform generates a plan and prompts you for your approval before modifying your infrastructure.
- It also keeps track of your real infrastructure in a state file, which acts as a source of truth
 for your environment.
- Terraform configuration files are declarative, meaning that they describe the end state of your infrastructure.
- Terraform supports reusable configuration components called modules.

### Use Cases

- Terraform lets you use the same workflow to manage multiple providers and handle cross-cloud dependencies.
- You can use Terraform to efficiently deploy, release, scale, and monitor infrastructure for multi-tier applications.
- Terraform can help you enforce policies on the types of resources teams can provision and use.
- Terraform can interact with Software Defined Networks (SDNs) to automatically configure the network according to the needs of the applications running in it.
- Terraform lets you both deploy a Kubernetes cluster and manage its resources (e.g., pods, deployments, services, etc.).

### The Core Terraform Workflow

- The core Terraform workflow has three steps:
    - **Write** - Author infrastructure as code.
        - `terraform init`.
    - **Plan** - Preview changes before applying.
        - `terraform plan`.
    - **Apply** - Provision reproducible infrastructure.
        - `terraform apply`.

## Terraform Language Documentation

## Plugin Development
