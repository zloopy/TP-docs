---
title: TP Python 2 - Mécanique et 2e loi de Newton
tags: physique-chimie, terminale, python, numpy, matplotlib
---

# TP Python n°2 – Mécanique : 2ᵉ loi de Newton

[TOC]

**Niveau :** Terminale, spécialité Physique-Chimie | **Durée :** 1 h
**Outils :** Python 3, `numpy`, `matplotlib` (Capytale, Jupyter, Spyder, Edupython…)
**Objectif :** exploiter le pointage d'un mouvement avec Python (à la place d'un tableur) pour vérifier la 2ᵉ loi de Newton, puis confronter les mesures à un modèle théorique.

:::info
**Comment travailler :** les codes sont déjà écrits. Vous devez **lire les commentaires (`#`)**, **remplacer les `___`**, **exécuter dans votre éditeur Python**, puis **répondre aux questions de physique**. Revenez à l'aide-mémoire dès que vous hésitez.
:::

| Partie | Contenu | Durée |
|---|---|---|
| 0 | Aide-mémoire | 5 min |
| A | Trajectoire, vitesse, accélération, 2ᵉ loi de Newton | 28 min |
| B | Modèle théorique et comparaison aux mesures | 22 min |
| Bilan | Compte rendu | 5 min |

## Partie 0 – Aide-mémoire Python

### Calculs et tableaux

| Je veux… | J'écris… | Remarque |
|---|---|---|
| Charger les bibliothèques | `import numpy as np` et `import matplotlib.pyplot as plt` | Une fois, tout en haut |
| Créer un tableau de nombres | `t = np.array([0, 0.04, 0.08])` | Virgules entre les valeurs, **point** pour les décimales |
| Calculer sur tout le tableau | `x**2`, `2*x`, `x + y`, `x / y` | Pas besoin de boucle |
| Puissance | `t**2` | **Jamais** `^` |
| Racine carrée | `np.sqrt(x)` | |
| Valeur absolue | `np.abs(x)` | |
| Premier / dernier élément | `x[0]` / `x[-1]` | Le premier indice est **0** |
| Enlever le 1ᵉʳ et le dernier élément | `ay[1:-1]` | Les extrémités sont moins précises |
| Maximum / moyenne | `y.max()`, `y.mean()` | |
| Dériver | `np.gradient(y, t)` | Donne dy/dt |
| Ajuster par un polynôme | `np.polyfit(x, y, 2)` | `2` = degré. Renvoie les coefficients, du plus grand degré au plus petit |
| Angle d'un vecteur (vx, vy) | `np.arctan2(vy, vx)` | Résultat en radians |
| Radians → degrés | `np.degrees(angle)` | |
| Arrondir | `round(x, 2)` ou `np.round(tableau, 2)` | 2 chiffres après la virgule |
| Afficher | `print("g =", g, "m/s²")` | Texte entre guillemets, valeurs sans guillemets |

### Tracer un graphique

Un graphique, c'est toujours ces lignes, dans cet ordre :

```python
plt.figure()                       # 1. nouvelle figure (obligatoire pour chaque graphique)
plt.plot(x, y, "o-")               # 2. tracé : x d'abord, puis y. "o-" = points reliés
plt.xlabel("t (s)")                # 3. nom de l'axe x, avec l'unité
plt.ylabel("v (m/s)")              # 4. nom de l'axe y
plt.grid(True)                     # 5. quadrillage
plt.show()                         # 6. affichage
```

Options utiles (facultatives) :

```python
plt.plot(x, y, "o", label="mesures")   # "o" seul = points non reliés ; label = nom de la courbe
plt.plot(x, y, "-", label="modèle")    # "-" seul = trait continu
plt.legend()                           # affiche les noms (à mettre après les plt.plot)
plt.axis("equal")                      # même échelle sur x et y (pour une trajectoire)
```

### Si Python affiche une erreur

:::warning
- `NameError` : faute de frappe dans un nom, ou une cellule précédente n'a pas été exécutée.
- `SyntaxError` : parenthèse, guillemet ou virgule oublié (regarder la ligne indiquée et la précédente).
- `ValueError … same first dimension` : les deux tableaux n'ont pas la même longueur.
- Il reste des `___` : un trou n'a pas été complété.
- Deux courbes dans un même graphique alors que vous en vouliez deux : il manque `plt.figure()`.
:::

## Partie A – Projectile et 2ᵉ loi de Newton

### Contexte

Une balle de masse $m = 50{,}0$ g est lancée depuis le sol. Une chronophotographie pointée avec un logiciel donne sa position $(x ; y)$ toutes les 0,040 s. On suppose les frottements négligeables.

### Les données (à recopier puis exécuter)

```python
import numpy as np
import matplotlib.pyplot as plt

m = 0.0500        # masse en kg
g = 9.81          # m/s²

t = np.array([0.00, 0.04, 0.08, 0.12, 0.16, 0.20, 0.24, 0.28,
              0.32, 0.36, 0.40, 0.44, 0.48, 0.52, 0.56, 0.60])        # s

x = np.array([0.000, 0.104, 0.208, 0.312, 0.416, 0.520, 0.624, 0.728,
              0.832, 0.936, 1.040, 1.144, 1.248, 1.352, 1.456, 1.560])  # m

y = np.array([0.0000, 0.1162, 0.2166, 0.3014, 0.3704, 0.4238, 0.4615, 0.4835,
              0.4897, 0.4803, 0.4552, 0.4144, 0.3579, 0.2857, 0.1978, 0.0942])  # m

print(len(t), len(x), len(y))     # les trois nombres doivent être identiques
```

### A1. Trajectoire

**Q1.** Complétez et exécutez :

```python
plt.figure()
plt.plot(___, ___, "o-")         # trajectoire : y en fonction de x
plt.axis("equal")
plt.xlabel("x (m)")
plt.ylabel("___")
plt.grid(True)
plt.show()
```

**Q2.** Quelle est la forme de la trajectoire ? Quelle est la hauteur maximale ? (utilisez `print(y.max())`)

### A2. Vitesse

La vitesse est la dérivée de la position par rapport au temps. On la calcule numériquement :

```python
vx = np.gradient(x, t)        # composante horizontale
vy = np.gradient(y, t)        # composante verticale
```

**Q3.** Tracez $v_x(t)$ puis $v_y(t)$ (deux figures séparées). Complétez et exécutez :

```python
plt.figure()
plt.plot(t, ___, "o-")
plt.xlabel("t (s)")
plt.ylabel("v_x (m/s)")
plt.grid(True)
plt.show()

plt.figure()
plt.plot(t, ___, "o-")
plt.xlabel("t (s)")
plt.ylabel("v_y (m/s)")
plt.grid(True)
plt.show()
```

**Q4.** Quelle est la nature de $v_x(t)$ ? de $v_y(t)$ ? Que peut-on en déduire sur $a_x$ et $a_y$ ?

**Q5.** Calculez la vitesse initiale et l'angle de tir :

```python
v0 = np.sqrt(vx[0]**2 + vy[0]**2)               # norme de la vitesse à t = 0
alpha = np.degrees(np.arctan2(vy[0], vx[0]))    # angle de tir en degrés
print("v0 =", round(v0, 2), "m/s")
print("angle =", round(alpha), "degrés")
```

### A3. Accélération et 2ᵉ loi de Newton

**Q6.** L'accélération est la dérivée de la vitesse. Complétez, exécutez et observez :

```python
ay = np.gradient(___, t)             # dérivée de vy par rapport à t

plt.figure()
plt.plot(t, ay, "o-")
plt.xlabel("t (s)")
plt.ylabel("a_y (m/s²)")
plt.grid(True)
plt.show()

print("a_y moyen =", ay[1:-1].mean())    # [1:-1] : on enlève les deux extrémités
```

Les points sont dispersés. Pourquoi ? Comparez la moyenne à $-g$.

:::spoiler Indice pour Q6
On dérive **deux fois** des positions pointées à environ un millimètre près : l'incertitude est amplifiée à chaque dérivation.
:::

**Q7.** Méthode plus précise : on ajuste $y(t)$ par un polynôme de degré 2, $y = c_2 t^2 + c_1 t + c_0$. En dérivant deux fois, on trouve $a_y = 2c_2$.

```python
coef = np.polyfit(t, y, 2)       # renvoie [c2, c1, c0]
a_y = 2 * coef[0]                # coef[0] est c2
print("a_y =", round(a_y, 2), "m/s²")
```

Quelle méthode (Q6 ou Q7) donne le résultat le plus proche de $-g$ ?

**Q8.** Appliquez la 2ᵉ loi de Newton :

```python
F_y = m * ___                    # somme des forces verticales (N), avec a_y de Q7
P = m * g                        # poids (N)
print("m*a_y =", round(F_y, 3), "N")
print("P     =", round(P, 3), "N")
```

Comparez $F_y$ et $-P$. La balle est-elle soumise à d'autres forces que son poids ? L'hypothèse « frottements négligeables » est-elle justifiée ?

## Partie B – Modèle théorique et comparaison aux mesures

La 2ᵉ loi de Newton appliquée à la balle (seul le poids agit) donne $a_x = 0$ et $a_y = -g$. Par intégration, avec les conditions initiales $x(0) = y(0) = 0$ :

$$x(t) = v_{0x}\,t \qquad y(t) = -\frac{1}{2}g\,t^2 + v_{0y}\,t$$

### B1. Tracé du modèle

**Q9.** Le modèle utilise $v_{0x}$ (la valeur moyenne de $v_x$) et $v_{0y}$ (le coefficient de $t$ dans l'ajustement polynomial de la Q7). Complétez et exécutez :

```python
v0x = vx.mean()             # vitesse horizontale (constante)
v0y = coef[1]               # coefficient c1 de l'ajustement de la Q7

x_th = v0x * t
y_th = -g * t**2 / 2 + v0y * t

plt.figure()
plt.plot(x, y, "o", label="mesures")
plt.plot(x_th, ___, "-", label="modèle")      # trajectoire du modèle : y_th en fonction de x_th
plt.axis("equal")
plt.xlabel("x (m)")
plt.ylabel("y (m)")
plt.legend()
plt.grid(True)
plt.show()

print("v0x =", round(v0x, 2), "m/s ; v0y =", round(v0y, 2), "m/s")
```

**Q10.** Les mesures et le modèle sont-ils en accord ?

### B2. Écart entre mesures et modèle

**Q11.** Complétez et exécutez :

```python
ecart = y - y_th                                       # écart point par point
print("écart maximal =", round(np.abs(ecart).max(), 4), "m")
```

Comparez cet écart à la précision du pointage (environ 1 mm) et à la hauteur maximale de la balle. Le modèle « chute libre » est-il validé ?

### B3. Prédictions du modèle

**Q12.** Sur papier, à partir de $y(t)$ et de $v_y(t) = -g\,t + v_{0y}$, établissez :

- l'instant du sommet de la trajectoire $t_s$ (là où $v_y = 0$) ;
- la hauteur maximale $y_{max}$ ;
- la durée du vol $t_{vol}$ (retour au sol, $y = 0$, avec $t \neq 0$) ;
- la portée $d = v_{0x}\,t_{vol}$.

**Q13.** Calculez ces valeurs avec Python et comparez $y_{max}$ à `y.max()`. Complétez :

```python
t_s = v0y / g                      # instant du sommet
y_max = ___ / (2 * g)              # hauteur maximale : v0y au carré divisé par 2g
t_vol = 2 * v0y / g                # durée du vol
portee = v0x * t_vol               # portée

print("t_s =", round(t_s, 2), "s")
print("y_max =", round(y_max, 3), "m ; mesuré :", y.max(), "m")
print("t_vol =", round(t_vol, 2), "s")
print("portée =", round(portee, 2), "m")
```

:::spoiler Indice pour la formule de y_max
$y_{max} = y(t_s) = \dfrac{v_{0y}^2}{2g}$ : remplacez $t$ par $t_s = \dfrac{v_{0y}}{g}$ dans $y(t)$.
:::

## Pour aller plus loin (si vous avez terminé)

:::success
Simulation de la 2ᵉ loi de Newton pas à pas (programme fourni, rien à compléter). À chaque petit pas de temps `dt`, on met à jour la vitesse puis la position :

```python
dt = 0.001                  # pas de temps (s)
n = 640                     # nombre de pas

xs = np.zeros(n)            # tableaux remplis de zéros
ys = np.zeros(n)
vxs = np.zeros(n)
vys = np.zeros(n)
vxs[0] = v0x                # conditions initiales
vys[0] = v0y

for i in range(n - 1):                    # on répète n-1 fois
    vxs[i+1] = vxs[i]                     # a_x = 0
    vys[i+1] = vys[i] - g * dt            # a_y = -g
    xs[i+1] = xs[i] + vxs[i+1] * dt       # nouvelle position
    ys[i+1] = ys[i] + vys[i+1] * dt

plt.figure()
plt.plot(x, y, "o", label="mesures")
plt.plot(xs, ys, "-", label="simulation")
plt.axis("equal")
plt.xlabel("x (m)")
plt.ylabel("y (m)")
plt.legend()
plt.grid(True)
plt.show()
```

Que se passe-t-il si vous prenez un pas `dt = 0.04` avec `n = 16` ? Pourquoi `dt` doit-il être petit ?
:::

## Compte rendu

Enregistrez votre fichier sous le nom `NOM_Prenom_TP2.py` (ou partagez le lien Capytale) avec toutes les figures et les réponses aux questions écrites en commentaires `#`.
