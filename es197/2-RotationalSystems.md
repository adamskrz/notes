# Lecture 2 - Rotational Mechanical Systems

## Key variables

Two basic variables are used to describe the dynamic
behaviour of roatational mechanical systems:

| Variable                      | Unit                         |
| ----------------------------- | ---------------------------- |
| Torque, $\tau(t)$             | Newton Metres ($Nm$)         |
| Angular velocity, $\omega(t)$ | radians/second ($rads^{-1}$) |
| Displacement, $\theta(t)$     | radians ($rad$)              |

## Key Elements

- Inertia (Rotational mass)
  - stores kinetic energy and potential energy
  - reversible
- Rotational Spring
  - stores potential energy (by twisting)
  - reversible
- Rotational Damper
  - dissipates energy as heat
  - non reversible

## Element Equations

### Mass

$$J\frac{d^2}{dt^2}\theta(t) = \tau(t)$$
$$J\frac{d}{dt}\omega(t) = \tau(t)$$
J (units $kgm^2$)

#### Kinetic energy stored

$$W_k(t) = \frac{1}{2}J\omega^2(t)$$
