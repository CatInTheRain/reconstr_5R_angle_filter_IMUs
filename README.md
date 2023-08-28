# Reconstruction of kinematic angles of 5R manipulator with 2 IMUs

In this project two different sensors systems have been read to reconstruct the pose of a serial manipulator through the implementation of motion tracking algorithm. The purpose is to compare the result of the algorithm executed on data provided by IMUs to the angles measurements of the potentiometers, which are a valid reference for the comparison.

The serial manipulator consists of 5 revolute joints and it represents the model of a human arm.
![Manipolatore_Mio](https://github.com/CatInTheRain/reconstr_5R_angle_filter_IMUs/assets/55113554/2475cd96-c6d1-44cc-8fe0-73307cf6424f)

The two sensor systems are:
- Five potentiometers WH148-1A-2 single turn wire wound.
- Two IMU MPU9250.

The readings are managed by STM32 Nucleo-144 development board with STM32F767ZIT6 MCU.
![foto1](https://github.com/CatInTheRain/reconstr_5R_angle_filter_IMUs/assets/55113554/f027bbd1-8e6c-402e-a52c-a4c037b79d9f)

Potentiometers measurements will test the precision of the IMU algorithm to estimate the manipulator pose.
Data must be time signed and it must be read on Simulink to be stored and analyzed. The next step is a signal processing to increase accuracy and eliminate unwanted offsets from sensors. Then the algorithm implemented on Simulink
will be embedded on the microcontroller. The final results of the two sensor systems will be displayed on Simulink, while the code for sensors reading and the motion tracking algorithm are executed on the microcontroller.

## Motion Tracking Algorithm
A basic method for the reconstruction of an arbitrary kinematic chain is described below. The Figure 41 briefly represents the reconstruction method that it consists of two parts: the first is filltration of gravitation and magnetic
field measurements by a Kalman fillter; the second is the TRIAD algorithm for estimation of the rotation matrix, respect to a reference system.
![schema](https://github.com/CatInTheRain/reconstr_5R_angle_filter_IMUs/assets/55113554/1e09cfb6-471b-4cc5-8b84-b88f1cf8e053)

Kalman filter applied on the time-variant dynamic model can rejecti linear accelerations in the case of acceleration spikes. In the experiment performed below, the sensor was moved repeatedly in the Z-direction with linear acceleration components not negligible with respect to the gravitational contribution. Although the accelerometer registers the sum of the two acceleration contributions, the model does not notice the sudden variations because the axes of the gyroscope record low angular velocities (in the case of only linear acceleration components, in addition to the gravitational contribution)
![reject](https://github.com/CatInTheRain/reconstr_5R_angle_filter_IMUs/assets/55113554/32807fc2-c9d2-452b-924a-6090c47315d9)


The complete report and code are available and can be requested in private.

## Bibliography
- [1] A. Filippeschi, N. Schmitz, M. Miezal, G. Bleser, E. Ruffaldi, and D. Stricker, "Survey of motion tracking methods based on inertial sensors: A focus on upper limb human motion," Sensors, vol. 17, no. 6, p. 1257, 2017.
- [2] R. Zhu and Z. Zhou, "A real-time articulated human motion tracking using tri-axis inertial/magnetic sensors package," IEEE Transactions on Neural systems and rehabilitation engineering, vol. 12, no. 2, pp. 295-302, 2004.
- [3] M. D. Shuster and S. D. Oh, "Three-axis attitude determination from vector observations," Journal of guidance and Control, vol. 4, no. 1, pp. 70-77, 1981.
