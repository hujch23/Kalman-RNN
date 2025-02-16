# 🧸 Kalman + RNN 

## 🌟 0. Overview
By introducing Recurrent Neural Network (RNN) modules to learn the Kalman Gain, it overcomes nonlinearity and model mismatch problems while maintaining the low complexity and interpretability of the classic Kalman filter.

---  


## 🔬 1. 

🙌 Official implementation of ICML 2025 under-review paper " "

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
- **Experimental Setup**:
  - Evaluation on linear, nonlinear, and chaotic systems.  
  - Tasks include kinematic state estimation, chaotic Lorenz system tracking, and UAV localization.  
  - Comparison with KalmanNet, EKF, UKF, and PF methods. 
- **Performance Metrics**:
  - Mean Squared Error (MSE) of state estimation.  
  - Computation time and inference latency.  
  - Robustness under model mismatch conditions.
- **Conclusions**:
  - Outperforms traditional model-based filters in nonlinear and model mismatch conditions.  
  - 28.2% faster inference speed compared to KalmanNet while maintaining comparable accuracy.  
  - 20.8% reduction in localization error for UAV positioning tasks.  
  - Excellent real-time performance in resource-constrained scenarios.




