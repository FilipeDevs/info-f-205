# 📘 Fiche d'étude — Exercice 10 : Interpolation
## Avantages des splines + fonctions comme vecteurs dans une base

---

## 🧠 Théorie à comprendre — Nouveau chapitre : l'Interpolation

> ⚠️ **Nouveau chapitre !** Voici toute la théorie de base pour comprendre l'interpolation avant d'attaquer les exercices.

---

### C'est quoi l'interpolation ?

**L'interpolation**, c'est construire une **fonction simple** (souvent un polynôme) qui passe **exactement** par un ensemble de points donnés.

> 💡 **Analogie :** Tu as 5 mesures d'une expérience (5 points sur un graphe). L'interpolation, c'est tracer une courbe qui passe pile sur chacun de ces points. Ensuite tu peux utiliser cette courbe pour estimer des valeurs entre les points.

**Les données :**
- $n+1$ points : $(x_0, y_0), (x_1, y_1), \ldots, (x_n, y_n)$
- Les $x_i$ s'appellent les **nœuds** (ou abscisses)
- Les $y_i = f(x_i)$ s'appellent les **observations** (ou valeurs)

**L'objectif :** trouver un polynôme $\pi(x)$ tel que $\pi(x_i) = y_i$ pour tout $i$.

---

### Les polynômes de Lagrange $l_i(x)$

C'est la façon la plus classique de construire un polynôme interpolant.

Pour $n+1$ nœuds $x_0, x_1, \ldots, x_n$, le **polynôme de Lagrange** $l_i(x)$ associé au nœud $x_i$ est :

$$l_i(x) = \prod_{\substack{j=0 \\ j \neq i}}^{n} \frac{x - x_j}{x_i - x_j}$$

> 💡 **En clair :** on multiplie des fractions de la forme $\dfrac{x - x_j}{x_i - x_j}$ pour tous les nœuds $j$ **sauf** $i$.

**Propriété clé :**
$$l_i(x_j) = \begin{cases} 1 & \text{si } j = i \\ 0 & \text{si } j \neq i \end{cases}$$

Autrement dit : $l_i$ vaut 1 à son propre nœud, et 0 à tous les autres.

**Le polynôme interpolant de Lagrange :**
$$\pi(x) = \sum_{i=0}^{n} y_i \cdot l_i(x) = y_0 l_0(x) + y_1 l_1(x) + \cdots + y_n l_n(x)$$

---

### Le polynôme nodal $\omega_{n+1}(x)$

C'est le polynôme dont les **racines sont exactement les nœuds** $x_0, x_1, \ldots, x_n$ :

$$\omega_{n+1}(x) = (x - x_0)(x - x_1) \cdots (x - x_n)$$

Il intervient dans la formule d'erreur d'interpolation (voir exo 11).

---

### L'interpolation par splines

#### Le problème avec les polynômes de haut degré

Quand on a beaucoup de points ($n$ grand), le polynôme interpolant est de degré $n$. Or, un polynôme de haut degré a tendance à **osciller sauvagement** entre les nœuds — il passe parfaitement par tous les points, mais entre les points il peut faire des montagnes russes énormes.

> 💡 C'est le **phénomène de Runge** : plus on ajoute de points, plus le polynôme oscillera. C'est contre-intuitif mais bien réel.

#### La solution : les splines

Au lieu d'un seul polynôme de haut degré, une **spline** utilise des **polynômes de bas degré** (souvent de degré 1, 2 ou 3), **un par intervalle entre les nœuds**, raccordés entre eux de façon lisse.

**Spline de degré 1 :** des segments de droite (interpolation linéaire par morceaux)

**Spline de degré 3 (cubique) :** des morceaux de polynômes du 3e degré, raccordés avec continuité de la dérivée (courbe lisse)

---

### Les fonctions comme vecteurs dans une base

C'est un concept fondamental en mathématiques : on peut voir les **fonctions** comme des **vecteurs** dans un **espace vectoriel**.

**Rappel sur les vecteurs ordinaires :** tout vecteur de $\mathbb{R}^3$ peut s'écrire comme combinaison linéaire des vecteurs de base $e_1, e_2, e_3$ :

$$v = c_1 e_1 + c_2 e_2 + c_3 e_3$$

**Analogie pour les fonctions :** une fonction $f(x)$ peut s'écrire comme combinaison linéaire de fonctions de base $\phi_0(x), \phi_1(x), \ldots, \phi_n(x)$ :

$$f(x) \approx c_0 \phi_0(x) + c_1 \phi_1(x) + \cdots + c_n \phi_n(x)$$

> 💡 Les $\phi_i(x)$ jouent le rôle des **vecteurs de base**, et les $c_i$ sont les **coordonnées** (coefficients).

**Exemples de bases de fonctions :**
- Les **polynômes de Lagrange** $l_i(x)$ : le polynôme interpolant $\pi(x) = \sum y_i l_i(x)$ exprime $\pi$ dans la base des $l_i$
- Les fonctions $\phi_i(x) = x^i$ : tout polynôme $a_0 + a_1 x + a_2 x^2 + \ldots$ est une combinaison linéaire de cette base
- Les fonctions utilisées en **régression linéaire** $\phi_i(x)$

---

## 🔢 L'exercice 10 — Énoncé

> **(a)** Quel est l'avantage principal des splines, en comparaison à l'usage des polynômes, dans une interpolation ?
>
> **(b)** Donner deux exemples de fonctions qui se manifestent comme des vecteurs dans une base vectorielle.

---

## 🧩 Résolution complète

### Partie (a) — Avantage principal des splines

**La réponse :**

L'interpolation par splines permet d'**ajouter des nœuds sans devoir augmenter le degré du polynôme**. Ceci évite les **fluctuations/oscillations** qui apparaissent avec les polynômes de haut degré.

**Expliqué en détail :**

Avec un polynôme classique, si on a $n+1$ points, on utilise un polynôme de degré $n$. Si on veut ajouter un nouveau point, le degré augmente de 1. Plus le degré est grand, plus le polynôme peut osciller sauvagement entre les nœuds (phénomène de Runge).

Avec une spline, quel que soit le nombre de nœuds qu'on ajoute, le degré de chaque morceau de polynôme reste fixe (par exemple, toujours du degré 3 pour une spline cubique). On ajoute juste un nouveau morceau de polynôme sur le nouvel intervalle, raccordé proprement avec les morceaux voisins.

**En résumé :**

| | Polynôme classique | Spline |
|---|---|---|
| Degré | Augmente avec le nb de points | **Reste fixe** |
| Oscillations | Potentiellement grandes | **Évitées** |
| Ajout d'un nœud | Recalcul complet | Ajout d'un morceau |

---

### Partie (b) — Deux exemples de fonctions comme vecteurs dans une base

**Exemple 1 : Les polynômes de Lagrange $l_i(x)$**

Le polynôme interpolant $\pi(x)$ s'écrit comme une **combinaison linéaire** des polynômes de Lagrange :

$$\pi(x) = \sum_{i=0}^{n} y_i \cdot l_i(x)$$

Ici, les $l_i(x)$ sont les **vecteurs de base**, et les $y_i$ (les observations) sont les **coordonnées** (coefficients). Chaque $l_i$ "s'occupe" d'un nœud.

> 💡 C'est exactement comme écrire un vecteur $v = 3e_1 + 2e_2 - e_3$ dans la base canonique. Ici $\pi(x) = y_0 l_0(x) + y_1 l_1(x) + \ldots$

**Exemple 2 : Les fonctions $\phi_i(x)$ utilisées en régression linéaire**

En régression, on approche une fonction $f$ par une combinaison linéaire de fonctions de base $\phi_0, \phi_1, \ldots, \phi_m$ :

$$f(x) \approx c_0 \phi_0(x) + c_1 \phi_1(x) + \cdots + c_m \phi_m(x)$$

Les $\phi_i(x)$ jouent le rôle de vecteurs de base, et les coefficients $c_i$ sont déterminés par la méthode des moindres carrés.

> 💡 Par exemple, en régression polynomiale : $\phi_0(x) = 1$, $\phi_1(x) = x$, $\phi_2(x) = x^2$, etc.

---

## 🍳 La recette / le modèle à retenir

### Pour toute question sur l'avantage des splines :
→ **Degré fixe** + **pas d'oscillations** = les deux mots clés.

### Pour toute question sur "fonctions comme vecteurs" :
→ Une fonction exprimée comme $f = \sum c_i \phi_i(x)$ est une **combinaison linéaire** de fonctions de base $\phi_i$.
→ Les deux exemples à connaître : **polynômes de Lagrange** $l_i(x)$ et **fonctions de régression** $\phi_i(x)$.

---

## ⚠️ Ce que tu dois savoir par cœur

**Polynôme de Lagrange** $l_i(x)$ (dans le formulaire) :
$$l_i(x) = \prod_{j \neq i} \frac{x - x_j}{x_i - x_j}$$

**Propriété clé** : $l_i(x_j) = 1$ si $i = j$, $0$ sinon.

**Polynôme interpolant de Lagrange** :
$$\pi(x) = \sum_{i=0}^n y_i \cdot l_i(x)$$

**Avantage splines vs polynômes** (à savoir formuler) :
> *Les splines maintiennent un degré fixe par morceau, ce qui évite les oscillations dues aux polynômes de haut degré.*

---

*Fiche préparée pour l'examen INFO-F-205 — Exercice 10 (chapitre Interpolation)*