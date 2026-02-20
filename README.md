# Disconnected OpenShift 4.18 Deployment Guide

> **Bare Metal · UPI · Air-Gapped** — A complete step-by-step breakdown of deploying a fully disconnected OpenShift cluster from scratch. No internet. No shortcuts. Full control.

---

## 📄 Download the Guide

👉 **[Download PDF Guide](./OCP_4.18_Disconnected_Deployment.pdf)**

---

## 🧭 What's Inside

This guide covers a full **15-step, 4-phase** deployment process for an air-gapped OpenShift 4.18 cluster on bare metal using the **User Provisioned Infrastructure (UPI)** method.

| Phase | Name | Steps |

|-------|------|-------|

| 01 | Preparation | Steps 01–03 |

| 02 | Infrastructure Setup | Steps 04–07 |

| 03 | Cluster Installation | Steps 08–13 |

| 04 | Verification & Go-Live | Steps 14–15 |

---

## 🏗️ Cluster Architecture

```

HAProxy LB → Bootstrap → Masters (x3) → Workers (x2)

                ↓

         Mirror Registry (Quay)

                ↓

         Ignition Server (Apache)

                ↓

            RHCOS + RHEL

```

---

## ⚡ Key Highlights

- **Zero internet required** — all images pre-mirrored to internal Quay registry

- **imageDigestSources** — redirects all quay.io pulls to your internal mirror

- **Custom CA certs** — full TLS trust chain for internal registry

- **CSR approval** — manual two-round certificate approval process (UPI requirement)

- **Strict boot order** — Bootstrap → Masters → Workers (no exceptions)

---

## 🔒 Who Is This For?

Disconnected (air-gapped) environments are mandatory in:

- **Banking & Financial Services** — strict network isolation policies

- **Defense & Government** — classified or sovereign cloud setups

- **Healthcare** — HIPAA and data residency compliance

- **Critical Infrastructure** — power grids, telecom, utilities

- **Manufacturing** — OT/IT separation

---

## ⚠️ Critical Steps at a Glance

| Step | What | Why Critical |

|------|------|-------------|

| Step 04 | Mirror Registry Setup | Missing images = install fails, no exceptions |

| Step 07 | install-config.yaml | Wrong config = no images pulled |

| Step 10 | Boot Order | Wrong order = cluster never forms |

| Step 13 | Approve CSRs | Skipping = nodes never join |

---

## 🛠️ Tech Stack

| Component | Tool |

|-----------|------|

| Platform | OpenShift 4.18 |

| Install Method | UPI (User Provisioned Infrastructure) |

| OS | RHCOS + RHEL |

| Load Balancer | HAProxy |

| Registry | Quay (Internal Mirror) |

| Ignition Server | Apache HTTPD |

| Kubernetes | v1.31.10 |

---

## 📝 Related Article

Read the full breakdown on LinkedIn:  

👉 *[How I Deployed a Fully Disconnected OpenShift 4.18 UPI Cluster — A Complete Breakdown](#)*

---

## 👤 Author

**Shivang Bhardwaj.**  

LinkedIn: https://www.linkedin.com/in/shivang-bhardwaj-7a4516242/

---

> *"In connected installs, the cloud fills the gaps. In disconnected installs — every image, cert, and binary is your responsibility."*
