### **Q1 - Recherche d'une valeur dans une liste**

**Code :**
```python
def search(x, y):
    # x est la valeur à chercher
    # y est une liste de valeurs
    for i in range(len(y)):
        if x == y[i]:
            return i
    return None
```

**Question :** Quel est le coût de cet algorithme ?

**Réponses possibles :**
- A- constant
- B- logarithmique
- C- linéaire
- D- quadratique

---

### **Analyse :**
1. **Description de l'algorithme :**
   - L'algorithme parcourt chaque élément de la liste `y` un par un.
   - Il compare chaque élément avec `x`.
   - Si `x` est trouvé, il retourne l'indice `i`.
   - Sinon, il retourne `None` après avoir parcouru toute la liste.

2. **Complexité :**
   - Dans le pire des cas, l'algorithme parcourt toute la liste de taille `n`.
   - Il effectue donc `n` comparaisons.
   - La complexité est donc **linéaire**, c'est-à-dire de l'ordre de `n`.

---

### **Réponse :**
**Réponse correcte : C- linéaire**

---

### **Q2 - Ordre de grandeur du coût du tri par insertion (dans le pire des cas)**

**Question :** Quel est l'ordre de grandeur du coût du tri par insertion (dans le pire des cas) ?

**Réponses possibles :**
- A- l'ordre de grandeur du coût dépend de l'ordinateur utilisé
- B- linéaire en la taille du tableau à trier
- C- quadratique en la taille du tableau à trier
- D- indépendant de la taille du tableau à trier

---

### **Analyse :**
1. **Description du tri par insertion :**
   - Le tri par insertion parcourt chaque élément du tableau et l'insère à sa place dans la partie déjà triée.
   - Dans le pire des cas (par exemple, si le tableau est trié en ordre décroissant), chaque insertion nécessite de parcourir toute la partie déjà triée.

2. **Complexité :**
   - Pour chaque élément, on effectue jusqu'à `i` comparaisons (où `i` est la position de l'élément).
   - Le nombre total de comparaisons est donc \( 1 + 2 + 3 + ... + n = \frac{n(n+1)}{2} \).
   - La complexité est donc **quadratique**, c'est-à-dire de l'ordre de \( n^2 \).

---

### **Réponse :**
**Réponse correcte : C- quadratique en la taille du tableau à trier**


----------------------------------


### **Q3 - Identification de l'algorithme**

**Code :**
```python
def f(x, L):
    i = 0
    j = len(L) - 1
    while i <= j:
        k = (i + j) // 2
        if x <= L[k]:
            j = k
        else:
            i = k + 1
    return i
```

**Question :** Cette fonction implémente :

**Réponses possibles :**
- A- le tri par insertion
- B- le tri par sélection
- C- la recherche dichotomique
- D- la recherche du plus proche voisin

---

### **Analyse :**
1. **Description de la fonction :**
   - La fonction prend en entrée une valeur `x` et une liste `L`.
   - Elle initialise deux indices, `i` à 0 et `j` à la fin de la liste.
   - Elle utilise une boucle `while` pour diviser l'intervalle de recherche en deux à chaque itération.
   - Elle calcule un indice médian `k` et compare `x` avec `L[k]` pour ajuster `i` ou `j`.

2. **Comportement :**
   - La fonction utilise une méthode de **recherche dichotomique** (ou recherche binaire).
   - Elle ne trie pas la liste, mais cherche une position où `x` pourrait être inséré pour maintenir l'ordre.
   - Elle ne retourne pas nécessairement un "plus proche voisin", mais plutôt la position où `x` devrait être inséré.

3. **Conclusion :**
   - Cette fonction est une variante de la **recherche dichotomique** pour trouver la position d'insertion d'un élément dans une liste triée.

---

### **Réponse :**
**Réponse correcte : C- la recherche dichotomique** (ou plus précisément, la recherche de la position d'insertion dans une liste triée, ce qui est une utilisation classique de la recherche dichotomique).










------------------------------------------

### **Exercice : Comparaison de coûts et efficacité des algorithmes**

#### **1. Compléter les tableaux suivants :**

##### **a) Coût linéaire : O(n)**

| Nb d'éléments \( n \) | Nb d'opérations pour un tri en coût linéaire : O(n) | Durée pour un tri en coût linéaire : O(n) |
|-----------------------|------------------------------------------------------|-------------------------------------------|
| 10                    | 10                                                   | 10 ns (nanoseconde)                       |
| 100                   | 100                                                  | 100 ns                                    |
| 1 000                 | 1 000                                                | 1 µs (microseconde)                       |
| 10 000                | 10 000                                               | 10 µs                                     |
| 100 000               | 100 000                                              | 100 µs                                    |
| 1 000 000             | 1 000 000                                            | 1 ms (milliseconde)                       |
| 10 000 000            | 10 000 000                                           | 10 ms                                     |
| 100 000 000           | 100 000 000                                          | 100 ms                                    |
| 1 000 000 000         | 1 000 000 000                                        | 1 s (seconde)                             |

---

##### **b) Coût quadratique : O(n²)**

| Nb d'éléments \( n \) | Nb d'opérations pour un tri en coût quadratique : O(n²) | Durée pour un tri en coût quadratique : O(n²) |
|-----------------------|----------------------------------------------------------|-----------------------------------------------|
| 10                    | 100                                                      | 100 ns                                        |
| 100                   | 10 000                                                   | 10 µs                                         |
| 1 000                 | 1 000 000                                                | 1 ms                                          |
| 10 000                | 100 000 000                                              | 100 ms                                        |
| 100 000               | 10 000 000 000                                           | 10 s                                          |
| 1 000 000             | 1 000 000 000 000                                        | 16 min 40 s                                   |
| 10 000 000            | 100 000 000 000 000                                      | 27 heures                                     |
| 100 000 000           | 10 000 000 000 000 000                                   | 115 jours                                     |
| 1 000 000 000         | 1 000 000 000 000 000 000                                 | 31 ans                                        |

---

##### **c) Coût logarithmique : O(log₂ n)**

| Nb d'éléments \( n \) | Nb d'opérations pour un tri en coût logarithmique : O(log₂ n) | Durée pour un tri en coût logarithmique : O(log₂ n) |
|-----------------------|----------------------------------------------------------------|-----------------------------------------------------|
| 10                    | 3 (car \( 2^3 = 8 \) et \( 2^4 = 16 \))                       | 3 ns                                               |
| 100                   | 7 (car \( 2^6 = 64 \) et \( 2^7 = 128 \))                     | 7 ns                                               |
| 1 000                 | 10 (car \( 2^9 = 512 \) et \( 2^{10} = 1024 \))              | 10 ns                                              |
| 10 000                | 14 (car \( 2^{13} = 8192 \) et \( 2^{14} = 16384 \))         | 14 ns                                              |
| 100 000               | 17 (car \( 2^{16} = 65536 \) et \( 2^{17} = 131072 \))      | 17 ns                                              |
| 1 000 000             | 20 (car \( 2^{19} = 524288 \) et \( 2^{20} = 1048576 \))    | 20 ns                                              |
| 10 000 000            | 23 (car \( 2^{23} = 8388608 \))                              | 23 ns                                              |
| 100 000 000           | 27 (car \( 2^{26} = 67108864 \) et \( 2^{27} = 134217728 \))| 27 ns                                              |
| 1 000 000 000         | 30 (car \( 2^{29} = 536870912 \) et \( 2^{30} = 1073741824 \))| 30 ns                                              |

---

#### **2. Observation et analyse :**

- **Pour un coût linéaire (O(n))** : Le nombre d'opérations et la durée augmentent proportionnellement avec le nombre d'éléments. C'est efficace pour des petites tailles, mais peut devenir lent pour des très grands ensembles de données.

- **Pour un coût quadratique (O(n²))** : Le nombre d'opérations et la durée augmentent de manière quadratique. Cela devient très inefficace pour des grands ensembles de données (ex. : 1 milliard d'éléments prendrait 31 ans !).

- **Pour un coût logarithmique (O(log₂ n))** : Le nombre d'opérations et la durée augmentent très lentement, même pour des très grands ensembles de données. C'est le plus efficace des trois pour des grands \( n \).

---

#### **3. Application à l'algorithme de Knuth ou de Fisher-Yates :**

L'algorithme de **Fisher-Yates** (ou tri de Knuth) est un algorithme de tri en **O(n)** pour un mélange aléatoire parfait. Il est très efficace pour mélanger une liste d'éléments.



-----------------------------------------------------------------


---
### **Algorithme de Fisher-Yates en Python :**

```python
import random

def shuffle(tab):
    # Parcourir le tableau de la fin vers le début
    for i in range(len(tab) - 1, 0, -1):
        # Choisir un index aléatoire entre 0 et i
        j = random.randint(0, i)
        # Échanger les éléments aux positions i et j
        tab[i], tab[j] = tab[j], tab[i]
    return tab

# Exemple d'utilisation
tab = [1, 2, 3, 4, 5, 6, 7, 8, 9]
print("Tableau initial :", tab)
shuffle(tab)
print("Tableau mélangé :", tab)
```

---

### **Explications :**
1. **Boucle principale :**
   - On parcourt le tableau de la fin vers le début (`for i in range(len(tab) - 1, 0, -1)`).
   - À chaque itération, on choisit un index `j` aléatoire entre `0` et `i`.

2. **Échange :**
   - On échange l'élément à la position `i` avec celui à la position `j`.

3. **Résultat :**
   - Après le parcours, le tableau est mélangé de manière aléatoire et uniforme.

---

### **Pourquoi cet algorithme est efficace ?**
- **Complexité :** O(n), car chaque élément est traité exactement une fois.
- **Uniformité :** Chaque permutation du tableau est équilibrée, ce qui garantit un mélange parfait.

---

### **Exemple de sortie :**
```
Tableau initial : [1, 2, 3, 4, 5, 6, 7, 8, 9]
Tableau mélangé : [3, 7, 1, 9, 2, 5, 8, 4, 6]
```


-----------------------------------------------------------------
### **Q7**
**Énoncé :**
Si le nombre `n` de données double, alors le temps d'exécution de ce script :
- A- reste le même
- B- double aussi
- C- est multiplié par n
- D- est multiplié par 4

**Code :**
```python
M = 0
for k in range(n):
    M = M + L[k]
M = M/n
```

**Analyse :**
Ce script calcule la moyenne des éléments d'une liste `L` de taille `n`. Il effectue une boucle `for` qui parcourt chaque élément de la liste une seule fois. La complexité de cet algorithme est donc **linéaire**, c'est-à-dire proportionnelle à `n`.

**Réponse :**
Si `n` double, le temps d'exécution double aussi.
**Réponse correcte : B- double aussi**

---

### **Q8**
**Énoncé :**
Quel est le coût d'un algorithme de tri par insertion ?

**Réponses possibles :**
- A- constant
- B- logarithmique
- C- linéaire
- D- quadratique

**Analyse :**
Le tri par insertion a une complexité de **O(n²)** dans le pire des cas, ce qui signifie qu'il est **quadratique**.

**Réponse :**
**Réponse correcte : D- quadratique**

---

### **Q9**
**Énoncé :**
Quelle est la complexité du tri par sélection ?

**Réponses possibles :**
- A- inconnue
- B- linéaire
- C- quadratique
- D- exponentielle

**Analyse :**
Le tri par sélection a une complexité de **O(n²)**, ce qui signifie qu'il est **quadratique**.

**Réponse :**
**Réponse correcte : C- quadratique**

---

### **Q10**
**Énoncé :**
Pour trier par sélection une liste de 2500 entiers, le nombre de comparaisons nécessaires à l'algorithme est de l'ordre de :

**Réponses possibles :**
- A- √2500
- B- 2500
- C- 2500²
- D- 2²⁵⁰⁰

**Analyse :**
Le tri par sélection effectue environ \( \frac{n(n-1)}{2} \) comparaisons pour trier une liste de taille \( n \). Pour \( n = 2500 \), cela donne un ordre de grandeur de \( n^2 \), soit \( 2500^2 \).

**Réponse :**
**Réponse correcte : C- 2500²**

---

### **Q11**
**Énoncé :**
Quelle valeur permet de compléter l'affirmation suivante : "Le nombre d'opérations nécessaires pour rechercher un élément séquentiellement dans un tableau de longueur \( n \) est de l'ordre de ... ?"

**Réponses possibles :**
- A- 1
- B- n
- C- n²
- D- n³

**Analyse :**
La recherche séquentielle dans un tableau de taille \( n \) nécessite, dans le pire des cas, de parcourir tous les éléments du tableau. La complexité est donc **linéaire**, c'est-à-dire de l'ordre de \( n \).

**Réponse :**
**Réponse correcte : B- n**
---


-----------------------------------------------------------------


### **Q12**

**Énoncé :**
On considère la fonction Python suivante, qui prend en argument une liste `L` et renvoie le maximum des éléments de la liste :
```python
def rechercheMaximum(L):
    max = L[0]
    for i in range(len(L)):
        if L[i] > max:
            max = L[i]
    return max
```
On note `n` la taille de la liste. Quelle est la complexité en nombre d'opérations de l'algorithme ?

**Réponses possibles :**
- A- constante, c'est-à-dire ne dépend pas de `n`
- B- linéaire, c'est-à-dire de l'ordre de `n`
- C- quadratique, c'est-à-dire de l'ordre de `n²`
- D- cubique, c'est-à-dire de l'ordre de `n³`

---

### **Analyse :**
1. **Initialisation :**
   `max = L[0]` est une opération constante (1 opération).

2. **Boucle `for` :**
   La boucle `for i in range(len(L)):` parcourt chaque élément de la liste une seule fois. Cela signifie que la boucle s'exécute exactement `n` fois (où `n` est la taille de la liste).

3. **Condition `if` :**
   À chaque itération de la boucle, il y a une comparaison (`if L[i] > max`) et éventuellement une affectation (`max = L[i]`). Ces opérations sont constantes et ne dépendent pas de `n`.

4. **Complexité globale :**
   Puisque la boucle `for` s'exécute `n` fois et que chaque itération effectue un nombre constant d'opérations, la complexité globale de cet algorithme est **linéaire**, c'est-à-dire de l'ordre de `n`.

---

### **Réponse :**
**Réponse correcte : B- linéaire, c'est-à-dire de l'ordre de `n`**





-----------------------------------------------------------------



### **Q4**
Tri a bulle ca ce voit


### **Q5**

**Énoncé :**
Un algorithme de tri d'une liste d'entiers est implémenté de la façon suivante :
```python
def tri(L):
    for i in range(len(L)):
        indice_min = i
        for j in range(i+1, len(L)):
            if L[j] < L[indice_min]:
                indice_min = j
        L[i], L[indice_min] = L[indice_min], L[i]
    return L
```

**Question :**
Quelle est l'affirmation exacte ?

**Réponses possibles :**
- A- cet algorithme est celui du tri par sélection
- B- cet algorithme est celui du tri par sélection au coût linéaire en la taille de la liste à trier
- C- cet algorithme est celui du tri par insertion au coût linéaire en la taille de la liste à trier
- D- cet algorithme est celui du tri par sélection au coût quadratique en la taille de la liste à trier

---

### **Analyse :**
1. **Description de l'algorithme :**
   - L'algorithme parcourt la liste avec une boucle externe (`i`).
   - Pour chaque `i`, il cherche l'indice de l'élément minimum dans le reste de la liste (`j` allant de `i+1` à `len(L)`).
   - Une fois l'indice du minimum trouvé, il échange cet élément avec l'élément à la position `i`.

2. **Type de tri :**
   - Cet algorithme correspond au **tri par sélection**.

3. **Complexité :**
   - La boucle externe s'exécute `n` fois (où `n` est la taille de la liste).
   - La boucle interne s'exécute `n-i` fois pour chaque `i`.
   - La complexité totale est donc de l'ordre de \( n + (n-1) + (n-2) + ... + 1 = \frac{n(n+1)}{2} \), ce qui est de l'ordre de \( n^2 \) (quadratique).

4. **Conclusion :**
   - L'algorithme est bien celui du tri par sélection, avec un coût quadratique.

---

### **Réponse :**
**Réponse correcte : D- cet algorithme est celui du tri par sélection au coût quadratique en la taille de la liste à trier**

---

### **Q6**

**Énoncé :**
Soit `T` le temps nécessaire pour trier, à l'aide du même algorithme, une liste de 1000 nombres entiers. Quel est l'ordre de grandeur du temps nécessaire, avec le même algorithme, pour trier une liste de 10 000 entiers, c'est-à-dire une liste dix fois plus grande ?

**Réponses possibles :**
- A- à peu près le même temps `T`
- B- environ 10 × `T`
- C- environ 100 × `T`
- D- environ `T²`

---

### **Analyse :**
1. **Complexité du tri par insertion :**
   - Le tri par insertion a une complexité quadratique, c'est-à-dire de l'ordre de \( n^2 \).

2. **Calcul du rapport des temps :**
   - Pour une liste de taille `n = 1000`, le temps est proportionnel à \( 1000^2 \).
   - Pour une liste de taille `10n = 10 000`, le temps est proportionnel à \( (10 \times 1000)^2 = 100 \times 1000^2 \).

3. **Conclusion :**
   - Le temps nécessaire pour trier une liste dix fois plus grande sera environ 100 fois plus long.

---

### **Réponse :**
**Réponse correcte : C- environ 100 × T**






### **Q14 - Algorithme de tri par sélection**

#### **Description de l'algorithme :**
L'algorithme présenté est une variante du **tri par sélection**. Voici ce qu'il fait :
- Pour chaque indice `i` de 0 à `n-1`, il cherche l'indice `rang_min` de l'élément minimum dans la sous-liste `L[i+1:]`.
- Une fois trouvé, il échange `L[i]` avec `L[rang_min]`.

#### **Complexité temporelle :**
L'explication donnée dans l'image montre que le nombre total de comparaisons est :
\[
(n-1) + (n-2) + (n-3) + \ldots + 1 = \frac{n(n-1)}{2} = \frac{n^2 - n}{2}
\]
- Le terme dominant est \( n^2 \).
- La complexité est donc **quadratique**, notée \( O(n^2) \).

---

### **Q15 - Coder l'algorithme en Python**

#### **Code Python :**
```python
def tri_selection(L):
    n = len(L)
    for i in range(n):
        rang_min = i
        for j in range(i+1, n):
            if L[j] < L[rang_min]:
                rang_min = j
        L[i], L[rang_min] = L[rang_min], L[i]
    return L

# Tests
liste_nombres = [29, 10, 14, 37, 13]
liste_chaines = ["pomme", "orange", "banane", "kiwi"]

print("Liste de nombres triée :", tri_selection(liste_nombres))
print("Liste de chaînes triée :", tri_selection(liste_chaines))
```

#### **Explication :**
- La fonction `tri_selection` prend une liste `L` en entrée.
- Elle parcourt chaque élément de la liste et cherche le minimum dans la sous-liste non triée.
- Elle échange ensuite l'élément courant avec le minimum trouvé.
- Les tests montrent comment utiliser cette fonction avec des listes de nombres et de chaînes de caractères.

---

### **Résumé :**
- **Complexité :** \( O(n^2) \) (quadratique).
- **Code :** Implémentation en Python fournie ci-dessus.


