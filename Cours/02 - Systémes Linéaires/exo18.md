# 📘 Fiche d'étude — Exercice 18 : Systèmes Linéaires

## Pourquoi une boucle itérative peut ne jamais s'arrêter ?

---

## 🧠 Théorie à comprendre (et à retenir !)

### Rappel des 3 types d'erreurs (synthèse des exos 15, 16, 17)

| Type | D'où ça vient ? | Dépend de quoi ? |
|---|---|---|
| **Génération** | Arrondis pendant les calculs | La méthode + $\kappa(A)$ |
| **Propagation** | Imprécision des données d'entrée | Le problème ($\kappa(A)$) seulement |
| **Approximation** | Arrêt prématuré d'une méthode itérative | $\rho(B)$ et le nombre d'itérations |

### Rappel : vers quoi converge une méthode itérative ?

Une méthode itérative $x^{(k+1)} = Bx^{(k)} + f$ avec $\rho(B) < 1$ converge vers la solution du système $Ax = b$ — **mais uniquement si $b$ est exact**.

Si $b$ est calculé avec une petite erreur (ce qui est inévitable en machine), la méthode converge vers la solution du **système perturbé** $Ax = b_{\text{perturbé}}$, pas vers la vraie solution.

> 💡 **Analogie :** Si tu vises une cible en utilisant une boussole légèrement déréglée, tu arrives à un endroit précis et stable — mais ce n'est **pas** là où tu voulais aller. Ta méthode a convergé, juste pas vers le bon point.

---

### C'est quoi `eps` en Matlab ?

`eps` est la **précision machine** (epsilon machine), notée $\varepsilon$ dans le cours. C'est le plus petit nombre tel que l'ordinateur ne peut pas distinguer $1$ de $1 + \varepsilon$.

En Matlab, `eps` $\approx 2{,}22 \times 10^{-16}$.

La condition `max(abs(x - x_it)) > eps` signifie : *"tant que la différence maximale entre $x$ et $x\_it$ est plus grande que la précision machine, continuer"*. En d'autres termes, la boucle s'arrête uniquement quand $x\_it$ est **pratiquement identique** à $x$ (à la précision machine près).

---

## 🔢 L'exercice 18 — Énoncé

> Considérer l'algorithme suivant pour simuler la convergence d'une méthode itérative dont $\rho(B) < 1$ :
>
> ```matlab
> x = (1:n)';          % Ligne 1
> b = A*x;             % Ligne 2
> x_it = zeros(n,1);   % Ligne 3
> while max(abs(x - x_it)) > eps,   % Ligne 4
>     x_it = B*x_it + f;            % Ligne 5
> end
> ```
>
> La boucle devrait se terminer dès que la convergence se manifeste, mais en réalité **la boucle n'aura pas de fin**. Expliquer en se référant aux trois formes d'erreurs.

---

## 🧩 Résolution complète — étape par étape

### Étape 1 — Comprendre le code ligne par ligne

**Ligne 1 :** `x = (1:n)'`

On crée un vecteur $x$ dont les composantes sont $[1, 2, 3, \ldots, n]$. Ce vecteur est connu **exactement** — c'est juste des entiers, pas d'erreur possible ici.

**Ligne 2 :** `b = A*x`

On calcule $b = A \cdot x$. **C'est ici que tout se joue.** Ce calcul implique des multiplications et additions de nombres flottants → des **erreurs d'arrondi** sont inévitablement introduites.

Le résultat stocké en mémoire est donc :

$$b_{\text{calculé}} = b_{\text{exact}} \cdot (1 + \rho_b) \neq b_{\text{exact}}$$

où $\rho_b$ est une toute petite erreur relative, mais non nulle.

**Ligne 3 :** `x_it = zeros(n,1)`

On initialise l'estimation de départ à zéro. Pas de problème ici.

**Ligne 4 :** `while max(abs(x - x_it)) > eps`

La condition d'arrêt : la boucle continue tant que $x\_it$ est différent de $x$ (à la précision machine près). En d'autres termes, on demande à la méthode itérative de converger **exactement vers le vecteur $x$ de la ligne 1**.

**Ligne 5 :** `x_it = B*x_it + f`

Une étape d'itération. Puisque $\rho(B) < 1$, ces itérations convergent — c'est garanti.

---

### Étape 2 — Identifier les erreurs présentes

#### Erreurs de génération

Le calcul `b = A*x` à la ligne 2 introduit des **erreurs de génération** (arrondis des multiplications matrice-vecteur). Le vecteur $b$ stocké en mémoire est donc **légèrement faux** :

$$b_{\text{calculé}} = b_{\text{exact}} + \delta b \quad \text{avec } \delta b \neq 0 \text{ (mais très petit)}$$

> ⚠️ Ces erreurs de génération sur $b$ ne disparaissent pas — elles sont "figées" dans la variable `b` dès la ligne 2.

#### Erreurs de propagation

Le vecteur $b_{\text{calculé}}$ contient une petite erreur $\delta b$. Cette erreur va se **propager** à travers toutes les itérations suivantes, car c'est sur la base de ce $b$ perturbé que la méthode itérative travaille.

Le degré d'amplification de cette erreur dépend de $\kappa(A)$ : si $\kappa(A)$ est grand, même un tout petit $\delta b$ peut donner une grande erreur sur la solution.

#### Erreurs d'approximation

Après $k$ itérations, l'erreur d'approximation est proportionnelle à $\rho(B)^k$. Puisque $\rho(B) < 1$, ces erreurs **convergent bien vers zéro** — la méthode itérative fait correctement son travail.

---

### Étape 3 — Comprendre pourquoi la boucle ne s'arrête jamais

Voici le nœud du problème, expliqué progressivement :

**Ce que la boucle cherche :** converger vers le vecteur $x$ exact de la ligne 1 (les entiers $[1, 2, \ldots, n]$).

**Ce vers quoi la méthode itérative converge réellement :** la solution du système $Ax = b_{\text{calculé}}$, c'est-à-dire la solution avec le $b$ **perturbé** par les erreurs de génération de la ligne 2.

Appelons $x^* = A^{-1} b_{\text{calculé}}$ cette solution perturbée. On a :

$$x^* = A^{-1}(b + \delta b) = x + A^{-1}\delta b \neq x$$

La méthode itérative converge parfaitement vers $x^*$... mais $x^* \neq x$.

**Donc :**

$$x\_it \xrightarrow{k \to \infty} x^* \neq x$$

La différence $|x - x\_it|$ ne tend **pas vers zéro** — elle tend vers $|x - x^*| = |A^{-1}\delta b| > 0$.

Cette valeur est petite (car $\delta b$ est petit), mais elle est **strictement supérieure à `eps`** (précision machine). La condition de la boucle `max(abs(x - x_it)) > eps` reste donc vraie **pour toujours**.

**La boucle ne s'arrête jamais.**

---

### Étape 4 — Résumé du raisonnement

```
Ligne 2 : b = A*x
    → Erreurs de GÉNÉRATION introduites : b_calculé ≠ b_exact
          │
          ▼
    → Ces erreurs se PROPAGENT : la méthode itérative
      travaille avec un mauvais b
          │
          ▼
    → Erreurs d'APPROXIMATION convergent vers 0 ✅
      (la méthode itérative converge bien)
          │
          ▼
    → Mais elle converge vers x* ≠ x (solution du système perturbé)
          │
          ▼
    → |x - x_it| → |x - x*| > eps  → boucle infinie ❌
```

---

### La phrase clé à écrire à l'examen

> Le calcul `b = A*x` introduit des **erreurs de génération** : le vecteur $b$ calculé est légèrement perturbé ($b_{\text{calculé}} = b(1 + \rho_b)$). Ces erreurs se **propagent** : la méthode itérative converge non pas vers $x$, mais vers la solution du système perturbé $x^* = A^{-1}b_{\text{calculé}} \neq x$. Les **erreurs d'approximation** convergent bien vers zéro (la méthode est stable par Lax-Richtmyer), mais la limite est $x^*$ et non $x$. La différence $\|x - x\_it\|$ ne tombe donc jamais en dessous de `eps`, et la boucle ne se termine jamais.

---

## 🍳 La recette / le modèle à retenir

Pour tout exercice où on demande **pourquoi une boucle itérative ne s'arrête pas** :

1. **Identifier où les erreurs de génération entrent** — chercher les calculs en virgule flottante (multiplications matricielles, etc.) qui créent un $b$ ou un $A$ légèrement faux.

2. **Montrer la propagation** — ces erreurs sur les données d'entrée se propagent dans toutes les itérations suivantes.

3. **Distinguer "converge" et "converge vers quoi"** — la méthode peut très bien converger (erreurs d'approximation → 0), mais converger vers la **mauvaise solution** (solution du système perturbé).

4. **Conclure** — si la cible de la boucle est la vraie solution $x$, mais que la méthode converge vers $x^* \neq x$, la condition d'arrêt n'est jamais satisfaite → boucle infinie.

---

## ⚠️ Ce que tu dois savoir par cœur

**La distinction cruciale :**

| Ce qu'on croit | La réalité |
|---|---|
| La méthode ne converge pas | La méthode **converge** ($\rho(B) < 1$) |
| La boucle est infinie parce que c'est instable | La boucle est infinie parce qu'elle converge vers **la mauvaise valeur** |

**La chaîne causale à mémoriser :**

$$\text{Erreur de génération sur } b \xrightarrow{\text{propagation}} x^* \neq x \xrightarrow{} \|x - x\_it\| \not\to 0 \xrightarrow{} \text{boucle infinie}$$

**Théorème de Lax-Richtmyer** (toujours utile ici) :

> La méthode itérative est **stable** (erreurs de génération des itérations disparaissent) — mais ça ne sauve pas la situation, car l'erreur vient des données d'entrée $b$, pas des itérations.

---

*Fiche préparée pour l'examen INFO-F-205 — Exercice 18 sur 18 (chapitre Systèmes Linéaires)*