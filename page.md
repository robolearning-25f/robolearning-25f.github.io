## HDMI-DP: Humanoid Loco-Manipulation with Direct Perception

### Overview

**HDMI-DP** investigates humanoid loco-manipulation under a *direct perception* paradigm, where task-relevant states—such as object contact points and relative motion—are inferred directly from onboard visual observations, without reliance on motion-capture systems or privileged simulator states.
By integrating perception-driven contact estimation with humanoid control, HDMI-DP enables robust manipulation in visually rich and unstructured environments.

Our approach demonstrates that perception-based pipelines can effectively replace traditional MoCap-dependent setups, while maintaining competitive performance on standard humanoid loco-manipulation tasks.

---

### Authors

**Yutian Chen**, **Hao-Tang Tsui**, **Hang Xu**, **Pang-Chi Lo**, **Yu-Rou Tuan**, **Jiting Cai**
Carnegie Mellon University

Contact:

* [yutianch@andrew.cmu.edu](mailto:yutianch@andrew.cmu.edu)
* [henrytsu@andrew.cmu.edu](mailto:henrytsu@andrew.cmu.edu)
* [wx2@andrew.cmu.edu](mailto:wx2@andrew.cmu.edu)
* [pangchil@andrew.cmu.edu](mailto:pangchil@andrew.cmu.edu)
* [yurout@andrew.cmu.edu](mailto:yurout@andrew.cmu.edu)
* [jitingc@andrew.cmu.edu](mailto:jitingc@andrew.cmu.edu)

---

### Key Idea

<p align="center">
  <img src="overall.gif" width="80%">
</p>

**Direct perception enables humanoid loco-manipulation without motion capture.**
Instead of relying on ground-truth object poses or contact states, HDMI-DP estimates task-critical signals directly from egocentric camera observations and learned perception modules, enabling deployment in environments where external sensing infrastructure is unavailable.

---

### Method

#### Direct Perception Pipeline

Given egocentric RGB observations, the perception module predicts:

* 2D contact point locations in image space,
* Corresponding 3D contact positions via depth and camera geometry,
* Relative object motion for downstream control and state estimation.

These signals are consumed directly by the humanoid controller, forming a closed-loop perception–action pipeline.

---

### Experiments

#### Quantitative Evaluation

We evaluate perception accuracy under different camera fields of view (FOVs), measuring both image-space and 3D contact errors.

```latex
\begin{table}[t]
    \centering
    \caption{Perception and odometry errors under different camera FOVs.}
    \begin{tabular}{c|cc|cc}
        \toprule
        \multirow{2}{*}{FOV} &
        \multicolumn{2}{c|}{Perception error} &
        \multicolumn{2}{c}{Odometry error} \\
        \cmidrule(lr){2-3}\cmidrule(lr){4-5}
        & 3D distance [cm] ($\downarrow$)
        & 2D error [px] ($\downarrow$)
        & $t_{rel}$ [cm/frame] & $r_{rel}$ [deg/frame] \\
        \midrule
        69.2° 
            & $0.384 \,\pm\, 0.175$
            & $0.272 \,\pm\, 0.171$
            & -- & -- \\
        120°
            & -- & -- & -- & -- \\
        \bottomrule
    \end{tabular}
\end{table}
```

---

#### Perception-Driven Control in Simulation

We evaluate HDMI-DP on standard humanoid manipulation tasks using only perception-based inputs.

| Task      | Egocentric View  | 3D Visualization |
| --------- | ---------------- | ---------------- |
| Push Box  | push_box_2d.gif  | push_box_3d.gif  |
| Push Door | push_door_2d.gif | push_door_3d.gif |

---

#### Error Analysis

We visualize temporal error profiles for contact estimation during task execution:

* **2D contact error (pixels)**: `push_box_2d_error.png`
* **3D contact error (centimeters)**: `push_box_3d_error.png`

These plots highlight stable perception performance over long-horizon interactions.

---

### Perception Proxy

<p align="center">
  <img src="cartpole.gif" width="60%">
</p>

To further validate generality, we introduce a **perception proxy** setting, where simplified environments (e.g., cart-pole–like dynamics) are used to study perception–control coupling in isolation.
This allows controlled analysis of error propagation from visual perception to downstream control.

---

### Summary

HDMI-DP demonstrates that:

* Humanoid loco-manipulation can be achieved using *direct visual perception* alone,
* Motion-capture systems and privileged simulator states are not strictly necessary,
* Perception-driven pipelines generalize across manipulation tasks and camera configurations.

This work supports a shift toward perception-centric humanoid systems that operate robustly in realistic, uninstrumented environments.
