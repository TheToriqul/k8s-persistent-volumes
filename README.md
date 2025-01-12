# 🌟 Mastering Kubernetes Persistent Storage: A Deep Dive into PV & PVC

[![GitHub Repository](https://img.shields.io/badge/GitHub-k8s--persistent--volumes-blue?style=flat&logo=github)](https://github.com/TheToriqul/k8s-persistent-volumes)
[![GitHub Stars](https://img.shields.io/github/stars/TheToriqul/k8s-persistent-volumes?style=social)](https://github.com/TheToriqul/k8s-persistent-volumes/stargazers)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat&logo=kubernetes&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=flat&logo=ubuntu&logoColor=white)
![VS Code](https://img.shields.io/badge/VS_Code-007ACC?style=flat&logo=visual-studio-code&logoColor=white)

## 📋 Project Overview

This project represents my comprehensive exploration of Kubernetes storage management, focusing on implementing and mastering persistent storage solutions. Through hands-on development with Persistent Volumes (PV) and Persistent Volume Claims (PVC), I've created a practical guide for handling stateful applications in Kubernetes. This repository demonstrates real-world implementation patterns and best practices for maintaining data persistence in containerized environments.

## 🎯 Key Objectives

- Master Kubernetes storage architecture and implementation
- Develop expertise in PV and PVC management
- Implement various storage access modes and policies
- Create production-ready storage solutions
- Document comprehensive storage management patterns
- Build practical examples for real-world scenarios

## 🏗️ Project Architecture
In this Kubernetes storage architecture, the Administrator creates a Persistent Volume (PV db-pv) with 1Gi capacity, while the Developer creates a Persistent Volume Claim (PVC db-pvc) requesting 256Mi of that storage. The PVC acts as a binding request to the PV, and once bound, a Pod can mount this storage to persist data in the underlying storage path (/data/db).

```mermaid
graph LR
    subgraph Kubernetes[Kubernetes Cluster]
        Admin[Administrator] -->|Creates| PV[PV db-pv]
        style Admin fill:#e1f5fe,stroke:#01579b
        style PV fill:#b2dfdb,stroke:#004d40
        
        Dev[Developer] -->|Creates| PVC[PVC db-pvc]
        style Dev fill:#e1f5fe,stroke:#01579b
        style PVC fill:#c8e6c9,stroke:#1b5e20
        
        Pod[Pod] -->|Mounts| PVC
        style Pod fill:#f3e5f5,stroke:#4a148c
        
        PVC -->|Claims 256Mi| PV
        PV -->|Provides 1Gi| PVC
    end
    
    subgraph Storage[Storage]
        Path[data/db]
        style Path fill:#ffecb3,stroke:#ff6f00
    end
    
    Path -->|Provides| PV
    
    style Kubernetes fill:#f5f5f5,stroke:#212121
    style Storage fill:#fafafa,stroke:#212121
```

## 💻 Technical Stack

- **Platform**: 
  - Kubernetes 1.21+
  - Container Runtime Interface (CRI)
  - Container Storage Interface (CSI)
- **Storage**:
  - Persistent Volumes (PV)
  - Persistent Volume Claims (PVC)
  - StorageClasses
  - Dynamic Provisioners
- **Development Environment**:
  - Ubuntu 20.04 LTS
  - VS Code with Kubernetes extensions
  - Docker CE
- **Monitoring & Management**:
  - kubectl
  - Kubernetes Dashboard
  - Storage metrics
- **Version Control**: Git

## 🚀 Getting Started

<details>
<summary>🐳 Prerequisites</summary>

- Kubernetes cluster (v1.21 or higher)
- kubectl command-line tool
- Access to cluster storage resources
- Basic understanding of Kubernetes concepts
- Git for version control
- VS Code or similar text editor
- Docker installed and configured
- Storage backend (local or cloud provider)

</details>

<details>
<summary>⚙️ Installation</summary>

1. Clone the repository:
   ```bash
   git clone https://github.com/TheToriqul/k8s-persistent-volumes.git
   ```

2. Navigate to the project directory:
   ```bash
   cd k8s-persistent-volumes
   ```

3. Create storage directories:
   ```bash
   sudo mkdir -p /data/db
   sudo chmod 777 /data/db
   ```

4. Verify cluster access:
   ```bash
   kubectl cluster-info
   kubectl get nodes
   ```

5. Set up storage classes:
   ```bash
   kubectl apply -f storage-class/
   ```

</details>

<details>
<summary>🎮 Usage</summary>

1. Create a persistent volume:
   ```bash
   kubectl apply -f manifests/pv.yaml
   ```

2. Create a persistent volume claim:
   ```bash
   kubectl apply -f manifests/pvc.yaml
   ```

3. Deploy a stateful application:
   ```bash
   kubectl apply -f manifests/statefulset.yaml
   ```

4. Verify the deployment:
   ```bash
   kubectl get pv,pvc,pods
   ```

For detailed commands and explanations, refer to the [reference-commands.md](reference-commands.md) file.

</details>

## 💡 Key Learnings

### Technical Mastery:

1. Implementation of storage solutions in Kubernetes
2. Understanding of storage access modes and policies
3. Expertise in storage lifecycle management
4. Proficiency in storage troubleshooting
5. Advanced knowledge of volume provisioning

### Professional Development:

1. Cloud-native storage architecture design
2. Best practices in storage management
3. Systematic problem-solving approach
4. Technical documentation skills
5. Infrastructure planning

### 🔄 Future Enhancements

<details>
<summary>View Planned Improvements</summary>

1. Implement dynamic volume provisioning
2. Add cloud provider integrations
3. Create automated backup solutions
4. Develop storage monitoring system
5. Implement disaster recovery
6. Add performance benchmarking

</details>

## 🙌 Contribution

Contributions are welcome! Feel free to:
- [Open an issue](https://github.com/TheToriqul/k8s-persistent-volumes/issues)
- [Submit a pull request](https://github.com/TheToriqul/k8s-persistent-volumes/pulls)
- [Fork the repository](https://github.com/TheToriqul/k8s-persistent-volumes/fork)

## 📧 Connect with Me

- 📧 Email: toriqul.int@gmail.com
- 📱 Phone: +65 8936 7705, +8801765 939006
- 🌐 LinkedIn: [@TheToriqul](https://www.linkedin.com/in/thetoriqul/)
- 🐙 GitHub: [@TheToriqul](https://github.com/TheToriqul)
- 🌍 Portfolio: [TheToriqul.com](https://thetoriqul.com)

Let's connect and discuss cloud-native technologies!

## 👏 Acknowledgments

- [Poridhi for providing comprehensive labs and inspiring this project](https://devops.poridhi.io/)
- The Kubernetes community for excellent documentation
- Fellow developers who provided valuable feedback
- Open source contributors who inspire continuous learning

---

Thank you for exploring this repository! I hope you find it valuable for understanding Kubernetes storage management. Happy learning! 🚀