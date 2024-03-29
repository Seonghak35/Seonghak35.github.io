---
layout: post
title: Colloidal Dispersion
date: 2024-01-23
description: 
tags: microfluidics
categories: CFD
giscus_comments: false
related_posts: false
toc:
  sidebar: left
---

## Colloidal Dispersion

콜로이드 분산계 (colloidal dispersion)는 $$10\mu m$$ 이하의 크기를 갖는 고체 입자들이 서로 응집되지 않고 안정한 혼합액을 이뤄 액체 속에 퍼져있는 분산액을 말한다. colloid를 구성하는 고체 미립자는 dispersed phase에 해당하며, 고체 미립자가 분산되어 있는 액체는 dispersion medium이라 한다. 거시적으로 colloidal dispersion은 single phase로 인식되지만, 미시적으로는 multiphase로써 Brownian motion이나 Tyndall effect 와 같은 특성을 나타낸다.

+ Brownian motion: dispersion medium를 구성하는 분자들이 열운동에 의해 입자와 충돌하여 발생하는 colloid 입자의 불규칙한 운동
+ Tyndall effect: dispersion medium에 분산된 colloid에 의한 빛의 산란으로 인해 발생

liquid-liquid 또는 solid-liquid interface를 포함하는 경우에는 수력학적 상호작용력 이외에 colloid 힘을 유발시키며, interface와 입자간의 거리가 매우 짧을 경우에는 수력학적 상호작용력보다 electrostatic force나 분자 수준의 상호작용에 의한 van der Waals force가 매우 커지게 된다. 이러한 Colloid 힘은 유체의 미세구조 형성과 안정성에 많은 영향을 주기 때문에 미세구조 유체의 거동을 해석하기 위해 필수적으로 이해해야한다. 

## Electric Double Layer (EDL)

### Surface Charge

solid wall이 electrolyte solution과 접촉하게 되면 electric charge를 갖게 되며 이는 액상의 electric charge distribution을 비균일하게 만든다. 예를 들어, solid wall가 positive charge를 띠게 된다면, 정전기력에 의해 solid wall 근방에는 negative ion들이 모이게 될것이며 positive ion들은 solid wall에 가까이 접근할 수 없을 것이다. 이에 따라, solution의 electric charge distribution이 비균일해지고, electric potential의 기울기가 발생하여 하전 입자의 거동에 영향을 주게 된다.

### Poisson-Boltzmann Equation

Poisson-Boltzmann equation을 통해 electric charge 및 electric potential distribution의 상관 관계를 결정할 수 있다. 이는 interface 근방을 stern layer와 diffuse layer의 double layer로 고려한다. Stern layer는 interface에 바로 접하고 있는 layer로, solid wall의 electric charge에 반대되는 ion들이 interface와 접촉하고 있으며, 강한 정전기적 인력으로 인하여 ion들이 거의 이동할 수 없다. Diffuse layer로 진입하게 되면, stern layer의 screening으로 인하여 정전기력이 약해져 ion들의 mobility가 비교적 좋아지게 되는데, 여기에서는 ion에 작용하는 힘은 ion의 확산과 관련된 thermal fluctuation과 정전기력이 된다. 

일반적으로 electric charge와 electric potential의 관계는 Maxwell equation으로 규명되지만 자기장이 존재하지 않을 때는 charge density $$\rho_e$$와 electric potential $$\psi$$ 사이의 관계는 linearized Poisson equation으로 표현할 수 있다.

$$
\nabla^2\psi = -\frac{\rho_e}{\epsilon}
$$

여기서, $$\epsilon$$은 solution의 permittivity이며, 이는 진공상태인 경우의 permittivity $$\epsilon_0$$에 relative permittivity $$\epsilon_r$$를 곱한것이다.

Interface를 포함하는 커다란 면으로 둘러싸인 solution 부피에서, Poisson equation에 divergence theorem을 적용하면 다음과 같이, interface에서의 electric potential 기울기와 표면 charge density $$q_s$$와의 관계를 구할 수 있다.

$$
\epsilon\left(\nabla\psi\right)_s\cdot\vec{n}=q_s
$$

여기서 $$\vec{n}$$는 interface에서 solution쪽으로의 수직인 단위 벡터이다.

평형 상태에서의 확산층에서는 확산을 유도하는 힘과 대류를 일으키는 정전기력이 균형을 이룬다. 여기서 확산은 chemical potential의 기울기에 의하여 진행 (ref. Brownian motion)되기 때문에 solution에 포함되어 있는 ion 중에서 valence가 $$z_k$$인 $$k$$ ion의 평형식은 다음과 같다.

$$
-k_bT\nabla\ln{C^k}=ez^k\nabla\psi
$$

여기서, $$C^k$$는 $$k$$ ion의 농도이고, $$e$$는 전자 하나의 전하량이다. solid wall에서 먼 곳에서의 ion 농도가 bulk solution의 농도 $$C^k_\infty$$와 같고, electric potential이 $$\psi_\infty=0$$이라 하면 다음과 같이 식을 풀수 있다.

$$
C^k=C^k_\infty\exp{\left(-\frac{F_ez^k\psi}{RT}\right)}
$$

따라서, 확산층에서의 ion 농도는 Boltzmann distribution $$(\propto\exp{\left(-\frac{e}{kT}\right)})$$을 형성한다. solution이 $$N$$종의 ion을 포함하고 있으면 확산층의 charge density $$\rho_e$$는 다음과 같다.

$$
\rho_e=\sum^N_{k=1}F_ez^kC^k
$$

이를 linearized Poisson equation에 대입하면, 아래와 같은 Poisson-Boltzmann equation을 얻을 수 있으며, 이를 통해 charged surface 근방의 확산층에서의 electric potential distribution을 구할 수 있다.

$$
\epsilon\nabla^2\psi=-F_e\sum^N_{k=1}z^kC^k_\infty\exp{\left(-\frac{F_ez^k\psi}{RT}\right)}
$$

여기에, 표면에서의 electric potential $$\psi=\psi_s$$와 bulk에서의 electrical potential $$\psi=0$$를 적용하면 electrical potential distribution을 결정할 수 있고, 위의 식들을 통해 궁극적으로 표면 charge density $$q_s$$를 구할 수 있다. 

## Electro-osmosis

전기삼투 (electro-osmosis)는 electrical charge를 띠고 있는 solid wall과 접촉하고 있는 electrolyte solution에 electrical potential difference를 걸어주면 전기적 힘에 의해 solution이 흐르게 되는 현상을 말한다. Electro-osmosis는 interface가 electrical charge를 띠고 있을 때만 발생하는 현상인데, 만약 electrical charge가 띠지 않고 있다면 positive ion과 negative ion에 작용하는 전기적 힘이 서로 상쇄되어 흐름이 발생하지 않는다. Electro-osmosis를 활용하면 solid wall에서의 표면 electrical potential또는 $$\zeta$$-potential 같은 electro-kinetic 물성을 측정할 수 있다. 여기서, $$\zeta$$-potential는 stern layer와 diffuse layer의 경계에서 측정된 electrical potential이라 한다.

반지름이 $$a$$인 straight cylindrical 모세관속에 완전히 해리된 solution이 채워져 있고, 모세관 양끝에 설치된 전극을 통하여 electric potential difference를 걸게되면, 모세관 표면은 solution과 접해 있기 때문에 이온화하여 negative ion을 띠게 된다. 축방향 속도를 $$u$$라고 하면 steady state에서 fully developed 한 방향 흐름에서는 $$u=u(r)$$이기 때문에 연속방정식이 만족하게 된다. 또한, 전기장에 의하여 유체의 unit volume이 받는 힘은 charge density와 전기장의 세기 (i.e., electrical potential 기울기)의 곱으로 표현되기 때문에 Naiver-Stokes equation의 $$z$$-방향 성분은 다음과 같이 쓸 수 있다.

$$
0=\frac{1}{r}\frac{\partial}{\partial r}\left(\mu r\frac{\partial u}{\partial r}\right)-\rho_e\frac{\partial}{\partial z}\left(\phi + \psi\right)
$$

여기서 monovalent symmetric solution이기 때문에, charge density $$\rho_e$$는 다음과 같이 표현될 수 있으며,

$$
\begin{aligned}
\rho_e&=\sum^N_{k=1}F_ez^kC^k \\
&=F_e\left(z^+C^+ - z^-C^-\right),
\end{aligned}
$$

$$\phi$$는 외부에서 전극을 통하여 걸어준 electric potential이고 (i.e., $$\phi=\phi(z)$$), $$\psi$$는 관표면 electric charge에 의하여 형성된 EDL potential이다 (i.e., $$\psi=\psi(r)$$).  또한, solution의 viscosity $$\mu$$가 온도에 따라 변하므로, 이는 관내 위치의 함수 $$\mu=\mu(r)$$로 표현될 수 있다. 여기서, charge density $$\rho_e$$는 EDL potential $$\psi$$와 linearized Poisson equation를 만족하기 때문에 다음과 같이 표현할 수 있다.

$$
\begin{aligned}
\frac{1}{r}\frac{\partial}{\partial r}\left(\mu r\frac{\partial u}{\partial r}\right)&=\rho_e\frac{\partial}{\partial z}\left(\phi + \psi\right)\\
&=\epsilon\frac{1}{r}\frac{\partial}{\partial r}\left(r\frac{\partial\psi}{\partial r}\right)E^\infty
\end{aligned}
$$

여기서, $$E^\infty=\left(\partial\phi/\partial z\right)$$는 외부에서 전극을 통하여 걸어준 전기장의 세기이다. 이를 풀면 다음과 같이 전개할 수 있다.

$$
u(r)=-\frac{\epsilon \zeta E^\infty}{\mu(r)}\left[1-\frac{\psi(r)}{\zeta}\right]
$$

Poisson-Boltzmann equation으로부터 $$\psi$$를 구해 적용하게 되면, electro-osmosis 흐름의 속도 분포인 $$u(r)$$를 계산할 수 있다. 다만, 여기서 solution의 viscosity가 온도의 함수이기 때문에 완전한 속도 분포를 얻기 위해서는 energy equation을 풀어서 온도 분포와 이에 따른 viscosity 분포를 구해야하지만, 일반적으로 모세관은 매우 가늘어서 부피에 비하여 표면적이 매우 넓기 때문에 전기저항으로 발생한 열이 관 밖으로 쉽게 전달되므로 viscosity을 일정하다고 생각해도 타당하다. 따라서, 일정한 viscosity에 대해서 유체의 평균 속도 $$\left<u\right>$$는 다음과 같다.

$$
\left<u\right>=-\frac{\epsilon \zeta E^\infty}{\mu}\left[1-\frac{2}{\zeta a^2}\int_0^a\psi r dr \right]
$$


## Electrophoresis

전기영동 (electrophoresis)는 electric charge를 갖고 있는 입자가 전기장에 의하여 이동하는 화학현상이다. 

### Electric Field Disturbances

Electrophoresis에서는 외부에서 전기장을 걸어주기 때문에 입자는 힘을 받게 된다. 전기장에서 입자가 받는 힘을 구하기 위해서는 입자에 의해 교란된 전기장을 결정해야 한다. 전하 밀도가 균일하여 순 전하농도가 $$\rho_e=0$$인 유체 속에 존재하는 입자를 고려할때, 유체와 입자 내부의 electrical potential $$\phi, \tilde{\phi}$$는 모두 Laplace equation에 의해 다음과 같다.

$$
\nabla^2\phi = 0, \quad \nabla^2\tilde{\phi}=0
$$

입자가 균일한 미교란 전기장 $$E^{\infty}_i$$에 놓여 있다고 하면, 무한히 먼 곳에서의 electrical potential은 다음의 조건을 만족한다.

$$
\phi=-E^\infty_i x_i,\quad\text{for}\quad r\rightarrow\infty
$$

또한, 입자 표면 $$\partial D$$에서는 electrical potential과 current가 연속이기 때문에 다음의 조건을 만족한다.

$$
\phi = \tilde{\psi}
$$

$$
\chi n_i \frac{\partial \phi}{\partial x_i}=\tilde{\chi}n_i\frac{\partial\tilde{\phi}}{\partial x_i}
$$

여기서, $$\chi, \tilde{\chi}$$는 유체와 입자의 전기 전도도로서 전기 저항의 역수이다. 위의 식들을 풀게 되면 임의의 모양을 가진 입자에 입자에 의하여 교란되는 electric potential를 계산할 수 있으며, 이 때 표면에 형성되는 표면 charge density $$q_s$$는 다음과 같다.

$$
\epsilon n_i \frac{\partial \phi}{\partial x_i}-\tilde{\epsilon} n_i \frac{\partial\tilde{\phi}}{\partial x_i}=-q_s
$$

### Electrophoresis Velocity

반경이 $$a$$인 구가 외부에서 걸어준 전기장에 의하여 이동할 때 전기장에 의하여 받는 힘과 구의 electrophoresis velocity를 구하는 방법은 다음과 같다. 구 근방에는 외부 전기장에 의하여 유도되는 electric potential $$\phi$$외에 표면 electrical charge에 의하여 존재하는 EDL potential $$\psi$$이 존재하기 때문에 구 근방에 형성되는 electrical potential distribution은 $$\phi + \psi$$가 된다. charge density $$\rho_e$$인 유체의 운동은 연속방정식과 비균일 Stokes equation을 만족하기 때문에 다음과 같다.

$$
\nabla P=\mu\nabla^2\vec{u}+\vec{f}
$$

여기서, $$\vec{f}=-\rho_e\nabla\left(\phi+\psi\right)$$이며, 전기장 속에 분포하는 전하에 의한 유체의 교란은 유체 속에 점힘 $$\vec{f}$$이 분포하고 있을 때 유체가 점힘들에 의하여 교란되는 것과 동일함을 의미한다. Stokes 흐름의 일반해를 활용하면 임의의 점 $${\xi}$$에서의 속도는 다음과 같다.

$$
u_i=\frac{1}{8\pi \mu}\int_D\left[\frac{\delta_{ij}}{R}+\frac{(\xi_i-x_i)(\xi_j-x_j)}{R^3}\right]f_idV
$$

여기서 $$R=\vert \vec{\xi}-\vec{x} \vert$$를 의미하며, $$\vec{x}$$는 점힘의 위치벡터이고, 적분은 점힘이 분포하고 있는 공간 전체에 대한 것이다. 이를 통해, 구의 중심에서의 미교란 속도 $$(u_i)_0$$와 $$(\nabla^2u_i)_0$$는 다음과 같다.

$$
(u_i)_0=\frac{1}{8\pi \mu}\int_D\left[\frac{\delta_{ij}}{r}+\frac{x_ix_j}{r^3}\right]f_jdV
$$

$$
(\nabla^2u_i)_0=-\frac{1}{4\pi \mu}\int_D\left[-\frac{\delta_{ij}}{r^3}+\frac{3x_ix_j}{r^5}\right]f_jdV
$$

따라서, 구에 작용하는 힘은 다음과 같다.

$$
F_i=6\pi\epsilon\zeta E^\infty_ia\left[1-5a^5\int^\infty _a\frac{\psi/\zeta}{r^6}dr + 2a^3\int_a^\infty\frac{\psi/\zeta}{r^4}dr\right]
$$

여기서, EDL potential $$\psi$$ distribution을 이용하면 구에 작용하는 힘을 구할 수 있다. 계산의 편의성을 위해 매우 낮은 electrical potential의 경우, 아래와 같은 Debye-Huckel 가정을 적용하면,

$$
\tilde{\zeta}=\frac{F_ez\zeta}{RT}\ll1
$$

$$\psi$$는 다음과 같이 구할 수 있다.

$$
\psi=\frac{\zeta a}{r}\exp{\left[-\frac{(r-a)}{\lambda_D}\right]}
$$

여기서, $$\lambda_D$$는 Debye length라고 하며, EDL의 두께에 대한 특성길이로, 아래와 같이 정의된다.

$$
\lambda_D\equiv\sqrt\frac{\epsilon RT}{2F^2_ez^2C_\infty}
$$

위의 $$\psi$$를 통해, 구에 작용하는 힘을 결정할 수 있으며, 여기에 Stokes law를 적용하여 전기장 $$E_i$$속에서 구가 이동하는 속도인 electrophoresis velocity를 구하면 다음과 같다.

$$
\begin{aligned}
U_i=\frac{2}{3}\frac{\epsilon\zeta E^\infty _i}{\mu}\left[1+\frac{1}{16\chi^2}-\frac{5}{48\chi^3}-\frac{1}{96\chi^4}+\frac{1}{96\chi^5}-\frac{e^{-\chi}}{8\chi^4}\left(1-\frac{1}{12\chi^2}\right)\int^\infty _{1/\chi}\frac{e^{-s}}{s}ds\right]
\end{aligned}
$$
