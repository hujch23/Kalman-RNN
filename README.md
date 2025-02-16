# KalmanNet: 基于神经网络的卡尔曼滤波器，用于部分已知动态系统  

KalmanNet 是一种结合经典卡尔曼滤波器（Kalman Filter, KF）和深度学习的混合算法，专为处理部分已知动态系统的实时状态估计问题而设计。它通过引入循环神经网络（RNN）模块，学习卡尔曼增益（Kalman Gain），从而克服非线性和模型失配问题，同时保留了经典卡尔曼滤波器的低复杂度和可解释性。  

---  


## 🔬 1. 


---  
#### 🚀 1.1 Research Background 
- **Problem Definition**: How to achieve efficient state estimation in scenarios with unknown noise statistics, model mismatches, and limited computational resources.  
- **Research Significance**:
  - Traditional filtering methods heavily rely on domain knowledge and system models, limiting performance in complex scenarios.  
  - DNN-enhanced filtering methods provide powerful learning capabilities but with high computational complexity.  
  - Need for a lightweight real-time state estimator that balances performance and efficiency.
- **Challenges**:
  - Handling unknown noise statistics and model mismatches.  
  - Ensuring real-time performance in resource-constrained environments.  
  - Designing compact and efficient neural network architectures.

#### 🛰️ 1.2 Research Methods  


  
#### 🏆 1.3 Experimental Results  
- **Experimental Setup**: Tested in multiple simulation environments (e.g., AI2-THOR, Habitat). 
- **Performance Metrics**:
  - Mean Squared Error (MSE) of state estimation  
  - Computation time and inference latency  
  - Robustness under model mismatch conditions
- **Conclusions**:
  - Outperforms traditional model-based filters in nonlinear and model mismatch conditions  
  - 28.2% faster inference speed compared to KalmanNet while maintaining comparable accuracy  
  - 20.8% reduction in localization error for UAV positioning tasks  
  - Excellent real-time performance in resource-constrained scenarios




