# Kubernetes ConfigMap & Secret Lab

## Overview

This repository contains my solution for a **Kubernetes ConfigMap & Secret lab** focused on practicing configuration management inside Kubernetes clusters.

The lab demonstrates how to:

* Create and inspect **ConfigMaps**
* Create and manage **Secrets**
* Inject configuration into containers using **Environment Variables**
* Inject specific keys from ConfigMaps
* Combine **ConfigMaps and Secrets** inside the same Pod
* Use configuration inside a **Deployment with multiple replicas**

The exercises were implemented using **kubectl commands and YAML manifests**, following common Kubernetes best practices.

---

# Lab Objectives

The goal of this lab was to understand how Kubernetes separates **application configuration** from **container images**, which is a key concept in cloud-native and DevOps environments.

Main concepts covered:

* ConfigMap creation and inspection
* Secret creation and base64 encoding
* Environment variable injection
* Selective key injection
* Combining ConfigMap and Secret
* Using configuration with Deployments

---

# Repository Structure

```
k8s-configmap-secret-lab/
│
├── 02-configmap-as-envvars.yaml
├── 03-configmap-selective-env.yaml
├── 06-secret-as-envvars.yaml
├── 08-combined-cm-and-secret.yaml
├── 09-deployment-with-config.yaml
│
├── lab-instructions.pdf
├── lab-solution-with-screenshots.pdf
│
└── README.md
```

---

# Kubernetes Resources Implemented

## 1. ConfigMap Creation

A ConfigMap named:

```
app-config
```

was created to store application configuration values such as:

* `APP_ENV`
* `APP_PORT`
* `APP_COLOR`
* `MAX_CONNECTIONS`

This demonstrates how Kubernetes manages **non-sensitive configuration data**.

---

## 2. Inject ConfigMap as Environment Variables

A Pod was created to inject all ConfigMap keys using:

```
envFrom → configMapRef
```

This automatically loads all configuration values into the container as environment variables.

---

## 3. Selective ConfigMap Key Injection

Another Pod demonstrates how to inject **specific keys only** using:

```
configMapKeyRef
```

Example mapping:

| ConfigMap Key | Container Variable |
| ------------- | ------------------ |
| APP_COLOR     | COLOR              |
| APP_PORT      | PORT               |

---

## 4. Secret Creation

A Kubernetes Secret named:

```
db-secret
```

was created to store sensitive database credentials:

* `DB_USER`
* `DB_PASSWORD`
* `DB_NAME`

Secrets are stored in **Base64 encoded format** inside Kubernetes resources.

---

## 5. Inject Secret into Pods

A Pod was created to read database credentials from the Secret and expose them as **environment variables** inside the container.

This demonstrates how Kubernetes securely injects sensitive configuration.

---

## 6. Combined ConfigMap + Secret Pattern

A Pod named:

```
fullapp-pod
```

uses both:

* ConfigMap (`app-config`)
* Secret (`db-secret`)

This reflects a **real-world configuration pattern**, where applications require both regular configuration and sensitive credentials.

---

## 7. Deployment with Shared Configuration

A Kubernetes Deployment was created:

```
webapp-configured
```

with:

```
replicas: 3
```

All Pods created by the Deployment automatically receive the same configuration from:

* ConfigMap
* Secret

This demonstrates how Kubernetes ensures **consistent configuration across multiple replicas**.

---

# Key Kubernetes Concepts Practiced

* ConfigMap management
* Secret management
* Environment variable injection
* Pod configuration
* Deployment configuration
* Separation of configuration from application code

These concepts are fundamental for:

* **DevOps Engineers**
* **Cloud Engineers**
* **Kubernetes Administrators**
* **CKA exam preparation**

---

# Tools Used

* Kubernetes
* kubectl
* YAML manifests
* BusyBox container image
* Local Kubernetes environment (VM / Lab cluster)

---

# Author

**Rana Elmazeny**
Cloud DevOps Engineer

---

# Notes

The repository includes:

* Original lab instructions
* My solved lab with explanations and screenshots
* Kubernetes YAML manifests used to complete the exercises

This lab was completed as part of my Kubernetes hands-on practice.
