# KalmanNet: 基于神经网络的卡尔曼滤波器，用于部分已知动态系统  

KalmanNet 是一种结合经典卡尔曼滤波器（Kalman Filter, KF）和深度学习的混合算法，专为处理部分已知动态系统的实时状态估计问题而设计。它通过引入循环神经网络（RNN）模块，学习卡尔曼增益（Kalman Gain），从而克服非线性和模型失配问题，同时保留了经典卡尔曼滤波器的低复杂度和可解释性。  

---  


## 🔬 1. Model-free

🙌 Official implementation of IEEE Robotics and Automation Letters accepted paper ["A New Representation of Universal Successor Features for Enhancing the Generalization of Target-driven Visual Navigation"](https://ieeexplore.ieee.org/document/10623277)

---  
#### 🚀 1.1 Research Background 
- **Problem Definition**: How to achieve efficient state estimation in scenarios with unknown noise statistics, model mismatches, and limited computational resources.  
- **Research Significance**:
  - Traditional filtering methods heavily rely on domain knowledge and system models, limiting performance in complex scenarios  
  - DNN-enhanced filtering methods provide powerful learning capabilities but with high computational complexity  
  - Need for a lightweight real-time state estimator that balances performance and efficiency
- **Challenges**:
  - Handling unknown noise statistics and model mismatches.  
  - Ensuring real-time performance in resource-constrained environments.  
  - Designing compact and efficient neural network architectures.

#### 🛰️ 1.2 Research Methods  
- The framework incorporates Successor Features into the A3C architecture.（Derived from cognitive science principles, SF emulates neural mechanisms for constructing reusable predictive maps. This approach achieves reward-dynamics decomposition, facilitating rapid policy adaptation to reward modifications and enabling the acquisition of transferable environmental dynamics representations across task distributions.）📝 中文翻译：将SF与A3C算法结合。SF源自认知科学领域，模拟大脑如何创建可重用的预测地图。将奖励和环境动态解耦，使得策略可以快速适应奖励变化，能够学习多个任务之间可迁移的环境动态表征。
- Implementation of state-feature-based prediction mechanisms to establish parsimonious dynamics models in latent space for SF estimation. 📝 中文翻译：使用状态特征预测SF来创建潜在的简约动力学模型。
- Acquisition of compact rule sets within the latent state manifold to optimize successor feature prediction and extraction, enhancing the model's representational capacity.📝 中文翻译：在潜在状态中学习规则集，有助于预测和获取后继特征。

![Example Image](Train/figs/SF.jpg)  
  
#### 🏆 1.3 Experimental Results  
- **Datasets**: Tested in multiple simulation environments (e.g., AI2-THOR, Habitat). 
- **Performance Metrics**:
  - Success Rate (SR)
  - Success weighted by Path Length (SPL)
  - Continuous Learning Performance 
- **Conclusions**:
  - Achieving state-of-the-art performance in the generalization of target, scenarios, and domains.
  - Demonstrating strong resistance to catastrophic forgetting in continual learning.


## 核心特点  

1. **混合架构**：结合模型驱动（Model-Based, MB）和数据驱动（Data-Driven, DD）方法的优势。  
2. **低复杂度**：无需矩阵求逆，计算开销小，适合资源受限设备。  
3. **高鲁棒性**：能够处理非线性动力学和模型失配问题。  
4. **数据高效**：通过结合部分领域知识，减少对大规模数据的依赖。  
5. **可解释性**：保留了卡尔曼滤波器的结构化流程，提供中间特征的物理意义。  



## 算法流程  

### 1. 状态空间模型  
KalmanNet 适用于离散时间状态空间模型，定义如下：  
- **状态转移方程**：
 x(t) = f(x(t-1)) + w(t), w(t) ~ N(0, Q)

- **观测方程**：
 y(t) = h(x(t)) + v(t), v(t) ~ N(0, R)

其中：  
- x(t)：系统的隐藏状态向量  
- y(t)：观测向量  
- f(·)：状态转移函数（可能是非线性）  
- h(·)：观测函数（可能是非线性）  
- w(t)、v(t)：分别为过程噪声和观测噪声  

### 2. KalmanNet 的高层架构  
KalmanNet 的核心思想是通过 RNN 学习卡尔曼增益 K(t)，并将其集成到卡尔曼滤波器的流程中：  

1. **预测步骤**：  
 - 预测当前状态：  
   ```  
   x̂(t|t-1) = f(x̂(t-1|t-1))  
   ```  
 - 预测当前观测：  
   ```  
   ŷ(t|t-1) = h(x̂(t|t-1))  
   ```  

2. **更新步骤**：  
 - 使用 RNN 学习的 K(t) 更新状态估计：  
   ```  
   x̂(t|t) = x̂(t|t-1) + K(t)·(y(t) - ŷ(t|t-1))  
   ```  

### 3. 输入特征  
为了学习 K(t)，RNN 使用以下特征作为输入：  

- **观测差分**：Δỹ(t) = y(t) - y(t-1)  
- **新息项**：Δy(t) = y(t) - ŷ(t|t-1)  
- **状态更新差分**：Δx̂(t) = x̂(t|t) - x̂(t|t-1)  

### 4. 网络架构  
KalmanNet 的内部 RNN 使用 GRU（门控循环单元）实现，具体架构包括：  
- 输入层：处理输入特征  
- GRU 层：隐式跟踪统计信息  
- 输出层：生成卡尔曼增益 K(t)

---  

## 实验与结果  

### 1. 实验设置  
- **数据集**：  
  - 合成数据：线性和非线性状态空间模型。  
  - 实际数据：Michigan NCLT 数据集。  
- **对比方法**：  
  - 经典滤波器：KF、EKF、UKF、PF。  
  - 数据驱动方法：端到端 RNN。  

### 2. 实验结果  
1. **线性模型**：  
   - KalmanNet 在已知和部分已知模型下均能达到或接近 KF 的最优性能。  
   - 相较于端到端 RNN，KalmanNet 收敛更快，泛化能力更强。  
2. **非线性模型**：  
   - 在混沌 Lorenz 系统和非线性观测模型下，KalmanNet 显著优于 EKF、UKF 和 PF。  
   - KalmanNet 能够学习并适应模型失配，表现出更强的鲁棒性。  
3. **实际应用**：  
   - 在 Michigan NCLT 数据集中，KalmanNet 成功实现了基于噪声里程计数据的实时定位，显著优于 KF 和端到端 RNN。  

---  

## 优势  

1. **低复杂度**：无需矩阵求逆，计算复杂度低，适合资源受限设备。  
2. **鲁棒性**：能够处理非线性动力学和模型失配问题。  
3. **数据效率**：结合领域知识，减少对大规模数据的依赖。  
4. **可解释性**：保留了卡尔曼滤波器的结构化流程，提供了中间特征的物理意义。  




