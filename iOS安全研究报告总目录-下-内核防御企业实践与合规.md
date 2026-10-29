# iOS安全研究报告总目录（下）：内核防御与企业实践索引

- 定位：本仓库的索引页之二。把「防御架构 → 检测响应 → 合规约束」这条主线的 46 篇分析按主题归组，给出直达链接。
- 范围：只收录本仓库已公开的中文报告；不包含未发布草稿、外部原文与厂商内部资料。
- 说明：每篇正文自带资料来源与置信边界声明，本页只做导航；涉及具体漏洞的结论以正文的证据等级为准。
## 摘要

防御侧的难点在于「代际差」：同一条攻击链，在 PPL 时代与 SPTM/TXM 时代的成本结构完全不同，用旧结论评估新系统会系统性高估风险或低估残余面。这 46 篇按三层组织：内核与内存安全（PAC、PPL/SPTM、MIE、XNU 与 IOKit 的攻防演进）、威胁情报与企业防御（从 GTIG 类公开分析到检测工程与响应流程）、法律与合规（出口管制与取证标准）。

阅读建议：第一章用于校准「现在还剩多少可攻击空间」，第二章用于把情报转成可执行的检测与响应动作，第三章用于判断研究、披露与共享的合规边界。

## 本页收录说明

- 全仓库共 97 篇技术分析（不含 README 与本索引两篇），本页收录第 52–97 篇，另一半见《iOS安全研究报告总目录（上）：攻击入口、漏洞家族与数据边界》。
- 文件名为仓库内的原始文件名，链接为相对路径，在 GitHub 与 Gitee 镜像中均可直接打开。
- 内核主题存在多篇同系列分析，保留原样以便交叉印证；引用时建议注明具体文件名。

## 一、内核与内存安全

- [ARM64e安全体系-PAC-MTE与Apple-Silicon防御演进-从指针认证到内存标记的层次化设计](ARM64e安全体系-PAC-MTE与Apple-Silicon防御演进-从指针认证到内存标记的层次化设计.md)
- [BootROM与不可修补漏洞-checkm8时代的长期安全影响分析](BootROM与不可修补漏洞-checkm8时代的长期安全影响分析.md)
- [Coruna-Kernel阶段解析-XNU-IOKit与PAC-PPL绕过技术路线](Coruna-Kernel阶段解析-XNU-IOKit与PAC-PPL绕过技术路线.md)
- [Coruna漏洞研究-从传统Kernel-Exploit到SPTM时代](Coruna漏洞研究-从传统Kernel-Exploit到SPTM时代.md)
- [Coruna与DarkSword入侵设备数字取证方法论-内存取证APFS分析与网络流量捕获的实战框架](Coruna与DarkSword入侵设备数字取证方法论-内存取证APFS分析与网络流量捕获的实战框架.md)
- [Darksword与iOS-Kernel-Exploit关系分析-从Safari入口到XNU内核控制](Darksword与iOS-Kernel-Exploit关系分析-从Safari入口到XNU内核控制.md)
- [iOS-Kernel漏洞案例库-从IOKit到SPTM时代](iOS-Kernel漏洞案例库-从IOKit到SPTM时代.md)
- [iOS-Kernel漏洞案例库-从IOKit到SPTM时代-XNU内核攻击面演进与苹果防御体系变化](iOS-Kernel漏洞案例库-从IOKit到SPTM时代-XNU内核攻击面演进与苹果防御体系变化.md)
- [iOS-Kernel漏洞案例库-从IOKit到SPTM时代的攻击演进-XNU内核漏洞硬件防护与现代Exploit-Chain发展路线](iOS-Kernel漏洞案例库-从IOKit到SPTM时代的攻击演进-XNU内核漏洞硬件防护与现代Exploit-Chain发展路线.md)
- [iOS安全技术深度解析-从硬件信任根到高级漏洞攻击链](iOS安全技术深度解析-从硬件信任根到高级漏洞攻击链.md)
- [iOS安全架构全面解析-从硬件信任根到内核隔离与纵深防御-安全启动Secure-Enclave代码签名沙箱数据保护PAC与BlastDoor的分层设计](iOS安全架构全面解析-从硬件信任根到内核隔离与纵深防御-安全启动Secure-Enclave代码签名沙箱数据保护PAC与BlastDoor的分层设计.md)
- [iOS安全架构与纵深防御合并版-从硬件信任根运行时隔离到PAC与MIE的完整分层防御分析](iOS安全架构与纵深防御合并版-从硬件信任根运行时隔离到PAC与MIE的完整分层防御分析.md)
- [iOS内存无文件攻击与漏洞套件安全分析报告-2026](iOS内存无文件攻击与漏洞套件安全分析报告-2026.md)
- [iOS内核安全机制深度解析-从XNU架构到现代移动安全防御体系-上](iOS内核安全机制深度解析-从XNU架构到现代移动安全防御体系-上.md)
- [iOS内核安全机制深度解析-从XNU架构到现代移动安全防御体系-下](iOS内核安全机制深度解析-从XNU架构到现代移动安全防御体系-下.md)
- [iOS内核漏洞分析方法论-从Mach到XNU](iOS内核漏洞分析方法论-从Mach到XNU.md)
- [iOS内核文件系统竞态类缺陷防御演进-VFS路径的并发风险审计要点与苹果缓解机制覆盖评估](iOS内核文件系统竞态类缺陷防御演进-VFS路径的并发风险审计要点与苹果缓解机制覆盖评估.md)
- [iOS指针认证PAC覆盖范围评估方法-用户态与内核态保护差异关键指针类型与可复核实验设计](iOS指针认证PAC覆盖范围评估方法-用户态与内核态保护差异关键指针类型与可复核实验设计.md)
- [iOS纵深防御架构研究-从安全启动到内存完整性保护-硬件信任根运行时隔离PAC与MIE的分层防御分析](iOS纵深防御架构研究-从安全启动到内存完整性保护-硬件信任根运行时隔离PAC与MIE的分层防御分析.md)
- [Memory-Integrity-Enforcement苹果下一代内存安全战略分析](Memory-Integrity-Enforcement苹果下一代内存安全战略分析.md)
- [PAC绕过技术演进-ARM64e时代控制流保护分析](PAC绕过技术演进-ARM64e时代控制流保护分析.md)
- [PAC与MIE现代iOS内存安全防护的演进-从指针认证到EMTE与内核内存完整性](PAC与MIE现代iOS内存安全防护的演进-从指针认证到EMTE与内核内存完整性.md)
- [PPL与SPTM-TXM区别解析-iOS内核保护机制如何从页面保护演进到页表信任分离](PPL与SPTM-TXM区别解析-iOS内核保护机制如何从页面保护演进到页表信任分离.md)
- [SPTM-TXM深度解析-苹果如何重新定义Kernel安全边界](SPTM-TXM深度解析-苹果如何重新定义Kernel安全边界.md)
- [SPTM-TXM深度解析-苹果如何重新定义Kernel安全边界-从PPL到分层信任监控器的架构演进](SPTM-TXM深度解析-苹果如何重新定义Kernel安全边界-从PPL到分层信任监控器的架构演进.md)
- [SPTM-TXM深度解析-苹果如何重新定义Kernel安全边界-页表隔离与硬件信任机制的架构变化](SPTM-TXM深度解析-苹果如何重新定义Kernel安全边界-页表隔离与硬件信任机制的架构变化.md)
- [SPTM-TXM与Exclaves苹果下一代安全架构解析](SPTM-TXM与Exclaves苹果下一代安全架构解析.md)
- [SPTM-TXM与MIE时代攻击链可持续性评估-Coruna与DarkSword类链在iOS防御代际演进下的成本抬升与残余风险分析](SPTM-TXM与MIE时代攻击链可持续性评估-Coruna与DarkSword类链在iOS防御代际演进下的成本抬升与残余风险分析.md)
- [XNU-Kernel漏洞演进史-从iOS10到iOS18安全架构变化](XNU-Kernel漏洞演进史-从iOS10到iOS18安全架构变化.md)
- [苹果平台安全机制在高级攻击下的压力测试-SPTMPAC与沙箱防御层对Coruna和DarkSword的实际效力分析](苹果平台安全机制在高级攻击下的压力测试-SPTMPAC与沙箱防御层对Coruna和DarkSword的实际效力分析.md)
- [商业间谍软件终结时代-MIE对Pegasus类攻击链的影响分析](商业间谍软件终结时代-MIE对Pegasus类攻击链的影响分析.md)
- [现代iOS-Kernel漏洞挖掘方法论-从源码审计到安全验证](现代iOS-Kernel漏洞挖掘方法论-从源码审计到安全验证.md)
- [现代iOS-Kernel漏洞挖掘方法论-从源码审计到漏洞验证-XNU-IOKit-Mach-IPC与安全研究流程](现代iOS-Kernel漏洞挖掘方法论-从源码审计到漏洞验证-XNU-IOKit-Mach-IPC与安全研究流程.md)

## 二、威胁情报与企业防御

- [Coruna与DarkSword恶意载荷技术分析-C2协议指纹IOC提取与SOC检测规则构建](Coruna与DarkSword恶意载荷技术分析-C2协议指纹IOC提取与SOC检测规则构建.md)
- [Coruna与DarkSword供应链攻击路径与国家行为体归因分析-从组件依赖到C2基础设施的纵深追踪](Coruna与DarkSword供应链攻击路径与国家行为体归因分析-从组件依赖到C2基础设施的纵深追踪.md)
- [Coruna与DarkSword两条iOS高级攻击链技术对比-GTIG公开分析中的版本覆盖漏洞组合与防御建议](Coruna与DarkSword两条iOS高级攻击链技术对比-GTIG公开分析中的版本覆盖漏洞组合与防御建议.md)
- [Coruna与DarkSword漏洞的版本瞄准经济学-iOS补丁节奏逆向工程成本与碎片化博弈模型](Coruna与DarkSword漏洞的版本瞄准经济学-iOS补丁节奏逆向工程成本与碎片化博弈模型.md)
- [DarkSword威胁与数据窃取分析-iOS移动威胁情报技术报告-载荷家族数据外传反取证与分级响应](DarkSword威胁与数据窃取分析-iOS移动威胁情报技术报告-载荷家族数据外传反取证与分级响应.md)
- [iOS分发链与配置描述文件在企业环境中的滥用面-Coruna与DarkSword类攻击上下文下的审核MDM与证书防御](iOS分发链与配置描述文件在企业环境中的滥用面-Coruna与DarkSword类攻击上下文下的审核MDM与证书防御.md)
- [iOS高级移动威胁检测与应急响应实践报告-Coruna与DarkSword类攻击链的分级研判取证限制与处置流程](iOS高级移动威胁检测与应急响应实践报告-Coruna与DarkSword类攻击链的分级研判取证限制与处置流程.md)
- [iOS攻击链补丁窗口与暴露风险量化分析-Coruna与DarkSword公开版本区间到设备群覆盖率的度量方法与指标体系](iOS攻击链补丁窗口与暴露风险量化分析-Coruna与DarkSword公开版本区间到设备群覆盖率的度量方法与指标体系.md)
- [iOS攻击链持久化与重启后驻留问题研究综述-公开案例的概念边界检测方法与取证限制](iOS攻击链持久化与重启后驻留问题研究综述-公开案例的概念边界检测方法与取证限制.md)
- [面向Coruna与DarkSword级攻击的企业级iOS防御体系构建-零信任架构移动EDR与事件响应实战](面向Coruna与DarkSword级攻击的企业级iOS防御体系构建-零信任架构移动EDR与事件响应实战.md)
- [移动威胁情报MTI企业落地实践-从GTIG公开分析到TTP建模检测工程与IOC使用限制](移动威胁情报MTI企业落地实践-从GTIG公开分析到TTP建模检测工程与IOC使用限制.md)
- [针对Coruna与DarkSword威胁的情报共享框架构建-ISAC协作STIXTAXII标准化与组织级威胁情报生态](针对Coruna与DarkSword威胁的情报共享框架构建-ISAC协作STIXTAXII标准化与组织级威胁情报生态.md)

## 三、法律、合规与生态

- [Coruna与DarkSword漏洞的法律合规影响-Wassenaar出口管制GDPR第32条与跨国网络犯罪取证标准](Coruna与DarkSword漏洞的法律合规影响-Wassenaar出口管制GDPR第32条与跨国网络犯罪取证标准.md)

## 结语

把防御写清楚，比把攻击写清楚更难：攻击可以只描述"能做什么"，防御必须回答"在什么前提下不成立、成本落在谁身上、失效后如何发现"。本页收录的分析都在正文里保留了这类前提与限制，索引只负责把它们放在一起。

如果要做一次内部技术评审，建议从「SPTM/TXM 与 PPL 的差异」「MIE 的覆盖边界」「补丁窗口与暴露量化」三处切入，先确认代际判断，再谈具体检测规则。

## 维护说明

- 收录原则：只放本仓库自有分析；不收录二手转述，不索引未公开材料。
- 更新节奏：与仓库发布同步（每批新增文章发布后补充对应条目）。
- 勘误：链接失效时以仓库根目录文件列表为准。

联系方式（Telegram）：https://t.me/one00190
