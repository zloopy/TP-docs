# TP Python n°1 – Chimie : acides, bases et constantes d'équilibre

**Niveau :** Terminale, spécialité Physique-Chimie | **Durée :** 1 h
**Outils :** Python 3, `numpy`, `matplotlib` (Capytale, Jupyter, Spyder, Edupython…)
**Objectif :** utiliser Python à la place d'un tableur pour exploiter un dosage pH-métrique et déterminer des grandeurs liées à un équilibre acido-basique.

> **Comment travailler :** les codes sont déjà écrits. Vous devez **lire les commentaires (`#`)**, **remplacer les `___`** par la bonne variable ou la bonne valeur, **exécuter**, puis **répondre aux questions de chimie**. Revenez à l'aide-mémoire dès que vous hésitez.

| Partie | Contenu | Durée |
|---|---|---|
| 0 | Aide-mémoire et données | 8 min |
| 1 | Courbe de dosage | 10 min |
| 2 | Volume équivalent | 12 min |
| 3 | pKa et constante K de la réaction de dosage | 10 min |
| 4 | Diagramme de distribution | 10 min |
| 5 | Taux d'avancement et dilution | 10 min |

---

## Partie 0 – Aide-mémoire Python

### Calculs et tableaux

| Je veux… | J'écris… | Remarque |
|---|---|---|
| Charger les bibliothèques | `import numpy as np` et `import matplotlib.pyplot as plt` | Une fois, tout en haut |
| Créer un tableau de nombres | `V = np.array([1, 2, 3])` | Virgules entre les valeurs, **point** pour les décimales |
| Calculer sur tout le tableau | `V * 2`, `V + 1`, `V / 5` | Pas besoin de boucle |
| Puissance | `10**(-pH)` | **Jamais** `^` |
| Logarithme décimal | `np.log10(x)` | |
| Premier / dernier élément | `V[0]` / `V[-1]` | Le premier indice est **0** |
| Nombre d'éléments | `len(V)` | |
| Arrondir | `round(x, 2)` ou `np.round(tableau, 2)` | 2 chiffres après la virgule |
| Afficher | `print("V_E =", V_E, "mL")` | Texte entre guillemets, valeurs sans guillemets |
| Dériver | `np.gradient(y, x)` | Donne dy/dx |
| Position du maximum | `np.argmax(tableau)` | Donne la **position**, pas la valeur |
| Lire une valeur à un endroit précis | `np.interp(x0, x, y)` | Donne le `y` correspondant à `x0` |
| 500 valeurs régulières de 0 à 14 | `np.linspace(0, 14, 500)` | |

### Tracer un graphique

Un graphique, c'est toujours ces lignes, dans cet ordre :

```python
plt.figure()                       # 1. nouvelle figure (obligatoire pour chaque graphique)
plt.plot(x, y, "o-")               # 2. tracé : x d'abord, puis y. "o-" = points reliés
plt.xlabel("V (mL)")               # 3. nom de l'axe x, avec l'unité
plt.ylabel("pH")                   # 4. nom de l'axe y
plt.grid(True)                     # 5. quadrillage
plt.show()                         # 6. affichage
```

Options utiles (facultatives) :

```python
plt.plot(x, y, label="nom")        # donne un nom à la courbe
plt.legend()                       # affiche les noms (à mettre après les plt.plot)
plt.title("Mon titre")             # titre du graphique
plt.axvline(4.76, linestyle="--")  # droite verticale pointillée en x = 4.76
```

### Si Python affiche une erreur
- `NameError` → faute de frappe dans un nom, ou une cellule précédente n'a pas été exécutée.
- `SyntaxError` → parenthèse, guillemet ou virgule oublié (regarder la ligne indiquée et la précédente).
- `ValueError … same first dimension` → les deux tableaux n'ont pas la même longueur.
- Il reste des `___` → un trou n'a pas été complété.
- Deux courbes dans un même graphique alors que vous en vouliez deux → il manque `plt.figure()`.

---

## Le contexte de l'expérience

On dose $V_A = 20{,}0$ mL d'acide éthanoïque $\mathrm{CH_3COOH}$ (noté HA), de concentration $C_A$ inconnue, par une solution de soude de concentration $C_B = 0{,}100$ mol·L⁻¹. On mesure le pH en fonction du volume $V$ de soude versé.

$$\mathrm{CH_3COOH(aq) + HO^-(aq) \longrightarrow CH_3COO^-(aq) + H_2O(\ell)}$$

Données : $K_e = 10^{-14}$ ; $c^\circ = 1$ mol·L⁻¹.

### Les mesures (à recopier telles quelles puis exécuter)

```python
import numpy as np
import matplotlib.pyplot as plt

V = np.array([0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 19, 19.5,
              20, 20.5, 21, 22, 24, 26, 30])          # volume de soude (mL)

pH = np.array([2.88, 3.81, 4.16, 4.39, 4.58, 4.76, 4.94, 5.13, 5.36, 5.71,
               6.04, 6.35, 8.73, 11.09, 11.39, 11.68, 11.96, 12.12, 12.30])

print(len(V), len(pH))      # les deux nombres doivent être égaux
```

**Q0.** Combien y a-t-il de mesures ? Que valent `V[0]` et `pH[0]` ? Que représentent-ils chimiquement ?

---

## Partie 1 – La courbe de dosage

**Q1.** Complétez le code pour tracer pH = f(V), puis exécutez-le.

```python
plt.figure()
plt.plot(___, ___, "o-")          # x d'abord, puis y
plt.xlabel("___")                 # avec l'unité
plt.ylabel("___")
plt.grid(True)
plt.show()
```

**Q2.** Décrivez l'allure de la courbe. Repérez à l'œil la zone du saut de pH et estimez le volume équivalent.

---

## Partie 2 – Volume équivalent par la méthode de la dérivée

À l'équivalence, la dérivée $\dfrac{d\mathrm{pH}}{dV}$ est **maximale**.

**Q3.** Complétez, exécutez et observez la courbe de la dérivée :

```python
dpH_dV = np.gradient(pH, V)       # dérivée de pH par rapport à V

plt.figure()
plt.plot(V, ___, "s-")            # le tableau de la dérivée
plt.xlabel("V (mL)")
plt.ylabel("dpH/dV (1/mL)")
plt.grid(True)
plt.show()
```

**Q4.** Trouvez le volume équivalent. Ces trois lignes sont à comprendre, puis à exécuter :

```python
i = np.argmax(dpH_dV)      # position du maximum dans le tableau
V_E = V[i]                 # volume qui correspond à cette position
print("V_E =", V_E, "mL")
```

Que vaut $V_E$ ? Est-ce cohérent avec votre estimation de Q2 ?

**Q5.** Écrivez la relation à l'équivalence entre $C_A V_A$ et $C_B V_E$ (tableau d'avancement), puis complétez :

```python
C_B = 0.100        # mol/L
V_A = 20.0         # mL
C_A = ___ * V_E / V_A      # à compléter avec la relation établie
print("C_A =", C_A, "mol/L")
```

---

## Partie 3 – pKa et constante de la réaction de dosage

À la demi-équivalence ($V = V_E/2$), $[\mathrm{HA}] = [\mathrm{A^-}]$ donc $\mathrm{pH} = \mathrm{p}K_A$.

**Q6.** Le volume $V_E/2$ n'est pas forcément une mesure : `np.interp` permet de lire le pH correspondant. Complétez et exécutez :

```python
pKA = np.interp(V_E / 2, V, pH)     # pH lu pour V = V_E/2
print("pKA =", round(pKA, 2))

KA = 10**(-___)                      # KA à partir de pKA
print("KA =", KA)
```

**Q7.** Sur papier : montrez que la constante d'équilibre de la réaction de dosage est $K = \dfrac{K_A}{K_e}$ (indice : multipliez l'expression de $K$ en haut et en bas par $[\mathrm{H_3O^+}]$). Puis calculez-la :

```python
K = KA / ___
print("K =", K)
```

**Q8.** La réaction de dosage est-elle totale ? Pourquoi est-ce nécessaire pour un dosage ?

---

## Partie 4 – Diagramme de distribution

Les proportions de HA et de A⁻ en fonction du pH sont :

$$\%\mathrm{HA} = \frac{100}{1 + 10^{\mathrm{pH} - \mathrm{p}K_A}} \qquad \%\mathrm{A^-} = 100 - \%\mathrm{HA}$$

**Q9.** Lisez le code, complétez les trous, puis exécutez.

```python
pH_th = np.linspace(0, 14, 500)               # 500 valeurs de pH entre 0 et 14
pct_HA = 100 / (1 + 10**(pH_th - pKA))        # % de HA pour chaque pH
pct_A = 100 - pct_HA                          # % de A-

plt.figure()
plt.plot(pH_th, pct_HA, label="CH3COOH")
plt.plot(pH_th, ___, label="CH3COO-")         # courbe de A-
plt.axvline(___, linestyle="--")              # droite verticale en pH = pKA
plt.xlabel("pH")
plt.ylabel("Proportion (%)")
plt.legend()
plt.grid(True)
plt.show()
```

**Q10.** Que valent les proportions de HA et A⁻ au point d'intersection ? Quelle espèce prédomine à pH = 3 ? À pH = 8 ?

---

## Partie 5 – Taux d'avancement final et dilution

On mesure le pH de solutions d'acide éthanoïque de concentrations différentes :

```python
C = np.array([1e-1, 1e-2, 1e-3, 1e-4])        # mol/L  (1e-2 signifie 10^-2)
pH_sol = np.array([2.88, 3.39, 3.91, 4.47])
```

On rappelle que $\tau = \dfrac{x_f}{x_{max}} = \dfrac{[\mathrm{H_3O^+}]_f}{C}$ et que $Q_{r,éq} = \dfrac{[\mathrm{H_3O^+}]^2}{C - [\mathrm{H_3O^+}]}$ pour un acide faible dans l'eau.

**Q11.** Complétez, exécutez et lisez les résultats :

```python
h = 10**(-pH_sol)               # concentration en H3O+ (mol/L) pour chaque solution
tau = h / ___                   # taux d'avancement final
Qr = h**2 / (C - h)             # quotient de réaction à l'équilibre

print("C   =", C)
print("tau =", np.round(tau, 3))
print("Qr  =", Qr)
```

**Q12.** Que remarquez-vous sur $Q_{r,éq}$ ? Comparez avec $K_A$ trouvé en Q6.

**Q13.** Tracez $\tau$ en fonction de $C$. `plt.semilogx` fonctionne comme `plt.plot`, mais l'axe des abscisses est en échelle logarithmique :

```python
plt.figure()
plt.semilogx(C, tau, "o-")
plt.xlabel("C (mol/L)")
plt.ylabel("___")
plt.grid(True)
plt.show()
```

Comment évolue $\tau$ quand on dilue ? La transformation est-elle totale ?

---

## Pour aller plus loin (si vous avez terminé)

1. Sur le graphique de la dérivée (Q3), ajoutez une droite verticale pointillée en $V_E$ avec `plt.axvline(V_E, linestyle="--")`.
2. Comparez votre pKA à la valeur tabulée 4,76 : calculez l'écart relatif en %.

## Compte rendu

Enregistrez votre fichier sous le nom `NOM_Prenom_TP1.py` (ou le lien Capytale) avec toutes les figures et les réponses aux questions écrites en commentaires `#`.
