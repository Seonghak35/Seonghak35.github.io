---
layout: post
title: Mathematical Derivations and Basic Analytical Models of Two-Phase Flow (1)
date: 2024-01-14
description: This is based on the Two-phase flow heat transfer book.
tags: multiphase_flow
categories: CFD
giscus_comments: false
related_posts: false
toc:
  sidebar: left
---

## Two-Phase Flow

Two-phase flow는 density와 viscous가 다른 2개의 유체가 함께 흐르는 것이기 때문에 각 phase간의 상대운동이 혼합 유동에 미치는 영향을 추가로 고려해야 한다. 즉, two-phase 흐름에서는 단위 체적당 기체 (or 액체)가 액체 (or 기체)에서 어떻게 분산되어 흐르는가에 따라 관내에서 발생하는 마찰저항 (or 압력강화)과 각 상간의 열 및 물질전달량이 변화하게 된다.


### Analytical Models

이를 수학적으로 표현하기 위해, 기체와 액체의 속도가 같고, 평균 density와 평균 viscosity를 가정하는 *homogeneous flow model*과 기체와 액체의 서로 다른 속도를 반영하고, 2상간의 상호작용을 유동조건에 연결시키는 *separated flow model*, 그리고 평균유동과 이에 대한 각 상의 상대 유동을 기술하는 *drift flux model*등이 제안되었다. 기술한 방법들은 거시적인 관점에서 다루기 때문에, 많은 부분을 경험에 의존하게 된다. 반면, 미시적 관점의 모델로는 flow pattern model이 있으며, 이는 특정 flow pattern에 대해 한정적으로 적용된다. 이는 거시적 관점에서 본 모델들과 비교해서 더 정확하지만, flow pattern을 미리 예측해야한다는 단점이 있다. 

미시적 관점을 임의의 flow pattern에 일반화하게 되면, instantaneous conservation equation (local instantaneous equations)을 유도할 수 있으며, 적절한 averaging process를 거치면 two-fluid model, separated flow model, or homogeneous flow model등 을 유도할 수 있다 (but, averaging process를 거치게되면 수식을 간단화할 수는 있지만, 유동에 대한 중요 정보를 잃어버릴 수 있기 때문에 이를 반영하는 constitutive relation을 구해야할 필요가 있다). 또한, continuous phase는 Eulerain관점에서, dispersed phase는 Lagrangian관전에서 다루는 Eulerain-Lagrangian model을 유도할 수 있다.

## Integral Balance Relations

각 phase의 내부는 단상유동와 유사하게 differential equation 형태의 보존방정식을 유도할 수 있지만, interface에서는 density와 viscosity가 discontinuity하기 때문에 적절한 jump condition을 설정해야한다. 각 phase의 보존방정식과 jump condition으로부터 Local Instantaneous Equation을 유도할 수 있다.

### Mass Balance Relation

고정된 임의 형태의 control volume에 대해서, 액체가 차지하는 체적과 표면적을 각각 $$V_{\ell}(t), a_{\ell}(t)$$, 기체가 차지하는 체적과 표면적을 각각 $$V_{g}(t), a_{g}(t)$$, 그리고 기체와 액체간의 경계면적을 $$a_{i}(t)$$라고 하면, mass balance relation은 다음과 같다.

$$
\begin{aligned}
  & \frac{d}{d t} \int_{V_{\ell}(t)}^{} \rho_{\ell} d V+\frac{d}{d t} \int_{V_g(t)}^{} \rho_g d V \\
  & +\int_{a_{\ell}(t)}^{} \rho_{\ell}\left(\vec{u}_{\ell} \cdot \vec{n}_{\ell}\right) d a+\int_{a_g(t)}^{} \rho_g\left(\vec{u}_g \cdot \vec{n}_g\right) d a \\
  & =0
\end{aligned}

$$

여기서, 

$$
\frac{d}{d t} \int_{V_{\ell}(t)}^{} \rho_{\ell} d V+\frac{d}{d t} \int_{V_g(t)}^{} \rho_g d V
$$

는 control volume내의 시간에 대한 질량의 변화량이며,

$$
\int_{a_{\ell}(t)}^{} \rho_{\ell}\left(\vec{u}_{\ell} \cdot \vec{n}_{\ell}\right) d a+\int_{a_g(t)}^{} \rho_g\left(\vec{u}_g \cdot \vec{n}_g\right) d a
$$

는 control volume의 surface를 통한 질량의 순수 유입량이다.

### Momentum Balance Relation

동일하게, Momentum balance relation은 다음과 같이 표현할 수 있다.

$$
\begin{aligned}
  & \frac{d}{d t} \int_{V_{\ell}(t)} \rho_{\ell} \vec{u}_{\ell} d V+\frac{d}{d t} \int_{V_g(t)} \rho_g \vec{u}_{g} d V \\
  & +\int_{a_{\ell}(t)} \rho_{\ell} \vec{u}_{\ell} \left(\vec{u}_{\ell} \cdot \vec{n}_{\ell}\right) d a +\int_{a_g(t)} \rho_g \vec{u}_{g} \left(\vec{u}_g \cdot \vec{n}_g\right) d a \\ 
  & =\int_{V_{\ell}(t)} \rho_{\ell}\vec{F} dV + \int_{V_{g}(t)} \rho_{g}\vec{F} dV \\
  & + \int_{a_{\ell}(t)} \vec{n}_{\ell}\cdot\vec{T}_{\ell} da + \int_{a_{g}(t)} \vec{n}_{g}\cdot\vec{T}_{g} da
\end{aligned}
$$

여기서, 

$$
\frac{d}{d t} \int_{V_{\ell}(t)} \rho_{\ell} \vec{u}_{\ell} d V+\frac{d}{d t} \int_{V_g(t)} \rho_g \vec{u}_{g} d V
$$

는 control volume내의 시간에 대한 운동량의 변화량이고, 

$$
\int_{a_{\ell}(t)} \rho_{\ell} \vec{u}_{\ell} \left(\vec{u}_{\ell} \cdot \vec{n}_{\ell}\right) d a+\int_{a_g(t)} \rho_g \vec{u}_{g} \left(\vec{u}_g \cdot \vec{n}_g\right) d a
$$

는 control volume의 surface를 통한 운동량의 순수 유입량이며,

$$
\begin{aligned}
& \int_{V_{\ell}(t)} \rho_{\ell}\vec{F} dV + \int_{V_{g}(t)} \rho_{g}\vec{F} dV \\
& + \int_{a_{\ell}(t)} \vec{n}_{\ell}\cdot\vec{T}_{\ell} da + \int_{a_{g}(t)} \vec{n}_{g}\cdot\vec{T}_{g} da
\end{aligned}

$$

는 control volume에 작용하는 체적력 (e.g., 중력)과 surface에 작용하는 표면력 (e.g., 압력, 전단력)을 의미한다. 여기서, 표면장력에 의한 momentum 변화는 고려하지 않았다.

### Energy Balance Relation

또한, energy balance relation은 다음과 같다.

$$
\begin{aligned}
& \frac{d}{d t} \int_{V_{\ell}(t)} \rho_{\ell} E_{\ell} d V+\frac{d}{d t} \int_{V_g(t)} \rho_g E_{g} d V \\
& +\int_{a_{\ell}(t)} \rho_{\ell} E_{\ell} \left(\vec{u}_{\ell} \cdot \vec{n}_{\ell}\right) d a+\int_{a_g(t)} \rho_g E_{g} \left(\vec{u}_g \cdot \vec{n}_g\right) d a \\
& =\int_{V_{\ell}(t)} \rho_{\ell}\vec{F}\cdot \vec{u}_{\ell} dV + \int_{V_{g}(t)} \rho_{g}\vec{F}\cdot \vec{u}_{g} dV \\
& + \int_{a_{\ell}(t)} \vec{n}_{\ell}\cdot\left(\vec{T}_{\ell}\cdot \vec{u}_{\ell}\right) da + \int_{a_{g}(t)} \vec{n}_{g}\cdot\left(\vec{T}_{g}\cdot \vec{u}_{g}\right) da  \\
& - \int_{a_{\ell}(t)} \vec{q}_{\ell}\cdot \vec{n}_{\ell} da - \int_{a_{g}(t)} \vec{q}_g\cdot \vec{n}_{g} da
\end{aligned}
$$

여기서, $$E_{k}=\frac{1}{2}u_{k}^2+e_{k}$$, $$(k=\ell, g)$$이다.

$$
\frac{d}{d t} \int_{V_{\ell}(t)} \rho_{\ell} E_{\ell} d V+\frac{d}{d t} \int_{V_g(t)} \rho_g E_{g} d V
$$

는 control volume내의 시간에 대한 총에너지 변화량이고,

$$
\int_{a_{\ell}(t)} \rho_{\ell} E_{\ell} \left(\vec{u}_{\ell} \cdot \vec{n}_{\ell}\right) d a+\int_{a_g(t)} \rho_g E_{g} \left(\vec{u}_g \cdot \vec{n}_g\right) d a
$$

는 control volume의 surface를 통한 총에너지의 순수 유입량이다. 또한,

$$
\int_{V_{\ell}(t)} \rho_{\ell}\vec{F}\cdot \vec{u}_{\ell} dV + \int_{V_{g}(t)} \rho_{g}\vec{F}\cdot \vec{u}_{g} dV
$$

는 체적력에 의한 power이고,

$$
\int_{a_{\ell}(t)} \vec{n}_{\ell}\cdot\left(\vec{T}_{\ell}\cdot \vec{u}_{\ell}\right) da + \int_{a_{g}(t)} \vec{n}_{g}\cdot\left(\vec{T}_{g}\cdot \vec{u}_{g}\right) da
$$

는 표면력에 의한 power를 나타내며,

$$
\int_{a_{\ell}(t)} \vec{q}_{\ell}\cdot \vec{n}_{\ell} da + \int_{a_{g}(t)} \vec{q}_g\cdot \vec{n}_{g} da
$$

는 표면적을 통해 전달되는 열전달량이다.

### Entropy Balance Relation

마지막으로, entropy balance relation은 다음과 같다.

$$
\begin{aligned}
& \frac{d}{d t} \int_{V_{\ell}(t)} \rho_{\ell} s_{\ell} d V+\frac{d}{d t} \int_{V_g(t)} \rho_g s_{g} d V\\
& +\int_{a_{\ell}(t)} \rho_{\ell} s_{\ell} \left(\vec{u}_{\ell} \cdot \vec{n}_{\ell}\right) d a+\int_{a_g(t)} \rho_g s_{g} \left(\vec{u}_g \cdot \vec{n}_g\right) d a \\
& + \int_{a_\ell(t)}\frac{1}{T_\ell}\left(\vec{q}_{\ell}\cdot \vec{n}_{\ell}\right)da + \int_{a_g(t)}\frac{1}{T_g}\left(\vec{q}_{g}\cdot \vec{n}_{g}\right)da \\
& = \int_{V_\ell(t)}\Delta_\ell dV + \int_{V_g(t)}\Delta_g dV+\int_{a_i(t)}\Delta_ida \ge0
\end{aligned}
$$

여기서, 

$$
\frac{d}{d t} \int_{V_{\ell}(t)} \rho_{\ell} s_{\ell} d V+\frac{d}{d t} \int_{V_g(t)} \rho_g s_{g} d V
$$

는 control volume내의 시간에 대한 엔트로피 변화량이고,

$$
\int_{a_{\ell}(t)} \rho_{\ell} s_{\ell} \left(\vec{u}_{\ell} \cdot \vec{n}_{\ell}\right) d a+\int_{a_g(t)} \rho_g s_{g} \left(\vec{u}_g \cdot \vec{n}_g\right) d a
$$

는 control volume의 surface를 통한 엔트로피의 순수 유입량을 나타내며,


$$
\int_{a_\ell(t)}\frac{1}{T_\ell}\left(\vec{q}_{\ell}\cdot \vec{n}_{\ell}\right)da + \int_{a_g(t)}\frac{1}{T_g}\left(\vec{q}_{g}\cdot \vec{n}_{g}\right)da
$$

는 표면을 통해 전달되는 열전도에 의한 엔트로피 변화량이다. 또한, $$\Delta_\ell, \Delta_g$$ 및 $$\Delta_i$$는 각각 단위체적당 엔트로피 생성량 및 경계면에서의 단위면적당 엔트로피 생성량을 의미한다. Entropy relation은 열역학 제2법칙에 따라 항상 0보다 크다.

### Generalization

위의 식들을 모두 내포하는 generalized 적분형태의 보존관계식은 다음과 같다.

$$
\begin{aligned}
& \sum_{k=\ell, g} \frac{d}{d t} \int_{V_k(t)} \rho_k \psi_k d V+\sum_{k=\ell, g} \int_{a_k(t)} \rho_k \psi_k\left(\vec{u}_k \cdot \vec{n}_k\right) d a \\
& =\sum_{k=\ell, g} \int_{V_k(t)} \rho_k \phi_k d V+\sum_{k=\ell, g} \int_{a_k(t)} \vec{n}_k \cdot \vec{J}_k d a+\int_{a_i(t)} \phi_i d a \\
&
\end{aligned}
$$

여기서, $$\psi_k, \vec{J}_{k}, \phi_k, \phi_i$$는 각각 다음과 같이 표현할 수 있다.


| Balance relation | $$\psi_k$$       | $$\phi_k$$ | $$\vec{J}_k$$      |  $$\phi_i$$      | 
| -----------      | ------------     | ------------     | ------------ | ------------ |
| Mass             | 1                | 0                  | 0              | 0              |
| Momentum         | $$\vec{u}_k$$    | $$\vec{F}$$ | $$\vec{T}_k$$ | 0 |
| Total Energy     | $$E_k$$          | $$\vec{F}\cdot\vec{u}_k$$ | $$\vec{T}_k\cdot\vec{u}_k - \vec{q}_{k}$$ | 0 |
| Entropy          | $$s_k$$          | $${\Delta_k}/{\rho_k}$$ | $$-{\vec{q}_k}/{T_k}$$ | $$\Delta_i$$ |

<br/>

## Local Instantaneous Equations

Generalized 적분형태의 보존관계식에 Leibniz rule과 Gauss theorem을 적용하면 다음과 같이 된다.

$$
\begin{aligned}
& \sum_{k=\ell, g}\int_{V_\ell(t)}\left[ \frac{\partial}{\partial t}\left(\rho_k\psi_k\right) + \nabla\cdot\left(\rho_k\psi_k\vec{u}_k\right) - \nabla\cdot\vec{J}_k - \rho_k\phi_k \right]dV \\
&- \int_{a_i(t)}\left[\sum_{k=\ell,g}\left(\dot{m}_k\psi_k-\vec{n}_k\cdot\vec{J}_k\right) +\phi_i\right]da=0
\end{aligned}
$$

여기서, $$\dot{m}_k\equiv\rho_k\left(\vec{u}_k-\vec{u}_i\right)\cdot\vec{n}_k$$ 는 interface를 통한 단위면적당 물질전달량 (i.e., evaporation, condensation)을 의미한다. 본 식은 임의의 control volume과 interface에 대해서 항상 성립해야하기 때문에 적분내의 항들도 각각 0이어야 한다. 따라서,

$$
\frac{\partial}{\partial t}\left(\rho_k\psi_k\right) + \nabla\cdot\left(\rho_k\psi_k\vec{u}_k\right) - \nabla\cdot\vec{J}_k - \rho_k\phi_k = 0
$$

$$
\sum_{k=\ell,g}\left(\dot{m}_k\psi_k-\vec{n}_k\cdot\vec{J}_k\right) +\phi_i=0
$$

여기서, 위 식을 local instantaneous equation이라 하고, 아래 식을 local instantaneous jump condition이라 한다.

### Local Instantaneous Equations
#### Continuity Equation

$$
\frac{\partial\rho_k}{\partial t}+\nabla\cdot\left(\rho_k\vec{u}_k\right) = 0
$$

#### Momentum Equation

$$
\frac{\partial\left(\rho_k\vec{u}_k\right)}{\partial t}+\nabla\cdot\left(\rho_k \vec{u}_k\vec{u}_k\right)-\rho_k\vec{F}-\nabla\cdot\vec{T}_k=0
$$

#### Energy Equation

$$
\frac{\partial\left(\rho_kE_k\right)}{\partial t}+\nabla\cdot\left(\rho_kE_k\vec{u}_k\right)-\rho_k\vec{F}\cdot\vec{u}_k-\nabla\cdot\left(\vec{T}_k\cdot\vec{u}_k\right)+\nabla\cdot\vec{q}_k=0
$$

#### Entropy Inequality

$$
\frac{\partial\left(\rho_ks_k\right)}{\partial t}+\nabla\cdot\left(\rho_ks_k\vec{u}_k\right)+\nabla\cdot\frac{\vec{q}_k}{T_k}=\Delta_k\ge0
$$

위의 기술된 식들은 단상 유동에서 나타나는 보존방정식들의 형태와 동일하다.

### Local Instantaneous Jump Condition

#### Mass Jump Condition

$$
\dot{m}_\ell + \dot{m}_g = 0
$$

이를 풀어서 적으면 다음과 같다.

$$
\rho_\ell(\vec{u}_\ell-\vec{u}_i)\cdot\vec{n}_\ell + \rho_g(\vec{u}_g-\vec{u}_i)\cdot\vec{n}_g = 0
$$

##### Momentum Jump Condition

$$
\dot{m}_\ell\vec{u}_\ell-\vec{n}_\ell\cdot\vec{T}_\ell + 
\dot{m}_g\vec{u}_g-\vec{n}_g\cdot\vec{T}_g=0
$$

여기에, mass jump condition을 활용하면 다음과 같이 된다.

$$
\dot{m}_\ell\left(\vec{u}_\ell - \vec{u}_g\right)-\vec{n}_\ell\cdot\vec{T}_\ell-\vec{n}_g\cdot\vec{T}_g=0
$$

여기서, 기체-액체 2상유동의 interface에서 발생하는 표면장력의 영향을 고려하면 다음과 같아진다.

$$
\dot{m}_\ell\left(\vec{u}_\ell - \vec{u}_g\right)-\vec{n}_\ell\cdot\vec{T}_\ell-\vec{n}_g\cdot\vec{T}_g
+ S_\text{st}=0
$$

$$
S_\text{st}=\left(\vec{t}_\alpha A^{\alpha\beta}\sigma\right)_{,\beta}
$$

여기서, 만약 직교좌표계 $$y^k$$ 상에서 $$(u^1, u^2)$$로 정의되는 surface의 한 점이 $$y^{k}=y^k(u^1, u^2)$$로 주어진다고 하면, surface metric tensor, $$A^{\alpha \beta}$$는 다음과 같이 표현된다.

$$
A^{\alpha \beta} = \sum^3_{k=1}\frac{\partial y^k}{\partial u^\alpha}\frac{\partial y^k}{\partial u^\beta}
$$

또한, 공간과 표면사이의 hybrid tensor, $$\vec{t}_{\alpha}$$는 general space coordinate, $$x^i$$에서 표현되는 surface position, $$x^i=x^i(u^1, u^2)$$를 활용하여 다음과 같이 정의된다.

$$
t^i_{\alpha}=\frac{\partial x^i}{\partial u^{\alpha}}
$$

그리고, $$()_{,\beta}$$는 space derivative와 유사하지만, curved coordinates effects도 고려하는 covariance surface derivative를 나타내며, $$\sigma$$는 isotropic surface tension을 의미한다.

[Reference about surface tension term](https://link.springer.com/chapter/10.1007/978-0-387-29187-1_9) (pp.28-34)

##### Energy Jump Condition

$$
\dot{m}_\ell E_\ell - \vec{n}_\ell\cdot \left(\vec{T}_\ell\cdot \vec{u}_\ell-\vec{q}_\ell\right) +
\dot{m}_g E_g - \vec{n}_g\cdot \left(\vec{T}_g\cdot \vec{u}_g-\vec{q}_g\right)=0
$$

여기서도, 기체-액체 interface에서의 표면장력 영향을 고려하기 위해서는 다음과 같이 추가적인 term이 필요하다.

$$
\dot{m}_\ell E_\ell - \vec{n}_\ell\cdot \left(\vec{T}_\ell\cdot \vec{u}_\ell-\vec{q}_\ell\right) +
\dot{m}_g E_g - \vec{n}_g\cdot \left(\vec{T}_g\cdot \vec{u}_g-\vec{q}_g\right) + S_\text{st}=0
$$

$$
S_\text{st} = T_i\left[\frac{d_s}{dt}\left(\frac{d\sigma}{dT_i}\right)+\left(\frac{d\sigma}{dT_i}\right)\nabla_s\cdot\vec{u}_i\right]+\left(\vec{t}_\alpha A^{\alpha\beta}\sigma\right)_{,\beta}\cdot\vec{u}_i
$$

여기서, surface tension는 interface 온도의 함수, $$\sigma=\sigma(T_i)$$이며 $$\frac{d_s}{dt}, \nabla_s$$는 interface coordinates에 대한 미분값들이다.

##### Interface Entropy Inequality

$$
\dot{m}_{\ell}s_{\ell}+\vec{n}_{\ell}\cdot\frac{\vec{q}_\ell}{T_\ell}+
\dot{m}_{g}s_{g}+\vec{n}_{g}\cdot\frac{\vec{q}_g}{T_g}+\Delta_i=0
$$

이는 다음과 같이 표현할 수 있다.

$$
\Delta_i = -\dot{m}_{\ell}s_{\ell}-\vec{n}_{\ell}\cdot\frac{\vec{q}_\ell}{T_\ell}-
\dot{m}_{g}s_{g}-\vec{n}_{g}\cdot\frac{\vec{q}_g}{T_g}\ge0
$$

<!-- ## Averaged Equations 

### Space-Averaged Equations

### Time-Averaged Equations

## Separated Flow Model

## Homogeneous Flow Model

## Drift-Flux Model

## Eulerian-Lagrangian Method -->
