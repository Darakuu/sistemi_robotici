---
tags:
  - SistemiRobotici
  - SistemiRobotici/Esempi
---
# Carrello

Consideriamo un carrello che si muove in uno spazio 1-Dimensionale, con una massa $M$, dotato di motori elettrici. 

All'istante $T=0$ accendiamo i motori, così da fornire una fornire una forza di trazione sul tempo: $f(t)$.

Vogliamo capire:
- Come si comporta il carrello;
- Qual è il trend della **velocità** sul tempo?
- Qual è il trend della **posizione** sul tempo?

Inoltre, vogliamo agire sulla forza per controllare **velocità** e **posizione**.

![[Pasted image 20240310162043.png]]

Usando la seconda legge di Newton: la somma delle forze in un corpo rigido è uguale alla massa del corpo moltiplicato per l'accelerazione.

$\displaystyle\sum F(t)=M \cdot a(t)$

Da cui ricaviamo:

- $f(t) - b \cdot v(t) = M \cdot a(t)$
- $f(t) - b \cdot v(t) = M \cdot \dfrac{d  v(t)}{d t}$

Anche la velocità può essere rappresentata in forma differenziale, in quanto la posizione è integrale (primitiva) della velocità, quindi:

- $v(t)= \dfrac{dp(t)}{dt}$

Il nostro modello è dunque:

$$
\begin{cases}
f(t)-bv(t)=M \cdot{\dfrac{dv(t)}{dt}} \\
v(t)=\dfrac{dp(t)}{dt}
\end{cases}
$$

L'ideale sarebbe ottenere una singola funziona analitica da questo sistema:

- $v(t)=f_{unc}(t,F(t))$

Che non è semplice, ma fortunatamente, non ci interessa in realtà.

Per non appesantire ulteriormente le formule, introduciamo la notazione puntata:


> [!def]- Notazione Puntata
> - $\dot{x}=\dfrac{dx(t)}{dt}$ - Derivata
> - $\ddot{x}=\dfrac{d^2x(t)}{d^2t}$ - Derivata seconda

E quindi, semplficando:

$$
\begin{cases}
f-bv=M \cdot{\dot{v}} \\
v=\dot{p}
\end{cases}
$$

Questa semplificazione ci va bene perché la dipendenza dal tempo è **fondamentale** in questo ambito.

Inoltre, per convenzione, mettiamo a primo membro le variabili derivate:

$$
\begin{cases}
\dot{v}=-\dfrac{b}{M}v+\dfrac{1}{M}\cdot f \\
\dot{p}=v
\end{cases}
$$


> [!info] Osservazione
> Dato che stiamo trattando sistemi robotici (e quindi digitali, almeno per la loro componente software), siamo costretti a discretizzare, o in altre parole, approssimare.
> Passiamo da $dt$ a $\Delta t$, sostituendo con il rapporto incrementale.


> [!info]- Passaggio a quanto di tempo discreto con rapporto incrementale
> Sappiamo che:
> $f'(t)=\lim_{ \Delta t \to 0 }\dfrac{f(t+\Delta t)+f(t)}{\Delta t}$
> Se consideriamo $\Delta t$ molto piccolo possiamo approssimare come segue:
> $f'(t)\backsimeq\dfrac{f(t+\Delta t)+f(t)}{\Delta t}$


Passiamo da Equazioni Differenziali (continue) $\iff$ Equazioni delle Differenze (discrete), che non risolviamo analiticamente.

Ci dà solo un aggiornamento sul quanto di tempo (**tick**).

Il [[Control System Model|Controllore]] avrà infatti solo il valore delle variabili all'istante successivo del calcolo. Possiamo vederlo come un update sulle variabili $p$ e $v$.

Difatti, il nostro modello finale diventa:

$$
\begin{cases}
v(t+\Delta t)= \left( 1-\dfrac{b\Delta t}{M} \right)v(t)+\dfrac{\Delta T}{M}f(t) \\
p(t+\Delta t)=p(t)+v(t)\Delta t
\end{cases}
$$


