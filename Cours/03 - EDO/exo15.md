# 📘 Fiche d'étude — Exercice 15 : EDO

## Vérification de solution, Lipschitz, Euler explicite et implicite (suite)

---

## 🧠 Rappel théorie (exo 14)

Tout ce qu'il faut savoir est dans la fiche de l'exo 14 (rappel dérivées, Lipschitz, Euler). On applique exactement les mêmes outils ici.

---

## 🔢 L'exercice 15 — Énoncé

> Considérer le problème aux valeurs initiales :
> $$y'(t) = \frac{4t}{1+t^2}\sqrt{|y(t)|} \quad \text{avec } y(0) = y_0$$
>
> **(a)** Vérifier que $y(t) = \left[\ln(1+t^2) + \sqrt{y_0}\right]^2$ est une solution, à condition que $y_0 > 0$. Quelle est la solution si $y_0 < 0$ ?
>
> **(b)** La solution est-elle unique, en particulier si $y_0 = 0$ ? Expliquer.
>
> **(c)** Écrire la formule d'Euler **explicite**.
>
> **(d)** Écrire la formule d'Euler **implicite** (sans développer).

---

## 🧩 Résolution complète — étape par étape

---

### Partie (a) — Vérifier que $y(t) = \left[\ln(1+t^2) + \sqrt{y_0}\right]^2$ est solution

**Étape 0 — Identifier $f(t, y)$**

L'EDO est $y'(t) = \dfrac{4t}{1+t^2}\sqrt{|y(t)|}$, donc :

$$f(t, y) = \frac{4t}{1+t^2}\sqrt{|y|}$$

**Étape 1 — Calculer $y'(t)$ en dérivant la solution proposée**

On a $y(t) = \left[\ln(1+t^2) + \sqrt{y_0}\right]^2$.

C'est une fonction de la forme $[u(t)]^2$, où $u(t) = \ln(1+t^2) + \sqrt{y_0}$.

On applique la **règle de la chaîne** :

$$y'(t) = 2 \cdot \left[\ln(1+t^2) + \sqrt{y_0}\right] \cdot \frac{d}{dt}\left[\ln(1+t^2) + \sqrt{y_0}\right]$$

On dérive maintenant le contenu de la dérivée :
- La dérivée de $\ln(1+t^2)$ est $\dfrac{2t}{1+t^2}$ (règle de la chaîne, vue à l'exo 14)
- La dérivée de $\sqrt{y_0}$ est $0$ (c'est une constante, elle ne dépend pas de $t$)

Donc :

$$y'(t) = 2\left[\ln(1+t^2) + \sqrt{y_0}\right] \cdot \frac{2t}{1+t^2}$$

$$y'(t) = \frac{4t}{1+t^2} \cdot \left[\ln(1+t^2) + \sqrt{y_0}\right]$$

**Étape 2 — Relier $y'(t)$ à $\sqrt{y(t)}$**

On remarque que $y(t) = \left[\ln(1+t^2) + \sqrt{y_0}\right]^2$, donc :

$$\sqrt{y(t)} = \sqrt{\left[\ln(1+t^2) + \sqrt{y_0}\right]^2} = \left|\ln(1+t^2) + \sqrt{y_0}\right|$$

Si $y_0 > 0$, alors $\sqrt{y_0} > 0$ et $\ln(1+t^2) \geq 0$ pour tout $t$, donc la quantité entre crochets est positive :

$$\sqrt{y(t)} = \ln(1+t^2) + \sqrt{y_0}$$

On peut donc réécrire $y'(t)$ :

$$y'(t) = \frac{4t}{1+t^2} \cdot \sqrt{y(t)} \quad \checkmark$$

C'est exactement l'EDO de départ. ✅

**Étape 3 — Vérifier la condition initiale $y(0) = y_0$**

On remplace $t = 0$ dans la solution :

$$y(0) = \left[\ln(1 + 0^2) + \sqrt{y_0}\right]^2 = \left[\ln(1) + \sqrt{y_0}\right]^2 = \left[0 + \sqrt{y_0}\right]^2 = (\sqrt{y_0})^2 = y_0 \quad \checkmark$$

La condition initiale est bien satisfaite pour $y_0 > 0$. ✅

---

**Si $y_0 < 0$ ?**

La solution proposée contient $\sqrt{y_0}$, qui n'est pas définie pour $y_0 < 0$ dans les réels. La solution devient alors :

$$y(t) = -\left[\ln(1+t^2) + \sqrt{|y_0|}\right]^2$$

(On prend le signe négatif pour satisfaire $y(0) = y_0 < 0$.)

**Si $y_0 = 0$ :**

Les deux solutions $y(t) = [\ln(1+t^2)]^2$ et $y(t) = -[\ln(1+t^2)]^2$ sont toutes les deux valides → **deux solutions** pour $y_0 = 0$.

---

### Partie (b) — Unicité de la solution

**Étape 1 — Identifier $f(t, y)$ sous forme standard**

En mettant l'EDO sous la forme $y'(t) = f(t, y(t))$ :

$$f(t, y) = \frac{4t}{1+t^2} \cdot \sqrt{|y|}$$

**Étape 2 — Calculer $\dfrac{\partial f}{\partial y}$**

On dérive $f$ par rapport à $y$. Le facteur $\dfrac{4t}{1+t^2}$ ne dépend pas de $y$ — il reste intact. On dérive seulement $\sqrt{|y|}$ :

Pour $y > 0$ : $\sqrt{|y|} = \sqrt{y} = y^{1/2}$, donc sa dérivée est $\dfrac{1}{2}y^{-1/2} = \dfrac{1}{2\sqrt{y}}$

$$\frac{\partial f}{\partial y} = \frac{4t}{1+t^2} \cdot \frac{1}{2\sqrt{y}} = \frac{2t}{(1+t^2)\sqrt{y}}$$

**Étape 3 — Vérifier si c'est borné**

$$\left|\frac{\partial f}{\partial y}\right| = \frac{2|t|}{(1+t^2)\sqrt{|y|}}$$

Quand $y \to 0$, $\sqrt{|y|} \to 0$, donc $\dfrac{1}{\sqrt{|y|}} \to \infty$.

**La dérivée n'est pas bornée en $y = 0$** → Lipschitz **n'est pas satisfaite** en $y = 0$.

**Conclusion :**

- Si $y_0 \neq 0$ : Lipschitz est satisfaite dans le voisinage de $y_0$ → la solution est **unique** ✅
- Si $y_0 = 0$ : Lipschitz **échoue** → la solution n'est **pas unique** ❌ (cohérent avec les deux solutions trouvées en (a))

---

### Partie (c) — Formule d'Euler explicite

La formule générale d'Euler explicite (formulaire) :

$$\hat{y}_{n+1} = \hat{y}_n + h \cdot f(t_n,\ \hat{y}_n)$$

On remplace $f(t, y) = \dfrac{4t}{1+t^2}\sqrt{|y|}$ avec $t = t_n$ et $y = \hat{y}_n$ :

$$\boxed{\hat{y}_{n+1} = \hat{y}_n + h \cdot \frac{4t_n}{1+t_n^2}\sqrt{\hat{y}_n}}$$

> 💡 On utilise $\sqrt{\hat{y}_n}$ directement car si $y_0 > 0$, la solution reste positive — pas besoin de valeur absolue.

---

### Partie (d) — Formule d'Euler implicite (sans développer)

La formule générale d'Euler implicite (formulaire) :

$$\hat{y}_{n+1} = \hat{y}_n + h \cdot f(t_{n+1},\ \hat{y}_{n+1})$$

On remplace $f$ avec $t = t_{n+1}$ et $y = \hat{y}_{n+1}$ :

$$\boxed{\hat{y}_{n+1} = \hat{y}_n + h \cdot \frac{4t_{n+1}}{1+t_{n+1}^2}\sqrt{\hat{y}_{n+1}}}$$

> ⚠️ $\hat{y}_{n+1}$ est présent **des deux côtés**, et notamment sous une racine carrée. En développant, on obtiendrait une équation **non-linéaire** en $\hat{y}_{n+1}$ (plus compliquée qu'une simple équation quadratique). L'énoncé demande de ne **pas** développer.

---

## 🆚 Comparaison exo 14 vs exo 15

Ces deux exercices sont très similaires. Voici les différences clés :

| | Exo 14 | Exo 15 |
|---|---|---|
| **EDO** | $(1+t^2)y'y = t$ | $y' = \dfrac{4t}{1+t^2}\sqrt{\|y\|}$ |
| **Solution** | $\sqrt{\ln(1+t^2) + y_0^2}$ | $\left[\ln(1+t^2) + \sqrt{y_0}\right]^2$ |
| **Forme de la solution** | Racine carrée d'une expression | Carré d'une expression |
| **Technique de vérification** | Dériver $[y(t)]^2$ | Dériver $y(t) = [\ldots]^2$ directement |
| **Lipschitz échoue en** | $y = 0$ ($\partial f/\partial y \propto 1/y^2$) | $y = 0$ ($\partial f/\partial y \propto 1/\sqrt{y}$) |
| **Euler implicite mène à** | Équation quadratique | Équation non-linéaire |

---

## 🍳 La recette / le modèle à retenir

C'est la même recette qu'à l'exo 14 — appliquée à une forme de solution différente :

### Pour vérifier une solution de la forme $y(t) = [g(t)]^2$ :
1. Dériver avec la règle de la chaîne : $y'(t) = 2\,g(t) \cdot g'(t)$
2. Reconnaître que $\sqrt{y(t)} = g(t)$ (si $g(t) > 0$)
3. Réécrire $y'(t)$ en faisant apparaître $\sqrt{y(t)}$ → comparer avec l'EDO
4. Vérifier $y(t_0) = y_0$

### Lipschitz et unicité (même règle qu'exo 14) :
- Calculer $\left|\dfrac{\partial f}{\partial y}\right|$
- Si $\to \infty$ en $y = 0$ → Lipschitz échoue → **non unique** pour $y_0 = 0$

---

## ⚠️ Ce que tu dois savoir par cœur (du formulaire)

Les mêmes formules qu'à l'exo 14 :

**Euler explicite :** $\hat{y}_{n+1} = \hat{y}_n + h \cdot f(t_n,\ \hat{y}_n)$

**Euler implicite :** $\hat{y}_{n+1} = \hat{y}_n + h \cdot f(t_{n+1},\ \hat{y}_{n+1})$

**Condition de Lipschitz :** $\left|\dfrac{\partial f}{\partial y}\right|$ bornée → unique ; non bornée en $y=0$ → non unique pour $y_0 = 0$.

---

*Fiche préparée pour l'examen INFO-F-205 — Exercice 15 (chapitre EDO)*