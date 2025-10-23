## 1. Check if your processor supports Intel/AMD virtualization technology. Enable Intel virtualization technology in BIOS if possible.

**To check support:**
- **Windows**: Open **Task Manager → Performance tab → CPU → Virtualization**  
  - If shown as “Enabled” or “Disabled”, your processor supports virtualization.  
  - If not shown, your processor might not support it.
<img width="987" height="812" alt="image" src="https://github.com/user-attachments/assets/8e7981ec-a820-4450-adfa-c488d872671e" />


**To enable in BIOS:**
1. Restart your computer and press the BIOS key (e.g., **Del, F2, F10, F12**).  
2. Find options like **Advanced → CPU Configuration → Virtualization Technology**.  
3. Set **Intel Virtualization Technology (VT-x)** or **AMD-V** to **Enabled**.  
4. Save and exit (usually **F10**).


## 2️⃣ 云计算成功的根本原因与优缺点

### 🌐 (1) Fundamental reasons for success / 成功的根本原因

| English | 中文 |
|----------|------|
| **Cost optimization** – Shifts IT spending from CapEx to OpEx. | **成本优化**：将高额前期投入（CapEx）转为按需付费（OpEx）。 |
| **Elasticity & scalability** – Automatically adjusts computing resources. | **弹性与可扩展性**：可根据实时需求自动扩展或收缩资源。 |
| **Ubiquitous access** – Access from any device & location via internet. | **随时随地访问**：可通过互联网从任何设备访问资源。 |

---

### ☁️ (2) Three pros of cloud / 云计算的三大优点

| English | 中文 |
|----------|------|
| **Reduced IT management burden** | **降低IT管理负担**：云服务商负责硬件维护与安全更新。 |
| **Rapid deployment** | **快速部署**：新服务几分钟即可上线。 |
| **Disaster recovery** | **灾难恢复能力强**：跨地域冗余备份，提高可靠性。 |

---

### ⚠️ (3) Three cons of cloud / 云计算的三大缺点

| English | 中文 |
|----------|------|
| **Dependency on internet** | **依赖网络连接**：无网络时无法访问云服务。 |
| **Security & privacy risks** | **安全与隐私风险**：存在数据泄露、合规问题。 |
| **Vendor lock-in** | **供应商锁定**：迁移云服务困难且成本高。 |

---

## 3️⃣ The primary function of a hypervisor / 虚拟机管理程序的主要功能

### **English**
A **hypervisor (VMM)** creates, manages, and isolates **multiple virtual machines** on one physical host.  
It enables:  
- **Resource allocation** (CPU, memory, storage)  
- **Isolation** between VMs  
- **Hardware abstraction** to run different OSs on one host  

### **中文**
**虚拟机管理程序（Hypervisor 或 VMM）** 的主要功能是：  
在单台物理主机上创建、管理并隔离多个虚拟机，实现：  
- **资源分配**：按需分配 CPU、内存、磁盘等。  
- **隔离性**：各虚拟机互不干扰。  
- **硬件抽象**：屏蔽底层硬件细节，使不同系统共存。  

---

## 4️⃣ What is a Virtual Machine (VM)? / 什么是虚拟机？

### **English**
A **VM** is a software-based emulation of a physical computer.  
It runs its own **guest operating system** and applications, managed by a **hypervisor** that shares physical resources (CPU, memory, storage, network) among VMs.

### **中文**
**虚拟机（VM）** 是一种基于软件的计算机仿真系统。  
它拥有独立的 **客户操作系统（Guest OS）** 和应用程序，通过 **虚拟化管理器（Hypervisor）** 与其他虚拟机共享物理资源，同时保持逻辑隔离。  

---

## 5️⃣ Benefits of using virtual machines / 使用虚拟机的好处

| English | 中文 |
|----------|------|
| **Resource efficiency** | **资源高效利用**：多台VM共享主机硬件，节省成本。 |
| **Isolation & security** | **隔离与安全性**：故障或病毒不会影响其他VM。 |
| **Flexible testing & development** | **灵活的测试环境**：可测试不同系统而不影响主机。 |
| **Easy backup & recovery** | **便捷的备份与恢复**：VM可导出为镜像文件。 |
| **Legacy app support** | **兼容旧系统**：可运行老旧应用和操作系统。 |

---

## 6️⃣ Five use cases of virtual machines / 虚拟机的五大应用场景

1. **Software development & testing** — 软件开发与测试  
2. **Server consolidation** — 服务器整合与虚拟化部署  
3. **Education & training** — 教育培训环境的统一与保护  
4. **Cloud computing services (IaaS)** — 云计算服务（如 AWS EC2、Azure VM）  
5. **Legacy system migration** — 旧系统迁移与业务延续  

---

## 7️⃣ In virtualization, what is the guest operating system? / 虚拟化中的客户操作系统是？

> ✅ **Answer / 答案：**  
> **b) The operating system installed on a virtual machine**  
> **虚拟机中安装的操作系统。**

---

## 8️⃣ What does virtual machine isolation mean? / 虚拟机隔离是什么意思？

> ✅ **Answer / 答案：**  
> **c) Virtual machines run independently and are isolated from each other and the host system.**  
> **虚拟机彼此独立运行，与主机系统相互隔离。**

---

## 9️⃣ Benefit of virtual machine portability / 虚拟机可移植性的好处

> ✅ **Answer / 答案：**  
> **c) It allows virtual machines to be moved between different physical machines with compatible hypervisors.**  
> **可以在不同但兼容的主机之间迁移虚拟机。**

---

## 🔟 Purpose of cloning a virtual machine / 克隆虚拟机的目的

### **English**
Cloning creates an **exact copy** of an existing VM (OS, apps, configs, data) for:
- **Rapid deployment**  
- **Testing and debugging**  
- **Disaster recovery**  
- **Consistent environments**

### **中文**
克隆虚拟机是创建现有虚拟机的 **完整副本**（包括系统、软件、配置与数据），用于：
- **快速部署**：快速创建同配置的虚拟机；  
- **测试调试**：避免影响原系统；  
- **灾备恢复**：在主机故障时迅速恢复；  
- **环境一致性**：保证团队测试环境统一。  
