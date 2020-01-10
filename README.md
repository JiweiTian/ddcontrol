# Data-Driven Control
The design of the controller are based entirely on experimental data collected from the plant.

## Simple Example
```python
from ddc import PIDContoller, PIDTuner
from time import time

start, end = 4.0, 8.0 #Tuning start time[sec], Tuning end time[sec]
ref = 50.0 #Reference value for controller
kp, kd, ki, nn = 0.0, 0.0, 0.0, 0.0 #Initial PID gains
amp = 1.0, init_freq=1.0 #Identification sin amplitude, Initial freq for identificaion sin

pid = PIDController(kp, ki, kd, nn)
tuner = PIDTuner(pid, amp, init_freq)

timer_start = time()
while True:
    timer = time() - timer_start
    if timer>start and timer<end:
        u_cont = tuner.update(ref, y_meas, tune=True)
    else:
        u_cont = tuner.update(ref, y_meas, tune=True)
    y_meas = 0.0 ## Apply the control signal to plant and measure the output signal of plant
```

## PID controller
PID contoller
A proportional–integral–derivative controller (PID controller or three-term controller)
is a control loop mechanism employing feedback that is widely used inindustrial control systems
and a variety of other applications requiring continuously modulated control.::

```python
class ddc.PIDController(kp, ki, kd, nn, lmin=-inf, lmax=+inf):
```
<img src="https://latex.codecogs.com/gif.latex?u&space;=&space;K_p&space;e(t)&space;&plus;&space;K_i&space;\int_{0}^{t}&space;e(t)&space;&plus;&space;\delta(t)" title="u = K_p e(t) + K_i \int_{0}^{t} e(t) + \delta(t)" />
<img src="https://latex.codecogs.com/gif.latex?\delta(t)&space;=&space;N&space;(K_d&space;e(t)-\int_{0}^{t}&space;\delta(t))" title="\delta(t) = N (K_d e(t)-\int_{0}^{t} \delta(t))" />

## Roadmap
- Real time PID controller tuning
- Real time frequency response analysis
- Implementation of state observer
