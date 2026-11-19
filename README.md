## Changwu Li

**华中科技大学（HUST）博士研究生** · [CGCL](https://github.com/CGCL-codes) / [IntelliStream Lab](https://github.com/intellistream) · [vLLM-HUST](https://github.com/vLLM-HUST)

专注于 **大模型推理系统（LLM Serving Systems）** 与 **昇腾 NPU / NVIDIA GPU 异构系统优化**，围绕受限显存与异构执行控制边界开展系统研究与开源构建：

- **图兼容 MoE 专家缓存与卸载**：面向昇腾 NPU 与 CUDA GPU 双后端，研究保持捕获计算图稳定权重地址的固定槽位专家缓存、图外异步 Staging 与有界溢出分波机制。
- **低延迟设备驻留解码控制面**：探索消除逐 Token Host-Device 往返的昇腾设备驻留解码周期（Device-Resident Decode Epochs），将内层解码控制、Paged-KV 更新与采样下沉至设备侧。
- **数据流系统与推理社区基础设施**：非平稳数据流在线指纹数据选择（WWW '26），以及 vLLM / vLLM-Ascend 社区性能优化追踪与深度技术专题综述建设。

---

### 代表推理系统

| 项目 | 方向与平台 | 核心机制与关键结果 |
| :--- | :--- | :--- |
| **[LatchMoE (NPU)](https://github.com/vLLM-HUST/vllm-ascend-hust-LatchMoE)**<br>**[LatchMoE-GPU](https://github.com/Li-changwu/LatchMoE-GPU)** | 图兼容 MoE 专家缓存卸载<br>`Ascend NPU` · `CUDA Graph` · `vLLM` | 面向受限显存的地址稳定、图重放兼容 MoE 专家缓存框架（论文工作，昇腾 NPU + CUDA GPU 双后端）；通过预分配固定槽位、持久设备映射、图外异步 Staging、有界溢出分波（Bounded Waves）与槽位租约生命周期保护，在保持捕获计算图稳定权重地址的同时消除远端按需访存瓶颈。 |
| **[Cruise](https://github.com/Li-changwu/Cruise)** | 设备驻留解码控制面<br>`Ascend 910B2` · `CANN` · `vLLM V1` | 基于 CANN DataFlow Device UDF 将解码内层控制循环、Paged-KV 状态更新与采样下沉至昇腾设备侧按有界 Epoch 连续执行；单 Epoch 控制边界载荷从 **136.9 MB 降至 628 B**，Host 控制耗时降低 **3.54×**。 |

---

### 学术论文

- **[WWW '26]** **Changwu Li**, Tongjun Shi, Shuhao Zhang, Binbin Chen, Bingsheng He, Xiaofei Liao, Hai Jin.  
  *StreamFP: Fingerprint-guided Data Selection for Efficient Stream Learning.*  
  In *Proceedings of the ACM Web Conference 2026*. [[Code](https://github.com/CGCL-codes/StreamFP)] · [[DOI](https://doi.org/10.1145/3774904.3792584)]

---

### 开源社区与开发者工具

- **[vLLM & vLLM-Ascend 推理研究日报与技术专题工作台](https://lab.sage.org.ai/auto-research-report-website/)** · [[GitHub](https://github.com/intellistream/auto-research-report-website)]  
  社区研报网站负责人，持续追踪 vLLM 与 vLLM-Ascend 核心性能优化演进，建设 ACLGraph 图执行等系统技术专题综述，并参与 [vLLM-HUST](https://github.com/vLLM-HUST) 国产算力推理运行时生态建设。
- **[Codex Provider Switcher](https://github.com/Li-changwu/codex-provider-switcher)** · [[VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=Li-changwu.codex-provider-switcher-vscode)]  
  面向 Windows 本地与 Linux Remote-SSH 环境的 VS Code 扩展，支持多套 Codex Provider 配置的安全切换、SecretStorage 凭据隔离、事务级备份回滚与原生会话续接。

---

### 技术栈

- **推理引擎与异构运行时**：`vLLM (V1 Engine / Platform Plugins)` · `PyTorch` · `CUDA / CUDA Graph` · `Ascend CANN (ACLGraph / DataFlow Device UDF)` · `Triton`
- **系统开发与性能剖析**：`Python` · `C / C++` · `TypeScript` · `PyTorch Profiler / Nsight / Ascend Profiling` · `Linux`
