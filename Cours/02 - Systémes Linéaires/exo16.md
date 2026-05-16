# 📘 Fiche d'étude — Exercice 16 : Systèmes Linéaires

## Norme matricielle — Vérifier la convergence sans calculer les valeurs propres

---

## 🧠 Théorie à comprendre (et à retenir !)

### Rappel rapide : la convergence d'une méthode itérative

On l'a vu à l'exercice 14 : une méthode $x^{(k+1)} = Bx^{(k)} + f$ converge si et seulement si $\rho(B) < 1$ (le rayon spectral de $B$).

**Problème :** calculer les valeurs propres d'une grande matrice est coûteux et compliqué. Est-ce qu'il existe un raccourci ?

**Oui !** On peut utiliser une **norme matricielle**.

---

### C'est quoi une norme matricielle ?

Une norme d'une matrice $A$, notée $\|A\|$, est un **nombre qui mesure la "taille" de la matrice** — comme une valeur absolue pour les matrices.

Il en existe plusieurs. Celle de l'exercice est la **norme 1**, notée $\|A\|_1$.

---

### La norme 1 d'une matrice : $\|A\|_1$

**La règle :**

$$\|A\|_1 = \max_{j} \sum_{i} |a_{ij}|$$

En français : on **additionne les valeurs absolues de chaque colonne**, et on prend le **maximum** parmi tous ces totaux.

> 💡 **Moyen mnémotechnique :** norme **1** → somme des colonnes (c'est l'inverse de ce qu'on pourrait croire, mais retenez : **1 = colonnes**).

**Exemple avec une matrice $3 \times 3$ :**

$$A = \begin{bmatrix} 2 & -3 & 1 \\ -1 & 4 & -2 \\ 5 & 0 & 3 \end{bmatrix}$$

- Colonne 1 : $|2| + |-1| + |5| = 2 + 1 + 5 = 8$
- Colonne 2 : $|-3| + |4| + |0| = 3 + 4 + 0 = 7$
- Colonne 3 : $|1| + |-2| + |3| = 1 + 2 + 3 = 6$

$\|A\|_1 = \max(8, 7, 6) = 8$

---

### Pourquoi la norme permet de tester la convergence ?

Il y a une propriété fondamentale (dans le formulaire) :

$$\rho(B) \leq \|B\|$$

En clair : le rayon spectral de $B$ est **toujours inférieur ou égal** à n'importe quelle norme de $B$.

Donc si on trouve $\|B\|_1 < 1$, on sait automatiquement que $\rho(B) \leq \|B\|_1 < 1$, et donc **la méthode converge** !

> 💡 **C'est un raccourci puissant :** plutôt que de calculer les valeurs propres (compliqué), on calcule juste une somme de colonnes (facile) et on vérifie si c'est $< 1$.

> ⚠️ **Attention :** la réciproque n'est pas vraie. Si $\|B\|_1 \geq 1$, on ne peut pas conclure que ça diverge — ça peut quand même converger. La norme donne une **condition suffisante** (pas nécessaire) de convergence.

---

### Comment dériver une itération par consistance ?

On part d'un système $Ax = b$ et on cherche à écrire une itération $x^{(k+1)} = Bx^{(k)} + f$ **consistante** avec la matrice $B$ qu'on nous donne.

La méthode :
1. On part de $Ax = b$
2. On manipule algébriquement pour isoler $x$ du côté gauche, et faire apparaître $B$ du côté droit
3. On lit $B$ et $f$ dans l'expression obtenue

---

## 🔢 L'exercice 16 — Énoncé

> Considérer la matrice :
> $$A = \frac{1}{100} \begin{bmatrix} 25 & 2 & 3 \\ 4 & 50 & 6 \\ 7 & 8 & 75 \end{bmatrix}$$
> et la matrice d'itération $B = I - A$.
>
> **(a)** Écrire la formule d'une étape de l'itération (avec deuxième membre $\vec{b}$), en imposant la consistance.
>
> **(b)** Calculer $\|B\|_1$ pour examiner la convergence des itérations.

---

## 🧩 Résolution complète — étape par étape

---

### Partie (a) — Trouver la formule d'itération par consistance

**Objectif :** On nous donne $B = I - A$. On veut trouver une itération $x^{(k+1)} = Bx^{(k)} + f$ qui soit consistante, c'est-à-dire que la vraie solution de $Ax = b$ soit aussi un point fixe de l'itération.

**Étape 1 — Partir de $Ax = b$ et faire apparaître $B = I - A$**

On sait que $B = I - A$, donc $A = I - B$. On peut réécrire $Ax = b$ comme :

$$Ax = b \iff (I - B)x = b$$

On développe $(I - B)x$ :

$$Ix - Bx = b$$

$$x - Bx = b$$

**Étape 2 — Isoler $x$ tout seul à gauche**

On veut $x = \ldots$, donc on déplace $Bx$ de l'autre côté :

$$x = b + Bx$$

**Étape 3 — Lire l'itération**

On a maintenant $x = Bx + b$, ce qui donne directement la formule d'itération :

$$\boxed{x^{(k+1)} = B \cdot x^{(k)} + \vec{b}}$$

avec $B = I - A$ et $f = \vec{b}$.

**Vérification de la consistance :** si $x^*$ est la vraie solution ($Ax^* = b$), est-ce que $x^* = Bx^* + b$ ? On vient de montrer que $x = b + Bx$ est équivalent à $Ax = b$, donc oui ✅.

---

### Partie (b) — Calculer $\|B\|_1$

**Étape 1 — Calculer la matrice $B = I - A$**

On a :
$$A = \frac{1}{100} \begin{bmatrix} 25 & 2 & 3 \\ 4 & 50 & 6 \\ 7 & 8 & 75 \end{bmatrix}$$

et $I$ est la matrice identité :

$$I = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix} = \frac{1}{100}\begin{bmatrix} 100 & 0 & 0 \\ 0 & 100 & 0 \\ 0 & 0 & 100 \end{bmatrix}$$

Donc :

$$B = I - A = \frac{1}{100}\begin{bmatrix} 100 & 0 & 0 \\ 0 & 100 & 0 \\ 0 & 0 & 100 \end{bmatrix} - \frac{1}{100}\begin{bmatrix} 25 & 2 & 3 \\ 4 & 50 & 6 \\ 7 & 8 & 75 \end{bmatrix}$$

On soustrait terme à terme (en gardant le facteur $\frac{1}{100}$ devant) :

$$B = \frac{1}{100}\begin{bmatrix} 100-25 & 0-2 & 0-3 \\ 0-4 & 100-50 & 0-6 \\ 0-7 & 0-8 & 100-75 \end{bmatrix} = \frac{1}{100}\begin{bmatrix} 75 & -2 & -3 \\ -4 & 50 & -6 \\ -7 & -8 & 25 \end{bmatrix}$$

**Étape 2 — Calculer la somme en valeur absolue de chaque colonne**

Pour calculer $\|B\|_1$, on prend chaque colonne, on passe tout en valeur absolue (les signes négatifs deviennent positifs), et on additionne.

**Colonne 1 :**
$$\frac{1}{100}(|75| + |-4| + |-7|) = \frac{1}{100}(75 + 4 + 7) = \frac{86}{100} = 0{,}86$$

**Colonne 2 :**
$$\frac{1}{100}(|-2| + |50| + |-8|) = \frac{1}{100}(2 + 50 + 8) = \frac{60}{100} = 0{,}60$$

**Colonne 3 :**
$$\frac{1}{100}(|-3| + |-6| + |25|) = \frac{1}{100}(3 + 6 + 25) = \frac{34}{100} = 0{,}34$$

**Étape 3 — Prendre le maximum**

$$\|B\|_1 = \max(0{,}86 \;;\; 0{,}60 \;;\; 0{,}34) = 0{,}86$$

**Étape 4 — Conclure sur la convergence**

On a $\|B\|_1 = 0{,}86 < 1$.

Puisque $\rho(B) \leq \|B\|_1 = 0{,}86 < 1$, on conclut que le rayon spectral est strictement inférieur à 1.

**Conclusion :** Les itérations $x^{(k+1)} = Bx^{(k)} + \vec{b}$ **convergent** ✅.

---

## 🍳 La recette / le modèle à retenir

### Pour dériver une itération consistante à partir d'une matrice $B$ donnée :

1. Écrire $B = I - A$ (ou autre relation donnée dans l'énoncé)
2. Réécrire $Ax = b$ en faisant apparaître $B$ : $(I - B)x = b$
3. Développer et isoler $x$ : $x = b + Bx$
4. Lire l'itération : $x^{(k+1)} = Bx^{(k)} + \vec{b}$

### Pour calculer $\|B\|_1$ et tester la convergence :

1. **Calculer $B$** explicitement (faire la soustraction de matrices)
2. **Pour chaque colonne** : additionner les valeurs absolues de tous les éléments
3. **Prendre le maximum** parmi tous ces totaux de colonnes
4. **Conclure :**
   - Si $\|B\|_1 < 1$ → $\rho(B) < 1$ → **converge** ✅
   - Si $\|B\|_1 \geq 1$ → on ne peut pas conclure (il faut calculer les valeurs propres)

---

## ⚠️ Ce que tu dois savoir par cœur (du formulaire)

**La norme 1 d'une matrice** (dans le formulaire, section 3) :

$$\|A\|_1 = \max_{j} \sum_{i} |a_{ij}| \quad \text{(max des sommes de colonnes en valeur absolue)}$$

**La relation norme / rayon spectral :**

$$\rho(B) \leq \|B\| \quad \text{(pour n'importe quelle norme)}$$

Donc : $\|B\|_1 < 1 \implies \rho(B) < 1 \implies$ **convergence** ✅

> 💡 **À retenir :** norme **1** = sommes de **colonnes** (en valeur absolue) → on prend le **max**.

---

*Fiche préparée pour l'examen INFO-F-205 — Exercice 16 sur 18 (chapitre Systèmes Linéaires)*