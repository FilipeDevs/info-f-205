# 📘 Fiche d'étude — Exercice 14 : Systèmes Linéaires
## Méthodes itératives — Consistance & Convergence


## 🧠 Théorie à comprendre (et à retenir !)

### C'est quoi une méthode itérative ?

Au lieu de résoudre $Ax = b$ d'un coup (méthode directe comme Gauss), une **méthode itérative** part d'une approximation initiale $x^{(0)}$ et l'améliore à chaque étape :

$$x^{(k+1)} = B \cdot x^{(k)} + f$$

- $B$ s'appelle la **matrice d'itération**
- $f$ est un vecteur constant
- On répète jusqu'à ce que ça converge vers la vraie solution $x^*$

> 💡 **Analogie** : C'est comme affiner une estimation à tâtons. Tu commences avec une valeur au pif, et à chaque tour de boucle tu te rapproches de la bonne réponse.

---

### ✅ Consistance — c'est quoi ?

Une méthode est **consistante** si, quand on branche la vraie solution $x^*$ dans la formule, ça tombe juste. Autrement dit :

$$x^* = B \cdot x^* + f$$

> 💡 **En clair** : la vraie solution doit être un **point fixe** de l'itération — si on repart de la solution, on doit retrouver la solution.

**Comment vérifier la consistance ?** On injecte $x^* = x$ (la vraie solution) dans la formule et on vérifie que l'égalité est respectée.

---

### 📉 Convergence — c'est quoi ?

La méthode converge si, quelle que soit la valeur de départ $x^{(0)}$, la suite $x^{(k)}$ tend vers $x^*$ quand $k \to \infty$.

**La règle d'or :**

$$\text{Convergence} \iff \rho(B) < 1$$

où $\rho(B)$ est le **rayon spectral** de $B$, c'est-à-dire la **valeur absolue maximale parmi toutes les valeurs propres** de $B$.

$$\rho(B) = \max_{\lambda \in \sigma(B)} |\lambda|$$

> 💡 **En clair** : si la "valeur propre la plus grande" (en valeur absolue) de $B$ est strictement inférieure à 1, la méthode converge. Sinon, elle diverge.

**Comment trouver les valeurs propres $\lambda$ de $B$ ?**

On résout :
$$\det(B - \lambda I) = 0$$

C'est l'**équation caractéristique**. Pour une matrice $2 \times 2$, ça donne un polynôme du second degré en $\lambda$.

---

### 📋 Formules du formulaire à connaître

Du formulaire officiel (section **3. Systèmes Linéaires**) :

| Méthode | Matrice d'itération $B$ |
|--------|--------------------------|
| Jacobi | $B_J = D^{-1}(D - A)$, avec $f = D^{-1}b$ |
| Gauss-Seidel | $B_{GS} = (D-E)^{-1}F$ |
| **Générale** | $x^{(k+1)} = Bx^{(k)} + f$ |

**Convergence** (à retenir !) :
$$\lim_{k \to \infty} B^k = 0 \iff \rho(B) < 1$$

---

## 🔢 L'exercice 14 — énoncé

> Considérer le système linéaire $Ax = b$ et les itérations :
> $$x^{(k+1)} = (\alpha A + I)x^{(k)} - \alpha b$$
> où $I$ est la matrice d'identité.
>
> **(a)** Montrer la consistance des itérations.
>
> **(b)** Prendre $A = \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix}$ et examiner la convergence en fonction de $\alpha$. Quelle est la conclusion ?

---

## 🧩 Résolution complète — étape par étape

---

### Partie (a) — Vérifier la consistance

**Objectif :** Montrer que si $x$ est la vraie solution de $Ax = b$, alors elle vérifie aussi $x = (\alpha A + I)x - \alpha b$.

**Étape 1 — Identifier $B$ et $f$**

On met l'itération sous la forme standard $x^{(k+1)} = B \cdot x^{(k)} + f$ :

$$x^{(k+1)} = \underbrace{(\alpha A + I)}_{B} \cdot x^{(k)} + \underbrace{(-\alpha b)}_{f}$$

Donc : $B = \alpha A + I$ et $f = -\alpha b$.

**Étape 2 — Injecter la vraie solution**

On suppose que $x$ est la vraie solution, donc $Ax = b$. On veut vérifier que :

$$x = (\alpha A + I)x - \alpha b$$

On développe le membre de droite :

$$(\alpha A + I)x - \alpha b = \alpha A x + I x - \alpha b = \alpha A x + x - \alpha b$$

Puisque $Ax = b$, on remplace $Ax$ par $b$ :

$$= \alpha b + x - \alpha b = x \checkmark$$

**Conclusion :** L'égalité est vérifiée. La méthode est **consistante** ✅.

---

### Partie (b) — Étudier la convergence en fonction de $\alpha$

**Avec :**
$$A = \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix}$$

**Étape 1 — Écrire la matrice d'itération $B$**

$$B = \alpha A + I = \alpha \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix} + \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} = \begin{bmatrix} \alpha + 1 & 2\alpha \\ 3\alpha & 4\alpha + 1 \end{bmatrix}$$

**Étape 2 — Trouver les valeurs propres de $B$**

La condition de convergence est $\rho(B) < 1$, donc on doit trouver les valeurs propres $\lambda$ telles que $\det(B - \lambda I) = 0$.

On calcule $B - \lambda I$ :

$$B - \lambda I = \begin{bmatrix} \alpha + 1 - \lambda & 2\alpha \\ 3\alpha & 4\alpha + 1 - \lambda \end{bmatrix}$$

Le déterminant d'une matrice $2 \times 2$ : $\det\begin{bmatrix} a & b \\ c & d \end{bmatrix} = ad - bc$

Donc :
$$\det(B - \lambda I) = (\alpha + 1 - \lambda)(4\alpha + 1 - \lambda) - (2\alpha)(3\alpha)$$

**Étape 3 — Développer le déterminant terme par terme**

On a :
$$\det(B - \lambda I) = (\alpha + 1 - \lambda)(4\alpha + 1 - \lambda) - (2\alpha)(3\alpha) = 0$$

Pour développer $(\alpha + 1 - \lambda)(4\alpha + 1 - \lambda)$, on multiplie **chaque terme du premier bloc** par **chaque terme du second bloc**. C'est exactement comme développer $(a)(b)$ avec $a = \alpha + 1 - \lambda$ et $b = 4\alpha + 1 - \lambda$ :

$$(\alpha + 1 - \lambda) \times (4\alpha + 1 - \lambda)$$

On distribue le premier bloc sur chaque terme du second :

| Multiplication | Résultat |
|---|---|
| $(\alpha) \times (4\alpha)$ | $4\alpha^2$ |
| $(\alpha) \times (1)$ | $\alpha$ |
| $(\alpha) \times (-\lambda)$ | $-\alpha\lambda$ |
| $(1) \times (4\alpha)$ | $4\alpha$ |
| $(1) \times (1)$ | $1$ |
| $(1) \times (-\lambda)$ | $-\lambda$ |
| $(-\lambda) \times (4\alpha)$ | $-4\alpha\lambda$ |
| $(-\lambda) \times (1)$ | $-\lambda$ |
| $(-\lambda) \times (-\lambda)$ | $+\lambda^2$ |

On regroupe tout :

$$= 4\alpha^2 + \alpha - \alpha\lambda + 4\alpha + 1 - \lambda - 4\alpha\lambda - \lambda + \lambda^2$$

On rassemble les termes **sans $\lambda$**, les termes **avec $\lambda$**, et ceux **avec $\lambda^2$** :

- Termes sans $\lambda$ : $4\alpha^2 + \alpha + 4\alpha + 1 = 4\alpha^2 + 5\alpha + 1$
- Termes avec $\lambda$ : $-\alpha\lambda - \lambda - 4\alpha\lambda - \lambda = -(5\alpha + 2)\lambda$
- Terme avec $\lambda^2$ : $+\lambda^2$

Donc :

$$(\alpha + 1 - \lambda)(4\alpha + 1 - \lambda) = \lambda^2 - (5\alpha + 2)\lambda + 4\alpha^2 + 5\alpha + 1$$

Maintenant on soustrait $(2\alpha)(3\alpha) = 6\alpha^2$ :

$$\det(B - \lambda I) = \lambda^2 - (5\alpha + 2)\lambda + 4\alpha^2 + 5\alpha + 1 - 6\alpha^2$$

$$= \lambda^2 - (5\alpha + 2)\lambda + (-2\alpha^2 + 5\alpha + 1) = 0$$

**Étape 4 — Résoudre pour $\lambda$ avec la formule quadratique**

On a un polynôme du second degré en $\lambda$ :

$$\underbrace{1}_{a}\lambda^2 \underbrace{- (5\alpha + 2)}_{b}\lambda + \underbrace{(-2\alpha^2 + 5\alpha + 1)}_{c} = 0$$

La formule quadratique dit : $\lambda = \dfrac{-b \pm \sqrt{b^2 - 4ac}}{2a}$

Ici : $a = 1$, $b = -(5\alpha+2)$, $c = -2\alpha^2 + 5\alpha + 1$

Donc $-b = +(5\alpha + 2)$ et :

$$\lambda = \frac{(5\alpha+2) \pm \sqrt{\Delta}}{2}$$

**Calcul du discriminant $\Delta = b^2 - 4ac$ :**

$$\Delta = \bigl(-(5\alpha+2)\bigr)^2 - 4 \cdot 1 \cdot (-2\alpha^2 + 5\alpha + 1)$$

**Calcul de $(5\alpha+2)^2$ :**

$$(5\alpha+2)^2 = (5\alpha)^2 + 2 \cdot (5\alpha) \cdot 2 + 2^2 = 25\alpha^2 + 20\alpha + 4$$

**Calcul de $-4 \cdot 1 \cdot (-2\alpha^2 + 5\alpha + 1)$ :**

$$-4 \times (-2\alpha^2 + 5\alpha + 1) = +8\alpha^2 - 20\alpha - 4$$

**On additionne les deux :**

$$\Delta = 25\alpha^2 + 20\alpha + 4 + 8\alpha^2 - 20\alpha - 4$$

Les $+20\alpha$ et $-20\alpha$ s'annulent, les $+4$ et $-4$ s'annulent :

$$\Delta = 33\alpha^2$$

**Racine carrée du discriminant :**

$$\sqrt{\Delta} = \sqrt{33\alpha^2} = \sqrt{33} \cdot |\alpha|$$

> 💡 On a $\sqrt{\alpha^2} = |\alpha|$ (valeur absolue), pas $\alpha$, car $\alpha$ peut être négatif.

**Les deux valeurs propres :**

$$\lambda = \frac{(5\alpha+2) \pm \sqrt{33}\,|\alpha|}{2}$$

**Étape 5 — Simplifier et interpréter**

En développant la fraction (on suppose $\alpha > 0$ pour simplifier, donc $|\alpha| = \alpha$) :

$$\lambda_{1,2} = \frac{5\alpha + 2 \pm \sqrt{33}\,\alpha}{2} = \frac{2}{2} + \frac{(5 \pm \sqrt{33})\,\alpha}{2} = 1 + \frac{5 \pm \sqrt{33}}{2}\,\alpha$$

On sait que $\sqrt{33} \approx 5{,}745$. Donc :

$$\lambda_1 = 1 + \frac{5 + 5{,}745}{2}\,\alpha = 1 + \frac{10{,}745}{2}\,\alpha \approx 1 + 5{,}37\,\alpha$$

$$\lambda_2 = 1 + \frac{5 - 5{,}745}{2}\,\alpha = 1 + \frac{-0{,}745}{2}\,\alpha \approx 1 - 0{,}37\,\alpha$$

Ces deux valeurs propres sont des **fonctions linéaires de $\alpha$**, c'est-à-dire deux droites :
- $\lambda_1$ : droite de pente $+5{,}37$ → **monte** quand $\alpha$ augmente
- $\lambda_2$ : droite de pente $-0{,}37$ → **descend** quand $\alpha$ augmente
- Pour $\alpha = 0$ : $\lambda_1 = \lambda_2 = 1$ → elles se croisent au point $(0,\ 1)$

**Étape 6 — Tester la condition de convergence**

Pour converger, il faut **les deux conditions en même temps** :

$$|\lambda_1| < 1 \quad \text{ET} \quad |\lambda_2| < 1$$

Examinons chaque cas :

**Cas $\alpha = 0$ :** $\lambda_1 = \lambda_2 = 1$. On a $|1| = 1$, ce n'est pas $< 1$. → ❌

**Cas $\alpha > 0$ :** $\lambda_1 = 1 + 5{,}37\alpha > 1$ car on ajoute quelque chose de positif. → $|\lambda_1| > 1$ ❌

**Cas $\alpha < 0$ :** $\lambda_2 = 1 - 0{,}37\alpha$. Comme $\alpha < 0$, on a $-0{,}37\alpha > 0$, donc $\lambda_2 = 1 + \text{(positif)} > 1$. → $|\lambda_2| > 1$ ❌

Dans tous les cas, **au moins une valeur propre est toujours $\geq 1$ en valeur absolue**.

**Conclusion :** La méthode $x^{(k+1)} = (\alpha A + I)x^{(k)} - \alpha b$ **ne converge jamais**, quelle que soit la valeur de $\alpha$ ❌.

---

## 🍳 La recette / le modèle à retenir

Pour tout exercice sur la **consistance et convergence d'une méthode itérative** :

### Étape 1 — Identifier $B$ et $f$
Mettre sous la forme $x^{(k+1)} = B \cdot x^{(k)} + f$.

### Étape 2 — Vérifier la consistance
Injecter la vraie solution $x^*$ (avec $Ax^* = b$) dans l'itération et vérifier que $x^* = Bx^* + f$. Si oui → consistante.

### Étape 3 — Trouver les valeurs propres de $B$
Résoudre $\det(B - \lambda I) = 0$.

- Pour une $2\times2$ : développer le déterminant → polynôme du 2e degré → formule quadratique.
- Pour une $3\times3$ : développer selon la première ligne (ou la méthode des cofacteurs).

### Étape 4 — Calculer le rayon spectral $\rho(B) = \max|\lambda_i|$

### Étape 5 — Conclure
- $\rho(B) < 1$ → **converge** ✅
- $\rho(B) \geq 1$ → **ne converge pas** ❌

---

## ⚠️ Ce que tu dois savoir par cœur (du formulaire)

1. **Forme standard d'une méthode itérative :**
$$x^{(k+1)} = Bx^{(k)} + f$$

2. **Condition de convergence :**
$$\rho(B) < 1 \quad \text{où} \quad \rho(B) = \max_\lambda |\lambda|, \quad \det(B - \lambda I) = 0$$

3. **Déterminant d'une matrice $2\times2$ :**
$$\det\begin{bmatrix} a & b \\ c & d \end{bmatrix} = ad - bc$$

4. **Formule quadratique :**
$$\lambda = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$$

---

*Fiche préparée pour l'examen INFO-F-205 — Exercice 14 sur 18 (chapitre Systèmes Linéaires)*
