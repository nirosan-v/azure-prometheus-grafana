# Deployment Proof – Prometheus & Grafana on Azure VM

This walkthrough shows the full lifecycle: **Azure VM setup → Prometheus install → Node Exporter → Grafana integration → Live dashboard**.  

The goal is to demonstrate end-to-end monitoring setup on Azure using **open-source tools (Prometheus, Node Exporter, Grafana)**.

> Sensitive details (subscription IDs, public IPs) are blurred or redacted.

---

## 1) Azure Resource Group
The resource group **`monitoring-rg`** acts as the logical container for all monitoring components.  
![Resource Group](./01-resource-group.png)

---

## 2) Virtual Network
Virtual network **`monitoring-vnet`** provides the internal IP range (`10.0.0.0/16`) for the monitoring VM.  
![Virtual Network](./02-vnet.png)

---

## 3) Virtual Machine
Linux VM **`monitoring-vm`** (Ubuntu 24.04 LTS) was deployed in **North Europe** to host Prometheus and Grafana.  
![Virtual Machine](./03-vm.png)

---

## 4) Network Security Group
The NSG **`monitoring-vm-nsg`** allows inbound access to Prometheus (9090), Node Exporter (9100), Grafana (3000) and SSH (22).  
![NSG Rules](./04-nsg-rules.png)

---

## 5) SSH Access
A PEM key was used to securely connect from macOS Terminal to the VM via SSH.  
![SSH Connection](./05-ssh-connection.png)

---

## 6) Prometheus Installation
Prometheus 2.53.1 was downloaded, configured and registered as a systemd service.  
The service shows **active (running)** status.  
![Prometheus Running](./06-prometheus-running.png)

---

## 7) Node Exporter Installation
Node Exporter was configured as a service to expose system-level metrics (CPU, RAM, Disk I/O).  
![Node Exporter Running](./07-node-exporter-running.png)

---

## 8) Prometheus Web UI
Prometheus UI (http://\<vm-ip\>:9090) confirms the service is operational and ready to scrape metrics.  
![Prometheus UI](./08-prometheus-ui.png)

---

## 9) Prometheus Targets
The **Node Exporter target** (`localhost:9100/metrics`) shows UP status, verifying successful metric scraping.  
![Prometheus Targets](./09-prometheus-targets.png)

---

## 10) Grafana Installation
Grafana v12 was installed and enabled as a systemd service.  
![Grafana Installation](./10-grafana-install.png)

---

## 11) Connect Prometheus as Data Source
Grafana was configured to use **Prometheus** (`http://localhost:9090`) as its data source.  
![Add Prometheus Data Source](./11-add-prometheus-datasource.png)

---

## 12) Explore Metrics in Grafana
System metrics (CPU, memory, goroutines, Go heap allocations) are visualised in real time from Prometheus.  
![Grafana Metrics View](./12-grafana-metrics.png)

---

## 13) Grafana Dashboard
A **Node Exporter Full** dashboard provides a detailed visual overview of CPU usage, memory consumption, disk I/O and network traffic.  
![Grafana Dashboard](./13-grafana-dashboard.png)

---

## ✅ Summary
This deployment demonstrated how Prometheus, Node Exporter and Grafana can be used together to implement a complete monitoring stack on Azure.  

--> Key components included: a Linux VM (Ubuntu 24.04), Prometheus for metric collection, Node Exporter for system data and Grafana for visualisation.  

Together, they provide **real-time observability** of infrastructure performance, making it easy to track CPU, memory, disk and network usage in one unified dashboard.
