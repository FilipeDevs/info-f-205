# 📘 Fiche d'étude — Exercice 18 : EDO
## Vérification de deux solutions, Lipschitz, Euler implicite avec équation quadratique en $\sqrt{y}$

---

## 🧠 Rappel théorie utile

Tout est dans les fiches précédentes. Cet exercice combine :
- Vérification de solution (exos 14/15/16)
- Lipschitz et unicité (exos 14/15)
- Euler implicite → équation quadratique (exo 16)

La nouveauté ici : l'équation quadratique se pose en $\sqrt{\hat{y}_{n+1}}$ et non en $\hat{y}_{n+1}$ directement.

---

## 🔢 L'exercice 18 — Énoncé

> Considérer l'EDO $y'(t) = 3\sqrt{y(t)} - t$ avec la condition initiale $y(0) = 0$.
>
> **(a)** Vérifier que les deux fonctions $y(t) = t^2$ et $y(t) = t^2/4$ sont des solutions du problème aux valeurs initiales.
>
> **(b)** Expliquer pourquoi ce problème aux valeurs initiales admet deux solutions.
>
> **(c)** Écrire la formule d'Euler rétrograde (implicite) pour la résolution numérique du problème.

---

## 🧩 Résolution complète — étape par étape

---

### Partie (a) — Vérifier que $y(t) = t^2$ et $y(t) = t^2/4$ sont solutions

L'EDO est $y'(t) = 3\sqrt{y(t)} - t$, donc $f(t, y) = 3\sqrt{y} - t$.

Pour vérifier une solution, on fait toujours deux choses :
1. Calculer $y'(t)$ et $f(t, y(t))$ séparément
2. Vérifier que $y'(t) = f(t, y(t))$
3. Vérifier la condition initiale $y(0) = 0$

---

#### Vérification de $y(t) = t^2$

**Étape 1 — Calculer $y'(t)$**

On dérive $y(t) = t^2$ :

$$y'(t) = 2t$$

**Étape 2 — Calculer $f(t, y(t)) = 3\sqrt{y(t)} - t$**

On remplace $y(t) = t^2$ :

$$f(t, y(t)) = 3\sqrt{t^2} - t = 3|t| - t$$

Pour $t \geq 0$ : $|t| = t$, donc $f = 3t - t = 2t$.

$$f(t, y(t)) = 2t$$

**Étape 3 — Comparer**

$$y'(t) = 2t = f(t, y(t)) \quad \checkmark \; ✅$$

**Étape 4 — Vérifier la condition initiale**

$$y(0) = 0^2 = 0 \quad \checkmark \; ✅$$

$y(t) = t^2$ est bien solution. ✅

---

#### Vérification de $y(t) = t^2/4$

**Étape 1 — Calculer $y'(t)$**

On dérive $y(t) = \dfrac{t^2}{4}$ :

$$y'(t) = \frac{2t}{4} = \frac{t}{2}$$

**Étape 2 — Calculer $f(t, y(t)) = 3\sqrt{y(t)} - t$**

On remplace $y(t) = t^2/4$ :

$$f(t, y(t)) = 3\sqrt{\frac{t^2}{4}} - t = 3 \cdot \frac{|t|}{2} - t$$

Pour $t \geq 0$ : $|t| = t$, donc :

$$f(t, y(t)) = \frac{3t}{2} - t = \frac{3t}{2} - \frac{2t}{2} = \frac{t}{2}$$

**Étape 3 — Comparer**

$$y'(t) = \frac{t}{2} = f(t, y(t)) \quad \checkmark \; ✅$$

**Étape 4 — Vérifier la condition initiale**

$$y(0) = \frac{0^2}{4} = 0 \quad \checkmark \; ✅$$

$y(t) = t^2/4$ est bien solution. ✅

---

**Conclusion de (a) :** Les deux fonctions $t^2$ et $t^2/4$ vérifient l'EDO **et** la condition initiale. Il y a donc bien **deux solutions** distinctes.

---

### Partie (b) — Pourquoi deux solutions ? → Lipschitz

**Étape 1 — Identifier $f(t, y)$**

$$f(t, y) = 3\sqrt{y} - t$$

**Étape 2 — Calculer $\dfrac{\partial f}{\partial y}$**

Le terme $-t$ ne dépend pas de $y$ → sa dérivée par rapport à $y$ est $0$.

Pour $3\sqrt{y} = 3y^{1/2}$ :

$$\frac{\partial}{\partial y}(3y^{1/2}) = 3 \cdot \frac{1}{2}y^{-1/2} = \frac{3}{2\sqrt{y}}$$

Donc :

$$\frac{\partial f}{\partial y} = \frac{3}{2\sqrt{y}}$$

**Étape 3 — Vérifier si c'est borné**

$$\left|\frac{\partial f}{\partial y}\right| = \frac{3}{2\sqrt{y}}$$

Quand $y \to 0$, $\sqrt{y} \to 0$, donc $\dfrac{1}{\sqrt{y}} \to \infty$.

La dérivée **n'est pas bornée en $y = 0$** → Lipschitz **n'est pas satisfaite** en $y = 0$.

---

**Étape 4 — Confirmation par la définition de Lipschitz**

Le correctif montre une façon plus directe de vérifier que Lipschitz échoue, en utilisant la définition même. La condition de Lipschitz dit :

$$|f(t, y_1) - f(t, y_2)| \leq L \cdot |y_1 - y_2|$$

Ici, avec $f(t,y) = 3\sqrt{y} - t$ :

$$|f(t, y_1) - f(t, y_2)| = 3|\sqrt{y_1} - \sqrt{y_2}|$$

On utilise l'identité algébrique suivante (le correctif l'utilise) :

$$\sqrt{y_1} - \sqrt{y_2} = \frac{y_1 - y_2}{\sqrt{y_1} + \sqrt{y_2}}$$

> 💡 **D'où vient cette identité ?** On multiplie et divise par $\sqrt{y_1} + \sqrt{y_2}$ — c'est la même astuce que $(a-b)(a+b) = a^2 - b^2$, ici utilisée à l'envers.

Donc :

$$3|\sqrt{y_1} - \sqrt{y_2}| = \frac{3|y_1 - y_2|}{|\sqrt{y_1} + \sqrt{y_2}|}$$

Pour que Lipschitz soit satisfaite, il faudrait que $\dfrac{3}{|\sqrt{y_1} + \sqrt{y_2}|}$ soit borné par une constante $L$. Mais quand $y_1, y_2 \to 0$, le dénominateur $\sqrt{y_1} + \sqrt{y_2} \to 0$, donc le rapport $\to \infty$.

Il est **impossible** de trouver une constante $L$ qui borne cela autour de $y = 0$.

**Conclusion :** Lipschitz **échoue en $y = 0$** → la solution n'est pas unique pour $y_0 = 0$ ❌. C'est pourquoi les deux solutions $t^2$ et $t^2/4$ sont toutes les deux valides.

---

### Partie (c) — Formule d'Euler rétrograde (implicite)

**Étape 1 — Écrire la formule générale**

$$\hat{y}_{n+1} = \hat{y}_n + h \cdot f(t_{n+1},\ \hat{y}_{n+1})$$

**Étape 2 — Remplacer $f(t, y) = 3\sqrt{y} - t$**

$$\hat{y}_{n+1} = \hat{y}_n + h\left(3\sqrt{\hat{y}_{n+1}} - t_{n+1}\right)$$

$$\hat{y}_{n+1} = \hat{y}_n + 3h\sqrt{\hat{y}_{n+1}} - h\,t_{n+1}$$

> ⚠️ **Ici, $\hat{y}_{n+1}$ apparaît sous une racine carrée à droite.** Si on pose $u = \sqrt{\hat{y}_{n+1}}$, alors $\hat{y}_{n+1} = u^2$ et l'équation devient une équation quadratique **en $u$** :

**Étape 3 — Substitution $u = \sqrt{\hat{y}_{n+1}}$**

On remplace $\hat{y}_{n+1} = u^2$ et $\sqrt{\hat{y}_{n+1}} = u$ :

$$u^2 = \hat{y}_n + 3hu - h\,t_{n+1}$$

On déplace tout d'un côté :

$$u^2 - 3hu - (\hat{y}_n - h\,t_{n+1}) = 0$$

C'est une équation quadratique en $u$ avec :
- $a = 1$
- $b = -3h$
- $c = -(\hat{y}_n - h\,t_{n+1}) = h\,t_{n+1} - \hat{y}_n$

**Étape 4 — Appliquer la formule quadratique**

$$u = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a} = \frac{3h \pm \sqrt{9h^2 + 4(\hat{y}_n - h\,t_{n+1})}}{2}$$

Et donc $\hat{y}_{n+1} = u^2$.

**La formule d'Euler implicite est donc :**

$$\boxed{\hat{y}_{n+1} = \hat{y}_n + h\left(3\sqrt{\hat{y}_{n+1}} - t_{n+1}\right)}$$

> 💡 L'énoncé ne demande pas de développer — on laisse la formule telle quelle avec $\sqrt{\hat{y}_{n+1}}$ des deux côtés. Le correctif montre cependant qu'en posant $u = \sqrt{\hat{y}_{n+1}}$, on obtient une équation quadratique en $u$.

---

## 🆚 Comparaison des trois cas d'Euler implicite vus dans le chapitre

| Exercice | $f(t,y)$ | Euler implicite mène à... |
|---|---|---|
| Exo 14 | $\dfrac{t}{(1+t^2)y}$ | Équation quadratique en $\hat{y}_{n+1}$ |
| Exo 15 | $\dfrac{4t}{1+t^2}\sqrt{y}$ | Équation non-linéaire en $\hat{y}_{n+1}$ |
| Exo 16 | $r\lambda t^{r-1}y^2$ | Équation quadratique en $\hat{y}_{n+1}$ → formule explicite |
| **Exo 18** | $3\sqrt{y} - t$ | Équation quadratique **en $\sqrt{\hat{y}_{n+1}}$** → substitution $u = \sqrt{\hat{y}_{n+1}}$ |

---

## 🍳 La recette / le modèle à retenir

### Pour vérifier deux solutions d'une même EDO :
1. Calculer $y'(t)$ pour **chacune** séparément
2. Calculer $f(t, y(t))$ pour **chacune** séparément
3. Vérifier $y'(t) = f(t, y(t))$ pour chacune ✅
4. Vérifier $y(t_0) = y_0$ pour chacune ✅

### Pour Lipschitz avec une racine carrée :
- L'astuce clé : $\sqrt{y_1} - \sqrt{y_2} = \dfrac{y_1 - y_2}{\sqrt{y_1} + \sqrt{y_2}}$ → le dénominateur $\to 0$ quand $y_1, y_2 \to 0$ → Lipschitz échoue

### Pour Euler implicite avec $\sqrt{\hat{y}_{n+1}}$ :
1. Écrire la formule implicite
2. Poser $u = \sqrt{\hat{y}_{n+1}}$ (donc $\hat{y}_{n+1} = u^2$)
3. Obtenir une équation quadratique en $u$
4. Résoudre avec la formule quadratique → $u$ → $\hat{y}_{n+1} = u^2$

---

## ⚠️ Ce que tu dois savoir par cœur

**Identité algébrique clé (pour Lipschitz avec racine) :**
$$\sqrt{y_1} - \sqrt{y_2} = \frac{y_1 - y_2}{\sqrt{y_1} + \sqrt{y_2}}$$

**Euler implicite général :**
$$\hat{y}_{n+1} = \hat{y}_n + h \cdot f(t_{n+1},\ \hat{y}_{n+1})$$

**Formule quadratique :**
$$ax^2 + bx + c = 0 \implies x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$$

**Règle d'or Lipschitz + racine carrée :** $f$ contient $\sqrt{y}$ → Lipschitz échoue en $y = 0$ → solution non unique pour $y_0 = 0$.

---

*Fiche préparée pour l'examen INFO-F-205 — Exercice 18 (chapitre EDO) — Dernier exo EDO !*