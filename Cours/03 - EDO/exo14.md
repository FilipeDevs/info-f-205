# 📘 Fiche d'étude — Exercice 14 : EDO
## Vérification de solution, condition de Lipschitz, Euler explicite et implicite

---

## 🧠 Théorie à comprendre (et à retenir !)

> ⚠️ **Nouveau chapitre !** On quitte les systèmes linéaires et on entre dans le monde des **EDO** (Équations Différentielles Ordinaires). Voici tout ce qu'il faut savoir pour démarrer.

---

### C'est quoi une EDO ?

Une EDO est une équation qui implique une **fonction inconnue** $y(t)$ et sa **dérivée** $y'(t)$. La dérivée $y'(t)$ représente la vitesse de variation de $y$.

**Forme générale :**
$$y'(t) = f(t, y(t))$$

> 💡 **Analogie :** Imagine que $y(t)$ est la position d'une voiture à l'instant $t$, et $y'(t)$ est sa vitesse. L'EDO te dit comment la vitesse dépend du temps et de la position. Si tu connais la position de départ (condition initiale), tu peux reconstruire toute la trajectoire.

---

### Le problème aux valeurs initiales (PVI)

Un PVI, c'est une EDO **plus une condition de départ** :

$$\begin{cases} y'(t) = f(t, y(t)) \\ y(t_0) = y_0 \end{cases}$$

- $y_0$ : la **valeur initiale** (ce qu'on sait au départ)
- $t_0$ : le **temps de départ**

> 💡 Reprenant l'analogie : on sait que la voiture part de la position $y_0$ à l'instant $t_0$. L'EDO nous dit comment elle évolue ensuite.

---

### Comment vérifier qu'une fonction est solution d'une EDO ?

C'est comme vérifier qu'un nombre est solution d'une équation. Il faut :

1. **Calculer $y'(t)$** (la dérivée de la solution proposée)
2. **Calculer $f(t, y(t))$** (le membre de droite de l'EDO, en remplaçant $y$ par la solution proposée)
3. **Vérifier que $y'(t) = f(t, y(t))$**
4. **Vérifier la condition initiale** : $y(t_0) = y_0$

Si les deux étapes sont vérifiées, c'est bien une solution.

---

### La condition de Lipschitz — clé pour l'unicité

La **condition de Lipschitz** dit : la fonction $f(t, y)$ est Lipschitz (par rapport à $y$) s'il existe une constante $L$ telle que :

$$|f(t, y_1) - f(t, y_2)| \leq L \cdot |y_1 - y_2|$$

> 💡 **En clair :** Si on change légèrement $y$, $f$ ne change pas de façon explosive — le changement est **borné** par $L$ fois le changement de $y$.

**Pourquoi c'est important ?**

- Si $f$ satisfait Lipschitz → la solution est **unique**
- Si $f$ ne satisfait **pas** Lipschitz (notamment en certains points) → il peut y avoir **plusieurs solutions**

**Astuce pratique pour vérifier Lipschitz :**

Si $f(t, y)$ est dérivable par rapport à $y$, on vérifie que $\left|\dfrac{\partial f}{\partial y}\right|$ est bornée (ne part pas à l'infini). Si elle est bornée, Lipschitz est satisfaite.

> ⚠️ **Point de vigilance :** La condition Lipschitz peut échouer en des **points particuliers** (par exemple $y = 0$). C'est exactement là que des solutions multiples peuvent apparaître.

---

### Les méthodes d'Euler — résoudre numériquement une EDO

Quand on ne peut pas trouver la solution analytique (à la main), on l'approche numériquement en avançant pas par pas avec un **pas** $h$.

#### Euler explicite (= progressif = forward)

$$\boxed{\hat{y}(t + h) = \hat{y}(t) + h \cdot f(t,\ \hat{y}(t))}$$

**Idée :** on utilise la pente **au point actuel** pour estimer où on sera au prochain pas. C'est simple à calculer.

> 💡 **Analogie :** Tu es en voiture et tu regardes ta vitesse **maintenant** pour estimer où tu seras dans 1 minute.

#### Euler implicite (= rétrograde = backward)

$$\boxed{\hat{y}(t + h) = \hat{y}(t) + h \cdot f(t + h,\ \hat{y}(t + h))}$$

**Idée :** on utilise la pente **au point suivant** (qu'on ne connaît pas encore !). C'est plus compliqué car $\hat{y}(t+h)$ apparaît **des deux côtés** — il faut résoudre une équation. Mais cette méthode est plus stable.

> 💡 **Analogie :** Tu estimes où tu seras dans 1 minute en regardant **la vitesse que tu auras à ce moment-là** (pas celle de maintenant). C'est un peu comme conduire en regardant en avant plutôt qu'en regardant le sol sous tes roues.

---

### Notation utile

Dans les formules, on note souvent :
- $\hat{y}_n = \hat{y}(t_n)$ : l'approximation au temps $t_n$
- $t_n = t_0 + n \cdot h$ : le temps après $n$ pas
- $t_{n+1} = t_n + h$ : le temps suivant

---

---

## 📐 Rappel — Les dérivées à maîtriser

> 💡 Cette section est un rappel des règles de dérivation utilisées dans ce chapitre. Garde-la sous la main pour tous les exos EDO !

---

### Les dérivées de base (à savoir par cœur)

| Fonction $f(t)$ | Dérivée $f'(t)$ |
|---|---|
| Constante $c$ | $0$ |
| $t^n$ | $n \cdot t^{n-1}$ |
| $\sqrt{t} = t^{1/2}$ | $\dfrac{1}{2\sqrt{t}}$ |
| $e^t$ | $e^t$ |
| $\ln(t)$ | $\dfrac{1}{t}$ |
| $\sin(t)$ | $\cos(t)$ |
| $\cos(t)$ | $-\sin(t)$ |

---

### La règle de la chaîne (dériver une fonction composée)

C'est la règle la plus importante du chapitre. Quand tu as une fonction **dans** une autre fonction :

$$\frac{d}{dt} f(g(t)) = f'(g(t)) \times g'(t)$$

**En mots :** on dérive la fonction "externe" (en laissant l'intérieur intact), puis on multiplie par la dérivée de l'intérieur.

**Exemples concrets :**

**Exemple 1 — $\ln(1 + t^2)$**

- Fonction externe : $\ln(\ldots)$, dont la dérivée est $\dfrac{1}{\ldots}$
- Intérieur : $1 + t^2$, dont la dérivée est $2t$

$$\frac{d}{dt}\ln(1+t^2) = \frac{1}{1+t^2} \times 2t = \frac{2t}{1+t^2}$$

**Exemple 2 — $[y(t)]^2$**

- Fonction externe : $(\ldots)^2$, dont la dérivée est $2(\ldots)$
- Intérieur : $y(t)$, dont la dérivée est $y'(t)$

$$\frac{d}{dt}[y(t)]^2 = 2\,y(t) \times y'(t)$$

**Exemple 3 — $e^{-t^4}$**

- Fonction externe : $e^{\ldots}$, dont la dérivée est $e^{\ldots}$
- Intérieur : $-t^4$, dont la dérivée est $-4t^3$

$$\frac{d}{dt}e^{-t^4} = e^{-t^4} \times (-4t^3) = -4t^3\,e^{-t^4}$$

**Exemple 4 — $\sqrt{g(t)}$**

- Fonction externe : $\sqrt{\ldots} = (\ldots)^{1/2}$, dont la dérivée est $\dfrac{1}{2\sqrt{\ldots}}$
- Intérieur : $g(t)$, dont la dérivée est $g'(t)$

$$\frac{d}{dt}\sqrt{g(t)} = \frac{g'(t)}{2\sqrt{g(t)}}$$

---

### La règle du produit

Quand tu multiplies deux fonctions :

$$\frac{d}{dt}[u(t) \cdot v(t)] = u'(t) \cdot v(t) + u(t) \cdot v'(t)$$

**Exemple — $t \cdot e^{-t}$**

$$\frac{d}{dt}[t \cdot e^{-t}] = \underbrace{1}_{u'} \cdot e^{-t} + t \cdot \underbrace{(-e^{-t})}_{v'} = e^{-t}(1-t)$$

---

### La règle du quotient

Quand tu divises deux fonctions :

$$\frac{d}{dt}\left[\frac{u(t)}{v(t)}\right] = \frac{u'(t) \cdot v(t) - u(t) \cdot v'(t)}{[v(t)]^2}$$

> 💡 Moyen mnémotechnique : **"dérivée du haut × bas − haut × dérivée du bas, le tout sur le bas au carré"**

---

### La dérivation implicite

Quand on a une équation du type $[y(t)]^2 = g(t)$ et qu'on dérive **les deux membres** par rapport à $t$, on obtient :

$$2\,y(t)\,y'(t) = g'(t)$$

C'est la règle de la chaîne appliquée au membre gauche. On peut ensuite isoler $y'(t)$ :

$$y'(t) = \frac{g'(t)}{2\,y(t)}$$

---

## 🔢 L'exercice 14 — Énoncé

> Considérer le problème aux valeurs initiales :
> $$(1 + t^2)\,y'(t)\,y(t) = t \quad \text{avec } y(0) = y_0$$
>
> **(a)** Vérifier que $y(t) = \sqrt{\ln(1 + t^2) + y_0^2}$ est une solution, à condition que $y_0 > 0$. Quelle est la solution si $y_0 < 0$ ?
>
> **(b)** La solution est-elle unique, en particulier si $y_0 = 0$ ? Expliquer.
>
> **(c)** Écrire la formule d'Euler **explicite**.
>
> **(d)** Écrire la formule d'Euler **implicite** (sans développer).

---

## 🧩 Résolution complète — étape par étape

---

### Partie (a) — Vérifier que $y(t) = \sqrt{\ln(1+t^2) + y_0^2}$ est solution

**Étape 0 — Mettre l'EDO sous forme standard**

L'EDO donnée est $(1+t^2)y'(t)y(t) = t$. On peut la réécrire sous la forme $y'(t) = f(t, y)$ en divisant les deux membres par $(1+t^2)y(t)$ :

$$y'(t) = \frac{t}{(1+t^2)\,y(t)}$$

Donc $f(t,y) = \dfrac{t}{(1+t^2)\,y}$.

**Étape 1 — Calculer $[y(t)]^2$**

On part de $y(t) = \sqrt{\ln(1+t^2) + y_0^2}$. Pour simplifier les calculs, on va d'abord travailler avec $[y(t)]^2$ :

$$[y(t)]^2 = \ln(1+t^2) + y_0^2$$

**Étape 2 — Calculer $y'(t)$ par dérivation implicite**

On dérive les deux membres par rapport à $t$. À gauche, on utilise la règle de dérivation de $[y(t)]^2$ :

$$\frac{d}{dt}[y(t)]^2 = 2\,y(t)\,y'(t)$$

À droite, on dérive $\ln(1+t^2) + y_0^2$. La constante $y_0^2$ donne $0$, et pour $\ln(1+t^2)$ on applique la règle de dérivation du logarithme $(\ln(u))' = u'/u$ :

$$\frac{d}{dt}\ln(1+t^2) = \frac{2t}{1+t^2}$$

Donc l'équation dérivée est :

$$2\,y(t)\,y'(t) = \frac{2t}{1+t^2}$$

**Étape 3 — Retrouver l'EDO originale**

On multiplie les deux membres par $\dfrac{1+t^2}{2}$ :

$$(1+t^2)\,y(t)\,y'(t) = t \quad \checkmark$$

C'est exactement l'EDO de départ. ✅

**Étape 4 — Vérifier la condition initiale $y(0) = y_0$**

On remplace $t = 0$ dans la solution :

$$y(0) = \sqrt{\ln(1 + 0^2) + y_0^2} = \sqrt{\ln(1) + y_0^2} = \sqrt{0 + y_0^2} = \sqrt{y_0^2} = |y_0|$$

Si $y_0 > 0$ : $|y_0| = y_0$ ✅

Si $y_0 < 0$ : $|y_0| = -y_0 \neq y_0$ ❌

**Donc :** la solution $y(t) = \sqrt{\ln(1+t^2) + y_0^2}$ est valide **uniquement si $y_0 > 0$**.

**Si $y_0 < 0$ :** la solution est :
$$y(t) = -\sqrt{\ln(1+t^2) + y_0^2}$$
(on prend le signe négatif pour que $y(0) = -|y_0| = y_0$)

**Si $y_0 = 0$ :** les deux solutions $y(t) = \sqrt{\ln(1+t^2)}$ et $y(t) = -\sqrt{\ln(1+t^2)}$ sont toutes les deux valides — il y a **deux solutions** pour $y_0 = 0$.

---

### Partie (b) — Unicité de la solution

**Objectif :** Est-ce que la solution est unique ? On répond en vérifiant la condition de Lipschitz.

**Étape 1 — Identifier $f(t, y)$**

$$f(t, y) = \frac{t}{(1+t^2)\,y}$$

**Étape 2 — Calculer $\dfrac{\partial f}{\partial y}$**

$$\frac{\partial f}{\partial y} = \frac{\partial}{\partial y}\left[\frac{t}{(1+t^2)\,y}\right] = \frac{t}{1+t^2} \cdot \frac{\partial}{\partial y}\left[\frac{1}{y}\right] = \frac{t}{1+t^2} \cdot \left(-\frac{1}{y^2}\right) = -\frac{t}{(1+t^2)\,y^2}$$

**Étape 3 — Vérifier si c'est borné**

$$\left|\frac{\partial f}{\partial y}\right| = \frac{|t|}{(1+t^2)\,y^2}$$

Quand $y \to 0$, $y^2 \to 0$, donc $\dfrac{1}{y^2} \to \infty$.

**La dérivée n'est pas bornée en $y = 0$** → la condition de Lipschitz **n'est pas satisfaite** en $y = 0$.

**Conclusion :**

- Si $y_0 \neq 0$ : Lipschitz est satisfaite dans le voisinage de $y_0$ → la solution est **unique** ✅
- Si $y_0 = 0$ : Lipschitz **échoue** → la solution n'est **pas unique** ❌ (c'est cohérent avec le fait qu'on trouve deux solutions pour $y_0 = 0$ en (a))

---

### Partie (c) — Formule d'Euler explicite

La formule générale d'Euler explicite (dans le formulaire) est :

$$\hat{y}(t + h) = \hat{y}(t) + h \cdot f(t,\ \hat{y}(t))$$

On remplace $f(t, y)$ par $\dfrac{t}{(1+t^2)\,y}$ :

$$\boxed{\hat{y}_{n+1} = \hat{y}_n + h \cdot \frac{t_n}{(1+t_n^2)\,\hat{y}_n}}$$

C'est tout ! À chaque pas, on connaît $\hat{y}_n$ et $t_n$, donc on peut calculer $\hat{y}_{n+1}$ directement.

---

### Partie (d) — Formule d'Euler implicite (sans développer)

La formule générale d'Euler implicite (dans le formulaire) est :

$$\hat{y}(t + h) = \hat{y}(t) + h \cdot f(t + h,\ \hat{y}(t + h))$$

On remplace $f$ par $\dfrac{t}{(1+t^2)\,y}$, en utilisant $t+h$ et $\hat{y}_{n+1}$ :

$$\boxed{\hat{y}_{n+1} = \hat{y}_n + h \cdot \frac{t_{n+1}}{(1+t_{n+1}^2)\,\hat{y}_{n+1}}}$$

> ⚠️ **Remarque :** $\hat{y}_{n+1}$ apparaît **des deux côtés** de l'égalité ! En développant, on obtiendrait une équation quadratique en $\hat{y}_{n+1}$ (difficile à résoudre). L'énoncé demande de ne **pas** développer — on laisse la formule telle quelle.

---

## 🍳 La recette / le modèle à retenir

### Pour vérifier une solution d'EDO :
1. Calculer $[y(t)]^2$ si la solution est une racine carrée (c'est plus simple)
2. Dériver $[y(t)]^2$ des deux côtés → retrouver l'EDO
3. Vérifier la condition initiale $y(t_0) = y_0$

### Pour la condition de Lipschitz et l'unicité :
1. Identifier $f(t, y)$
2. Calculer $\left|\dfrac{\partial f}{\partial y}\right|$
3. Si bornée → Lipschitz satisfaite → **solution unique**
4. Si $\to \infty$ en un point (souvent $y = 0$) → **Lipschitz échoue** → solution **non unique** en ce point

### Pour écrire les formules d'Euler :
- **Explicite** : $\hat{y}_{n+1} = \hat{y}_n + h \cdot f(\mathbf{t_n},\ \hat{y}_n)$ → tout à gauche, calculable directement
- **Implicite** : $\hat{y}_{n+1} = \hat{y}_n + h \cdot f(\mathbf{t_{n+1}},\ \hat{y}_{n+1})$ → $\hat{y}_{n+1}$ des deux côtés, peut nécessiter de résoudre une équation

---

## ⚠️ Ce que tu dois savoir par cœur (du formulaire)

**Euler explicite :**
$$\hat{y}(t+h) = \hat{y}(t) + h \cdot f(t,\ \hat{y}(t))$$

**Euler implicite :**
$$\hat{y}(t+h) = \hat{y}(t) + h \cdot f(t+h,\ \hat{y}(t+h))$$

**Condition de Lipschitz :**
$$|f(t, y_1) - f(t, y_2)| \leq L \cdot |y_1 - y_2|$$

**Règle d'or : Lipschitz satisfaite → solution unique. Lipschitz échoue → possibilité de solutions multiples.**

> ✅ Les formules d'Euler sont dans le formulaire. La condition de Lipschitz aussi. Ce qu'il faut savoir faire, c'est les **appliquer** : substituer $f$, dériver, vérifier.

---

*Fiche préparée pour l'examen INFO-F-205 — Exercice 14 (chapitre EDO)*