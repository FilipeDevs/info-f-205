# 📘 Fiche d'étude — Exercice 12 : Interpolation
## Identifier si un polynôme peut être un polynôme nodal — et trouver les nœuds

---

## 🧠 Théorie à comprendre (et à retenir !)

### Les 3 conditions qu'un polynôme nodal DOIT respecter

Un polynôme $\omega(x)$ est un **polynôme nodal valide** si et seulement si les 3 conditions suivantes sont remplies :

---

#### ✅ Condition 1 — Coefficient dominant = 1 (normalisé)

Le coefficient devant la puissance la plus haute de $x$ doit être **exactement 1**.

> 💡 **Exemple :** $\omega(x) = 3x^3 - 5x + 2$ → coefficient devant $x^3$ est $3 \neq 1$ → **pas un polynôme nodal** ❌

---

#### ✅ Condition 2 — Toutes les racines sont réelles

Les nœuds sont des points sur la droite réelle. Si $\omega(x)$ a des racines **complexes** (imaginaires), elles ne peuvent pas être des nœuds. Donc $\omega(x)$ ne peut pas être un polynôme nodal dans ce cas.

**Comment détecter des racines complexes ?**

Quand on a un facteur du type $x^2 + c$ avec $c > 0$, les racines sont $x = \pm\sqrt{-c}$ — imaginaires ! → ❌

Quand on a $x^2 - c$ avec $c > 0$, les racines sont $x = \pm\sqrt{c}$ — réelles ! → ✅

> 💡 **Règle rapide :** $x^2 + (\text{positif})$ → racines imaginaires → pas un nœud.
> $x^2 - (\text{positif})$ → racines réelles → nœuds valides.

---

#### ✅ Condition 3 — Toutes les racines sont distinctes

Deux nœuds ne peuvent pas être identiques. Un polynôme nodal n'a donc **pas de racines répétées** (pas de facteurs du type $(x - a)^2$).

---

### Comment trouver les nœuds depuis un polynôme factorisé ?

Si $\omega(x) = (x - a)(x - b)(x^2 - c)$ avec $c > 0$ :

- $(x - a)$ → nœud $x = a$
- $(x - b)$ → nœud $x = b$
- $(x^2 - c) = (x - \sqrt{c})(x + \sqrt{c})$ → nœuds $x = \sqrt{c}$ et $x = -\sqrt{c}$

---

## 🔢 L'exercice 12 — Énoncé

> Donner pour chacun des polynômes suivants un argument pour lequel ce polynôme **ne peut pas être un polynôme nodal** dans le cadre d'une interpolation sur $\mathbb{R}$, ou bien, s'il s'agit d'un polynôme nodal, donner les nœuds.
>
> **(a)** $\omega_1(x) = (3x - 1)(5x + 2)(7x - 3)$
>
> **(b)** $\omega_2(x) = (x^2 - 2)(x + 2)$
>
> **(c)** $\omega_3(x) = (x^2 + 2)(x - 2)$

---

## 🧩 Résolution complète — étape par étape

---

### Partie (a) — $\omega_1(x) = (3x - 1)(5x + 2)(7x - 3)$

**Étape 1 — Vérifier le coefficient dominant**

On développe juste le terme de plus haut degré pour trouver le coefficient dominant. On multiplie les coefficients devant $x$ dans chaque facteur :

$$3x \cdot 5x \cdot 7x = 105x^3$$

Le coefficient dominant est $105 \neq 1$.

**Conclusion :** $\omega_1(x)$ **n'est pas un polynôme nodal** ❌ car il n'est pas normalisé (le coefficient de $x^3$ doit valoir 1).

> 💡 **Note :** les racines de $\omega_1$ sont $x = 1/3$, $x = -2/5$, $x = 3/7$ — elles sont bien réelles et distinctes, mais le problème de normalisation suffit à disqualifier $\omega_1$.

---

### Partie (b) — $\omega_2(x) = (x^2 - 2)(x + 2)$

**Étape 1 — Vérifier le coefficient dominant**

En développant juste le terme de plus haut degré : $x^2 \cdot x = x^3$ → coefficient $1$ ✅

**Étape 2 — Vérifier que toutes les racines sont réelles**

On analyse chaque facteur :

- Facteur $(x + 2)$ → racine $x = -2$ (réelle ✅)
- Facteur $(x^2 - 2)$ → racines $x = \pm\sqrt{2}$ (réelles, car on soustrait un positif) ✅

**Étape 3 — Vérifier que les racines sont distinctes**

Les trois racines sont $x = -2$, $x = -\sqrt{2} \approx -1{,}41$ et $x = \sqrt{2} \approx 1{,}41$ → toutes distinctes ✅

**Conclusion :** $\omega_2(x)$ **est un polynôme nodal** ✅ avec les nœuds :

$$x_0 = -2, \quad x_1 = -\sqrt{2}, \quad x_2 = \sqrt{2}$$

---

### Partie (c) — $\omega_3(x) = (x^2 + 2)(x - 2)$

**Étape 1 — Vérifier le coefficient dominant**

En développant juste le terme de plus haut degré : $x^2 \cdot x = x^3$ → coefficient $1$ ✅

**Étape 2 — Vérifier que toutes les racines sont réelles**

On analyse chaque facteur :

- Facteur $(x - 2)$ → racine $x = 2$ (réelle ✅)
- Facteur $(x^2 + 2)$ → racines $x = \pm\sqrt{-2}$ = **imaginaires** ❌

Pour vérifier : on résout $x^2 + 2 = 0 \iff x^2 = -2$. Or un carré ne peut pas être négatif dans les réels → **pas de solution réelle**.

**Conclusion :** $\omega_3(x)$ **n'est pas un polynôme nodal** ❌ car il possède des racines complexes (imaginaires) — un nœud d'interpolation doit être un nombre réel.

---

### Tableau récapitulatif

| Polynôme | Coefficient dominant | Racines réelles ? | Verdict |
|---|---|---|---|
| $\omega_1 = (3x-1)(5x+2)(7x-3)$ | $105 \neq 1$ ❌ | Oui | ❌ Pas nodal |
| $\omega_2 = (x^2-2)(x+2)$ | $1$ ✅ | $-2, -\sqrt{2}, \sqrt{2}$ ✅ | ✅ Nodal |
| $\omega_3 = (x^2+2)(x-2)$ | $1$ ✅ | $2$ réelle + $\pm\sqrt{-2}$ imaginaires ❌ | ❌ Pas nodal |

---

## 🍳 La recette / le modèle à retenir

Pour tout exercice **"est-ce un polynôme nodal ?"**, vérifier dans l'ordre :

### ✅ Check 1 — Coefficient dominant
Multiplier les coefficients devant $x$ dans chaque facteur → si le résultat $\neq 1$ → ❌ stop, pas nodal.

### ✅ Check 2 — Racines réelles
Pour chaque facteur quadratique $x^2 + c$ :
- Si $c < 0$ : $x^2 - |c|$ → racines $\pm\sqrt{|c|}$ → réelles ✅
- Si $c > 0$ : $x^2 + |c|$ → racines imaginaires ❌ → pas nodal

### ✅ Check 3 — Racines distinctes
Vérifier qu'aucune racine n'est répétée (pas de $(x-a)^2$).

### Si tout est ✅ → donner les nœuds
Écrire toutes les racines réelles : facteur $(x - a)$ → nœud $a$ ; facteur $(x^2 - c)$ → nœuds $\pm\sqrt{c}$.

---

## ⚠️ Ce que tu dois savoir par cœur

**Les 3 conditions d'un polynôme nodal :**
1. Coefficient dominant $= 1$ (normalisé)
2. Toutes les racines sont **réelles**
3. Toutes les racines sont **distinctes**

**Distinguer racines réelles vs complexes :**
$$x^2 - c \text{ avec } c > 0 \implies \text{racines } \pm\sqrt{c} \text{ (réelles ✅)}$$
$$x^2 + c \text{ avec } c > 0 \implies \text{racines imaginaires ❌}$$

---

*Fiche préparée pour l'examen INFO-F-205 — Exercice 12 (chapitre Interpolation)*