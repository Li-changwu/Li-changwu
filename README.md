## Changwu Li

**华中科技大学（HUST）博士研究生** · [CGCL](https://github.com/CGCL-codes) / [IntelliStream Lab](https://github.com/intellistream) · [vLLM-HUST](https://github.com/vLLM-HUST)

专注于 **大模型推理系统（LLM Serving Systems）** 与 **ACL Graph 图兼容机制（Graph-Compatible Execution）** 研究，围绕静态计算图捕获、回放约束下的动态状态管理与设备控制边界开展系统构建：

- **ACL Graph 图兼容专家缓存与卸载**：面向动态路由与受限显存场景，通过预分配地址稳定固定槽位、持久设备映射、图外异步 Staging 与有界溢出分波，解决权重动态换入换出破坏静态图捕获与回放的问题。
- **单步图回放之上的设备驻留控制面**：在计算图消除单次执行算子下发开销的基础上，利用昇腾 DataFlow Device UDF 将跨步解码循环、Paged-KV 更新与采样下沉至设备侧按有界 Epoch 连续执行，消除逐 Token Host 协调往返。
- **推理图执行综述与数据流系统**：负责维护社区 **ACL Graph 技术专题综述** 与 vLLM / vLLM-Ascend 性能演进研报工作台，并开展非平稳数据流在线指纹选择研究（WWW '26）。

---

### 代表推理系统

| 项目 | 方向与平台 | 核心机制与关键结果 |
| :--- | :--- | :--- |
| **[LatchMoE (NPU)](https://github.com/vLLM-HUST/vllm-ascend-hust-LatchMoE)**<br>**[LatchMoE-GPU](https://github.com/Li-changwu/LatchMoE-GPU)** | 图兼容 MoE 专家缓存卸载<br>`ACL Graph` · `vLLM` · `CUDA Graph` | 面向受限显存的地址稳定、图回放兼容 MoE 专家缓存框架（论文工作，昇腾 NPU 主实现 + CUDA `PIECEWISE` 图对照实现）；通过预分配固定槽位、持久设备映射、图外异步 Staging、有界溢出分波（Bounded Waves）与槽位租约保护，保持捕获计算图权重地址稳定并消除远端按需访存瓶颈。 |
| **[Cruise](https://github.com/Li-changwu/Cruise)** | 设备驻留解码控制面<br>`Ascend 910B2` · `CANN` · `vLLM V1` | 探索单次图回放之上的跨步控制边界：基于 CANN DataFlow Device UDF 将解码内层控制循环、Paged-KV 状态更新与采样下沉至昇腾设备侧按有界 Epoch 连续执行；单 Epoch 控制边界载荷从 **136.9 MB 降至 628 B**，Host 控制耗时降低 **3.54×**。 |

---

### 学术论文

- **[WWW '26]** **Changwu Li**, Tongjun Shi, Shuhao Zhang, Binbin Chen, Bingsheng He, Xiaofei Liao, Hai Jin.  
  *StreamFP: Fingerprint-guided Data Selection for Efficient Stream Learning.*  
  In *Proceedings of the ACM Web Conference 2026*. [[Code](https://github.com/CGCL-codes/StreamFP)] · [[DOI](https://doi.org/10.1145/3774904.3792584)]

---

### 开源社区建设

- **[vLLM & vLLM-Ascend 推理研究日报与技术专题工作台](https://lab.sage.org.ai/auto-research-report-website/)** · [[ACL Graph 旗舰综述](https://lab.sage.org.ai/auto-research-report-website/#/topics/aclgraph)] · [[GitHub](https://github.com/intellistream/auto-research-report-website)]  
  社区研报网站负责人，主编昇腾推理图执行（ACL Graph：捕获、回放与动态状态）深度技术综述与动态报告，持续追踪 vLLM / vLLM-Ascend 性能优化演进，并参与 [vLLM-HUST](https://github.com/vLLM-HUST) 推理运行时生态建设。

---

### 技术栈

- **图执行与推理运行时**：`vLLM (V1 Engine / vLLM-Ascend)` · `Ascend CANN (ACL Graph / DataFlow Device UDF)` · `PyTorch` · `CUDA Graph` · `Triton`
- **系统开发与性能剖析**：`Python` · `C / C++` · `Ascend Profiling / PyTorch Profiler` · `Linux`
