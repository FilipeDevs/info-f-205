# 📘 Fiche d'étude — Exercice 14 : Interpolation
## Système surdéterminé avec base de Lagrange — Matrice X et valeurs singulières

---

## 🧠 Théorie à comprendre (et à retenir !)

### C'est quoi un système surdéterminé ?

Un **système surdéterminé** est un système $X\vec{c} = \vec{y}$ où il y a **plus d'équations que d'inconnues** — en général pas de solution exacte. On cherche alors la solution **au sens des moindres carrés** : le vecteur $\vec{c}$ qui minimise $\|X\vec{c} - \vec{y}\|^2$.

> 💡 **Analogie :** Tu as 5 mesures expérimentales et tu veux les approcher par une droite (2 paramètres). Il n'existe pas de droite qui passe exactement par 5 points quelconques — tu cherches la droite "la moins mauvaise" au sens des moindres carrés.

---

### Le modèle : une combinaison de fonctions de base

On cherche à approcher $f$ par :

$$\pi(x) = c_0 \phi_0(x) + c_1 \phi_1(x) + \cdots + c_m \phi_m(x)$$

Les $\phi_j(x)$ sont des **fonctions de base** connues, et les $c_j$ sont les **coefficients inconnus** qu'on cherche.

Pour $n+1$ nœuds $x_0, x_1, \ldots, x_n$, la condition d'interpolation $\pi(x_i) \approx y_i$ pour tout $i$ donne le système :

$$\underbrace{\begin{bmatrix} \phi_0(x_0) & \phi_1(x_0) & \cdots & \phi_m(x_0) \\ \phi_0(x_1) & \phi_1(x_1) & \cdots & \phi_m(x_1) \\ \vdots & \vdots & \ddots & \vdots \\ \phi_0(x_n) & \phi_1(x_n) & \cdots & \phi_m(x_n) \end{bmatrix}}_{X} \underbrace{\begin{bmatrix} c_0 \\ c_1 \\ \vdots \\ c_m \end{bmatrix}}_{\vec{c}} = \underbrace{\begin{bmatrix} y_0 \\ y_1 \\ \vdots \\ y_n \end{bmatrix}}_{\vec{y}}$$

La **matrice $X$** est donc construite en évaluant chaque fonction de base $\phi_j$ à chaque nœud $x_i$ :

$$X_{ij} = \phi_j(x_i)$$

---

### La propriété clé des polynômes de Lagrange pour construire X

On l'a vu à l'exo 11 : les polynômes de Lagrange $l_j(x)$ vérifient :

$$l_j(x_i) = \begin{cases} 1 & \text{si } i = j \\ 0 & \text{si } i \neq j \end{cases}$$

Autrement dit : chaque $l_j$ vaut 1 à son propre nœud et 0 à tous les autres. Cette propriété rend la construction de $X$ très simple !

---

### C'est quoi les valeurs singulières ?

Les **valeurs singulières** de $X$, notées $\sigma_i$, sont les **racines carrées des valeurs propres** de $X^T X$ :

$$\sigma_i = \sqrt{\lambda_i(X^T X)}$$

**Pourquoi c'est utile ?**
- Elles mesurent à quel point la matrice $X$ "étire" l'espace
- Elles sont liées au conditionnement de $X$ : $\kappa(X) = \sigma_{\max} / \sigma_{\min}$
- Une valeur singulière nulle signifie que $X$ n'est pas de rang plein

**Comment les calculer :**
1. Calculer $X^T X$ (matrice carrée $m \times m$)
2. Trouver les valeurs propres $\lambda_i$ de $X^T X$ en résolvant $\det(X^T X - \lambda I) = 0$
3. Prendre les racines carrées : $\sigma_i = \sqrt{\lambda_i}$

---

## 🔢 L'exercice 14 — Énoncé

> Considérer le modèle :
> $$\pi_2(x) = \phi_0(x)c_0 + \phi_1(x)c_1 + \phi_2(x)c_2$$
> où $\phi_0(x) = 1$ et pour $j = 1, 2$ : $\phi_j(x) = l_j(x)$, avec $l_j(x)$ les polynômes de Lagrange définis sur la grille de nœuds $x_j$, $j = 0, 1, 2, 3, 4$.
>
> **(a)** Écrire la matrice $X$ du système surdéterminé $X\vec{c} = \vec{y}$ pour l'approximation de $y_i$ par $\pi(x_i)$ au sens des moindres carrés dans les mêmes nœuds $x_i$, $i = 0, 1, 2, 3, 4$.
>
> **(b)** Trouver les valeurs singulières de $X$.

---

## 🧩 Résolution complète — étape par étape

---

### Partie (a) — Construire la matrice $X$

**Étape 1 — Comprendre la situation**

On a **5 nœuds** : $x_0, x_1, x_2, x_3, x_4$ (indices $i = 0, 1, 2, 3, 4$)

Le modèle a **3 fonctions de base** :
- $\phi_0(x) = 1$ (constante)
- $\phi_1(x) = l_1(x)$ (polynôme de Lagrange associé au nœud $x_1$)
- $\phi_2(x) = l_2(x)$ (polynôme de Lagrange associé au nœud $x_2$)

La matrice $X$ a donc **5 lignes** (une par nœud) et **3 colonnes** (une par fonction de base) → c'est bien un système surdéterminé (5 équations, 3 inconnues).

**Étape 2 — Remplir colonne par colonne**

**Colonne 0 : $\phi_0(x_i) = 1$ pour tout $i$**

La constante 1 évaluée partout donne toujours 1 :

$$\phi_0(x_0) = 1, \quad \phi_0(x_1) = 1, \quad \phi_0(x_2) = 1, \quad \phi_0(x_3) = 1, \quad \phi_0(x_4) = 1$$

→ Colonne 0 : $[1, 1, 1, 1, 1]^T$

**Colonne 1 : $\phi_1(x_i) = l_1(x_i)$**

On utilise la propriété des polynômes de Lagrange : $l_1(x_i) = 1$ si $i = 1$, et $0$ si $i \neq 1$.

$$l_1(x_0) = 0, \quad l_1(x_1) = 1, \quad l_1(x_2) = 0, \quad l_1(x_3) = 0, \quad l_1(x_4) = 0$$

→ Colonne 1 : $[0, 1, 0, 0, 0]^T$

**Colonne 2 : $\phi_2(x_i) = l_2(x_i)$**

De même, $l_2(x_i) = 1$ si $i = 2$, et $0$ si $i \neq 2$.

$$l_2(x_0) = 0, \quad l_2(x_1) = 0, \quad l_2(x_2) = 1, \quad l_2(x_3) = 0, \quad l_2(x_4) = 0$$

→ Colonne 2 : $[0, 0, 1, 0, 0]^T$

**Étape 3 — Assembler la matrice $X$**

En mettant les colonnes ensemble (ligne $i$, colonne $j$) :

$$X = \begin{bmatrix} \phi_0(x_0) & \phi_1(x_0) & \phi_2(x_0) \\ \phi_0(x_1) & \phi_1(x_1) & \phi_2(x_1) \\ \phi_0(x_2) & \phi_1(x_2) & \phi_2(x_2) \\ \phi_0(x_3) & \phi_1(x_3) & \phi_2(x_3) \\ \phi_0(x_4) & \phi_1(x_4) & \phi_2(x_4) \end{bmatrix} = \begin{bmatrix} 1 & 0 & 0 \\ 1 & 1 & 0 \\ 1 & 0 & 1 \\ 1 & 0 & 0 \\ 1 & 0 & 0 \end{bmatrix}$$

> 💡 **Pourquoi c'est si simple ?** Grâce à la propriété des $l_j$ : dans chaque colonne $j \geq 1$, il y a un seul 1 (à la ligne $j$) et des 0 partout ailleurs. La première colonne est toute à 1 car $\phi_0 = 1$ partout.

---

### Partie (b) — Trouver les valeurs singulières de $X$

**Étape 1 — Calculer $X^T X$**

On doit transposer $X$ (échanger lignes et colonnes) :

$$X^T = \begin{bmatrix} 1 & 1 & 1 & 1 & 1 \\ 0 & 1 & 0 & 0 & 0 \\ 0 & 0 & 1 & 0 & 0 \end{bmatrix}$$

On calcule $X^T X$ (matrice $3 \times 3$). Pour rappel, l'élément $(i,j)$ de $X^T X$ est le **produit scalaire de la colonne $i$ de $X$ avec la colonne $j$ de $X$** :

- $(X^T X)_{00}$ = colonne 0 de $X$ · colonne 0 de $X$ = $1^2 + 1^2 + 1^2 + 1^2 + 1^2 = 5$
- $(X^T X)_{01}$ = colonne 0 · colonne 1 = $1\cdot0 + 1\cdot1 + 1\cdot0 + 1\cdot0 + 1\cdot0 = 1$
- $(X^T X)_{02}$ = colonne 0 · colonne 2 = $1\cdot0 + 1\cdot0 + 1\cdot1 + 1\cdot0 + 1\cdot0 = 1$
- $(X^T X)_{11}$ = colonne 1 · colonne 1 = $0^2 + 1^2 + 0^2 + 0^2 + 0^2 = 1$
- $(X^T X)_{12}$ = colonne 1 · colonne 2 = $0\cdot0 + 1\cdot0 + 0\cdot1 + 0\cdot0 + 0\cdot0 = 0$
- $(X^T X)_{22}$ = colonne 2 · colonne 2 = $0^2 + 0^2 + 1^2 + 0^2 + 0^2 = 1$

La matrice est symétrique ($(X^T X)_{ji} = (X^T X)_{ij}$), donc :

$$X^T X = \begin{bmatrix} 5 & 1 & 1 \\ 1 & 1 & 0 \\ 1 & 0 & 1 \end{bmatrix}$$

**Étape 2 — Trouver les valeurs propres de $X^T X$**

On résout $\det(X^T X - \lambda I) = 0$ :

$$\det\begin{bmatrix} 5 - \lambda & 1 & 1 \\ 1 & 1 - \lambda & 0 \\ 1 & 0 & 1 - \lambda \end{bmatrix} = 0$$

> 💡 **Comment calculer un déterminant $3\times3$ ? — Le développement de Laplace**
>
> On prend chaque élément de la **première ligne**, on le multiplie par le déterminant de la **sous-matrice** obtenue en **barrant sa ligne et sa colonne**, avec des signes alternés $+$, $-$, $+$ :
>
> $$\det\begin{bmatrix} a & b & c \\ d & e & f \\ g & h & k \end{bmatrix} = a \cdot \det\begin{bmatrix} e & f \\ h & k \end{bmatrix} - b \cdot \det\begin{bmatrix} d & f \\ g & k \end{bmatrix} + c \cdot \det\begin{bmatrix} d & e \\ g & h \end{bmatrix}$$
>
> **Comment trouver la sous-matrice ?** On "barre" la ligne 1 et la colonne de l'élément choisi, et on lit ce qui reste :
>
> - Pour $a$ → barrer ligne 1 et colonne 1 → il reste $\begin{bmatrix} e & f \\ h & k \end{bmatrix}$
> - Pour $b$ → barrer ligne 1 et colonne 2 → il reste $\begin{bmatrix} d & f \\ g & k \end{bmatrix}$
> - Pour $c$ → barrer ligne 1 et colonne 3 → il reste $\begin{bmatrix} d & e \\ g & h \end{bmatrix}$
>
> **Les signes :** toujours $+$, $-$, $+$ pour la première ligne. À retenir !

Ici $a = (5-\lambda)$, $b = 1$, $c = 1$. On applique :

$$= (5-\lambda) \cdot \det\begin{bmatrix} 1-\lambda & 0 \\ 0 & 1-\lambda \end{bmatrix} - 1 \cdot \det\begin{bmatrix} 1 & 0 \\ 1 & 1-\lambda \end{bmatrix} + 1 \cdot \det\begin{bmatrix} 1 & 1-\lambda \\ 1 & 0 \end{bmatrix}$$

On calcule chaque déterminant $2\times2$ :

- $\det\begin{bmatrix} 1-\lambda & 0 \\ 0 & 1-\lambda \end{bmatrix} = (1-\lambda)^2$

- $\det\begin{bmatrix} 1 & 0 \\ 1 & 1-\lambda \end{bmatrix} = (1)(1-\lambda) - (0)(1) = 1-\lambda$

- $\det\begin{bmatrix} 1 & 1-\lambda \\ 1 & 0 \end{bmatrix} = (1)(0) - (1-\lambda)(1) = -(1-\lambda)$

Donc :

$$= (5-\lambda)(1-\lambda)^2 - (1-\lambda) - (1-\lambda)$$

$$= (5-\lambda)(1-\lambda)^2 - 2(1-\lambda)$$

On factorise par $(1-\lambda)$ :

$$= (1-\lambda)\left[(5-\lambda)(1-\lambda) - 2\right] = 0$$

**Première valeur propre :** $\lambda_1 = 1$

**Pour les deux autres**, on résout $(5-\lambda)(1-\lambda) - 2 = 0$ :

$$5 - 5\lambda - \lambda + \lambda^2 - 2 = 0$$

$$\lambda^2 - 6\lambda + 3 = 0$$

On applique la formule quadratique avec $a=1$, $b=-6$, $c=3$ :

$$\lambda = \frac{6 \pm \sqrt{36 - 12}}{2} = \frac{6 \pm \sqrt{24}}{2} = \frac{6 \pm 2\sqrt{6}}{2} = 3 \pm \sqrt{6}$$

Donc $\lambda_2 = 3 - \sqrt{6} \approx 3 - 2{,}449 \approx 0{,}5505$ et $\lambda_3 = 3 + \sqrt{6} \approx 3 + 2{,}449 \approx 5{,}4495$.

**Étape 3 — Prendre les racines carrées pour obtenir les valeurs singulières**

$$\sigma_i = \sqrt{\lambda_i}$$

$$\sigma_1 = \sqrt{1} = 1$$

$$\sigma_2 = \sqrt{3 - \sqrt{6}} \approx \sqrt{0{,}5505} \approx 0{,}7420$$

$$\sigma_3 = \sqrt{3 + \sqrt{6}} \approx \sqrt{5{,}4495} \approx 2{,}3344$$

$$\boxed{\sigma \in \{1;\; 0{,}7420;\; 2{,}3344\}}$$

---

## 🍳 La recette / le modèle à retenir

### Pour construire la matrice $X$ d'un système surdéterminé :
1. **Lignes** = nœuds $x_i$ ($i = 0, \ldots, n$)
2. **Colonnes** = fonctions de base $\phi_j$ ($j = 0, \ldots, m$)
3. **Élément $(i,j)$** = $\phi_j(x_i)$ (évaluer la $j$-ème base au $i$-ème nœud)

**Si les $\phi_j$ sont des polynômes de Lagrange :** exploiter la propriété $l_j(x_i) = \delta_{ij}$ pour remplir directement (0 partout sauf 1 sur la diagonale).

### Pour trouver les valeurs singulières de $X$ :
1. Calculer $X^T X$ (produits scalaires des colonnes de $X$)
2. Résoudre $\det(X^T X - \lambda I) = 0$ → valeurs propres $\lambda_i$
3. $\sigma_i = \sqrt{\lambda_i}$

---

## ⚠️ Ce que tu dois savoir par cœur

**Valeurs singulières :**
$$\sigma_i = \sqrt{\lambda_i(X^T X)}$$

**Propriété des polynômes de Lagrange** (indispensable ici) :
$$l_j(x_i) = \begin{cases} 1 & \text{si } i = j \\ 0 & \text{si } i \neq j \end{cases}$$

**Développement d'un déterminant $3\times3$ selon la première ligne :**
$$\det\begin{bmatrix} a & b & c \\ d & e & f \\ g & h & k \end{bmatrix} = a(ek - fh) - b(dk - fg) + c(dh - eg)$$

---

*Fiche préparée pour l'examen INFO-F-205 — Exercice 14 (chapitre Interpolation) — Dernier exo Interpolation !*