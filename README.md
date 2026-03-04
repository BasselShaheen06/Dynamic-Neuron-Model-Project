# Izhikevich Neuron Simulation: Numerical & PINN Solvers
### Biomedical Engineering | Numerical Analysis | Physics-Informed Deep Learning

This repository implements and evaluates multiple computational approaches to solving the **Izhikevich model**, a system of two non-linear Ordinary Differential Equations (ODEs) that simulate spiking neuron behavior. We compare classical numerical integration against **Physics-Informed Neural Networks (PINNs)** to analyze stability, accuracy, and computational performance.

---

## 🔬 Mathematical Framework
The model approximates neural excitability through two coupled equations:

$$\frac{dv}{dt} = 0.04v^2 + 5v + 140 - u + I$$
$$\frac{du}{dt} = a(bv - u)$$

Where **$v$** represents membrane potential and **$u$** represents the recovery variable. Upon reaching the peak threshold ($v \geq 30$ mV), the variables are reset: $v \leftarrow c$ and $u \leftarrow u + d$.

### Solvers & Methodology
We evaluated five distinct methods to address the system's non-linearity:

* **Midpoint Runge-Kutta (RK2):** Our primary benchmark; it provided the best balance of local truncation error and processing speed.
* **Explicit & Backward Euler:** Used to analyze the trade-off between computational simplicity and numerical stability in "stiff" regions.
* **ExpRESS-Euler:** An exponential integrator specifically implemented to handle sharp biological transitions.
* **PINNs (Physics-Informed Neural Networks):** A deep learning approach using **PyTorch** where the loss function is constrained by the ODE residuals, allowing the model to learn the physics of the neuron without traditional time-stepping.

---

## 📈 Benchmarking Results
Based on the results detailed in the [Technical Report](DNM_Report.pdf):

* **Numerical Stability:** While Implicit methods (Backward Euler) showed superior stability, they struggled to capture the sharp, discontinuous resets characteristic of the Izhikevich model.
* **PINN Performance:** The neural network successfully captured recovery dynamics ($u$), but showed a "smoothing" effect on high-frequency voltage peaks ($v$) compared to RK2.
* **Real-time Visualization:** An interactive **Unity** interface was developed to allow for live parameter tuning ($a, b, c, d$), enabling immediate observation of transitions between spiking regimes (e.g., Tonic Spiking vs. Chattering).



---

## 📁 Repository Structure
| Module | Contents |
| :--- | :--- |
| `Explicit_Euler_method/` | Implementation of baseline explicit integration. |
| `Backward_Euler_method.py` | Robust implicit solver for stable integration. |
| `Midpoint_(RK2)_method/` | Second-order Runge-Kutta implementation. |
| `adaptive_exponential/` | Advanced stiff solver (Rosenbrock method). |
| `DL_PINN_model/` | PyTorch implementation of the Physics-Informed model. |
| `unity/` | C# scripts and assets for the 3D interactive viewer. |

---

## 🚀 Execution
### Requirements
* Python 3.8+
* `numpy`, `torch`, `matplotlib`, `scipy`
* Unity (for interactive visuals)

### Running Solvers
```bash
# Clone the repository
git clone [https://github.com/MohamedBadawy19/Dynamic-Neuron-Model-Project.git](https://github.com/MohamedBadawy19/Dynamic-Neuron-Model-Project.git)
cd Dynamic-Neuron-Model-Project

# Run a numerical method (Example: RK2)
cd "Midpoint_(RK2)_method"
python simulate_rk2.py

# Train the PINN model
cd ../DL_PINN_model
python train_pinn.py

👨‍💻 Contributors
Developed by Bassel Shaheen, Mohamed Badawy, Kareem Taha, Engy Wael, Alaa Essam, Amat Al-Rahman, Ahmed Salem, Karim Hassan, Omar Gamal, Omar Amein, Ahmed AbdelMoety

📄 License: This project is licensed under the MIT License.
