## Changwu Li

**华中科技大学（HUST）博士研究生** · [CGCL](https://github.com/CGCL-codes) / [IntelliStream Lab](https://github.com/intellistream) · [vLLM-HUST](https://github.com/vLLM-HUST)

专注于 **大模型推理系统（LLM Serving Systems）** 与 **昇腾 NPU / NVIDIA GPU 异构系统优化**，围绕显存受限与异构互联场景下的执行瓶颈开展系统研究与开源构建：

- **存储层次与专家/KV 卸载**：单卡及受限 HBM 下的 MoE 专家缓存、异步搬运与图兼容固定槽位执行（CUDA Graph & Ascend NPU），以及多轮长上下文分层 KV Anti-Caching。
- **低延迟解码控制面与推测解码**：下沉逐 Token 控制循环的昇腾设备驻留解码周期（Device-Resident Decode Epochs），以及面向卸载场景与零额外模型开销的推测解码加速。
- **数据流系统与推理社区基础设施**：非平稳数据流在线指纹选择框架（WWW '26），以及 vLLM / vLLM-Ascend 社区推理演进追踪与技术综述工作台。

---

### 代表系统与开源项目

| 项目 | 方向与平台 | 核心机制与关键指标 |
| :--- | :--- | :--- |
| **[LatchMoE (NPU)](https://github.com/vLLM-HUST/vllm-ascend-hust-LatchMoE)**<br>**[LatchMoE-GPU](https://github.com/Li-changwu/LatchMoE-GPU)** | 图兼容 MoE 专家缓存卸载<br>`Ascend NPU` · `CUDA Graph` · `vLLM` | 面向受限显存的地址稳定、图重放兼容 MoE 专家缓存框架（论文工作，NPU + GPU 双后端）；通过预分配固定槽位、持久设备映射、图外异步 Staging、有界溢出分波（Bounded Waves）与槽位租约保护，在保持捕获计算图稳定权重地址的同时消除远端按需访存瓶颈。 |
| **[BriskMoE (MoE-SD)](https://github.com/Li-changwu/MoE-SD)** | MoE 卸载 × 推测解码<br>`CUDA` · `vLLM` | 非侵入式 vLLM 插件；通过 Pool-Direct、无同步路由（TASER）、草稿引导预取（DIPP）与推测感知替换消除缓存开销与瞬态溢出，单卡 RTX A6000 实现 Qwen3-30B-A3B **4.80×**、GPT-OSS-120B **5.00×** 解码加速。 |
| **[Cruise](https://github.com/Li-changwu/Cruise)** | 设备驻留解码控制面<br>`Ascend 910B2` · `CANN` | 基于 DataFlow Device UDF 将解码内层循环、Paged-KV 更新与采样下沉至昇腾设备侧按有界 Epoch 执行；单 Epoch 控制边界载荷从 **136.9 MB 降至 628 B**，Host 控制耗时降低 **3.54×**。 |
| **[KV_Cache](https://github.com/Li-changwu/KV_Cache)** | 长上下文分层 KV 管理<br>`vLLM` · `HBM/DRAM/SSD` | 面向多轮长上下文推理的 Persistent KV Anti-Caching 原型；通过内存常驻三级状态索引与执行前 PrePass，将 SSD 冷对象恢复移出在线请求关键路径。 |
| **[Flash-SD](https://github.com/Li-changwu/FlashSD)** | 零开销语义推测解码<br>`PyTorch` · `Transformers` | 无需训练、即插即用的推测解码框架；利用目标模型熵动态调节验证阈值并结合并行前瞻锚定，以 `O(1)` 标量投影校验开销实现语义级推理加速。 |

---

### 学术论文

- **[WWW '26]** **Changwu Li**, Tongjun Shi, Shuhao Zhang, Binbin Chen, Bingsheng He, Xiaofei Liao, Hai Jin.  
  *StreamFP: Fingerprint-guided Data Selection for Efficient Stream Learning.*  
  In *Proceedings of the ACM Web Conference 2026*. [[Code](https://github.com/CGCL-codes/StreamFP)] · [[DOI](https://doi.org/10.1145/3774904.3792584)]

---

### 开源社区与工具生态

- **[vLLM & vLLM-Ascend 推理研究日报与技术专题工作台](https://lab.sage.org.ai/auto-research-report-website/)** · [[GitHub](https://github.com/intellistream/auto-research-report-website)]  
  社区研报网站负责人，持续追踪 vLLM 与 vLLM-Ascend 核心性能优化演进，建设 ACLGraph 图执行、KV Cache 与推测解码等系统技术专题综述，并参与 [vLLM-HUST](https://github.com/vLLM-HUST) 国产算力推理运行时生态建设。
- **[Codex Provider Switcher](https://github.com/Li-changwu/codex-provider-switcher)** · [[VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=Li-changwu.codex-provider-switcher-vscode)]  
  面向 Windows 本地与 Linux Remote-SSH 环境的 VS Code 扩展，支持多套 Codex Provider 配置的安全切换、SecretStorage 凭据隔离、事务级备份回滚与原生会话续接。

---

### 技术栈

- **推理系统与异构算力**：`vLLM (V1 Engine / Platform Plugins)` · `PyTorch` · `CUDA / CUDA Graph` · `Ascend CANN (ACLGraph / DataFlow Device UDF)` · `Triton`
- **系统开发与性能剖析**：`Python` · `C / C++` · `TypeScript` · `PyTorch Profiler / Nsight / Ascend Profiling` · `Linux`
