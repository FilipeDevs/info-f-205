# 📘 Fiche d'étude — Exercice 15 : Systèmes Linéaires

## Le théorème de perturbation — Erreurs de génération vs propagation

---

## 🧠 Théorie à comprendre (et à retenir !)

### Les 3 types d'erreurs en calcul numérique

Quand on résout $Ax = b$ sur un ordinateur, il y a trois sources d'erreurs possibles. Il est **crucial** de les distinguer :

---

#### 🔴 Erreurs de génération (= erreurs d'arrondi accumulées pendant les calculs)

Quand un ordinateur fait des opérations (additions, multiplications...), chaque opération introduit une **petite erreur d'arrondi** (les nombres réels ne sont pas représentés exactement en machine). Ces erreurs s'accumulent tout au long de l'algorithme.

> 💡 **Analogie** : Imagine que chaque fois que tu fais une multiplication à la main, tu arrondis le résultat. Si tu fais 1000 multiplications de suite, les petites erreurs d'arrondi s'additionnent et peuvent devenir significatives.

Ces erreurs viennent **de l'algorithme lui-même**, pas des données d'entrée.

---

#### 🟡 Erreurs de propagation (= conditionnement du problème)

Ce sont les erreurs qui viennent des **données d'entrée** imprécises. Si $b$ est connu avec une légère imprécision (erreur de mesure, par exemple), cette imprécision va se **propager** jusqu'à la solution $x$.

> 💡 **Analogie** : Tu mesures une longueur avec une règle graduée en mm. Si tu as une erreur de 1 mm dans la mesure initiale, combien d'erreur auras-tu dans ton résultat final ? Ça dépend du conditionnement du problème — certains problèmes amplifient beaucoup les erreurs d'entrée, d'autres non.

Ces erreurs viennent des **données**, pas de l'algorithme.

---

#### 🟢 Erreurs d'approximation

Ce sont les erreurs dues au fait qu'une méthode itérative s'arrête après un nombre fini d'itérations, avant d'avoir atteint la vraie solution. Elles ne concernent pas l'exercice 15.

---

### Le théorème de perturbation

Ce théorème dit : si on résout $Ax = b$, et qu'il y a une perturbation $\delta A$ sur la matrice $A$ et une perturbation $\delta b$ sur le vecteur $b$, alors l'erreur relative sur la solution $x$ est bornée par :

$$\frac{\|\delta x\|}{\|x\|} \leq \frac{\kappa(A)}{1 - \kappa(A)\dfrac{\|\delta A\|}{\|A\|}} \left(\frac{\|\delta b\|}{\|b\|} + \frac{\|\delta A\|}{\|A\|}\right)$$

Avant d'interpréter, décortiquons chaque notation :

| Notation | Ce que ça veut dire |
|---|---|
| $x$ | La vraie solution exacte |
| $\delta x$ | L'écart entre la solution calculée et la vraie solution |
| $\|\delta x\| / \|x\|$ | L'**erreur relative** sur la solution (en %) |
| $\delta A$ | La **perturbation** sur la matrice $A$ |
| $\|\delta A\| / \|A\|$ | La taille relative de la perturbation sur $A$ |
| $\delta b$ | La **perturbation** sur le vecteur $b$ |
| $\|\delta b\| / \|b\|$ | La taille relative de la perturbation sur $b$ |
| $\kappa(A)$ | Le **conditionnement** de $A$ — amplifie tout |

> 💡 **Les doubles barres $\|\cdot\|$** signifient la "norme" d'un vecteur ou d'une matrice — c'est une façon de mesurer la "taille" d'un vecteur (comme sa longueur). Pour l'instant, pense-y comme une valeur absolue généralisée.

---

### Comment lire ce théorème ?

Le membre de gauche $\dfrac{\|\delta x\|}{\|x\|}$ représente **l'erreur relative sur la solution** — c'est ce qu'on veut borner (savoir à quel point on peut se tromper).

Le membre de droite dit que cette erreur est **au plus** proportionnelle à :
- $\kappa(A)$ : le conditionnement (coefficient amplificateur)
- $\dfrac{\|\delta b\|}{\|b\|}$ : l'erreur relative sur $b$
- $\dfrac{\|\delta A\|}{\|A\|}$ : l'erreur relative sur $A$

---

## 🔢 L'exercice 15 — Énoncé

> Expliquer comment le facteur $\|\delta A\|$ dans le théorème ci-dessus est un **modèle pour les erreurs de génération**. Qu'est-ce qui est modélisé par le facteur $\|\delta b\|$ ?

---

## 🧩 Résolution complète

Cet exercice est **conceptuel** — il n'y a pas de calcul à faire. Il faut expliquer en mots ce que représentent les deux facteurs $\delta A$ et $\delta b$ dans le théorème.

---

### Question 1 — Que modélise $\|\delta A\|$ ?

**$\|\delta A\|$ modélise les erreurs de génération.**

Voici l'idée clé : en analyse numérique, on utilise une **astuce de modélisation** pour analyser les erreurs d'arrondi accumulées pendant les calculs.

On fait le raisonnement suivant :

> *"Supposons que l'algorithme ne fasse aucune erreur d'arrondi pendant les calculs, mais qu'il parte d'une matrice légèrement fausse $A + \delta A$ au lieu de la vraie matrice $A$."*

Autrement dit, on **remplace** l'effet des erreurs d'arrondi (qui sont diffuses et dures à analyser) par une **perturbation équivalente sur la matrice $A$**.

**Pourquoi cette astuce fonctionne ?**

Parce que les erreurs d'arrondi accumulées pendant l'élimination de Gauss (par exemple) ont un effet mathématiquement équivalent à résoudre exactement un système légèrement perturbé. Au lieu d'analyser des millions de petites erreurs d'arrondi une par une, on les remplace toutes par un seul terme $\delta A$ sur la matrice.

**En résumé :**

| Dans la réalité | Dans le modèle |
|---|---|
| On calcule sur la vraie matrice $A$, mais avec des erreurs d'arrondi à chaque opération | On calcule **exactement** (sans arrondi), mais sur une matrice perturbée $A + \delta A$ |

Les erreurs de génération (arrondi des calculs) $\longleftrightarrow$ perturbation $\delta A$ sur la matrice.

> ⚠️ **Important :** La matrice $A + \delta A$ est supposée **connue exactement** dans le modèle. C'est juste que cette matrice est légèrement différente de la vraie $A$. C'est le prix à payer pour modéliser simplement les erreurs d'arrondi.

---

### Question 2 — Que modélise $\|\delta b\|$ ?

**$\|\delta b\|$ modélise les erreurs de propagation.**

Le facteur $\dfrac{\|\delta b\|}{\|b\|}$ représente une **perturbation sur les données d'entrée** $b$.

Rappel : les erreurs de propagation viennent des imprécisions sur les données. Si $b$ est connu avec une petite erreur (par exemple, $b$ vient d'une mesure expérimentale), cette erreur va se propager jusqu'à la solution $x$.

C'est exactement le **conditionnement du problème** : la sensibilité de la solution aux erreurs sur les données d'entrée. Un grand $\kappa(A)$ signifie qu'une petite erreur sur $b$ peut entraîner une grande erreur sur $x$.

---

### Résumé visuel

```
Erreur totale sur x
        │
        ├── due à δA   ←→   Erreurs de GÉNÉRATION
        │                   (arrondi pendant les calculs)
        │
        └── due à δb   ←→   Erreurs de PROPAGATION
                            (imprécision sur les données d'entrée)
```

Le théorème dit que l'erreur totale est bornée par une combinaison des deux, amplifiée par $\kappa(A)$.

---

## 🍳 La recette / le modèle à retenir

Pour tout exercice sur l'**interprétation du théorème de perturbation** :

1. **$\delta A$** = modélisation des **erreurs de génération** (arrondi des calculs)
   - Astuce : on remplace les erreurs d'arrondi dispersées par une unique perturbation sur $A$
   - On fait comme si on résolvait exactement, mais avec une matrice fausse

2. **$\delta b$** = modélisation des **erreurs de propagation** (conditionnement)
   - Ce sont les erreurs qui viennent des **données d'entrée**
   - Elles décrivent à quel point le problème est sensible aux imprécisions sur $b$

3. **$\kappa(A)$** amplifie les deux types d'erreurs
   - Grand $\kappa(A)$ = petit problème d'entrée → grande erreur sur $x$

---

## ⚠️ Ce que tu dois savoir par cœur (du formulaire)

Le théorème (donné dans le formulaire, section **3. Systèmes Linéaires**) :

$$\frac{\|\delta x\|}{\|x\|} \leq \frac{\kappa(A)}{1 - \kappa(A)\dfrac{\|\delta A\|}{\|A\|}} \left(\frac{\|\delta b\|}{\|b\|} + \frac{\|\delta A\|}{\|A\|}\right)$$

> ✅ Ce théorème est dans le formulaire — tu n'as pas besoin de le mémoriser. Mais tu dois savoir **expliquer ce que signifient $\delta A$ et $\delta b$**.

Les deux associations clés à retenir **par cœur** :

| Facteur | Type d'erreur |
|---|---|
| $\|\delta A\|$ | Erreurs de **génération** (arrondi des calculs) |
| $\|\delta b\|$ | Erreurs de **propagation** (données d'entrée imprécises) |

---

*Fiche préparée pour l'examen INFO-F-205 — Exercice 15 sur 18 (chapitre Systèmes Linéaires)*