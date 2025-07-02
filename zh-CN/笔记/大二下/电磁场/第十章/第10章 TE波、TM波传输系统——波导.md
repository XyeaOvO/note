# 第10章 TE波、TM波传输系统——波导

你好！欢迎来到第10章的学习。在本章中，我们将一同探索电磁波在特定结构——**波导**——中的传输行为。波导是一种非常重要的微波传输线，广泛应用于雷达、通信、粒子加速器等高频领域。

与之前学习的TEM波（如在同轴线或平行双导线中传播）不同，中空金属波导（我们本章主要讨论的类型）**不能**支持TEM波的传播。取而代之的是，它们支持 **TE (横电) 波** 和 **TM (横模) 波**。

本章的主要内容将围绕以下两个核心部分展开：

*   **10.1 矩形波导**: 这是最常见和基础的波导形式。我们将详细分析其内部的波动方程、不同模式（TE和TM）的场结构、截止特性以及关键传输参数。
*   **10.2 圆波导 (及光纤简介)**: 虽然PDF主要聚焦矩形波导，但我们会根据PDF内容提及圆波导（并简要关联到光纤的概念，尽管光纤的工作原理更为复杂，通常在专门的光通信课程中详述）。

在开始之前，请确保你对麦克斯韦方程组、波动方程以及基本的电磁场边界条件有较好的理解，这些都是我们本章学习的基石。让我们开始这段奇妙的电磁波导行之旅吧！🚀

---

### 一、矩形波导中的波动方程及其解

我们首先聚焦于**矩形波导**，它是一个具有矩形横截面的中空金属管。

#### 1.1 基本假设与坐标系设定 📐

*   **几何结构**: 考虑一个矩形波导，其横截面尺寸在 $x$ 方向为 $a$，在 $y$ 方向为 $b$。
    *   通常我们假设 $a > b$。
*   **传播方向**: 假设电磁波沿波导的轴向，即 $+z$ 方向传播。
*   **填充介质**: 假设波导内部填充的是**理想介质** (无损耗)，其介电常数为 $\epsilon$，磁导率为 $\mu$。
*   **波导壁**: 波导壁被认为是**理想导体** (PEC, Perfect Electric Conductor)。
![](Pic/Pasted%20image%2020250519114446.png)

#### 1.2 波动方程的分解与简化 🧠

**知识回顾**💡: 在无源自由空间中，电场 $\vec{E}$ 和磁场 $\vec{H}$ 满足波动方程：
$\nabla^2 \vec{E} + k^2 \vec{E} = 0$
$\nabla^2 \vec{H} + k^2 \vec{H} = 0$
其中 $k = \omega \sqrt{\mu\epsilon}$ 是自由空间中的波数（或相移常数）。

*   **场量的时间和空间依赖性**:
    由于我们假设波沿 $+z$ 方向传播，并且是时谐场 (time-harmonic)，所有场分量（如 $E_x, E_y, E_z, H_x, H_y, H_z$）都将包含一个因子 $e^{j\omega t - \gamma z}$。
    *   $\omega$ 是角频率。
    *   $\gamma$ 是传播常数。
    因此，对 $z$ 的偏导数可以简化为：
    $\boxed{ \frac{\partial}{\partial z} = -\gamma }$
    $\boxed{ \frac{\partial^2}{\partial z^2} = \gamma^2 }$
    对于**无损耗介质**，传播常数 $\gamma$ 是纯虚数，即 $\gamma = j\beta$，其中 $\beta$ 是相移常数。因此 $\gamma^2 = (j\beta)^2 = -\beta^2$。

*   **波动方程的分解**:
    $\nabla^2$ 算子可以分解为横向部分 $\nabla_T^2 = \frac{\partial^2}{\partial x^2} + \frac{\partial^2}{\partial y^2}$ 和纵向部分 $\frac{\partial^2}{\partial z^2}$。
    对于任意场分量 $\psi$ (代表 $E_x, E_y, E_z, H_x, H_y, H_z$ 中的任何一个)，波动方程变为：
    $(\nabla_T^2 + \frac{\partial^2}{\partial z^2}) \psi + k^2 \psi = 0$
    代入 $\frac{\partial^2}{\partial z^2} = \gamma^2$，我们得到：
    $\nabla_T^2 \psi + \gamma^2 \psi + k^2 \psi = 0$
    $\boxed{ \nabla_T^2 \psi + (k^2 + \gamma^2) \psi = 0 }$
    或者，如果我们使用 $\gamma = j\beta$ (无损耗情况):
    $\nabla_T^2 \psi + (k^2 - \beta^2) \psi = 0$

*   **引入截止波数 $k_c$**:
    我们定义一个非常重要的量，**截止波数 (cutoff wavenumber)** $k_c$：
    $\boxed{ k_c^2 = k^2 + \gamma^2 }$  (对于有损耗或传播/截止情况通用)
    或者，对于无损耗传播 ($\gamma=j\beta$):
    $\boxed{ k_c^2 = k^2 - \beta^2 }$
    这意味着 $\beta = \sqrt{k^2 - k_c^2}$。
    使用 $k_c$，横向波动方程（也称为亥姆霍兹方程的二维形式）可以统一写成：
    $\boxed{ \nabla_T^2 \psi + k_c^2 \psi = 0 }$
    这个方程对 $E_x, E_y, E_z, H_x, H_y, H_z$ 中的每一个分量都成立。

    **重要理解** ✨:
    *   $k = \omega\sqrt{\mu\epsilon}$ 是波在无界理想介质中传播时的波数。
    *   $k_c$ 是由波导的横截面几何形状和所考虑的模式决定的一个常数。它不依赖于频率 $\omega$（尽管它的值由特定模式在特定边界条件下产生，而模式本身与频率有关才能传播）。
    *   $\beta$ 是波在波导中沿 $z$ 方向传播时的相移常数。
    *   **传播条件**:
        *   如果 $k^2 > k_c^2$ (即 $\omega\sqrt{\mu\epsilon} > k_c$), 则 $\beta^2 > 0$, $\beta$ 为实数，$\gamma = j\beta$。波能够**传播**。
        *   如果 $k^2 < k_c^2$ (即 $\omega\sqrt{\mu\epsilon} < k_c$), 则 $\beta^2 < 0$, $\beta$ 为虚数 ($\beta = -j\alpha'$), $\gamma = \alpha'$ (实数)。波**不能传播**，而是会衰减，这种情况称为**截止 (cutoff)**。
        *   如果 $k^2 = k_c^2$, 则 $\beta = 0$，这是**临界截止状态**。

#### 1.3 横向场分量用纵向场分量表示 🔗

一个关键的简化步骤是：在波导中，所有的**横向场分量** ($E_x, E_y, H_x, H_y$) 都可以通过**纵向场分量** ($E_z, H_z$) 来表示。
推导这些关系需要用到麦克斯韦方程组的旋度方程（以复振幅形式，并代入 $\partial/\partial z = -\gamma$ 和 $\partial/\partial t = j\omega$）：
$\nabla \times \vec{E} = -j\omega\mu \vec{H}$
$\nabla \times \vec{H} = j\omega\epsilon \vec{E}$

展开这些旋度方程为分量形式，经过一系列代数运算（此处省略详细推导，可参考教材），可以得到以下重要关系式 (讲义P7)：
$\boxed{ E_x = -\frac{1}{k_c^2} \left( \gamma \frac{\partial E_z}{\partial x} + j\omega\mu \frac{\partial H_z}{\partial y} \right) }$
$\boxed{ E_y = -\frac{1}{k_c^2} \left( \gamma \frac{\partial E_z}{\partial y} - j\omega\mu \frac{\partial H_z}{\partial x} \right) }$
$\boxed{ H_x = -\frac{1}{k_c^2} \left( -j\omega\epsilon \frac{\partial E_z}{\partial y} + \gamma \frac{\partial H_z}{\partial x} \right) }$
$\boxed{ H_y = -\frac{1}{k_c^2} \left( j\omega\epsilon \frac{\partial E_z}{\partial x} + \gamma \frac{\partial H_z}{\partial y} \right) }$

其中 $k_c^2 = k^2 + \gamma^2 = \omega^2\mu\epsilon + \gamma^2$。

**这些公式的意义** 🤔:
它们告诉我们，只要我们能够求解出纵向分量 $E_z$ 和 $H_z$ (它们都满足二维亥姆霍兹方程 $\nabla_T^2 \psi + k_c^2 \psi = 0$)，我们就可以得到所有的横向场分量。这极大地简化了问题！

基于此，波导中的波可以分为三类：
1.  **TM (Transverse Magnetic) 波**: $H_z = 0$，$E_z \neq 0$。磁场完全在横向平面。
2.  **TE (Transverse Electric) 波**: $E_z = 0$，$H_z \neq 0$。电场完全在横向平面。
3.  **TEM (Transverse Electromagnetic) 波**: $E_z = 0$ 且 $H_z = 0$。电场和磁场都完全在横向平面。
    *   对于中空金属波导（单导体），将 $E_z=0$ 和 $H_z=0$ 代入上述四个公式，会导致 $k_c^2=0$ 才能有非零解。如果 $k_c^2=0$，则 $\gamma^2 = -k^2$，这正是无界介质中的TEM波传播常数。然而，对于有界波导，满足 $k_c=0$ 的边界条件通常无法实现非平凡解。因此，**中空金属波导不能支持TEM波**。

接下来，我们将分别求解TM波和TE波。

#### 1.4 TM 波在矩形波导中的解 🌊 (TM: $H_z=0, E_z \neq 0$)

对于TM波，我们设置 $H_z=0$。我们的任务是求解 $E_z$，它满足：
$\nabla_T^2 E_z + k_c^2 E_z = 0 \implies \frac{\partial^2 E_z}{\partial x^2} + \frac{\partial^2 E_z}{\partial y^2} + k_c^2 E_z = 0$
(注意：这里的 $E_z$ 是指 $E_z(x,y)$ 部分，已分离出 $e^{j\omega t - \gamma z}$ 因子。)

*   **分离变量法**:
    设 $E_z(x,y) = X(x)Y(y)$。代入上式并整理，得到：
    $\frac{1}{X(x)}\frac{d^2X(x)}{dx^2} + \frac{1}{Y(y)}\frac{d^2Y(y)}{dy^2} = -k_c^2$
    令 $\frac{1}{X(x)}\frac{d^2X(x)}{dx^2} = -k_x^2$ 和 $\frac{1}{Y(y)}\frac{d^2Y(y)}{dy^2} = -k_y^2$。
    则 $k_c^2 = k_x^2 + k_y^2$。
    两个常微分方程为：
    $\frac{d^2X(x)}{dx^2} + k_x^2 X(x) = 0 \implies X(x) = A \cos(k_x x) + B \sin(k_x x)$
    $\frac{d^2Y(y)}{dy^2} + k_y^2 Y(y) = 0 \implies Y(y) = C \cos(k_y y) + D \sin(k_y y)$

*   **边界条件 (BCs)**:
    由于波导壁是理想导体，切向电场必须为零。
    1.  $E_z$ 本身就是平行于 $z$ 轴的，它在所有四个壁上（$x=0, x=a, y=0, y=b$）都是切向的。
        *   $E_z(x=0, y) = 0 \implies X(0)Y(y)=0 \implies X(0)=0 \implies A=0$。所以 $X(x) = B \sin(k_x x)$。
        *   $E_z(x, y=0) = 0 \implies X(x)Y(0)=0 \implies Y(0)=0 \implies C=0$。所以 $Y(y) = D \sin(k_y y)$。
        *   $E_z(x=a, y) = 0 \implies B \sin(k_x a) D \sin(k_y y) = 0 \implies \sin(k_x a) = 0$ (为得到非零解)。
            $\boxed{ k_x = \frac{m\pi}{a}, \quad m = 1, 2, 3, \dots }$
        *   $E_z(x, y=b) = 0 \implies B \sin(k_x x) D \sin(k_y b) = 0 \implies \sin(k_y b) = 0$。
            $\boxed{ k_y = \frac{n\pi}{b}, \quad n = 1, 2, 3, \dots }$

    **重要** ❗: 对于TM波， $m$ 和 $n$ 都**不能为零**。如果 $m=0$ 或 $n=0$，则 $k_x=0$ 或 $k_y=0$，导致 $\sin(0)=0$，从而 $E_z \equiv 0$，这不是一个有效的TM模式。因此，TM波的最低阶模式是 TM<sub>11</sub>。

*   **$E_z$ 表达式**:
    $E_z(x,y) = E_0 \sin\left(\frac{m\pi x}{a}\right) \sin\left(\frac{n\pi y}{b}\right)$
    (其中 $E_0 = B \cdot D$ 是幅度常数)。
    完整的 $E_z(x,y,z,t) = E_0 \sin\left(\frac{m\pi x}{a}\right) \sin\left(\frac{n\pi y}{b}\right) e^{j\omega t - \gamma z}$。

*   **截止波数 $k_c$**:
    $\boxed{ k_c^2 = k_x^2 + k_y^2 = \left(\frac{m\pi}{a}\right)^2 + \left(\frac{n\pi}{b}\right)^2 }$
    每对 $(m,n)$ (其中 $m \ge 1, n \ge 1$) 定义了一个特定的 **TM<sub>mn</sub> 模式**。

*   **其他场分量 (TM<sub>mn</sub> 波)**:
    将 $H_z=0$ 和求得的 $E_z$ 代入1.3节中的四个公式即可得到 $E_x, E_y, H_x, H_y$。
    (讲义P12给出了包含 $e^{j\omega t - \beta z}$ 的完整表达式，这里 $\gamma = j\beta$)
    $E_x = -j\frac{\beta}{k_c^2} \left(\frac{m\pi}{a}\right) E_0 \cos\left(\frac{m\pi x}{a}\right) \sin\left(\frac{n\pi y}{b}\right) e^{j\omega t - j\beta z}$
    $E_y = -j\frac{\beta}{k_c^2} \left(\frac{n\pi}{b}\right) E_0 \sin\left(\frac{m\pi x}{a}\right) \cos\left(\frac{n\pi y}{b}\right) e^{j\omega t - j\beta z}$
    $H_x = j\frac{\omega\epsilon}{k_c^2} \left(\frac{n\pi}{b}\right) E_0 \sin\left(\frac{m\pi x}{a}\right) \cos\left(\frac{n\pi y}{b}\right) e^{j\omega t - j\beta z}$
    $H_y = -j\frac{\omega\epsilon}{k_c^2} \left(\frac{m\pi}{a}\right) E_0 \cos\left(\frac{m\pi x}{a}\right) \sin\left(\frac{n\pi y}{b}\right) e^{j\omega t - j\beta z}$
    $H_z = 0$

*   **TM 波传输特点 (讲义P13)**:
    1.  相位仅与 $z$ 有关，振幅与 $x,y$ 有关。在 $z$ 方向是行波，在 $x,y$ 方向是驻波。
    2.  $z=$常数的平面是波面，但振幅在波面上非均匀。TM波是非均匀平面波。
    3.  $m, n$ 必须为非零整数。$m$ 表示沿 $x$ (宽边) 方向的半个驻波的数目，$n$ 表示沿 $y$ (窄边) 方向的半个驻波的数目。
    4.  每对 $(m,n)$ 构成一种模式 (TM<sub>mn</sub>)。最低次模式是 TM<sub>11</sub>。
    5.  数值大的 $m, n$ 模式称为高次模，数值小的称为低次模。

#### 1.5 TE 波在矩形波导中的解 🌬️ (TE: $E_z=0, H_z \neq 0$)

对于TE波，我们设置 $E_z=0$。我们的任务是求解 $H_z$，它也满足：
$\nabla_T^2 H_z + k_c^2 H_z = 0 \implies \frac{\partial^2 H_z}{\partial x^2} + \frac{\partial^2 H_z}{\partial y^2} + k_c^2 H_z = 0$

*   **分离变量法**:
    类似地，设 $H_z(x,y) = X(x)Y(y)$。
    $X(x) = A' \cos(k_x x) + B' \sin(k_x x)$
    $Y(y) = C' \cos(k_y y) + D' \sin(k_y y)$
    且 $k_c^2 = k_x^2 + k_y^2$。

*   **边界条件 (BCs)**:
    $E_z=0$ 已满足。我们需要应用横向电场 $E_x, E_y$ 在导体壁上为零的条件。
    从1.3节的公式，当 $E_z=0$ 时：
    $E_x = -\frac{j\omega\mu}{k_c^2} \frac{\partial H_z}{\partial y}$
    $E_y = \frac{j\omega\mu}{k_c^2} \frac{\partial H_z}{\partial x}$
    1.  在 $x=0, a$ 处，$E_y=0 \implies \frac{\partial H_z}{\partial x} = 0$。
        *   $\frac{\partial H_z}{\partial x}|_{x=0} = 0 \implies X'(0)=0 \implies (-k_x A' \sin(0) + k_x B' \cos(0))Y(y) = 0 \implies k_x B' = 0 \implies B'=0$ (假设 $k_x \neq 0$)。
            所以 $X(x) = A' \cos(k_x x)$。
        *   $\frac{\partial H_z}{\partial x}|_{x=a} = 0 \implies -k_x A' \sin(k_x a) = 0 \implies \sin(k_x a) = 0$。
            $\boxed{ k_x = \frac{m\pi}{a}, \quad m = 0, 1, 2, \dots }$
    2.  在 $y=0, b$ 处，$E_x=0 \implies \frac{\partial H_z}{\partial y} = 0$。
        *   $\frac{\partial H_z}{\partial y}|_{y=0} = 0 \implies Y'(0)=0 \implies D'=0$ (类似推导)。
            所以 $Y(y) = C' \cos(k_y y)$。
        *   $\frac{\partial H_z}{\partial y}|_{y=b} = 0 \implies -k_y C' \sin(k_y b) = 0 \implies \sin(k_y b) = 0$。
            $\boxed{ k_y = \frac{n\pi}{b}, \quad n = 0, 1, 2, \dots }$

    **重要** ❗: 对于TE波， $m$ 和 $n$ **不能同时为零**。如果 $m=0$ 且 $n=0$，则 $k_x=0, k_y=0$，导致 $H_z$ 是一个常数。那么 $\partial H_z/\partial x = 0$ 和 $\partial H_z/\partial y = 0$，这将导致所有横向场 $E_x, E_y, H_x, H_y$ 也为零 (因为 $k_c^2=0$ 时1.3节公式分母为0，需要更仔细分析，但结果是平凡解)。
    因此，至少有一个模式数 $m$ 或 $n$ 必须非零。例如，TE<sub>10</sub> ($m=1, n=0$) 或 TE<sub>01</sub> ($m=0, n=1$) 是允许的。

*   **$H_z$ 表达式**:
    $H_z(x,y) = H_0 \cos\left(\frac{m\pi x}{a}\right) \cos\left(\frac{n\pi y}{b}\right)$
    (其中 $H_0 = A' \cdot C'$ 是幅度常数)。
    完整的 $H_z(x,y,z,t) = H_0 \cos\left(\frac{m\pi x}{a}\right) \cos\left(\frac{n\pi y}{b}\right) e^{j\omega t - \gamma z}$。

*   **截止波数 $k_c$**:
    $\boxed{ k_c^2 = k_x^2 + k_y^2 = \left(\frac{m\pi}{a}\right)^2 + \left(\frac{n\pi}{b}\right)^2 }$
    每对 $(m,n)$ (其中 $m,n$ 不全为零) 定义了一个特定的 **TE<sub>mn</sub> 模式**。

*   **其他场分量 (TE<sub>mn</sub> 波)**:
    将 $E_z=0$ 和求得的 $H_z$ 代入1.3节中的四个公式即可。
    (讲义P15给出了包含 $e^{j\omega t - \beta z}$ 的完整表达式)
    $E_x = j\frac{\omega\mu}{k_c^2} \left(\frac{n\pi}{b}\right) H_0 \cos\left(\frac{m\pi x}{a}\right) \sin\left(\frac{n\pi y}{b}\right) e^{j\omega t - j\beta z}$
    $E_y = -j\frac{\omega\mu}{k_c^2} \left(\frac{m\pi}{a}\right) H_0 \sin\left(\frac{m\pi x}{a}\right) \cos\left(\frac{n\pi y}{b}\right) e^{j\omega t - j\beta z}$
    $H_x = j\frac{\beta}{k_c^2} \left(\frac{m\pi}{a}\right) H_0 \sin\left(\frac{m\pi x}{a}\right) \cos\left(\frac{n\pi y}{b}\right) e^{j\omega t - j\beta z}$
    $H_y = j\frac{\beta}{k_c^2} \left(\frac{n\pi}{b}\right) H_0 \cos\left(\frac{m\pi x}{a}\right) \sin\left(\frac{n\pi y}{b}\right) e^{j\omega t - j\beta z}$
    $E_z = 0$

---

### 二、TE波和TM波的一些关键参量

#### 2.1 模式 (Mode) — 导模 (Guided Mode) 🌟

*   **模式**是指电磁场能量在波导中能够稳定传输的特定场分布形式。每一种TE<sub>mn</sub>或TM<sub>mn</sub>波都代表一种模式。
*   **言外之意**: 电磁场并不能以任意形式或任意频率在波导中稳定传输。只有满足特定条件（频率高于该模式的截止频率）的特定场型才能形成导模。

#### 2.2 截止频率 (Cutoff Frequency, $f_c$) 与截止波长 ($\lambda_c$) 🚦

*   **截止现象**:
    我们之前看到，对于传播 ($\gamma=j\beta$, $\beta$为实数)，需要 $k^2 > k_c^2$。
    其中 $k = \omega\sqrt{\mu\epsilon} = 2\pi f \sqrt{\mu\epsilon} = 2\pi/\lambda$ ($\lambda$ 是工作波长)。
    $k_c = \sqrt{(m\pi/a)^2 + (n\pi/b)^2}$。
    当 $k^2 = k_c^2$ 时，$\beta=0$，波处于临界截止状态。此时的频率称为**截止频率 $f_c$**，对应的波长称为**截止波长 $\lambda_c$**。
    $k_c = 2\pi f_c \sqrt{\mu\epsilon} = 2\pi/\lambda_c$。
    $\boxed{ f_c = \frac{k_c}{2\pi\sqrt{\mu\epsilon}} = \frac{1}{2\pi\sqrt{\mu\epsilon}} \sqrt{\left(\frac{m\pi}{a}\right)^2 + \left(\frac{n\pi}{b}\right)^2} = \frac{v}{2} \sqrt{\left(\frac{m}{a}\right)^2 + \left(\frac{n}{b}\right)^2} }$
    其中 $v=1/\sqrt{\mu\epsilon}$ 是无界介质中的相速。
    $\boxed{ \lambda_c = \frac{2\pi}{k_c} = \frac{2}{\sqrt{(m/a)^2 + (n/b)^2}} }$

*   **传播条件用频率/波长表示**:
    *   波能传播: $f > f_c$ 或 $\lambda < \lambda_c$。
    *   波截止: $f < f_c$ 或 $\lambda > \lambda_c$。
    *   临界截止: $f = f_c$ 或 $\lambda = \lambda_c$。
    **“波导是一种高通滤波器”**：对于一个给定的模式，只有当工作频率高于其截止频率时，该模式才能在波导中传播。

#### 2.3 相移常数 ($\beta$) 与波导波长 ($\lambda_g$) 📏

*   对于传播的模式 ($f > f_c$)，$\gamma = j\beta$。
    $\beta^2 = k^2 - k_c^2 = (\omega\sqrt{\mu\epsilon})^2 - k_c^2$
    $\boxed{ \beta = \sqrt{k^2 - k_c^2} = k \sqrt{1 - (k_c/k)^2} = k \sqrt{1 - (f_c/f)^2} = k \sqrt{1 - (\lambda/\lambda_c)^2} }$
    其中 $k = 2\pi/\lambda$ 是自由空间波数。

*   **波导波长 ($\lambda_g$)**: 指在波导内部，沿 $z$ 方向的场型重复一个周期的距离。
    $\boxed{ \lambda_g = \frac{2\pi}{\beta} = \frac{2\pi}{k \sqrt{1 - (f_c/f)^2}} = \frac{\lambda}{\sqrt{1 - (f_c/f)^2}} = \frac{\lambda}{\sqrt{1 - (\lambda/\lambda_c)^2}} }$
    *   可见 $\lambda_g > \lambda$。波导内的波长比自由空间波长要长。
    *   当 $f \to f_c$, $\lambda_g \to \infty$ (驻波状态)。
    *   当 $f \gg f_c$, $\lambda_g \to \lambda$ (趋近于TEM波行为，但仍不是TEM)。

#### 2.4 相速度 ($v_p$) 与群速度 ($v_g$) 🚗💨

*   **相速度 ($v_p$)**: 波导中等相位面沿 $z$ 方向移动的速度。
    $\boxed{ v_p = \frac{\omega}{\beta} = \frac{\omega}{k \sqrt{1 - (f_c/f)^2}} = \frac{v}{\sqrt{1 - (f_c/f)^2}} = \frac{v}{\sqrt{1 - (\lambda/\lambda_c)^2}} }$
    其中 $v=1/\sqrt{\mu\epsilon}$ 是无界介质中的相速。
    *   可见 $v_p > v$。波导中的相速大于光在对应无界介质中的速度！但这并不违反相对论，因为相速不代表能量或信息的传播速度。
    *   当 $f \to f_c$, $v_p \to \infty$。

*   **群速度 ($v_g$)**: 能量或信息在波导中传播的速度。
    $\boxed{ v_g = \frac{d\omega}{d\beta} }$
    通过对 $\beta = \sqrt{\omega^2\mu\epsilon - k_c^2}$ 求导，可得：
    $\boxed{ v_g = \frac{1}{\sqrt{\mu\epsilon}} \sqrt{1 - (k_c/\omega\sqrt{\mu\epsilon})^2} = v \sqrt{1 - (f_c/f)^2} = v \sqrt{1 - (\lambda/\lambda_c)^2} }$
    *   可见 $v_g < v$。能量传播速度小于光速。
    *   当 $f \to f_c$, $v_g \to 0$。
    *   **重要关系**: $\boxed{ v_p v_g = v^2 }$

*   **色散 (Dispersion)**:
    由于 $v_p$ 和 $v_g$ 都依赖于频率 $f$，说明波导是**色散**传输系统。不同频率的信号分量以不同的速度传播，会导致信号失真。

#### 2.5 波阻抗 ($Z_W$) 💰

波阻抗定义为横向电场与横向磁场之比。对于TE和TM波，其定义略有不同。
假设无损耗介质，$\gamma = j\beta$。
*   **TM 波的波阻抗**: $Z_{TM} = \frac{E_x}{H_y} = -\frac{E_y}{H_x}$
    $\boxed{ Z_{W(TM)} = \frac{\beta}{\omega\epsilon} = \frac{k\sqrt{1-(f_c/f)^2}}{\omega\epsilon} = \eta \sqrt{1-(f_c/f)^2} }$
    其中 $\eta = \sqrt{\mu/\epsilon}$ 是介质的本征阻抗。

*   **TE 波的波阻抗**: $Z_{TE} = \frac{E_x}{H_y} = -\frac{E_y}{H_x}$
    $\boxed{ Z_{W(TE)} = \frac{\omega\mu}{\beta} = \frac{\omega\mu}{k\sqrt{1-(f_c/f)^2}} = \frac{\eta}{\sqrt{1-(f_c/f)^2}} }$

*   **特性**:
    *   $Z_{W(TM)} < \eta$
    *   $Z_{W(TE)} > \eta$
    *   $\boxed{ Z_{W(TM)} Z_{W(TE)} = \eta^2 }$
    *   当 $f \to f_c$: $Z_{W(TM)} \to 0$, $Z_{W(TE)} \to \infty$。

---

### 三、最低次模、主模和单模传输

#### 3.1 最低次模 (Lowest Order Mode) 👇

*   **定义**: 具有**最高截止波长 $\lambda_c$** (或最低截止频率 $f_c$) 的模式称为最低次模。这是在波导中最容易激励和传播的模式。
*   **寻找最低次模**:
    $\lambda_c = \frac{2}{\sqrt{(m/a)^2 + (n/b)^2}}$
    我们需要找到使 $\lambda_c$ 最大的 $(m,n)$ 组合。
    *   **TM 波**: $m \ge 1, n \ge 1$。
        假设 $a>b$ (通常约定)。$\lambda_c$ 最大对应 $(m/a)^2 + (n/b)^2$ 最小。
        最低次TM模是 **TM<sub>11</sub>**。 $\lambda_{c(TM11)} = \frac{2}{\sqrt{(1/a)^2 + (1/b)^2}} = \frac{2ab}{\sqrt{a^2+b^2}}$。
    *   **TE 波**: $m, n$ 不全为零。
        *   TE<sub>10</sub> 模 ($m=1, n=0$): $\lambda_{c(TE10)} = \frac{2}{\sqrt{(1/a)^2 + 0^2}} = 2a$。
        *   TE<sub>01</sub> 模 ($m=0, n=1$): $\lambda_{c(TE01)} = \frac{2}{\sqrt{0^2 + (1/b)^2}} = 2b$。
        *   TE<sub>11</sub> 模 ($m=1, n=1$): $\lambda_{c(TE11)} = \frac{2ab}{\sqrt{a^2+b^2}}$。
    *   **TEM 波**: 前面已述，中空金属波导不能传输TEM波 (可以理解为 $k_c=0 \implies \lambda_c \to \infty$, 但无法满足BCs)。

#### 3.2 主模 (Dominant Mode) 👑

*   **定义**: 在所有可能的TE和TM模式中，具有**最高截止波长 $\lambda_c$** (即最低 $f_c$) 的那个模式称为**主模**。
*   **确定主模**:
    比较所有可能模式的 $\lambda_c$。通常约定 $a>b$。
    *   $\lambda_{c(TE10)} = 2a$
    *   $\lambda_{c(TE01)} = 2b$
    *   $\lambda_{c(TM11)} = \frac{2ab}{\sqrt{a^2+b^2}}$
    由于 $a > b$, 且 $a < \sqrt{a^2+b^2}$, $b < \sqrt{a^2+b^2}$。
    可以证明 $2a > 2b$ 且 $2a > \frac{2ab}{\sqrt{a^2+b^2}}$。
    因此，对于矩形波导（$a>b$），**TE<sub>10</sub> 模是主模**。
    $\boxed{ \text{主模 (Dominant Mode): TE}_{10}, \quad \lambda_c = 2a, \quad f_c = \frac{v}{2a} }$

#### 3.3 单模传输 (Single-Mode Operation) ☝️

*   **概念**: 如果选择的工作频率 $f$ (或工作波长 $\lambda$) 使得只有主模 (TE<sub>10</sub>) 能够传播，而所有其他更高次模都处于截止状态，则称波导工作在**单模传输**状态。
*   **条件**:
    为实现单模传输，工作频率 $f$ 必须满足：
    $f_{c(TE10)} < f < f_{c(\text{next higher mode})}$
    或者用波长表示：
    $\lambda_{c(\text{next higher mode})} < \lambda < \lambda_{c(TE10)}$
*   **次高模式**:
    假设 $a>b$。TE<sub>10</sub> 的 $\lambda_c = 2a$。
    
	为了保证只有 TE<sub>10</sub> 模传播，工作波长 $\lambda$ 必须大于所有其他模式的截止波长中最大的那个（即仅次于 $2a$ 的那个值），并且小于 TE<sub>10</sub> 的截止波长 $2a$。
	这个“其他模式中截止波长最大的”是 $\max(\lambda_{c(TE20)}, \lambda_{c(TE01)}, \lambda_{c(TE11)}, \dots)$。
	我们已经分析过，$\lambda_{c(TE11)}$ 等总是小于 $a$ 和 $2b$。
	所以这个值就是 TE<sub>20</sub> 的 $\lambda_c=a$ 和 TE<sub>01</sub> 的 $\lambda_c=2b$ 中，**较大的那个**。
	*   若 $a > 2b$, 则 $\max(a, 2b) = a$。单模范围是 $a < \lambda < 2a$。
	*   若 $b < a < 2b$, 则 $\max(a, 2b) = 2b$。单模范围是 $2b < \lambda < 2a$。
    通常选择 $a \approx 2b$ (例如 $a=2b$ 附近)。这时 TE<sub>20</sub> ($\lambda_c=a$) 和 TE<sub>01</sub> ($\lambda_c=2b \approx a$) 的截止频率相近。
    对于 $a=2b$ (标准波导常见比例)， $\lambda_{c(TE10)}=2a$, $\lambda_{c(TE20)}=a$, $\lambda_{c(TE01)}=2b=a$。
    此时，单模工作的波长范围是 $a < \lambda < 2a$。
    ![](Pic/Pasted%20image%2020250519131218.png)

#### 3.4 模式简并 (Mode Degeneracy) 👯

*   **定义**: 如果两个或多个不同的模式具有相同的截止频率 (或截止波长)，则称这些模式是**简并的**。
*   **示例**:
    *   若 $a=b$ (方波导)，则 TE<sub>10</sub> ($k_c = \pi/a$) 和 TE<sub>01</sub> ($k_c = \pi/b=\pi/a$) 简并。
    *   TE<sub>mn</sub> 和 TM<sub>mn</sub> (当 $m,n \ge 1$ 时) 通常具有相同的 $k_c = \sqrt{(m\pi/a)^2 + (n\pi/b)^2}$，因此它们是简并的。例如，TE<sub>11</sub> 和 TM<sub>11</sub> 简并。
    简并可能导致模式转换和信号失真，在某些应用中需要避免或利用。
![](Pic/Pasted%20image%2020250519131606.png)

---

### 四、TE<sub>10</sub> 模 (主模) 详解 🌟

由于 TE<sub>10</sub> 是矩形波导 ($a>b$) 的主模，在实际中应用最广，我们来详细分析它。
对于 TE<sub>10</sub> 模，$m=1, n=0$。

#### 4.1 TE<sub>10</sub> 模的场分量 (令 $\gamma=j\beta$)

将 $m=1, n=0$ 代入1.5节的TE波场分量表达式：
*   $k_x = \pi/a$, $k_y = 0$.
*   $k_c = \pi/a$.
*   $H_z(x,y,z,t) = H_0 \cos\left(\frac{\pi x}{a}\right) e^{j\omega t - j\beta z}$
*   $E_x = 0$ (因为 $n=0$)
*   $E_y = -j\frac{\omega\mu}{ (\pi/a)} H_0 \sin\left(\frac{\pi x}{a}\right) e^{j\omega t - j\beta z} = E_{y0} \sin\left(\frac{\pi x}{a}\right) e^{j\omega t - j\beta z}$
    (令 $E_{y0} = -j\frac{\omega\mu a}{\pi} H_0$)
*   $H_x = j\frac{\beta}{(\pi/a)} H_0 \sin\left(\frac{\pi x}{a}\right) e^{j\omega t - j\beta z} = H_{x0} \sin\left(\frac{\pi x}{a}\right) e^{j\omega t - j\beta z}$
    (令 $H_{x0} = j\frac{\beta a}{\pi} H_0$)
*   $H_y = 0$ (因为 $n=0$)
*   $E_z = 0$ (TE波定义)

**TE<sub>10</sub> 模只有三个非零场分量：$E_y, H_x, H_z$**。

$\boxed{ E_y = E_0 \sin\left(\frac{\pi x}{a}\right) e^{j(\omega t - \beta z)} }$
$\boxed{ H_x = -\frac{\beta}{\omega\mu} E_0 \sin\left(\frac{\pi x}{a}\right) e^{j(\omega t - \beta z)} = -\frac{1}{Z_{W(TE10)}} E_0 \sin\left(\frac{\pi x}{a}\right) e^{j(\omega t - \beta z)} }$
$\boxed{ H_z = j\frac{\pi/a}{\omega\mu} E_0 \cos\left(\frac{\pi x}{a}\right) e^{j(\omega t - \beta z)} }$

#### 4.2 TE<sub>10</sub> 模的场分布

*   **电场 $E_y$**:
    *   只在 $y$ 方向有分量。
    *   沿 $x$ 方向按 $\sin(\pi x/a)$ 分布：在 $x=0, x=a$ (侧壁) 处为零，在 $x=a/2$ (波导中心) 处最强。
    *   沿 $y$ 方向均匀分布 (不随 $y$ 变化)。
    *   电场线是平行于 $y$ 轴的直线，从一个宽壁 ($y=b$ 或 $y=0$ 的一个面) 指向另一个宽壁，中间最密。电力线不闭合，起于上壁止于下壁（或反之）。
*   **磁场 ($H_x, H_z$)**:
    *   $H_x$ 沿 $x$ 方向按 $\sin(\pi x/a)$ 分布 (中心强，壁处弱)。
    *   $H_z$ 沿 $x$ 方向按 $\cos(\pi x/a)$ 分布 (壁处强，中心弱)。
    *   磁场线在 $xz$ 平面内形成闭合环路，包围着 $E_y$ 电场线。
*   **电流分布**:
    *   壁电流由 $\vec{J}_s = \hat{n} \times \vec{H}$ 决定。
    *   在宽边 ($y=0, y=b$)，电流主要是纵向 ($z$ 方向) 和横向 ($x$ 方向) 的。
    *   在窄边 ($x=0, x=a$)，电流主要是 $y$ 方向的。

#### 4.3 TE<sub>10</sub> 模的关键参数

*   **截止频率/波长**: ($m=1, n=0$)
    $\boxed{ f_{c(TE10)} = \frac{v}{2a} }$
    $\boxed{ \lambda_{c(TE10)} = 2a }$
*   **相移常数 $\beta$**:
    $\boxed{ \beta = k \sqrt{1 - (f_c/f)^2} = \frac{2\pi}{\lambda} \sqrt{1 - (\lambda/2a)^2} }$
*   **波导波长 $\lambda_g$**:
    $\boxed{ \lambda_g = \frac{\lambda}{\sqrt{1 - (\lambda/2a)^2}} }$
*   **相速度 $v_p$**:
    $\boxed{ v_p = \frac{v}{\sqrt{1 - (\lambda/2a)^2}} }$
*   **群速度 $v_g$**:
    $\boxed{ v_g = v \sqrt{1 - (\lambda/2a)^2} }$
*   **波阻抗 $Z_{W(TE10)}$**:
    $\boxed{ Z_{W(TE10)} = \frac{\eta}{\sqrt{1 - (\lambda/2a)^2}} }$

#### 4.4 矩形波导中的能量传输和损耗

*   **传输功率 P**:
    功率通过坡印亭矢量 $\vec{S} = \frac{1}{2} \text{Re}(\vec{E} \times \vec{H}^*)$ 的面积分得到。
    对于TE<sub>10</sub>模，讲义给出的结果 (经过一些简化和定义) 是：
    $P_{TE10} = \frac{1}{2 Z_{TE}} \int_S |E_y|^2 dS = \dots = \frac{ab}{4 Z_{TE}} (\omega\mu \frac{a}{\pi})^2 H_{zm}^2$ (这里的 $H_{zm}$ 是 $H_z$ 的峰值)
    或者用 $E_y$ 的峰值 $E_0$ 表示：
    $P_{TE10} = \frac{ab}{4} \frac{\beta}{\omega\mu} E_0^2 = \frac{ab}{4 Z_{W(TE10)}} E_0^2$ (使用 $E_y$ 幅值 $E_0$)

*   **损耗**:
    实际波导壁不是理想导体，存在有限电导率 $\sigma_c$，会引起导体损耗。介质也可能有损耗 ($\epsilon = \epsilon' - j\epsilon''$)。这些损耗会导致传播常数 $\gamma = \alpha + j\beta$ 中的衰减常数 $\alpha$ 不为零。详细计算复杂，此处不赘述。

---

### 五、矩形波导知识的扩展——谐振腔

如果将一段波导的两端用理想导体板封起来，就形成了一个**谐振腔 (Resonant Cavity)**。
电磁波在腔内来回反射，当满足特定条件时，会形成驻波，腔内可以存储电磁能量。

*   **TE<sub>10l</sub> 模式**:
    考虑一个长度为 $l$ 的矩形波导，在 $z=0$ 和 $z=l$ 处短路。
    TE<sub>10</sub> 波入射到短路板会发生全反射。入射波和反射波叠加。
    为形成驻波，腔长 $l$ 必须是半个波导波长 $\lambda_g$ 的整数倍：
    $\boxed{ l = p \frac{\lambda_g}{2}, \quad p = 1, 2, 3, \dots }$
    这里的 $p$ 是沿 $z$ 方向的驻波数目。
    这种模式称为 **TE<sub>10p</sub> 模式** (或 TE<sub>mnp</sub> 中的 $m=1, n=0$)。
    其谐振频率由 $l = p \frac{\lambda}{2\sqrt{1-(\lambda/2a)^2}}$ 决定。

---
**小结与展望**:
本章我们详细学习了矩形波导中TE和TM波的分析方法、场结构和重要参数，特别关注了主模TE<sub>10</sub>。这些知识是微波工程和技术的基础。讲义后续可能会涉及圆波导、光纤以及更复杂的波导结构和器件。

希望这份笔记能帮助你更好地理解波导的奥秘！😊