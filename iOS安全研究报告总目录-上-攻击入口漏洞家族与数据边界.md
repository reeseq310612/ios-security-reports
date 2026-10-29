# iOS安全研究报告总目录（上）：攻击入口、漏洞家族与数据边界

- 定位：本仓库的索引页之一。把与「入口 → 利用 → 数据产出」主线相关的 51 篇分析按主题归组，给出直达链接，便于按阶段阅读。
- 范围：只收录本仓库已公开的中文报告；不包含未发布草稿、外部原文与厂商内部资料。
- 说明：每篇正文自带资料来源与置信边界声明，本页只做导航，不重复正文结论，也不对具体漏洞真实性作二次断言。

## 摘要

攻击面研究的问题不是「有没有漏洞」，而是「哪条路径在什么前置条件下成立、代价多高、留下多少痕迹」。这 51 篇按四层组织：漏洞链与商业攻击家族（谁在把漏洞做成产品）、WebKit 与浏览器入口（远程代码执行的第一步落在哪里）、硬件与无线接口（近场与物理路径的现实门槛）、沙箱与数据保护（攻击成功之后到底能取走什么）。

阅读顺序建议：先看第一章建立「攻击是工程」的判断，再用第二章确认入口形态，第三章判断物理可达性，第四章核对数据边界——四章合起来才构成一次完整的可行性评估。

## 本页收录说明

- 全仓库共 97 篇技术分析（不含 README 与本索引两篇），本页收录第 1–51 篇，另一半见《iOS安全研究报告总目录（下）：内核防御与企业实践索引》。
- 文件名为仓库内的原始文件名，链接为相对路径，在 GitHub 与 Gitee 镜像中均可直接打开。
- 同一主题下按文件名字母序排列，不代表重要性排序；同名系列的多篇（如 `-上`/`-下`、不同版本）保留原样，便于对照差异。

## 一、攻击链与漏洞家族

- [Coruna-vs-DarkSword两大iOS高级漏洞链全面对比](Coruna-vs-DarkSword两大iOS高级漏洞链全面对比.md)
- [Coruna漏洞链技术拆解-23个漏洞如何组成iOS攻击平台](Coruna漏洞链技术拆解-23个漏洞如何组成iOS攻击平台.md)
- [Coruna与DarkSword-iOS系统级攻击平台安全态势分析-2026](Coruna与DarkSword-iOS系统级攻击平台安全态势分析-2026.md)
- [Coruna与DarkSword漏洞利用链架构对比分析-从入口点到数据外传的十维深度解析](Coruna与DarkSword漏洞利用链架构对比分析-从入口点到数据外传的十维深度解析.md)
- [Coruna与DarkSword入侵的设备行为指纹-终端用户可见异常信号与全攻击阶段行为画像构建](Coruna与DarkSword入侵的设备行为指纹-终端用户可见异常信号与全攻击阶段行为画像构建.md)
- [Coruna与DarkSword完整攻击链安全研究报告](Coruna与DarkSword完整攻击链安全研究报告.md)
- [Coruna源码架构分析-JavaScript-Exploit-Framework如何管理23个漏洞模块](Coruna源码架构分析-JavaScript-Exploit-Framework如何管理23个漏洞模块.md)
- [Darksword漏洞研究-iOS18时代商业攻击链分析](Darksword漏洞研究-iOS18时代商业攻击链分析.md)
- [iOS-Coruna漏洞网络安全分析报告](iOS-Coruna漏洞网络安全分析报告.md)
- [iOS-Coruna漏洞与Darksword漏洞分析-现代iOS攻击链中的高级漏洞研究](iOS-Coruna漏洞与Darksword漏洞分析-现代iOS攻击链中的高级漏洞研究.md)
- [iOS-DarkSword漏洞网络安全分析报告](iOS-DarkSword漏洞网络安全分析报告.md)
- [iOS-Exploit-Chain工程化研究-从入口漏洞到设备控制](iOS-Exploit-Chain工程化研究-从入口漏洞到设备控制.md)
- [iOS-Exploit-Chain工程化研究-从入口漏洞到现代攻击平台](iOS-Exploit-Chain工程化研究-从入口漏洞到现代攻击平台.md)
- [iOS安全暗线-Coruna与DarkSword漏洞链深度分析报告](iOS安全暗线-Coruna与DarkSword漏洞链深度分析报告.md)
- [iOS攻击链工程化研究-Coruna漏洞编排框架的模块化设计与链选择策略-从Loader到版本兼容的公开技术分析与防御含义](iOS攻击链工程化研究-Coruna漏洞编排框架的模块化设计与链选择策略-从Loader到版本兼容的公开技术分析与防御含义.md)
- [iOS漏洞暗战-Coruna与DarkSword到三角行动](iOS漏洞暗战-Coruna与DarkSword到三角行动.md)
- [iOS系统漏洞详细网络安全报告-2026](iOS系统漏洞详细网络安全报告-2026.md)
- [iOS系统网络安全漏洞分析报告](iOS系统网络安全漏洞分析报告.md)
- [Pegasus完整技术演进史-从2016到现代零点击攻击](Pegasus完整技术演进史-从2016到现代零点击攻击.md)
- [商业间谍软件生态研究-Pegasus与Predator与iOS高级攻击链](商业间谍软件生态研究-Pegasus与Predator与iOS高级攻击链.md)
- [商业间谍软件终极图谱-Pegasus-Predator-Coruna-Darksword技术演进](商业间谍软件终极图谱-Pegasus-Predator-Coruna-Darksword技术演进.md)

## 二、WebKit 与浏览器攻击面

- [DarkSword攻击链威胁建模与ATT-CK映射分析-从水坑入口到数据访问各阶段的可观测信号检测机会与证据限制](DarkSword攻击链威胁建模与ATT-CK映射分析-从水坑入口到数据访问各阶段的可观测信号检测机会与证据限制.md)
- [DarkSword完整技术报告-现代iOS六漏洞全链攻击浏览器沙箱与内核安全研究](DarkSword完整技术报告-现代iOS六漏洞全链攻击浏览器沙箱与内核安全研究.md)
- [DarkSword现代iOS多阶段漏洞利用链深度分析-JavaScriptCore-PAC-沙箱逃逸与XNU内核六漏洞链条与防御策略](DarkSword现代iOS多阶段漏洞利用链深度分析-JavaScriptCore-PAC-沙箱逃逸与XNU内核六漏洞链条与防御策略.md)
- [iOS-Exploit-Chain工程化研究-从入口漏洞到现代攻击平台-WebKit-Sandbox-Kernel与商业化漏洞生态的演进](iOS-Exploit-Chain工程化研究-从入口漏洞到现代攻击平台-WebKit-Sandbox-Kernel与商业化漏洞生态的演进.md)
- [iOS-WebKit远程代码执行与内核提权安全分析报告](iOS-WebKit远程代码执行与内核提权安全分析报告.md)
- [iOS零点击漏洞攻击链深度拆解-从WebKit到Kernel](iOS零点击漏洞攻击链深度拆解-从WebKit到Kernel.md)
- [iOS水坑攻击解析-Coruna与DarkSword浏览器漏洞利用链](iOS水坑攻击解析-Coruna与DarkSword浏览器漏洞利用链.md)
- [iOS水坑攻击与网页零日漏洞分析报告](iOS水坑攻击与网页零日漏洞分析报告.md)
- [iOS水坑投递链与网页注入路径防御分析-Coruna与DarkSword公开报道中的投递环节DNS-CDN与链接预览信任边界](iOS水坑投递链与网页注入路径防御分析-Coruna与DarkSword公开报道中的投递环节DNS-CDN与链接预览信任边界.md)
- [JavaScriptCore-JIT类型混淆缺陷审计方法研究-编译器优化不变量对象生命周期与修复验证的防御视角](JavaScriptCore-JIT类型混淆缺陷审计方法研究-编译器优化不变量对象生命周期与修复验证的防御视角.md)
- [WebKit-MachIPC-Kernel-现代iOS-Exploit-Chain完整分析](WebKit-MachIPC-Kernel-现代iOS-Exploit-Chain完整分析.md)
- [WebKit漏洞研究方法-从JavaScriptCore到JIT安全](WebKit漏洞研究方法-从JavaScriptCore到JIT安全.md)

## 三、硬件、无线与物理接口

- [CarKey数字车钥匙与UWB-免提进入的中继攻击与密钥分享边界](CarKey数字车钥匙与UWB-免提进入的中继攻击与密钥分享边界.md)
- [HomeKit与Matter-智能家居配对的信任边界与跨生态风险](HomeKit与Matter-智能家居配对的信任边界与跨生态风险.md)
- [iOS外设与物理接口攻击面-USB限制模式配件认证与调试接口分析](iOS外设与物理接口攻击面-USB限制模式配件认证与调试接口分析.md)
- [iOS无线攻击面-从基带到蓝牙与AirDrop的射频入口分析](iOS无线攻击面-从基带到蓝牙与AirDrop的射频入口分析.md)

## 四、沙箱、数据保护与取证边界

- [AppAttest与DeviceCheck-设备证明机制的可信边界与代理风险](AppAttest与DeviceCheck-设备证明机制的可信边界与代理风险.md)
- [Apple私有云计算PCC安全架构-可验证透明度与无状态推理的信任边界](Apple私有云计算PCC安全架构-可验证透明度与无状态推理的信任边界.md)
- [iCloud高级数据保护ADP-端到端密钥层级恢复联系人与取证边界](iCloud高级数据保护ADP-端到端密钥层级恢复联系人与取证边界.md)
- [iOS-GPU进程与ANGLE攻击面分析-跨进程IPC参数校验WebContent到GPU进程的信任边界与沙箱层次](iOS-GPU进程与ANGLE攻击面分析-跨进程IPC参数校验WebContent到GPU进程的信任边界与沙箱层次.md)
- [iOS-SandboxEscape技术演进分析-从App隔离到安全边界突破](iOS-SandboxEscape技术演进分析-从App隔离到安全边界突破.md)
- [iOS备份通道与取证边界-本地备份加密密钥与提取限制分析](iOS备份通道与取证边界-本地备份加密密钥与提取限制分析.md)
- [iOS侧信道研究-功耗电磁与缓存泄漏的可行性边界](iOS侧信道研究-功耗电磁与缓存泄漏的可行性边界.md)
- [iOS零点击漏洞技术演进史-从Pegasus到BlastDoor](iOS零点击漏洞技术演进史-从Pegasus到BlastDoor.md)
- [iOS零点击消息路径与BlastDoor隔离有效性评估-从Pegasus到Coruna与DarkSword投递方式差异的防御含义](iOS零点击消息路径与BlastDoor隔离有效性评估-从Pegasus到Coruna与DarkSword投递方式差异的防御含义.md)
- [iOS数据保护与Keychain在攻击链上下文中的实际边界-锁定状态密钥层级与可恢复数据范围分析](iOS数据保护与Keychain在攻击链上下文中的实际边界-锁定状态密钥层级与可恢复数据范围分析.md)
- [iOS锁定模式深度解析-攻击面削减机制与高风险用户防御边界](iOS锁定模式深度解析-攻击面削减机制与高风险用户防御边界.md)
- [iOS卫星通信与紧急SOS-离线场景下的安全边界与隐私设计分析](iOS卫星通信与紧急SOS-离线场景下的安全边界与隐私设计分析.md)
- [辅助功能与覆盖攻击-iOS银行木马的可行性边界分析](辅助功能与覆盖攻击-iOS银行木马的可行性边界分析.md)
- [快捷指令与URLScheme-跨应用自动化的信任边界分析](快捷指令与URLScheme-跨应用自动化的信任边界分析.md)

## 结语

索引本身不产生结论，它的价值在于缩短「从问题到证据」的路径。如果只能读三篇，建议按「漏洞链架构对比 → 零点击入口拆解 → 数据保护边界」的顺序建立整体框架，再回到具体主题补齐细节。

本页会随仓库更新而增补；新增文章归档到对应章节，已更名的旧文件保留历史链接条目，避免外部引用失效。

## 维护说明

- 收录原则：只放本仓库自有分析；不收录二手转述，不索引未公开材料。
- 更新节奏：与仓库发布同步（每批新增文章发布后补充对应条目）。
- 勘误：条目链接如失效，请以仓库根目录文件列表为准。

联系方式（Telegram）：https://t.me/one00190
