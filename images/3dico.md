## **1. Qu’est-ce qu’un dictionnaire en Python ?**
Un **dictionnaire** est une structure de données qui permet de stocker des **paires clé-valeur**. Chaque valeur est associée à une clé unique, ce qui permet d’accéder rapidement aux données.

**Analogie** : Un dictionnaire est comme un annuaire téléphonique où chaque nom (clé) est associé à un numéro de téléphone (valeur).

**Syntaxe** :
```python
mon_dictionnaire = {"clé1": "valeur1", "clé2": "valeur2"}
```

---

## **2. Créer et manipuler un dictionnaire**

### **a. Création d’un dictionnaire**
```python
# Dictionnaire vide
dico_vide = {}

# Dictionnaire avec des valeurs
notes = {"Alice": 15, "Bob": 12, "Charlie": 18}
```

### **b. Accéder à une valeur**
On utilise la clé entre crochets :
```python
print(notes["Alice"])  # Affiche 15
```

**Attention** : Si la clé n’existe pas, Python lève une erreur `KeyError`. Pour éviter cela, utilisez la méthode `.get()` :
```python
print(notes.get("David", "Clé non trouvée"))  # Affiche "Clé non trouvée"
```

### **c. Ajouter ou modifier une valeur**
```python
notes["David"] = 14  # Ajoute la paire "David": 14
notes["Alice"] = 16  # Modifie la valeur associée à "Alice"
```

### **d. Supprimer une paire clé-valeur**
```python
del notes["Bob"]  # Supprime la paire "Bob": 12
# ou
valeur_supprimee = notes.pop("Charlie")  # Supprime et retourne la valeur
```

---

## **3. Parcourir un dictionnaire**
On peut parcourir les clés, les valeurs, ou les deux.

### **a. Parcourir les clés**
```python
for eleve in notes:
    print(eleve)  # Affiche chaque clé
```

### **b. Parcourir les valeurs**
```python
for note in notes.values():
    print(note)  # Affiche chaque valeur
```

### **c. Parcourir les paires clé-valeur**
```python
for eleve, note in notes.items():
    print(f"{eleve} a {note}/20")
```

---

## **4. Méthodes utiles des dictionnaires**
Voici les méthodes les plus importantes à connaître pour le bac :

| Méthode | Description | Exemple |
|---------|-------------|---------|
| `.keys()` | Retourne les clés | `notes.keys()` → `["Alice", "David"]` |
| `.values()` | Retourne les valeurs | `notes.values()` → `[16, 14]` |
| `.items()` | Retourne les paires (clé, valeur) | `notes.items()` → `[("Alice", 16), ("David", 14)]` |
| `.get(clé, défaut)` | Retourne la valeur ou une valeur par défaut | `notes.get("Bob", 0)` → `0` |
| `.pop(clé)` | Supprime une paire et retourne la valeur | `notes.pop("Alice")` → `16` |
| `.update(dico2)` | Met à jour avec un autre dictionnaire | `notes.update({"Eve": 19})` |

---

## **5. Exemple complet : Gestion des notes d’une classe**
```python
# Création du dictionnaire
notes = {"Alice": 15, "Bob": 12, "Charlie": 18}

# Ajout d'une note
notes["David"] = 14

# Affichage de la moyenne
moyenne = sum(notes.values()) / len(notes)
print(f"Moyenne de la classe : {moyenne:.2f}")

# Affichage des élèves et de leurs notes
for eleve, note in notes.items():
    print(f"{eleve} : {note}/20")
```

---

## **6. Cas particuliers et pièges à éviter**
- **Les clés doivent être uniques** : Si vous utilisez deux fois la même clé, la dernière valeur écrase la précédente.
- **Les clés doivent être immuables** : On ne peut pas utiliser une liste comme clé, mais on peut utiliser un tuple.
- **Les dictionnaires ne sont pas ordonnés** (avant Python 3.7). Depuis Python 3.7, l’ordre d’insertion est préservé, mais ce n’est pas une propriété garantie pour tous les usages.

---

## **7. Exercices types pour le bac**
### **Exercice 1 : Compter les occurrences**
Écrivez une fonction qui prend une chaîne de caractères et retourne un dictionnaire avec le nombre d’occurrences de chaque caractère.

```python
def compter_occurrences(chaine):
    occurrences = {}
    for caractere in chaine:
        if caractere in occurrences:
            occurrences[caractere] += 1
        else:
            occurrences[carere] = 1
    return occurrences
```

### **Exercice 2 : Fusionner deux dictionnaires**
Écrivez une fonction qui fusionne deux dictionnaires. Si une clé est présente dans les deux, on garde la valeur du second dictionnaire.

```python
def fusionner_dictionnaires(dico1, dico2):
    dico_fusionne = dico1.copy()
    dico_fusionne.update(dico2)
    return dico_fusionne
```

---

## **8. Résumé des points clés**
- Un dictionnaire associe des **clés uniques** à des **valeurs**.
- On accède aux valeurs avec `dico[clé]` ou `.get(clé)`.
- On parcourt un dictionnaire avec `.keys()`, `.values()`, ou `.items()`.
- Les méthodes `.update()`, `.pop()`, et `.get()` sont très utiles.

---

## **9. Pour aller plus loin (hors programme)**
- **Compréhensions de dictionnaires** :
  ```python
  carrés = {x: x**2 for x in range(5)}  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
  ```
- **Dictionnaires imbriqués** :
  ```python
  classes = {
      "Terminale A": {"Alice": 15, "Bob": 12},
      "Terminale B": {"Charlie": 18, "David": 14}
  }
  ```

---
