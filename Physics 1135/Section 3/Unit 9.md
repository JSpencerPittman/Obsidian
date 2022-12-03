### Angular measurement in radians
$$\Large\theta\text{ (in radians) = s/r}$$
> $s$ is an arc of a circle of radius $r$
> Complete Circle: $s = 2\pi r$ and $\theta = 2\pi$

### Angular kinematic vectors
Position: $\theta$ 
Angular Displacement: $\Delta\theta = \theta_f-\theta_i$
Angular VelocityL $\omega_z=\frac{d\theta}{dt}$

Angular velocity vector **Perpendicular** to the plane of rotation
Found with the right hand thumb rule

### Angular Kinematics
$$\Large\begin{align}
\theta &= \theta_0+\omega_{0z}t+\frac{1}{2}\alpha_zt^2\\
\omega_z&=\omega_{0z}+\alpha_zt\\
\omega_z^2&=\omega_{0z}^2+2\alpha_z(\theta-\theta_0)
\end{align}$$
### Relationship between angular and linear motion
Linear velocity is tangential to the circular path
$$\Large v=\frac{ds}{dt}=\frac{d}{dt}(r\theta)=r\frac{d\theta}{dt}=r\omega_z$$
Therefore $$\Large v = \omega r$$

Logically it follows that tangential acceleration can be described as
$$\Large a_{tan}=\alpha r$$
Radial acceleration is
$$\Large a_{rad}=\frac{v^2}{r}=\omega^2r$$
Angular speed $\omega$ is the same for all points of a rigid rotating body

### Rolling without slipping
Here $CM$ will be center of mass
The velocity of any point on the rim can be described as $v_{rim}=\omega R$
The $v_{bottom}$ must be 0
So if we superimpose $v_{cm}$ and $v_{rim}$ then we get
$$\Large v_{cm}=\omega r$$
### Rotational kinetic energy
$$\Large\begin{align}K_{rotation}=\sum\frac{1}{2}m_nv_n^2=\sum\frac{1}{2}m_n(\omega_nr_n)^2\\
=\sum\frac{1}{2}m_n(\omega r_n)^2=\frac{1}{2}[\sum m_nr_n^2]\omega^2\end{align}$$
Member $\omega$ is the same for all points on a rigid body
$$\Large K_{rot}=\frac{1}{2}I\omega^2$$
Where $I$ is the moment of intertia
$$\Large I=\sum_nm_nr_n^2$$
### Properties of the moment of inertia
1. Moment of inertia $I$ depends upon the axis of rotation. Different $I$ for different axes of same object
2. The more mass is farther from the axis of rotation, the greater the moment of inertia
3. It doesn't matter where mass is along the rotational axis, only radial distance $r_n$ from the axis counts

### Parallel axis theorem
$$\Large I_q=I_{cm||q}+Md^2$$
We can use the knowledge of an axis of rotation through the center of mass to find an axis that is parallel to it but not through the center of mass