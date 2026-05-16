# 📘 Fiche d'étude — Exercice 17 : EDO
## Algorithme à un pas, consistance et erreur de troncature locale

---

## 🧠 Théorie à comprendre (et à retenir !)

> ⚠️ **Cet exercice est entièrement conceptuel.** Pas de calcul numérique — il faut comprendre ce que représentent trois expressions mathématiques et les relier aux notions d'algorithme, de consistance et d'erreur de troncature.

---

### Le cadre général : les méthodes à un pas

Une méthode numérique "à un pas" pour résoudre $y'(t) = f(t, y(t))$ s'écrit sous la forme générale :

$$\hat{y}(t+h) = \hat{y}(t) + h \cdot \Phi(t,\ \hat{y}(t),\ t+h,\ \hat{y}(t+h))$$

où $\Phi$ est appelée la **fonction d'incrément** — c'est ce qui définit concrètement la méthode. Par exemple :
- Pour Euler explicite : $\Phi = f(t, \hat{y}(t))$
- Pour Euler implicite : $\Phi = f(t+h, \hat{y}(t+h))$

On peut réécrire cette formule comme :

$$\frac{\hat{y}(t+h) - \hat{y}(t)}{h} = \Phi(t,\ \hat{y}(t),\ t+h,\ \hat{y}(t+h))$$

C'est sous cette forme qu'on va travailler dans l'exercice.

---

### Les 3 expressions clés à distinguer

Voici les trois expressions de l'exercice. Avant de lire les explications, observe bien les différences :

**Expression A :**
$$\frac{\hat{y}(t+h) - \hat{y}(t)}{h} = \Phi(t,\ \hat{y}(t),\ t+h,\ \hat{y}(t+h))$$

**Expression B :**
$$\lim_{h \to 0} \frac{y(t+h) - y(t)}{h} = \Phi(t,\ y(t),\ t,\ y(t))$$

**Expression C :**
$$\lim_{h \to 0} \frac{\hat{y}^*(t+h) - y(t)}{h} = \Phi(t,\ y(t),\ t,\ y(t))$$

> 💡 **Indices clés pour les distinguer :**
> - Expression A : utilise $\hat{y}$ (approximation), **pas de limite** $h \to 0$
> - Expression B : utilise $y$ (vraie solution), **avec** la limite $h \to 0$
> - Expression C : utilise $\hat{y}^*$ (approximation qui part d'une valeur exacte), **avec** la limite $h \to 0$

---

### Ce que chacune représente

#### Expression A — L'algorithme à un pas

$$\frac{\hat{y}(t+h) - \hat{y}(t)}{h} = \Phi(t,\ \hat{y}(t),\ t+h,\ \hat{y}(t+h))$$

C'est simplement **la formule de la méthode numérique** réécrite. Elle décrit ce que fait concrètement l'algorithme : à partir de $\hat{y}(t)$, on calcule $\hat{y}(t+h)$ avec un pas $h$. Il n'y a pas de limite — c'est l'opération réelle, avec un $h$ fixé.

---

#### Expression B — La condition de consistance

$$\lim_{h \to 0} \frac{y(t+h) - y(t)}{h} = \Phi(t,\ y(t),\ t,\ y(t))$$

Observe le membre de gauche : $\displaystyle\lim_{h \to 0} \frac{y(t+h) - y(t)}{h}$ — c'est exactement **la définition de la dérivée** $y'(t)$ !

Donc cette expression dit simplement :

$$y'(t) = \Phi(t,\ y(t),\ t,\ y(t))$$

C'est la **condition de consistance** : quand $h \to 0$, la méthode doit être compatible avec l'EDO originale $y'(t) = f(t, y(t))$. En d'autres termes, si le pas tend vers 0, la fonction d'incrément $\Phi$ doit redonner $f$.

> 💡 **En clair :** Une méthode est consistante si, à la limite d'un pas infiniment petit, elle reproduit exactement l'EDO. C'est le minimum requis pour qu'une méthode ait un sens.

---

#### Expression C — Comportement avec sophistication infinie et valeur exacte

$$\lim_{h \to 0} \frac{\hat{y}^*(t+h) - y(t)}{h} = \Phi(t,\ y(t),\ t,\ y(t))$$

Ici, $\hat{y}^*(t+h)$ désigne **l'approximation obtenue si on part d'une valeur exacte** $y(t)$ (pas d'une approximation accumulée). On fait $h \to 0$ (pas infiniment petit = sophistication infinie).

C'est l'expression qui décrit le **comportement idéal** de l'algorithme : que se passe-t-il si on lui donne une valeur de départ parfaite et un pas infiniment petit ?

---

### L'erreur de troncature locale — comment on la dérive

Les expressions B et C ont **le même membre de droite** : $\Phi(t, y(t), t, y(t))$.

On peut donc les égaler entre elles :

$$\lim_{h \to 0} \frac{y(t+h) - y(t)}{h} = \lim_{h \to 0} \frac{\hat{y}^*(t+h) - y(t)}{h}$$

On réarrange (même dénominateur $h$, même limite) :

$$\lim_{h \to 0} \frac{\hat{y}^*(t+h) - y(t+h)}{h} = 0$$

Cette limite nulle dit que **l'écart entre l'approximation idéale $\hat{y}^*$ et la vraie solution $y$, rapporté à $h$, tend vers zéro**. C'est la condition de consistance.

On en déduit la définition de **l'erreur de troncature locale** $\tau(t, h)$ :

$$\boxed{\tau(t, h) = \frac{\hat{y}^*(t+h) - y(t+h)}{h}}$$

Et la condition de consistance s'écrit : $\displaystyle\lim_{h \to 0} \tau(t, h) = 0$.

> 💡 **En clair :** L'erreur de troncature locale mesure à quel point une étape de la méthode numérique (partant d'une valeur exacte) s'écarte de la vraie solution, divisé par $h$. Si cette erreur tend vers 0 quand $h \to 0$, la méthode est consistante.

---

## 🔢 L'exercice 17 — Énoncé

> Considérer les trois expressions suivantes :
>
> **(1)** $\displaystyle\lim_{h \to 0} \frac{y(t+h) - y(t)}{h} = \Phi(t, y(t), t, y(t))$
>
> **(2)** $\displaystyle\lim_{h \to 0} \frac{\hat{y}^*(t+h) - y(t)}{h} = \Phi(t, y(t), t, y(t))$
>
> **(3)** $\displaystyle\frac{\hat{y}(t+h) - \hat{y}(t)}{h} = \Phi(t, \hat{y}(t), t+h, \hat{y}(t+h))$
>
> - L'une représente **l'algorithme à un pas**. L'autre exprime la **condition de consistance**. La troisième concerne le **comportement de l'algorithme avec un pas infiniment précis et en partant d'une valeur exacte**. Identifier les trois.
>
> - La combinaison de deux de ces expressions conduit à **l'erreur de troncature locale**. Lesquelles ? Développer.

---

## 🧩 Résolution complète

### Première partie — Identifier les trois expressions

**Expression (3) → L'algorithme à un pas**

$$\frac{\hat{y}(t+h) - \hat{y}(t)}{h} = \Phi(t,\ \hat{y}(t),\ t+h,\ \hat{y}(t+h))$$

Pourquoi ? Parce que :
- Elle utilise $\hat{y}$ (les approximations, pas la vraie solution)
- Il n'y a **pas de limite** $h \to 0$ — le pas $h$ est fixé, c'est l'opération réelle de l'algorithme
- C'est simplement la formule d'itération réécrite sous forme de taux d'accroissement

---

**Expression (1) → La condition de consistance**

$$\lim_{h \to 0} \frac{y(t+h) - y(t)}{h} = \Phi(t,\ y(t),\ t,\ y(t))$$

Pourquoi ? Parce que :
- Le membre de gauche est la **définition de la dérivée** $y'(t)$
- L'équation dit donc $y'(t) = \Phi(t, y(t), t, y(t))$, c'est-à-dire que la méthode est compatible avec l'EDO quand $h \to 0$
- Elle utilise $y$ (la vraie solution) et fait $h \to 0$

---

**Expression (2) → Comportement avec sophistication infinie et valeur exacte**

$$\lim_{h \to 0} \frac{\hat{y}^*(t+h) - y(t)}{h} = \Phi(t,\ y(t),\ t,\ y(t))$$

Pourquoi ? Parce que :
- $\hat{y}^*(t+h)$ est l'approximation obtenue **en partant d'une valeur exacte** $y(t)$
- On fait $h \to 0$ (sophistication infiniment précise)
- C'est le comportement idéal de l'algorithme dans les meilleures conditions possibles

---

### Deuxième partie — Dériver l'erreur de troncature locale

**Étape 1 — Identifier les deux expressions à combiner**

Les expressions **(1)** et **(2)** ont exactement le **même membre de droite** : $\Phi(t, y(t), t, y(t))$.

On peut donc les égaler entre elles :

$$\lim_{h \to 0} \frac{y(t+h) - y(t)}{h} = \lim_{h \to 0} \frac{\hat{y}^*(t+h) - y(t)}{h}$$

**Étape 2 — Réarranger**

Les deux membres ont le même dénominateur $h$ sous la même limite. On peut écrire :

$$\lim_{h \to 0} \frac{y(t+h) - y(t)}{h} - \lim_{h \to 0} \frac{\hat{y}^*(t+h) - y(t)}{h} = 0$$

On fusionne les deux fractions sous la même limite (même dénominateur $h$, termes $y(t)$ qui s'annulent) :

$$\lim_{h \to 0} \frac{y(t+h) - \hat{y}^*(t+h)}{h} = 0$$

Ce qui revient à :

$$\lim_{h \to 0} \frac{\hat{y}^*(t+h) - y(t+h)}{h} = 0$$

**Étape 3 — Lire l'erreur de troncature locale**

L'expression $\dfrac{\hat{y}^*(t+h) - y(t+h)}{h}$ est exactement **l'erreur de troncature locale** :

$$\boxed{\tau(t, h) = \frac{\hat{y}^*(t+h) - y(t+h)}{h}}$$

La condition de consistance se lit directement : $\displaystyle\lim_{h \to 0} \tau(t, h) = 0$.

**Ce que ça signifie en mots :**

$\hat{y}^*(t+h)$ est ce que la méthode numérique calcule si elle part d'une valeur **exacte** $y(t)$.
$y(t+h)$ est la vraie valeur de la solution au temps suivant.
Leur différence $\hat{y}^*(t+h) - y(t+h)$ est l'erreur commise en **une seule étape** — c'est l'erreur locale.
On divise par $h$ pour normaliser.

Si cette erreur normalisée tend vers 0 quand $h \to 0$, la méthode est **consistante**.

---

## 🍳 La recette / le modèle à retenir

Pour identifier les trois expressions dans tout exercice similaire, utilise ce tableau de reconnaissance :

| Expression | Utilise quoi ? | Limite $h\to 0$ ? | Ce que c'est |
|---|---|---|---|
| Sans limite, avec $\hat{y}$ | $\hat{y}$ (approx.) | ❌ Non | **Algorithme** |
| Avec limite, avec $y$ (vraie solution) | $y$ (exacte) | ✅ Oui | **Consistance** |
| Avec limite, avec $\hat{y}^*$ (approx. depuis valeur exacte) | $\hat{y}^*$ | ✅ Oui | **Comportement idéal** |

**Pour dériver l'erreur de troncature :**
1. Prendre les expressions de **consistance** et de **comportement idéal** (même membre de droite)
2. Les égaler → simplifier → $\lim_{h\to 0} \frac{\hat{y}^* - y}{h} = 0$
3. Définir $\tau(t,h) = \frac{\hat{y}^*(t+h) - y(t+h)}{h}$

---

## ⚠️ Ce que tu dois savoir par cœur

**Définition de l'erreur de troncature locale :**
$$\tau(t, h) = \frac{\hat{y}^*(t+h) - y(t+h)}{h}$$

**Condition de consistance :**
$$\lim_{h \to 0} \tau(t, h) = 0$$

**La définition de la dérivée** (clé pour reconnaître l'expression de consistance) :
$$y'(t) = \lim_{h \to 0} \frac{y(t+h) - y(t)}{h}$$

---

*Fiche préparée pour l'examen INFO-F-205 — Exercice 17 (chapitre EDO)*