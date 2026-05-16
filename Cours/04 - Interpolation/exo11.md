# 📘 Fiche d'étude — Exercice 11 : Interpolation
## Polynôme nodal → trouver les nœuds → construire les polynômes de Lagrange → polynôme interpolant

---

## 🧠 Théorie à comprendre (et à retenir !)

### Le polynôme nodal $\omega_{n+1}(x)$ — rappel et approfondissement

Le polynôme nodal est le polynôme dont les **racines sont exactement les nœuds** $x_0, x_1, \ldots, x_n$ :

$$\omega_{n+1}(x) = (x - x_0)(x - x_1) \cdots (x - x_n)$$

> 💡 **Astuce clé :** si on te donne $\omega_{n+1}(x)$ sous forme factorisée, ses racines (les valeurs de $x$ qui l'annulent) sont directement les nœuds !

**Règle importante :** un polynôme nodal doit être **normalisé** — le coefficient devant $x^n$ (la puissance la plus haute) doit valoir **1**. Si ce coefficient est différent de 1, ce n'est pas un polynôme nodal valide.

---

### Comment construire $l_i(x)$ depuis le polynôme nodal ?

Une fois qu'on a les nœuds, on peut construire les polynômes de Lagrange. Mais il y a une formule compacte qui utilise directement $\omega_{n+1}(x)$ :

$$l_i(x) = \frac{\omega_{n+1}(x)}{(x - x_i) \cdot \omega'_{n+1}(x_i)}$$

> ⚠️ Cette formule est élégante mais peut sembler complexe. En pratique, il est souvent plus simple de construire $l_i(x)$ directement à partir de la définition :
> $$l_i(x) = \prod_{j \neq i} \frac{x - x_j}{x_i - x_j}$$

**Démarche directe (plus simple) :**

Si les nœuds sont $x_0, x_1, x_2$ :

$$l_0(x) = \frac{(x - x_1)(x - x_2)}{(x_0 - x_1)(x_0 - x_2)}$$

$$l_1(x) = \frac{(x - x_0)(x - x_2)}{(x_1 - x_0)(x_1 - x_2)}$$

$$l_2(x) = \frac{(x - x_0)(x - x_1)}{(x_2 - x_0)(x_2 - x_1)}$$

**Règle de construction :** pour $l_i(x)$, on met au **numérateur** tous les $(x - x_j)$ pour $j \neq i$, et au **dénominateur** les mêmes termes évalués en $x = x_i$.

---

### Le polynôme interpolant final

Une fois qu'on a les $l_i(x)$ et les valeurs $y_i = f(x_i)$ :

$$\pi(x) = \sum_{i=0}^{n} f(x_i) \cdot l_i(x)$$

On peut laisser la réponse **sous forme de Lagrange** (somme de $f(x_i) \cdot l_i(x)$) sans tout développer, sauf si l'énoncé le demande.

---

## 🔢 L'exercice 11 — Énoncé

> Étant donné le polynôme nodal $\omega(x) = x^3 + x^2 - 4x - 4 = (x^2 - 4)(x + 1)$, écrire les polynômes caractéristiques de Lagrange et le polynôme interpolant la fonction $\sin(x)$.
>
> *(Il suffit de laisser le polynôme dans la forme de Lagrange, pas besoin de réarranger les termes par puissance de $x$)*

---

## 🧩 Résolution complète — étape par étape

---

### Étape 1 — Trouver les nœuds depuis $\omega(x)$

On nous donne $\omega(x) = (x^2 - 4)(x + 1)$.

On factorise encore $x^2 - 4$ : c'est une **différence de carrés** $a^2 - b^2 = (a-b)(a+b)$ avec $a = x$ et $b = 2$ :

$$x^2 - 4 = (x - 2)(x + 2)$$

Donc :

$$\omega(x) = (x - 2)(x + 2)(x + 1)$$

Les **nœuds** sont les racines de $\omega(x)$, c'est-à-dire les valeurs de $x$ qui annulent $\omega$ :

$$x_0 = -2, \quad x_1 = -1, \quad x_2 = 2$$

> 💡 Vérification du coefficient dominant : $(x)(x)(x) = x^3$ → coefficient 1 ✅ → c'est bien un polynôme nodal valide.

---

### Étape 2 — Construire $l_0(x)$ pour le nœud $x_0 = -2$

On met au **numérateur** tous les $(x - x_j)$ pour $j \neq 0$, donc $(x - x_1)(x - x_2) = (x - (-1))(x - 2) = (x+1)(x-2)$.

Au **dénominateur**, les mêmes termes évalués en $x = x_0 = -2$ :

$$(x_0 - x_1)(x_0 - x_2) = (-2 - (-1))(-2 - 2) = (-1)(-4) = 4$$

Donc :

$$l_0(x) = \frac{(x+1)(x-2)}{(-2-(-1))(-2-2)} = \frac{(x+1)(x-2)}{(-1)(-4)} = \frac{(x+1)(x-2)}{4}$$

On peut développer le numérateur pour vérifier :

$$(x+1)(x-2) = x^2 - 2x + x - 2 = x^2 - x - 2$$

$$\boxed{l_0(x) = \frac{1}{4}(x^2 - x - 2)}$$

---

### Étape 3 — Construire $l_1(x)$ pour le nœud $x_1 = -1$

**Numérateur :** $(x - x_0)(x - x_2) = (x - (-2))(x - 2) = (x+2)(x-2)$

**Dénominateur :** $(x_1 - x_0)(x_1 - x_2) = (-1 - (-2))(-1 - 2) = (1)(-3) = -3$

Donc :

$$l_1(x) = \frac{(x+2)(x-2)}{(-1-(-2))(-1-2)} = \frac{(x+2)(x-2)}{(1)(-3)} = \frac{(x+2)(x-2)}{-3}$$

On développe le numérateur : $(x+2)(x-2) = x^2 - 4$ (différence de carrés).

$$\boxed{l_1(x) = \frac{-(x^2 - 4)}{3} = \frac{1}{3}(4 - x^2)}$$

---

### Étape 4 — Construire $l_2(x)$ pour le nœud $x_2 = 2$

**Numérateur :** $(x - x_0)(x - x_1) = (x - (-2))(x - (-1)) = (x+2)(x+1)$

**Dénominateur :** $(x_2 - x_0)(x_2 - x_1) = (2 - (-2))(2 - (-1)) = (4)(3) = 12$

Donc :

$$l_2(x) = \frac{(x+2)(x+1)}{(2-(-2))(2-(-1))} = \frac{(x+2)(x+1)}{(4)(3)} = \frac{(x+2)(x+1)}{12}$$

On développe le numérateur : $(x+2)(x+1) = x^2 + x + 2x + 2 = x^2 + 3x + 2$.

$$\boxed{l_2(x) = \frac{1}{12}(x^2 + 3x + 2)}$$

---

### Étape 5 — Vérification rapide

Chaque $l_i(x)$ doit valoir 1 à son propre nœud et 0 aux autres. Vérifions sur $l_0$ :

- $l_0(x_0) = l_0(-2) = \frac{(-2+1)(-2-2)}{4} = \frac{(-1)(-4)}{4} = \frac{4}{4} = 1$ ✅
- $l_0(x_1) = l_0(-1) = \frac{(-1+1)(-1-2)}{4} = \frac{(0)(-3)}{4} = 0$ ✅
- $l_0(x_2) = l_0(2) = \frac{(2+1)(2-2)}{4} = \frac{(3)(0)}{4} = 0$ ✅

---

### Étape 6 — Écrire le polynôme interpolant $\sin(x)$

On veut interpoler $f(x) = \sin(x)$ aux nœuds $x_0 = -2$, $x_1 = -1$, $x_2 = 2$.

Les valeurs de la fonction aux nœuds sont :
- $f(x_0) = \sin(-2)$
- $f(x_1) = \sin(-1)$
- $f(x_2) = \sin(2)$

Le polynôme interpolant est :

$$\boxed{\pi(x) = l_0(x) \cdot \sin(-2) + l_1(x) \cdot \sin(-1) + l_2(x) \cdot \sin(2)}$$

En remplaçant les $l_i(x)$ :

$$\pi(x) = \frac{x^2 - x - 2}{4} \cdot \sin(-2) + \frac{4 - x^2}{3} \cdot \sin(-1) + \frac{x^2 + 3x + 2}{12} \cdot \sin(2)$$

> 💡 L'énoncé dit de laisser sous forme de Lagrange — on s'arrête là, pas besoin de tout développer et regrouper par puissance de $x$.

---

## 🍳 La recette / le modèle à retenir

Pour tout exercice **polynôme nodal → Lagrange → interpolation** :

### Étape 1 — Trouver les nœuds depuis $\omega(x)$
Factoriser $\omega(x)$ au maximum → les racines sont les nœuds $x_0, x_1, \ldots, x_n$.

> Rappel factorisation utile : $x^2 - a^2 = (x-a)(x+a)$

### Étape 2 — Construire chaque $l_i(x)$

Pour $l_i(x)$ :
- **Numérateur :** produit de $(x - x_j)$ pour tous $j \neq i$
- **Dénominateur :** même produit mais avec $x = x_i$ (des nombres, pas de $x$)

### Étape 3 — Vérification rapide
$l_i(x_i) = 1$ et $l_i(x_j) = 0$ pour $j \neq i$.

### Étape 4 — Écrire le polynôme interpolant
$$\pi(x) = \sum_i f(x_i) \cdot l_i(x)$$

---

## ⚠️ Ce que tu dois savoir par cœur (du formulaire)

**Polynôme de Lagrange :**
$$l_i(x) = \prod_{j \neq i} \frac{x - x_j}{x_i - x_j}$$

**Polynôme interpolant :**
$$\pi(x) = \sum_{i=0}^n f(x_i) \cdot l_i(x)$$

**Factorisation différence de carrés** (souvent utile) :
$$x^2 - a^2 = (x - a)(x + a)$$

**Propriété fondamentale des $l_i$ :**
$$l_i(x_j) = \begin{cases} 1 & \text{si } i = j \\ 0 & \text{si } i \neq j \end{cases}$$

---

*Fiche préparée pour l'examen INFO-F-205 — Exercice 11 (chapitre Interpolation)*