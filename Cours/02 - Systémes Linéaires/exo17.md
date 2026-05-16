# 📘 Fiche d'étude — Exercice 17 : Systèmes Linéaires

## Méthode directe vs méthode itérative — Comparaison des erreurs

---

## 🧠 Théorie à comprendre (et à retenir !)

### Rappel : les 3 types d'erreurs

On les a vus à l'exercice 15, mais voici un récap plus complet avant d'attaquer l'exercice :

---

#### 🔴 Erreurs de génération (arrondi des calculs)

Ce sont les erreurs produites **par l'algorithme lui-même** lors des calculs (chaque opération arrondit le résultat). Elles dépendent :
- de la **méthode utilisée** (directe ou itérative)
- du **conditionnement** $\kappa(A)$

---

#### 🟡 Erreurs de propagation (conditionnement du problème)

Ce sont les erreurs dues aux **imprécisions sur les données d'entrée** $b$ (ou $A$). Elles dépendent uniquement du **problème lui-même**, pas de la méthode choisie.

> 💡 **Clé :** si tu changes de méthode de résolution, les erreurs de propagation restent **identiques** — elles ne dépendent que de $\kappa(A)$ et de la qualité des données d'entrée.

---

#### 🟢 Erreurs d'approximation (troncature itérative)

Ces erreurs n'existent que dans les **méthodes itératives**. Elles viennent du fait qu'on s'arrête après un nombre fini d'itérations — on n'attend pas que la suite converge parfaitement. Plus on fait d'itérations, plus ces erreurs diminuent.

Dans une méthode directe (comme la factorisation LU), on obtient la solution en un nombre fini d'étapes → **pas d'erreurs d'approximation**.

---

### Méthode directe (factorisation LU)

La factorisation LU résout $Ax = b$ en deux étapes :
1. Factoriser $A = LU$ (une fois)
2. Résoudre $Ly = b$ puis $Ux = y$ par substitution

**Complexité :** $\mathcal{O}(n^3)$ opérations (cubique en la taille de la matrice).

**Génération :** Pour une méthode directe, les erreurs d'arrondi accumulées pendant l'élimination de Gauss sont **contrôlées par $\kappa(A)$**. Si $\kappa(A)$ est énorme, les erreurs de génération seront également énormes.

**Approximation :** Aucune — la solution est exacte (en arithmétique infinie). En pratique, seul l'arrondi compte.

---

### Méthode itérative

Une méthode itérative $x^{(k+1)} = Bx^{(k)} + f$ converge si $\rho(B) < 1$.

**Génération — Le théorème de Lax-Richtmyer :**

> *Si une méthode itérative est consistante et converge, alors elle est stable (pas d'erreurs de génération).*

En clair : une méthode itérative **convergente** ne génère pas d'erreurs de génération — les petits arrondis commis à chaque itération finissent par disparaître grâce à la convergence. C'est une propriété remarquable !

**Approximation :** Ces erreurs diminuent à chaque itération. La vitesse de diminution dépend de $\rho(B)$ :
- Plus $\rho(B)$ est petit → convergence rapide
- $\rho(B)$ proche de 1 → convergence lente (il faut beaucoup d'itérations)

---

### Le conditionnement $\kappa(A)$ — rappel

$\kappa(A) = \|A^{-1}\| \cdot \|A\|$

- $\kappa(A) \geq 1$ toujours
- $\kappa(A) = 1$ → matrice parfaitement conditionnée (orthogonale)
- $\kappa(A) \gg 1$ → matrice très mal conditionnée → grandes erreurs de propagation et de génération (pour les méthodes directes)

Un conditionnement de $5 \times 10^{14}$ est **catastrophiquement grand** — c'est presque singulier.

---

## 🔢 L'exercice 17 — Énoncé

> On considère un **grand système linéaire non creux** $Ax = b$ avec :
> - `cond(A)` = $5{,}3529 \times 10^{14}$ (le conditionnement $\kappa(A)$ donné par Matlab)
> - Une matrice d'itération $B$ avec `max(abs(eig(B)))` = $0{,}9013$ (le rayon spectral $\rho(B)$)
>
> Comparer la **méthode directe (LU)** et la **méthode itérative** pour ce qui est des :
> - Erreurs de **génération**
> - Erreurs de **propagation**
> - Erreurs d'**approximation**
> - **Temps de calcul** (sachant que $A$ n'est pas creuse)

---

## 🧩 Résolution complète

Cet exercice est **conceptuel** — pas de calcul à faire. On analyse chaque critère pour chacune des deux méthodes.

Les deux informations clés de l'énoncé sont :

| Information | Valeur | Signification |
|---|---|---|
| $\kappa(A) = $ `cond(A)` | $5{,}35 \times 10^{14}$ | Conditionnement **extrêmement grand** → problème très mal conditionné |
| $\rho(B) = $ `max(abs(eig(B)))` | $0{,}9013$ | Rayon spectral $< 1$ → méthode itérative converge, mais **lentement** |

---

### Critère 1 — Erreurs de génération

**Méthode directe (LU) :**

Le conditionnement $\kappa(A)$ contrôle la stabilité de la méthode directe. Puisque $\kappa(A) = 5{,}35 \times 10^{14}$ est **gigantesque**, les erreurs de génération accumulées pendant l'élimination de Gauss seront elles aussi **considérables**.

> 💡 En clair : avec un si mauvais conditionnement, les erreurs d'arrondi s'amplifient massivement pendant les calculs. La solution calculée peut être très loin de la vraie solution.

→ **Méthode directe : erreurs de génération considérables ❌**

**Méthode itérative :**

Grâce au **théorème de Lax-Richtmyer** : une méthode itérative convergente est stable. Puisque $\rho(B) = 0{,}9013 < 1$, la méthode converge, donc elle est stable — les petites erreurs d'arrondi commises à chaque itération finissent par s'effacer.

→ **Méthode itérative : pas d'erreurs de génération ✅**

---

### Critère 2 — Erreurs de propagation

Les erreurs de propagation dépendent uniquement du **problème** (c'est-à-dire de $\kappa(A)$ et de la précision des données d'entrée), **pas de la méthode** utilisée.

$\kappa(A) = 5{,}35 \times 10^{14}$ est astronomique : une toute petite erreur sur les données $b$ va être amplifiée d'un facteur $\approx 10^{14}$ sur la solution $x$.

→ **Les deux méthodes : erreurs de propagation très grandes ❌** (identiques pour les deux, car c'est une propriété du problème)

---

### Critère 3 — Erreurs d'approximation

**Méthode directe (LU) :**

La méthode directe donne la solution en un nombre fini d'étapes — il n'y a pas d'"approximation" au sens itératif. Les seules erreurs sont celles de génération vues au critère 1.

→ **Méthode directe : pas d'erreurs d'approximation ✅**

**Méthode itérative :**

La méthode itérative approche la solution de plus en plus à chaque itération. Ces erreurs d'approximation **convergent vers zéro** — pour un nombre d'itérations suffisamment grand, elles deviennent arbitrairement petites.

→ **Méthode itérative : erreurs d'approximation qui tendent vers 0 ✅** (avec suffisamment d'itérations)

---

### Critère 4 — Temps de calcul

**Méthode directe (LU) :**

Complexité **cubique** : $\mathcal{O}(n^3)$ opérations. Pour une grande matrice dense (non creuse), c'est un coût fixe et prévisible.

**Méthode itérative :**

Le coût par itération est $\mathcal{O}(n^2)$ (un produit matrice-vecteur), mais il faut potentiellement **beaucoup d'itérations**.

Combien d'itérations faut-il ? La vitesse de convergence est liée à $\rho(B)$ : après $k$ itérations, l'erreur est proportionnelle à $\rho(B)^k$.

Avec $\rho(B) = 0{,}9013$, calculons combien d'itérations pour diviser l'erreur par $10^{10}$ :

$$0{,}9013^k < 10^{-10} \iff k \cdot \log(0{,}9013) < -10 \cdot \log(10) \iff k > \frac{10}{\log(1/0{,}9013)} \approx \frac{10}{0{,}0444} \approx 225 \text{ itérations}$$

> 💡 En clair : $\rho(B) = 0{,}9013$ est proche de 1, donc la convergence est **très lente**. Il faut des centaines d'itérations pour avoir une bonne précision. Chaque itération coûte $\mathcal{O}(n^2)$ → coût total élevé.

De plus, la matrice $A$ est **non creuse** (dense) : si $A$ était creuse, les produits matrice-vecteur seraient beaucoup moins coûteux et la méthode itérative pourrait être compétitive. Mais ici, chaque itération coûte autant que pour une matrice dense.

→ **La méthode directe est probablement plus rapide** dans ce cas ✅

---

### Tableau récapitulatif

| Critère | Méthode directe (LU) | Méthode itérative |
|---|---|---|
| **Génération** | ❌ Considérables ($\kappa(A)$ énorme) | ✅ Absentes (Lax-Richtmyer) |
| **Propagation** | ❌ Très grandes | ❌ Très grandes (identique — dépend du problème) |
| **Approximation** | ✅ Absentes | ✅ Tendent vers 0 (avec assez d'itérations) |
| **Temps** | ✅ $\mathcal{O}(n^3)$, coût fixe | ❌ Lent ($\rho = 0{,}90$), convergence lente |

---

## 🍳 La recette / le modèle à retenir

Pour tout exercice de **comparaison méthode directe / méthode itérative**, analyser chaque critère dans cet ordre :

### Génération
- Directe : erreurs contrôlées par $\kappa(A)$ → grandes si $\kappa(A)$ grand
- Itérative : **aucune** si $\rho(B) < 1$ (Lax-Richtmyer)

### Propagation
- **Identique pour les deux méthodes** — dépend uniquement du problème ($\kappa(A)$)
- Si $\kappa(A)$ grand → grandes erreurs de propagation dans les deux cas

### Approximation
- Directe : **aucune**
- Itérative : existent, mais **tendent vers 0** avec les itérations

### Temps de calcul
- Directe : $\mathcal{O}(n^3)$, coût fixe
- Itérative : dépend de $\rho(B)$ et de la structure de $A$ (creuse ou non)
  - $\rho(B)$ proche de 0 → rapide
  - $\rho(B)$ proche de 1 → lent (beaucoup d'itérations)
  - $A$ creuse → itérative souvent préférable
  - $A$ dense → directe souvent préférable

---

## ⚠️ Ce que tu dois savoir par cœur

**Théorème de Lax-Richtmyer** (à connaître en toutes lettres) :

> *Une méthode itérative consistante et convergente est stable → pas d'erreurs de génération.*

**Les deux propriétés clés :**
1. Les erreurs de **propagation** ne dépendent **pas** de la méthode → identiques pour les deux
2. Les erreurs de **génération** dépendent de la méthode :
   - Directe : amplifiées par $\kappa(A)$
   - Itérative convergente : **nulles** (Lax-Richtmyer)

---

*Fiche préparée pour l'examen INFO-F-205 — Exercice 17 sur 18 (chapitre Systèmes Linéaires)*