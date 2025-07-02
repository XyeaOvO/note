# 第九章 传输线理论 (Transmission Line Theory)
你好！欢迎来到“传输线理论”的学习之旅。这一章我们将深入探索电磁波在特定结构（即传输线）中是如何“行进”的。你可能会想，我们不是已经学了麦克斯韦方程组和平面电磁波在无界空间或简单介质中的传播了吗？为什么还要专门研究传输线呢？🤔

答案就在于“引导”二字。在实际应用中，我们往往需要将电磁能量（信号）从一点高效、可控地传输到另一点，而不是任其向四面八方辐射。传输线，如我们日常接触到的同轴电缆、手机内部的微带线等，正是扮演着这种“波的管道”的角色。

本章内容参照B站西北工业大学朱海亮教授的课件以及其编著的《微波技术与天线》教材。
https://www.bilibili.com/video/BV1oT4y1774h?p=3

---

### 为啥要学这一章？🤔 治波之道与高频挑战

想象一下古代大禹治水，疏导洪水，使其按照预定的河道安稳流淌。在电磁世界里，我们做着类似的事情：**我们“治波”，让微波沿着我们设定的“道路”（传输线）行走。**

这为什么如此重要，甚至需要专门作为一章来学习呢？

1.  **高频世界的“新规则”** 👑：
    *   在低频电路中（如我们熟悉的《电路分析基础》），连接导线通常被视为理想的等电位体，信号似乎是瞬时传递的。我们可以放心地使用集总参数模型（单个电阻、电容、电感）。
    *   然而，当信号频率升高到**微波频段**（通常指300MHz - 300GHz，波长在1米到1毫米之间），情况发生了根本性变化。信号的**波长 $\lambda$ 与传输线的物理尺寸 $l$ 变得可以相比拟**。这时：
        *   电压和电流不再是线上各点瞬时相同，而是会随时间和空间发生显著的**相位和幅度变化**，呈现出清晰的**波动特性**。
        *   我们再也不能简单地将连接导线视为“短路”或“开路”，也不能忽略其自身的**分布参数**——即沿线分布的电阻(R)、电感(L)、电导(G)和电容(C)。这些参数在高频下变得至关重要。
    *   **频率高了，什么事情都有可能发生。** 比如信号反射、能量损耗、驻波形成、甚至辐射干扰等，这些都是低频电路中很少遇到的“大问题”。

2.  **无处不在的应用** 📱📡：
    我们无时无刻不生活在传输线效应起作用的世界里。你手中的智能手机就是一个绝佳的例子：
    *   无论是接收还是发送信号，从天线到内部处理芯片，再从芯片到天线，信号都需要在电路板上通过微带线等传输线结构进行精确的引导和处理（如放大、调制/解调）。
    *   如果这些“微波道路”设计不当（例如，阻抗不匹配），信号就会在途中“迷路”或“受阻”（发生反射），导致能量无法有效传输，通信质量急剧下降，甚至可能损坏敏感的电子元器件。

**简而言之，不理解传输线理论，我们就无法设计和分析现代高频电子电路与系统。** 它是微波工程乃至整个电子信息领域的一块重要基石。

准备好了吗？让我们开始正式探索传输线是如何工作的，以及如何分析和设计它们！

---

### 3.1 传输线的分布参数及其等效电路 💡

要分析传输线上的电磁波传播，首先需要建立它的数学模型。与低频电路不同，传输线的电阻(R)、电感(L)、电导(G)和电容(C)不再是集中在某个器件上，而是均匀或非均匀地**分布**在其整个长度上。这些单位长度的参数被称为**分布参数**。

*   $R$: 单位长度导体的电阻 (单位: $\Omega/\text{m}$)，代表导体中的欧姆损耗。
*   $L$: 单位长度传输线的外部电感 (单位: $\text{H}/\text{m}$)，由围绕导体的磁场产生。
*   $G$: 单位长度导体间绝缘介质的电导 (单位: $\text{S}/\text{m}$)，代表介质中的泄漏损耗。
*   $C$: 单位长度导体间的电容 (单位: $\text{F}/\text{m}$)，由导体间的电场产生。
	
#### “长线”和“短线”的相对论 📏

我们常听到“长线效应”或说某个电路需要按“长线”处理。这里的“长”和“短”并非绝对的物理长度，而是**相对于线上传输信号的波长而言的**。

*   **与该传输线本身的长短没有必然关系，跟线上传输的信号的波长有关。**
*   此处“长”和“短”说的是**电长度**，而非物理长度。
    *   如果传输线的物理长度 $l$ 与信号波长 $\lambda$ 相比拟，甚至远大于波长 ($l \ge \lambda/10$ 或更严格)，那么电压和电流沿线的相位变化就不可忽略，必须按**长线（即传输线理论）**处理。
    *   如果 $l \ll \lambda$ (例如 $l < \lambda/100$)，则可以近似认为信号沿线瞬时传递，按**短线（即集总参数电路）** 处理。
*   **“短线”较为简单，“长线”相对复杂，实际中，微波传输线大多属于“长线”。**
    *   ![](Pic/Pasted%20image%2020250522112522.png)
    *   左图：波长很短，相对于线路长度，线上能容纳多个波，相位变化显著（长线）。
    *   右图：波长很长，相对于线路长度，线上相位变化微小（短线）。

#### 微波传输线长啥样? 🧐

有多种结构可以用来引导微波能量，常见的有：

![](Pic/Pasted%20image%2020250522123128.png)

*   **(a) 平行双导线 (Parallel Two-Wire Line)**: 两条平行的导体，如早期的电视馈线。易受外界干扰，辐射也较大。
*   **(b) 同轴线 (Coaxial Line)**: 由内导体和同轴外导体组成，中间填充介质。具有良好的屏蔽性，广泛应用于射频和微波信号传输。参数有内导体半径 $a$，外导体内半径 $b$。
*   **(c) 平行导体板 (Parallel Plate Line)**: 两块平行的导体板，间距为 $b$，板宽为 $W$。
*   **(d) 带状线 (Stripline)**: 一条窄导体带位于两块接地板之间，并由介质填充。
*   **微带线 (Microstrip Line)**: (下图左下角) 现代印制电路板(PCB)上最常见的传输线形式。由一块接地板、一层介质基板和基板上的一条导体带组成。其参数包括导体带宽度 $W$，介质厚度 $h$，介质相对介电常数 $\epsilon_r$。
    ![](Pic/Fig_7_Microstrip_and_Connectors.png)
    (上图右侧是实际的微带线器件和各种同轴连接器)

#### 如何建模分析微波传输线? --- 变长为短，由分布到集总 🧩

直接分析具有无限多分布参数的整条传输线是困难的。一个巧妙的方法是：将传输线分割成无限多个**长度为 $\Delta z$ 的微小段**。如果 $\Delta z$ 足够小 (远小于波长)，那么在这一小段内，可以认为电压和电流的变化是线性的，并且可以用**集总参数**来近似描述这一小段的电气特性。

*   **“集总 (lumped) 参数” 和 “分布 (distributed) 参数”**
    *   对于长度为 $\Delta z$ 的一小段均匀传输线，其总电阻为 $R\Delta z$，总电感为 $L\Delta z$，总电导为 $G\Delta z$，总电容为 $C\Delta z$。
    *   我们可以用一个包含这些集总元件的**等效电路模型**来表示这一小段传输线。最常用的模型是 **T型或 $\Pi$型等效电路**。下图 (b) 展示了一个L型（或不对称T型）的等效电路。

    ![](Pic/Fig_8_Lumped_vs_Distributed_and_Equivalent_Circuit.png)
    *   **(a) 传输系统**: 显示了整个传输线系统，包括信号源 ($e_g, Z_g$) 和负载 ($Z_l$)，以及线上的电压 $u(z,t)$ 和电流 $i(z,t)$。
    *   **(b) $\Delta z$ 段的等效电路**:
        *   串联阻抗: $R\Delta z + j\omega L\Delta z$ (如果考虑时谐场)
        *   并联导纳: $G\Delta z + j\omega C\Delta z$ (如果考虑时谐场)
        （图中显示的是串联电阻 $R\Delta z$ 和串联电感 $L\Delta z$，以及并联电导 $G\Delta z$ 和并联电容 $C\Delta z$。这是瞬时模型的基础。）

通过分析这个微元段上的电压和电流关系，当 $\Delta z \to 0$ 时，我们就能推导出描述整个传输线上电压和电流行为的**偏微分方程**，即**传输线方程 (Telegrapher's Equations)**。

(图8左下角展示了一个用分立元件搭建的电路板，这是典型的集总参数电路。右下角是微带线功率分配器，是典型的分布参数电路应用。)

---

### 3.2 一般形式的传输线方程及其解 🌊

现在，我们基于上一节建立的传输线微元段等效电路模型，来推导控制电压和电流沿线变化的数学方程。

#### 回顾：$\Delta z$ 段的等效电路

![](Pic/Fig_10_Equivalent_Circuit_Segment_for_Derivation.png)

*   在位置 $z$ 处的电压为 $u(z,t)$，电流为 $i(z,t)$。
*   在位置 $z+\Delta z$ 处的电压为 $u(z+\Delta z, t)$，电流为 $i(z+\Delta z, t)$。
*   该 $\Delta z$ 段的串联电阻为 $R\Delta z$，串联电感为 $L\Delta z$。
*   该 $\Delta z$ 段的并联电导为 $G\Delta z$，并联电容为 $C\Delta z$。

#### 基尔霍夫定律的应用  Kirchhoff's Laws ⚡

我们对这个等效电路应用基尔霍夫定律：

1.  **基尔霍夫电压定律 (KVL)** 应用于外回路 (A-B-C-D-A)：
    电压降之和等于0。
    $u(z,t) - (R\Delta z)i(z,t) - (L\Delta z)\frac{\partial i(z,t)}{\partial t} - u(z+\Delta z, t) = 0$
    (教材图中的 $i(z,t)$ 应该理解为在 $R\Delta z$ 和 $L\Delta z$ 上的电流，如果 $i(z,t)$ 是指进入该段的电流，那么在 $\Delta z$ 非常小时，这个近似是合理的。)
    整理并两边同除以 $\Delta z$:
    $-\frac{u(z+\Delta z, t) - u(z,t)}{\Delta z} = R i(z,t) + L \frac{\partial i(z,t)}{\partial t}$

2.  **基尔霍夫电流定律 (KCL)** 应用于节点 B (或等效地看流出上导线的电流)：
    流入节点的电流等于流出节点的电流。
    $i(z,t) - (G\Delta z)u(z+\Delta z, t) - (C\Delta z)\frac{\partial u(z+\Delta z, t)}{\partial t} - i(z+\Delta z, t) = 0$
    (这里的 $u(z+\Delta z, t)$ 近似等于并联支路上的电压 $u(z,t)$，当 $\Delta z$ 很小时)
    整理并两边同除以 $\Delta z$:
    $-\frac{i(z+\Delta z, t) - i(z,t)}{\Delta z} = G u(z+\Delta z, t) + C \frac{\partial u(z+\Delta z, t)}{\partial t}$

#### 传输线方程 (时域形式)  TELEGRAPHER'S EQUATIONS

当 $\Delta z \to 0$ 时，差商变为偏导数，并且 $u(z+\Delta z, t) \to u(z,t)$：
$\boxed{ -\frac{\partial u(z,t)}{\partial z} = R i(z,t) + L \frac{\partial i(z,t)}{\partial t} \quad \text{(3.9c)} }$
$\boxed{ -\frac{\partial i(z,t)}{\partial z} = G u(z,t) + C \frac{\partial u(z,t)}{\partial t} \quad \text{(3.9d)} }$

这就是著名的**传输线方程**或**电报方程**。它们是一对联立的、一阶线性偏微分方程，描述了电压和电流在有损耗传输线上随时间和空间的变化规律。

(图右侧是古斯塔夫·基尔霍夫 (Gustav Kirchhoff, 1824-1887)，德国物理学家，对电路理论和光谱学做出了巨大贡献。)
![](Pic/Fig_10_Kirchhoff.png)

#### 时谐情况下的传输线方程 (频域/相量形式) HARMONIC STEADY-STATE 🎶

在许多实际应用中，我们关心的是信号在**时谐稳态 (sinusoidal steady-state)**下的行为。这时，电压和电流可以表示为相量形式：
*   $u(z,t) = \text{Re}[\dot{U}(z)e^{j\omega t}]$
*   $i(z,t) = \text{Re}[\dot{I}(z)e^{j\omega t}]$
其中 $\dot{U}(z)$ 和 $\dot{I}(z)$ 是随位置 $z$ 变化的复振幅 (相量)，$\omega$ 是角频率。

在这种情况下，时域导数 $\partial/\partial t$ 可以替换为 $j\omega$。传输线方程 (3.9c) 和 (3.9d) 变为：
$\boxed{ -\frac{d\dot{U}(z)}{dz} = (R+j\omega L)\dot{I}(z) = Z\dot{I}(z) \quad \text{(3.14a)} }$
$\boxed{ -\frac{d\dot{I}(z)}{dz} = (G+j\omega C)\dot{U}(z) = Y\dot{U}(z) \quad \text{(3.14b)} }$

这里我们定义了：
*   **串联阻抗参数**: $Z = R+j\omega L$ ($\Omega/\text{m}$)
*   **并联导纳参数**: $Y = G+j\omega C$ ($\text{S}/\text{m}$)

注意，此时偏导数 $\partial/\partial z$ 变成了常微分 $d/dz$，因为时间变量已经被分离出去。
(式3.13是相量表示的说明，从瞬时值到复振幅的简记。)
![](Pic/Fig_11_From_Time_Domain_to_Phasor_Domain.png)

#### 波动方程的推导 WAVE EQUATIONS

为了求解 $\dot{U}(z)$ 和 $\dot{I}(z)$，我们可以将上述两个一阶常微分方程解耦，得到二阶常微分方程，即**波动方程**。

对 (3.14a) 两边关于 $z$ 求导，并将 (3.14b) 代入：
$\frac{d^2\dot{U}(z)}{dz^2} = -Z \frac{d\dot{I}(z)}{dz} = -Z (-Y\dot{U}(z)) = ZY\dot{U}(z)$
$\boxed{ \frac{d^2\dot{U}(z)}{dz^2} - \gamma^2 \dot{U}(z) = 0 \quad \text{(3.15a), (3.16a)} }$

类似地，对 (3.14b) 两边关于 $z$ 求导，并将 (3.14a) 代入：
$\frac{d^2\dot{I}(z)}{dz^2} = -Y \frac{d\dot{U}(z)}{dz} = -Y (-Z\dot{I}(z)) = ZY\dot{I}(z)$
$\boxed{ \frac{d^2\dot{I}(z)}{dz^2} - \gamma^2 \dot{I}(z) = 0 \quad \text{(3.15b), (3.16b)} }$

这里引入了一个非常重要的参数：
*   **传播常数 (Propagation Constant) $\gamma$**:
    $\boxed{ \gamma = \sqrt{ZY} = \sqrt{(R+j\omega L)(G+j\omega C)} = \alpha + j\beta }$
    $\gamma$ 是一个复数，其实部 $\alpha$ 称为**衰减常数 (Attenuation Constant)** (单位: Np/m 或 dB/m)，虚部 $\beta$ 称为**相移常数 (Phase Constant)** (单位: rad/m)。

#### 波动方程的通解 GENERAL SOLUTION

方程 (3.16a) 和 (3.16b) 是标准的二阶齐次常微分方程，其通解形式为：
$\boxed{ \dot{U}(z) = \dot{U}^+ e^{-\gamma z} + \dot{U}^- e^{\gamma z} \quad \text{(3.17a)} }$
$\boxed{ \dot{I}(z) = \dot{I}^+ e^{-\gamma z} + \dot{I}^- e^{\gamma z} }$ (注意：这里的 $\dot{I}^+$ 和 $\dot{I}^-$ 与 $\dot{U}^+$ 和 $\dot{U}^-$ 不是独立的，它们之间有关系)

*   $e^{-\gamma z} = e^{-\alpha z}e^{-j\beta z}$: 代表一个沿 $+z$ 方向传播的波，其振幅随 $z$ 按 $e^{-\alpha z}$ 衰减，相位随 $z$ 按 $e^{-j\beta z}$ 滞后。我们称之为**入射波 (Incident Wave)** 或前向行波。
*   $e^{\gamma z} = e^{\alpha z}e^{j\beta z}$: 代表一个沿 $-z$ 方向传播的波，其振幅随 $z$ (从负载端 $z=l$ 看向源端 $z=0$) 按 $e^{-\alpha (l-z)}$ 衰减 (或者说，当 $z$ 减小时，其幅度按 $e^{\alpha z}$ 衰减，如果源在 $z=0$)，相位随 $z$ 按 $e^{j\beta z}$ 超前。我们称之为**反射波 (Reflected Wave)** 或反向行波。
*   $\dot{U}^+, \dot{U}^-$: 是由边界条件决定的复常数，分别代表入射电压波和反射电压波在 $z=0$ 处的复振幅。

#### 特性阻抗 CHARACTERISTIC IMPEDANCE $Z_0$ 🌟

$\dot{U}(z)$ 和 $\dot{I}(z)$ 之间存在一个重要的关系。将 $\dot{U}(z)$ 的解代入 (3.14a)：
$-\frac{d}{dz}(\dot{U}^+ e^{-\gamma z} + \dot{U}^- e^{\gamma z}) = Z\dot{I}(z)$
$- (-\gamma \dot{U}^+ e^{-\gamma z} + \gamma \dot{U}^- e^{\gamma z}) = Z\dot{I}(z)$
$\gamma (\dot{U}^+ e^{-\gamma z} - \dot{U}^- e^{\gamma z}) = Z\dot{I}(z)$
所以，$\dot{I}(z) = \frac{\gamma}{Z}(\dot{U}^+ e^{-\gamma z} - \dot{U}^- e^{\gamma z})$

我们定义 **特性阻抗 (Characteristic Impedance) $Z_0$** 为：
$\boxed{ Z_0 = \frac{Z}{\gamma} = \frac{Z}{\sqrt{ZY}} = \sqrt{\frac{Z}{Y}} = \sqrt{\frac{R+j\omega L}{G+j\omega C}} \quad \text{(3.18)} }$

$Z_0$ 一般也是一个复数。它代表了传输线上**单一方向行波**（例如只有入射波，没有反射波）的电压与电流之比。即：
*   对于入射波：$\frac{\dot{U}^+(z)}{\dot{I}^+(z)} = \frac{\dot{U}^+e^{-\gamma z}}{(\dot{U}^+/Z_0)e^{-\gamma z}} = Z_0$
*   对于反射波：$\frac{\dot{U}^-(z)}{\dot{I}^-(z)} = \frac{\dot{U}^-e^{\gamma z}}{(-\dot{U}^-/Z_0)e^{\gamma z}} = -Z_0$ (注意负号，因为反射电流通常定义为与反射电压波同向传播，即也沿 $-z$ 方向，或者说，如果电流总是从左到右为正，则反射波的电压和电流相位差180度，或者幅度比为 $-Z_0$)

因此，电流的通解可以更简洁地写为：
$\boxed{ \dot{I}(z) = \frac{1}{Z_0}(\dot{U}^+ e^{-\gamma z} - \dot{U}^- e^{\gamma z}) = \dot{I}^+(z) + \dot{I}^-(z) \quad \text{(3.17b)} }$
其中 $\dot{I}^+(z) = \dot{U}^+(z)/Z_0$ 是入射电流波，$\dot{I}^-(z) = \dot{U}^-(z)/(-Z_0)$ 是反射电流波。

(图12的“通解”框图仅说明了从二阶微分方程到解的形式，并未涉及$Z_0$的推导)
![](Pic/Fig_12_General_Solution_Path.png)

#### 把时间和空间再次合在一起 (瞬时表达式) ⏳🌌

将相量解 $\dot{U}(z), \dot{I}(z)$ 转换回时域瞬时表达式 $u(z,t), i(z,t)$ (式3.20)：
令 $\dot{U}^+ = |\dot{U}^+|e^{j\varphi_+}$ 和 $\dot{U}^- = |\dot{U}^-|e^{j\varphi_-}$。
$u(z,t) = \text{Re}[ (|\dot{U}^+|e^{j\varphi_+} e^{-\alpha z}e^{-j\beta z}) e^{j\omega t} + (|\dot{U}^-|e^{j\varphi_-} e^{\alpha z}e^{j\beta z}) e^{j\omega t} ]$
$u(z,t) = |\dot{U}^+|e^{-\alpha z} \cos(\omega t - \beta z + \varphi_+) + |\dot{U}^-|e^{\alpha z} \cos(\omega t + \beta z + \varphi_-)$
$u(z,t) = u^+(z,t) + u^-(z,t)$

类似地，对于电流（假设 $Z_0$ 是实数，即无耗线，则 $\dot{I}^+ = \dot{U}^+/Z_0, \dot{I}^- = -\dot{U}^-/Z_0$）：
$i(z,t) = \frac{1}{Z_0} [ |\dot{U}^+|e^{-\alpha z} \cos(\omega t - \beta z + \varphi_+) - |\dot{U}^-|e^{\alpha z} \cos(\omega t + \beta z + \varphi_-) ]$
$i(z,t) = i^+(z,t) + i^-(z,t)$
(如果 $Z_0 = |Z_0|e^{j\theta_0}$ 是复数，则电流的相位会有一个额外的 $\theta_0$ 的偏移。)

(式3.18和3.19分别定义了 $Z_0$ 和 $\gamma$。)

#### 回头看一下刚才走过的路 🗺️

我们从传输线的微元等效电路出发，应用基尔霍夫定律，得到了描述电压电流沿线变化的偏微分方程（传输线方程）。然后，在时谐稳态条件下，将其转换为常微分的波动方程，并求得了其通解。这个解告诉我们，传输线上的总电压/电流是**入射波**和**反射波**的叠加。
![](Pic/Fig_13_Road_Traveled.png)
入射波从源端向负载端传播，反射波从负载（或其他不连续点）处产生并向源端传播。

**解的形式已经知道，就差确定未知系数了。**
这两个未知系数 $\dot{U}^+$ 和 $\dot{U}^-$ (或者等价的 $\dot{I}^+$ 和 $\dot{I}^-$，或 $\dot{U}^+$ 和 $\dot{U}^-/\dot{U}^+$) 需要由传输线的**边界条件**来确定。

---

### 确定未知系数：边界条件的应用 🔑

我们已经得到了电压和电流的通解：
$\dot{U}(z) = \dot{U}^+ e^{-\gamma z} + \dot{U}^- e^{\gamma z}$
$\dot{I}(z) = \frac{1}{Z_0}(\dot{U}^+ e^{-\gamma z} - \dot{U}^- e^{\gamma z})$

其中的 $\dot{U}^+$ 和 $\dot{U}^-$ 是待定常数，它们由传输线的两端（或某些特定点）的条件——即**边界条件**——来确定。

![](Pic/Fig_14_Typical_Transmission_Line_System_for_Boundary_Conditions.png)
上图是一个典型的传输线系统，长度为 $l$。
*   $z=0$ 处为始端 (通常接信号源 $E_g, Z_g$)。
*   $z=l$ 处为终端 (通常接负载 $Z_L$)。
*   **注意图中的坐标系**：有时为了方便分析从负载端看过去的特性（如输入阻抗），会引入一个新的坐标 $z' = l-z$，此时 $z'=0$ 对应负载端，$z'=l$ 对应始端。原始的 $z$ 坐标是从始端（电源端）指向负载端。

**常见的边界条件类型 (参考书 P47-49 页)**：

1.  **给定始端 ($z=0$) 电压 $\dot{U}_i$ 和电流 $\dot{I}_i$**：
    *   $\dot{U}(0) = \dot{U}_i = \dot{U}^+ + \dot{U}^-$
    *   $\dot{I}(0) = \dot{I}_i = \frac{1}{Z_0}(\dot{U}^+ - \dot{U}^-)$
    这是一个关于 $\dot{U}^+$ 和 $\dot{U}^-$ 的二元一次方程组，可以解出：
    $\dot{U}^+ = \frac{1}{2}(\dot{U}_i + Z_0 \dot{I}_i)$
    $\dot{U}^- = \frac{1}{2}(\dot{U}_i - Z_0 \dot{I}_i)$

2.  **给定终端 ($z=l$) 电压 $\dot{U}_L$ 和电流 $\dot{I}_L$**：
    *   $\dot{U}(l) = \dot{U}_L = \dot{U}^+ e^{-\gamma l} + \dot{U}^- e^{\gamma l}$
    *   $\dot{I}(l) = \dot{I}_L = \frac{1}{Z_0}(\dot{U}^+ e^{-\gamma l} - \dot{U}^- e^{\gamma l})$
    同样可以解出 $\dot{U}^+ e^{-\gamma l}$ 和 $\dot{U}^- e^{\gamma l}$，进而得到 $\dot{U}^+$ 和 $\dot{U}^-$：
    $\dot{U}^+ e^{-\gamma l} = \frac{1}{2}(\dot{U}_L + Z_0 \dot{I}_L) \Rightarrow \dot{U}^+ = \frac{1}{2}(\dot{U}_L + Z_0 \dot{I}_L)e^{\gamma l}$
    $\dot{U}^- e^{\gamma l} = \frac{1}{2}(\dot{U}_L - Z_0 \dot{I}_L) \Rightarrow \dot{U}^- = \frac{1}{2}(\dot{U}_L - Z_0 \dot{I}_L)e^{-\gamma l}$

    **特别地，如果已知负载阻抗 $Z_L = \dot{U}_L / \dot{I}_L$**:
    $\dot{U}_L - Z_0 \dot{I}_L = \dot{I}_L (Z_L - Z_0)$
    $\dot{U}_L + Z_0 \dot{I}_L = \dot{I}_L (Z_L + Z_0)$
    代入后可以得到 $\dot{U}^-$ 与 $\dot{U}^+$ 之间的关系，这引出了**反射系数**的概念（稍后详述）。

3.  **给定波源电动势 $E_g$、内阻 $Z_g$ 以及负载阻抗 $Z_L$**：
    *   在始端 $z=0$：$\dot{U}(0) = E_g - \dot{I}(0)Z_g$
    *   在终端 $z=l$：$\dot{U}(l) = \dot{I}(l)Z_L$
    将通解代入这两个方程，可以联立求解 $\dot{U}^+$ 和 $\dot{U}^-$。这种方法最为通用。

#### 以边界条件 (2) 为例推导 $U(z)$ 和 $I(z)$ 的另一种形式 📝

如果我们使用**从负载端算起的坐标 $z' = l-z$** (即 $z=l-z'$)，并利用终端条件 $\dot{U}(z'=0) = \dot{U}_L$ 和 $\dot{I}(z'=0) = \dot{I}_L$，则解的形式变为：
$\dot{U}(z') = \dot{U}_L^+ e^{-\gamma z'} + \dot{U}_L^- e^{\gamma z'}$
$\dot{I}(z') = \frac{1}{Z_0}(\dot{U}_L^+ e^{-\gamma z'} - \dot{U}_L^- e^{\gamma z'})$
(这里 $\dot{U}_L^+$ 和 $\dot{U}_L^-$ 是以 $z'=0$ 即负载处为参考点的前向和反向波幅值，与之前的 $\dot{U}^+, \dot{U}^-$ 不同)

在 $z'=0$ 处：
$\dot{U}_L = \dot{U}_L^+ + \dot{U}_L^-$
$Z_0 \dot{I}_L = \dot{U}_L^+ - \dot{U}_L^-$
解得：
$\dot{U}_L^+ = \frac{1}{2}(\dot{U}_L + Z_0 \dot{I}_L)$
$\dot{U}_L^- = \frac{1}{2}(\dot{U}_L - Z_0 \dot{I}_L)$

代回 $\dot{U}(z')$ 和 $\dot{I}(z')$ 的表达式：
$\dot{U}(z') = \frac{1}{2}(\dot{U}_L + Z_0 \dot{I}_L)e^{-\gamma z'} + \frac{1}{2}(\dot{U}_L - Z_0 \dot{I}_L)e^{\gamma z'}$
$\dot{U}(z') = \dot{U}_L \frac{e^{\gamma z'} + e^{-\gamma z'}}{2} + Z_0 \dot{I}_L \frac{e^{\gamma z'} - e^{-\gamma z'}}{2}$ (这里似乎PPT中用 $e^{\gamma z'}$ 的项与 $(\dot{U}_L - Z_0 \dot{I}_L)$ 关联， $e^{-\gamma z'}$ 的项与 $(\dot{U}_L + Z_0 \dot{I}_L)$ 关联，如果 $e^{-\gamma z'}$ 代表前向波，这是反的。我们按标准的双曲函数形式来。)

使用双曲函数 $\cosh x = (e^x+e^{-x})/2$ 和 $\sinh x = (e^x-e^{-x})/2$:
$\boxed{ \dot{U}(z') = \dot{U}_L \cosh(\gamma z') + \dot{I}_L Z_0 \sinh(\gamma z') \quad \text{(3.26a)} }$
$\boxed{ \dot{I}(z') = \dot{I}_L \cosh(\gamma z') + \frac{\dot{U}_L}{Z_0} \sinh(\gamma z') \quad \text{(3.26b)} }$
(这里的 $z'$ 是从负载端算起的距离。)
PPT中的 (3.24a) 和 (3.24b) 是在 $z$ 坐标系下，用 $z'=l-z$ 代换到 $(l-z)$ 的指数项，并用终端 $\dot{I}_L$ 和 $Z_L$ 来表示 $\dot{U}^+$ 和 $\dot{U}^-$。具体推导：
从式 (3.23) (PPT中的方程号)，$\dot{U}^+ = \frac{1}{2}(\dot{U}_L + Z_0 \dot{I}_L)e^{\gamma l}$ 和 $\dot{U}^- = \frac{1}{2}(\dot{U}_L - Z_0 \dot{I}_L)e^{-\gamma l}$。
代入 $\dot{U}(z) = \dot{U}^+ e^{-\gamma z} + \dot{U}^- e^{\gamma z}$：
$\dot{U}(z) = \frac{1}{2}(\dot{U}_L + Z_0 \dot{I}_L)e^{\gamma (l-z)} + \frac{1}{2}(\dot{U}_L - Z_0 \dot{I}_L)e^{-\gamma (l-z)}$
将 $\dot{U}_L = \dot{I}_L Z_L$ 代入，并整理：
$\dot{U}(z) = \frac{\dot{I}_L}{2} [ (Z_L+Z_0)e^{\gamma(l-z)} + (Z_L-Z_0)e^{-\gamma(l-z)} ] \quad \text{(3.24a)}$
$\dot{I}(z) = \frac{\dot{I}_L}{2Z_0} [ (Z_L+Z_0)e^{\gamma(l-z)} - (Z_L-Z_0)e^{-\gamma(l-z)} ] \quad \text{(3.24b)}$
这些公式以终端电流 $\dot{I}_L$ 和负载阻抗 $Z_L$ 作为已知量。
而式 (3.26a) 和 (3.26b) 是以终端电压 $\dot{U}_L$ 和终端电流 $\dot{I}_L$ 作为已知量，并用 $z'=l-z$ 表示。

![](Pic/Fig_15_Boundary_Condition_2_Example.png)
![](Pic/Fig_16_Simplified_Form_using_z_prime.png)
(图16中高亮了 $z'=l-z$ 的变换，并将结果简化为双曲函数形式。)

#### 怎么确定分布参数 $R, L, G, C$? 🔩 (参考书 P49-50 页)

这些参数取决于传输线的几何结构和构成材料的电磁特性 (电导率 $\sigma_c$, 磁导率 $\mu_c$ 对于导体；介电常数 $\epsilon$, 磁导率 $\mu$, 电导率 $\sigma$ 对于介质)。

对于一些常见的传输线结构，有现成的公式可以计算其分布参数：

![](Pic/Fig_17_Distributed_Parameters_Formulas.png)

*   **表3.1 三种传输线的分布参数**:
    *   **平行双导线**:
        *   $R = R_s / (\pi a)$ (这里 $R_s = \sqrt{\pi f \mu_c / \sigma_c}$ 是导体表面电阻，考虑了趋肤效应)
        *   $L = (\mu/\pi) \ln[(D/2a) + \sqrt{(D/2a)^2-1}]$ (忽略内电感)
        *   $G = \pi \sigma / \ln[(D/2a) + \sqrt{(D/2a)^2-1}]$
        *   $C = \pi \epsilon / \ln[(D/2a) + \sqrt{(D/2a)^2-1}]$
        (其中 $D$ 是两导体中心间距，$a$ 是导体半径，$\mu, \sigma, \epsilon$ 是周围介质的参数)
    *   **同轴线**:
        *   $R = (R_s / 2\pi) (1/a + 1/b)$ ($a$ 是内导半径, $b$ 是外导体内半径)
        *   $L = (\mu/2\pi) \ln(b/a)$
        *   $G = 2\pi \sigma / \ln(b/a)$
        *   $C = 2\pi \epsilon / \ln(b/a)$
    *   **平行导体板**:
        *   $R = 2R_s / W$ ($W$ 是板宽)
        *   $L = \mu b / W$ ($b$ 是板间距)
        *   $G = \sigma W / b$
        *   $C = \epsilon W / b$

**注意**: 这些公式是基于特定假设（如导体是良导体，TEM模传播等）推导的。对于更复杂的结构或高频情况，可能需要数值方法（如有限元法）来精确计算。

---

### 3.2.3 传输线的几个重要参数 ✨

我们已经接触到了特性阻抗 $Z_0$ 和传播常数 $\gamma$。它们是描述传输线行为的基石。让我们更深入地理解它们及其引申出的其他重要参数。

#### 1. 特性阻抗 $Z_0$ (Characteristic Impedance)

*   **从哪儿来?**
    $\boxed{ Z_0 = \sqrt{\frac{Z}{Y}} = \sqrt{\frac{R+j\omega L}{G+j\omega C}} \quad \text{(3.18)} }$
*   **有啥意义?**
    *   $Z_0$ 是传输线上**单一方向传播的行波**（无限长传输线，或终端匹配的传输线）的电压与电流之比。
        $\boxed{ Z_0 = \frac{\dot{U}^+(z)}{\dot{I}^+(z)} = -\frac{\dot{U}^-(z)}{\dot{I}^-(z)} \quad (\Omega) \quad \text{(3.34)} }$
    *   它反映了传输线本身固有的阻抗特性，与线的长度无关，仅取决于线的分布参数 $R, L, G, C$ 和工作频率 $\omega$。
    *   如果传输线终端接一个等于其特性阻抗 $Z_0$ 的负载 $Z_L$，那么在负载端就不会产生反射波，所有入射能量都被负载吸收。这种情况称为**阻抗匹配**。
*   **无耗情况下 (Lossless Line: $R=0, G=0$)**:
    此时 $Z_0$ 变为纯实数：
    $\boxed{ Z_c = Z_0 = \sqrt{\frac{j\omega L}{j\omega C}} = \sqrt{\frac{L}{C}} \quad \text{(3.35)} }$
    (通常用 $Z_c$ 表示无耗线的特性阻抗，或有时直接用 $Z_0$ 表示)
*   **以同轴线为例 (无耗)**:
    将 $L = (\mu/2\pi) \ln(b/a)$ 和 $C = 2\pi \epsilon / \ln(b/a)$ 代入 $Z_c = \sqrt{L/C}$：
    $Z_c = \sqrt{\frac{(\mu/2\pi) \ln(b/a)}{2\pi \epsilon / \ln(b/a)}} = \frac{1}{2\pi}\sqrt{\frac{\mu}{\epsilon}}\ln(b/a)$
    对于自由空间或空气介质，$\mu \approx \mu_0$, $\epsilon \approx \epsilon_0$，$\sqrt{\mu_0/\epsilon_0} \approx 120\pi \approx 377 \Omega$ (自由空间波阻抗)。
    则 $Z_c \approx \frac{1}{2\pi} (120\pi \frac{1}{\sqrt{\epsilon_r}}) \ln(b/a) = \frac{60}{\sqrt{\epsilon_r}} \ln(b/a) \quad (\Omega) \quad \text{(3.38)}$
    (这里PPT中假设介质是磁导率为 $\mu_0$ 的非磁性材料，但介电常数为 $\epsilon = \epsilon_0 \epsilon_r$)。
    ![](Pic/Fig_19_Characteristic_Impedance_Coaxial.png)

#### 2. 传播常数 $\gamma$ (Propagation Constant)

*   **从哪儿来?**
    $\boxed{ \gamma = \sqrt{ZY} = \sqrt{(R+j\omega L)(G+j\omega C)} = \alpha + j\beta \quad \text{(3.19)} }$
*   **有啥意义?**
    $\gamma$ 描述了电磁波在传输线上传播时的衰减和相移特性。
    *   **衰减常数 $\alpha$ (Np/m)**: 决定了行波振幅随传播距离指数衰减的快慢 ($e^{-\alpha z}$)。它由传输线的损耗 ($R$ 和 $G$) 引起。
    *   **相移常数 $\beta$ (rad/m)**: 决定了行波相位随传播距离线性变化的快慢 ($\omega t - \beta z$)。
*   **无耗情况下 ($R=0, G=0$)**:
    $\gamma = \sqrt{(j\omega L)(j\omega C)} = \sqrt{-\omega^2 LC} = j\omega\sqrt{LC}$
    此时，衰减常数 $\alpha = 0$ (无衰减)，相移常数 $\beta = \omega\sqrt{LC}$。
    $\boxed{ \gamma = j\beta = j\omega\sqrt{LC} \quad \text{或} \quad \alpha=0, \beta=\omega\sqrt{LC} \quad \text{(3.40)} }$
*   **微波频段近似 (低损耗情况 $R \ll \omega L, G \ll \omega C$)**:
    在高频时，通常 $L$ 和 $C$ 的效应远大于 $R$ 和 $G$ 的损耗效应。此时可以做近似：
    $\boxed{ \beta \approx \omega\sqrt{LC} \quad (\text{rad/m}) \quad \text{(3.42)} }$ (与无耗线相同)
    对于衰减常数 $\alpha$，可以使用二项式展开近似：
    $\gamma = \sqrt{j\omega L (1 + R/j\omega L) \cdot j\omega C (1 + G/j\omega C)}$
    $\gamma = j\omega\sqrt{LC} \sqrt{(1 - jR/\omega L)(1 - jG/\omega C)}$
    $\gamma \approx j\omega\sqrt{LC} [1 - \frac{jR}{2\omega L} - \frac{jG}{2\omega C} + \dots ]$
    $\gamma \approx j\omega\sqrt{LC} + \frac{R}{2}\sqrt{\frac{C}{L}} + \frac{G}{2}\sqrt{\frac{L}{C}}$
    $\gamma \approx j\omega\sqrt{LC} + \frac{R}{2Z_c} + \frac{G Z_c}{2}$ (其中 $Z_c = \sqrt{L/C}$ 是无耗特性阻抗)
    所以，衰减常数近似为：
    $\boxed{ \alpha \approx \frac{1}{2} R Y_c + \frac{1}{2} G Z_c = \frac{R}{2Z_c} + \frac{GZ_c}{2} \quad (\text{Np/m}) \quad \text{(3.43)} }$
    (PPT中 $Y_c = 1/Z_c$)
*   **$\alpha$ 和 $\beta$ 的意义体现在 (3.20) 的瞬时表达式中**:
    $u(z,t) = |\dot{U}^+|e^{-\alpha z} \cos(\omega t - \beta z + \varphi_+) + |\dot{U}^-|e^{\alpha z} \cos(\omega t + \beta z + \varphi_-)$
    这里的 $e^{-\alpha z}$ 和 $e^{\alpha z}$ 就是衰减项，$-\beta z$ 和 $+\beta z$ 就是相移项。
    ![](Pic/Fig_20_Propagation_Constant_Meaning.png)

#### 3. 相速 $v_p$ (Phase Velocity) 与 波长 $\lambda$ (Wavelength)

这些参数描述了波的传播速度和空间周期性，直接由相移常数 $\beta$ 决定。

*   **相速 $v_p$**:
    相速是指波形上某一相位点 (例如波峰) 的传播速度。对于相位项 $\omega t - \beta z = \text{const}$，对其求时间导数：
    $\omega - \beta \frac{dz}{dt} = 0 \Rightarrow v_p = \frac{dz}{dt} = \frac{\omega}{\beta}$
    $\boxed{ v_p = \frac{\omega}{\beta} \quad (\text{m/s}) \quad \text{(3.44)} }$
    对于无耗线或低损耗线，$\beta \approx \omega\sqrt{LC}$，所以 $v_p \approx \frac{\omega}{\omega\sqrt{LC}} = \frac{1}{\sqrt{LC}}$。
    如果传输线填充的是均匀的、理想的（无色散的）介质，其介电常数为 $\epsilon = \epsilon_0 \epsilon_r$ 和磁导率为 $\mu = \mu_0 \mu_r$，并且是TEM模传播（例如同轴线、平行板线），那么 $LC = \mu\epsilon$。
    此时 $v_p = 1/\sqrt{\mu\epsilon} = c/\sqrt{\mu_r\epsilon_r}$，其中 $c=1/\sqrt{\mu_0\epsilon_0}$ 是真空中的光速。
    对于非磁性介质 ($\mu_r=1$)， $v_p = c/\sqrt{\epsilon_r}$。

*   **波长 $\lambda$**:
    波长是指在空间上相位变化 $2\pi$ 所对应的距离，即 $\beta \lambda = 2\pi$。
    $\boxed{ \lambda = \frac{2\pi}{\beta} \quad (\text{m}) \quad \text{(3.45)} }$
    也可以表示为 $\lambda = v_p / f = (2\pi v_p) / \omega$。
    结合 $v_p = \omega/\beta$:
    $\lambda = \frac{2\pi}{\beta} = \frac{v_p}{f} = \frac{c/\sqrt{\epsilon_r}}{f} = \frac{\lambda_0}{\sqrt{\epsilon_r}}$
    其中 $\lambda_0 = c/f$ 是自由空间中的波长。
    ![](Pic/Fig_21_Phase_Velocity_and_Wavelength.png)

---

### 3.2 小结：均匀无耗微波传输线的初印象 🌟

到目前为止，我们已经建立了均匀传输线的基本理论框架。对于理想化的**均匀无耗传输线** ($R=0, G=0$)，我们可以总结出以下几个关键初步印象：

1.  **“长短”是相对的**：是否按传输线处理，取决于线长与信号波长的比值。
2.  **参数是分布的**：$L$ 和 $C$ (无耗时只有这两个) 是沿线分布的。
3.  **其上传输的信号是波 (电压波和电流波)**：电压和电流都满足波动方程。
4.  **既有入射波，又有反射波**：除非终端完美匹配，否则总会有反射波存在。
5.  **入射波的电压和电流比值是常数，叫特性阻抗 ($Z_c = \sqrt{L/C}$，为实数)。反射波的电压和电流比值的相反数也是特性阻抗。**
6.  **传输线中波的传播速度 ($v_p = 1/\sqrt{LC}$) 和传输线的填充介质有关系，真空（或空气）填充时等于光速 $c$ (对于TEM模)。** 波长 $\lambda = v_p/f$。

这些是分析后续更复杂情况（如终端不匹配、输入阻抗、驻波、阻抗匹配等）的基础。

![](Pic/Fig_22_Summary_of_Section_3_2.png)

---
**(接下来的内容是3.3 均匀传输线的输入阻抗和反射特性)**