**1. Project Overview and Objectives**

The objective of this project was to design and simulate a high-fidelity Battery-Operated DC Drive system for an electric vehicle using MATLAB/Simulink and Simscape Electrical. The project focused on creating a robust closed-loop control system capable of regulating vehicle speed according to a reference input while overcoming physical constraints such as inertia, aerodynamic drag, and road incline.

**2. System Architecture**

The model is structured into three primary domains:
**Electrical Power Stage**

At the heart of the propulsion system is a DC Motor driven by a PWM-controlled H-Bridge. This configuration allows for precise control over the average voltage supplied to the motor terminals. To ensure the model could reach a target speed of 20 m/s (72 km/h), the battery and H-Bridge were configured with a high-voltage reference (300V+) to counteract the motor's Back EMF at high RPMs

**Control and Modulation**

The Longitudinal Driver block acts as the central controller, simulating the behavior of a human driver or an automated cruise control system. It utilizes a Proportional-Integral (PI) control law to minimize the error between the Reference Velocity ($V_{ref}$) and the Feedback Speed ($V_{fdbk}$) from the vehicle. Through iterative tuning, the gains were optimized to $K_p = 100$ and $K_i = 7$ to ensure rapid response times.

**Mechanical Vehicle Dynamics**

The Vehicle Body subsystem incorporates the physical characteristics of a standard sedan, including a 1000 kg mass. The subsystem was designed to handle multi-variable inputs, specifically:Grade Angle: Accounting for gravity-induced resistance on inclines.Wind Speed: Simulating aerodynamic drag effects on the chassis.

**3. Technical Challenges and Iterative Troubleshooting**

The development process involved several critical troubleshooting phases that refined the model’s accuracy:

**Numerical Stability and Convergence:**

Initial simulations faced "failed to converge" and "linear algebra" errors. These were resolved by correctly implementing Electrical Reference points (grounding) for both the PWM and H-Bridge circuits, ensuring the solver had a $0V$ reference for all nodes.

**Velocity Directionality:**

A recurring issue involved the Distance block reporting negative values. Investigation revealed that the motor's electrical polarity was reversed relative to the vehicle's forward axis. Swapping the H-Bridge output terminals corrected the velocity vector, ensuring distance was calculated as a positive integral of speed.

**Control System Tuning:**

The initial $K_p$ and $K_i$ values led to a sluggish response where the vehicle could not reach its target within the simulation timeframe. Increasing the gains significantly improved acceleration but introduced overshoot. This was mitigated by adjusting damping coefficients and removing unnecessary feed-forward gains ($K_{ff}$), resulting in a stable steady-state response.

**4. Final Results and Conclusion**

The finalized simulation demonstrates a highly reliable electric vehicle drive. This project successfully demonstrates the integration of power electronics, control theory, and mechanical physics, providing a solid foundation for future work on Regenerative Braking or State of Charge (SOC) estimation.
