# 角色驱动的八股文分类体系

## 使用说明

本文档定义了不同岗位角色的八股文考察范围。在 `build-profile.md` 的 Step 1 中，系统根据用户的 `target_roles.primary` 匹配角色，激活对应的分类体系。

**设计原则：** 不同岗位的八股文考察范围完全不同。一刀切的 7 大类模板会导致用户浪费大量时间在无关内容上。AI 算法岗不需要背 MySQL 索引，Java 后端不需要学 Transformer。

---

## 1. Java 后端开发 (`java-backend`)

### 计算机网络
子主题：TCP/IP（三次握手/四次挥手/状态转换）、HTTP/HTTPS（1.0/1.1/2.0/3.0 区别、状态码）、DNS（解析过程、CDN）、负载均衡（L4/L7、常见算法）、网络安全（XSS/CSRF/SQL注入）

### 数据库
子主题：MySQL（索引 B+Tree/最左前缀/覆盖索引/索引下推/慢查询分析、事务 ACID/隔离级别/MVCC、锁 行锁/间隙锁/死锁检测、分库分表 垂直/水平/ShardingKey）、Redis（5 种数据结构及底层实现/使用场景、持久化 RDB/AOF 混合、集群 主从/哨兵/Cluster、缓存穿透/击穿/雪崩方案）

### 编程语言
子主题：Java 基础（集合 HashMap/ConcurrentHashMap/ArrayList 原理、泛型类型擦除、注解原理、反射）、JVM（内存模型 堆/栈/方法区/元空间、GC CMS/G1/ZGC 原理及调优、类加载 双亲委派/打破、JIT 编译）、并发编程（synchronized 锁升级/ReentrantLock/AQS 原理、线程池 7 参数/拒绝策略/常用线程池、ThreadLocal 原理及内存泄漏、volatile 可见性/禁止指令重排）

### 框架
子主题：Spring（IOC 容器/依赖注入/Bean 生命周期/循环依赖解决、AOP 原理/动态代理 JDK vs CGLIB、事务传播机制）、Spring Boot（自动配置原理/Starter 机制、启动流程）、MyBatis（一级/二级缓存、${} vs #{}、插件机制）、Spring Cloud（微服务组件 Nacos/Gateway/Feign/Sentinel）

### 操作系统
子主题：进程线程（区别/通信方式/同步方式）、内存管理（虚拟内存/分页/分段/页面置换 LRU,LFU）、IO 模型（BIO/NIO/AIO、select/poll/epoll）、文件系统（inode、硬链接 vs 软链接）

### 设计模式
子主题：创建型（单例 饿汉/懒汉/DCL/枚举、工厂、建造者）、结构型（代理 JDK/CGLIB、适配器、装饰器）、行为型（观察者、策略、模板方法）——每种在框架中的应用

### 分布式
子主题：CAP/BASE 理论、一致性算法（Raft 选举/日志复制、Paxos 概念）、消息队列（Kafka 架构/ISR/ACK 机制/高性能原因、RocketMQ 架构/事务消息）、RPC（Dubbo 架构/负载均衡/服务发现）、分布式事务（Seata AT/TCC/Saga）、分布式锁（Redis Redlock/Zookeeper 临时节点）

---

## 2. AI 算法工程师 (`ai-algorithm`)

### 大模型基础
子主题：Transformer 架构（Self-Attention/Multi-Head Attention/FFN 细节、Encoder-Decoder vs Decoder-Only）、位置编码（Sinusoidal/RoPE/ALiBi）、归一化方法（LayerNorm/RMSNorm/Pre-Norm vs Post-Norm）、激活函数（GELU/SwiGLU）

### 预训练
子主题：数据准备（数据清洗/去重/质量过滤、数据配比策略）、分布式训练（DP/DDP/TP/PP/ZeRO 三部曲）、混合精度训练（FP16/BF16/AMP）、Scaling Law（Kaplan/Chinchilla 的结论和应用）、预训练目标（MLM/NSP 到 GPT-style Next Token Prediction）

### SFT 监督微调
子主题：指令微调（数据格式/多样性/质量的重要性、Self-Instruct 演化方法）、数据构建（人工标注 vs 模型生成、数据配比实验设计）、多任务微调（防止灾难性遗忘）、Chat 模板（System/User/Assistant 角色格式）

### RLHF/PPO
子主题：奖励模型（Reward Model 训练/数据收集/排序偏好）、PPO 算法（重要性采样/Clipping/KL 散度约束）、DPO/ORPO（直接偏好优化原理/与 PPO 对比、什么时候用 DPO vs RLHF）、RLHF 工程实践（4 模型训练管线、reward hacking 问题）

### 推理优化
子主题：量化（GPTQ/AWQ/GGUF 原理和精度对比、INT8/INT4/NF4）、KV-Cache 优化（PagedAttention/vLLM、Prefix Caching）、投机采样（Speculative Decoding/Medusa）、模型蒸馏（知识蒸馏/任务蒸馏）、推理框架（vLLM/TGI/TensorRT-LLM）

### Prompt Engineering
子主题：基础技巧（Few-shot/CoT/ToT/ReAct、角色设定/输出格式控制）、RAG 基础（检索-增强-生成 Pipeline、Embedding 模型选择/Chunk 策略）、Function Calling（Tool Use/结构化输出、参数 Schema 设计）

### 评估体系
子主题：通用 Benchmark（MMLU/HellaSwag/HumanEval 测什么/局限性）、LLM-as-Judge（MT-Bench/Chatbot Arena、评价 bias 问题）、人工评估（评测标准设计/标注一致性）、红队测试（安全性/拒答率/Harmfulness 评估）

---

## 3. Agent 开发工程师 (`agent-dev`)

### Agent 架构
子主题：核心循环（Plan-Execute-Observe 循环设计、ReAct/Tool-use/Code-acting 模式对比）、记忆系统（短期记忆/长期记忆/工作记忆、向量存储 vs 结构化存储）、上下文管理（Token 预算/上下文压缩/摘要策略）、错误恢复（自动重试/降级策略/Human-in-the-loop）

### Vibe Coding
子主题：AI 辅助编程实践（Prompt 设计/迭代开发/代码生成策略）、快速原型（从想法到 MVP 的 AI 加速流程）、代码审查（AI 生成代码的质量检查/安全审查）、工程实践（版本控制/AI 代码的测试策略）

### Skills / 工具调用
子主题：Function Calling（OpenAI/Anthropic 的 Tool Use 机制对比、JSON Schema 设计最佳实践）、MCP 协议（Model Context Protocol 原理/Client-Server 架构/Transport 层）、工具注册与发现（工具描述的质量对调用成功率的影响）、错误处理（工具调用失败的重试和降级）

### 多 Agent 协作
子主题：通信协议（Agent 间消息格式/任务描述标准化）、任务分配（基于能力的路由/负载均衡/优先级调度）、上下文共享（共享记忆/知识图谱/黑板模式）、冲突解决（多 Agent 竞态条件/一致性保证）

### RAG
子主题：检索增强生成（Embedding/Rerank/生成三段式 Pipeline、Embedding 模型选型 中文/多语言）、向量数据库（Milvus/Pinecone/Weaviate 对比、索引类型 IVF/HNSW）、文档处理（Chunk 策略 Fixed/Recursive/Semantic/Agentic、Metadata 设计）、重排序（Cross-encoder Reranker/Cohere Rerank）

### LLM 集成
子主题：API 调用（OpenAI/Anthropic/国产模型 API 差异、Streaming/非 Streaming 处理）、Token 管理（Token 计数/预算控制/截断策略）、速率限制（Rate Limit 处理/指数退避/队列机制）、成本优化（Prompt Caching/模型选择策略/批处理）、多模型路由（根据任务复杂度路由到不同模型）

### Workflow 编排
子主题：框架对比（LangChain vs LangGraph vs Dify vs Coze vs n8n、适用场景和局限性）、工作流模式（顺序/条件/并行/循环、状态管理/检查点）、可观测性（Tracing/Logging/Metrics、LangSmith/Weave 等工具）、生产化（部署/扩缩容/监控告警）

---

## 4. Go 后端开发 (`go-backend`)

### Go 语言基础
子主题：goroutine（调度原理/GOMAXPROCS/抢占式调度）、channel（有缓冲 vs 无缓冲/select 多路复用/关闭语义）、interface（空接口/类型断言/底层 eface/iface 结构）、内存管理（GC 三色标记+混合写屏障/逃逸分析）

### 并发编程
子主题：GMP 模型（G/M/P 三者关系/工作窃取/ handoff）、锁（sync.Mutex 正常模式+饥饿模式/RWMutex）、sync 包（WaitGroup/Once/Pool/Cond 使用场景）、context（取消传播/超时控制/值传递）、并发模式（Pipeline/Fan-in/Fan-out/Or-Done）

### 框架
子主题：Gin（路由树/中间件机制/Context 设计）、Kratos（微服务框架/布局规范/中间件）、go-zero（API 网关/RPC 框架/缓存设计）、路由与中间件（中间件链/错误处理/请求日志）

### 数据库
子主题：MySQL（索引优化/连接池配置/sqlx vs GORM）、Redis（go-redis 使用/连接池/ Pipeline）、索引优化（慢查询定位/Explain 分析/覆盖索引）

### 分布式
子主题：微服务（服务拆分/API 设计/版本管理）、服务发现（Consul/Etcd/Nacos 对比）、gRPC（Protobuf/流式调用/拦截器/负载均衡）、消息队列（Kafka Go 客户端/sarama/消费者组）

### 容器化
子主题：Docker（多阶段构建/镜像优化/安全最佳实践）、Kubernetes（基础概念 Pod/Service/Deployment/Ingress、健康检查/资源限制）、CI/CD（GitHub Actions/GitLab CI 的 Go 项目 Pipeline）

---

## 5. C++ 开发 (`cpp-dev`)

### C++ 基础
子主题：指针与引用（智能指针 unique_ptr/shared_ptr/weak_ptr 实现原理、RAII 资源管理）、内存管理（new/delete vs malloc/free、内存泄漏检测工具 valgrind/AddressSanitizer）、STL（vector/map/unordered_map 底层原理/迭代器失效场景）、模板元编程（模板特化/SFINAE/constexpr/可变参数模板）

### 操作系统
子主题：进程线程（fork/pthread/Linux 进程地址空间/COW）、虚拟内存（页表/TLB/缺页中断/mmap）、文件 IO（阻塞/非阻塞/IO 多路复用 epoll 原理）、信号处理（signal/sigaction/信号集）

### 计算机网络
子主题：Socket 编程（TCP/UDP socket API 使用/非阻塞 IO 模型）、网络协议（TCP 拥塞控制/滑动窗口/Nagle 算法）、高性能网络（epoll/Reactor/Proactor 模式）

### 编译链接
子主题：编译过程（预处理→编译→汇编→链接 四阶段/静态库 vs 动态库）、链接（符号解析/重定位/GOT/PLT）、构建工具（CMake 核心语法/Makefile 入门）

### 性能优化
子主题：内存优化（内存池设计/对象池/内存对齐/Cache Line 优化）、并发优化（无锁编程 CAS/原子操作/内存序 memory order、RCU 机制）、性能工具（perf/火焰图/gprof/Valgrind 使用场景）、编译器优化（inline/PGO/LTO）

---

## 6. 前端开发 (`frontend`)

### HTML/CSS
子主题：语义化（HTML5 标签语义/SEO/可访问性）、布局（Flex/Grid/定位/居中方案）、响应式（媒体查询/rem-vw/移动端适配）、CSS 工程化（CSS Modules/Scope/Sass/Less 组织）

### JavaScript
子主题：原型链（prototype/__proto__/new 关键字/继承）、闭包与作用域（词法作用域/闭包应用与内存泄漏）、异步（Promise/async-await/事件循环宏任务微任务）、ES6+（解构/扩展运算符/箭头函数/Proxy/Reflect/模块化）

### 框架
子主题（React 路线）：Hooks（useState/useEffect/useMemo/useCallback 原理和依赖、自定义 Hooks）、状态管理（Redux/Zustand/Jotai/Context）、路由（React Router 动态路由/嵌套路由/懒加载）

子主题（Vue 路线）：响应式（Object.defineProperty vs Proxy/ref vs reactive）、Composition API（setup/watch/computed/lifecycle）、状态管理（Pinia/Vuex）

### 工程化
子主题：构建工具（Webpack 核心概念 Loader/Plugin/优化、Vite ESM/预构建/插件机制）、性能优化（代码分割/懒加载/Tree Shaking/首屏优化 Core Web Vitals）、测试（Jest/Vitest 单元测试/组件测试 E2E）、监控（Sentry/性能监控/错误收集）

### 浏览器原理
子主题：渲染流程（DOM/CSSOM/Render Tree/Layout/Paint/Composite 关键渲染路径）、事件循环（宏任务/微任务/requestAnimationFrame）、安全（XSS/CSRF/CSP/CORS/HTTPS）、缓存策略（强缓存/协商缓存/Service Worker）

### TypeScript
子主题：类型系统（基础类型/联合类型/交叉类型/类型推断/类型守卫）、泛型（泛型约束/条件类型/工具类型 Partial,Pick,Omit）、工程实践（tsconfig 配置/类型声明文件/与 JS 项目整合）

---

## 7. 数据开发 (`data-dev`)

### SQL
子主题：复杂查询（多表 JOIN 类型与性能/子查询 vs CTE/EXISTS vs IN）、窗口函数（ROW_NUMBER/RANK/LAG/LEAD/聚合窗口+PARTITION BY）、索引优化（Explain 执行计划解读/索引类型选择/索引失效场景）、数据倾斜（原因与解决方案/Join 倾斜/GroupBy 倾斜）

### 数据仓库
子主题：建模方法论（星型/雪花/Data Vault 选型、维度建模 缓慢变化维/退化维）、分层架构（ODS/DWD/DWS/ADS 职责与数据流转、指标体系设计 原子指标/派生指标/复合指标）、数据质量（完整性/准确性/一致性/及时性监控）

### 大数据引擎
子主题：Hive（HQL 优化/分区/分桶/文件格式 ORC/Parquet、UDF 开发）、Spark（RDD vs DataFrame vs DataSet/Shuffle 优化/内存管理/动态资源分配、Spark SQL Catalyst 优化器）、Flink（流处理 vs 批处理/Checkpoint/状态后端/CEP 复杂事件处理、Watermark/窗口 滚动/滑动/会话）

### 数据治理
子主题：数据血缘（字段级/表级血缘追踪、元数据管理 DataHub/Atlas）、数据安全（权限管理 Ranger/Sentry、数据脱敏/加密）、资产管理（数据目录/数据地图/数据生命周期）
