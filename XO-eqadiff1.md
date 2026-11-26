# Fiche méthode : équations différentielles d'ordre 1

Une équation différentielle d'ordre 1 relie une fonction $y(x)$ à sa dérivée $y'(x)$. Ici, on étudie les équations de la forme

$$y' + ay = f(x)$$

où $a$ est un nombre réel fixé.

- Si $f(x) = 0$, l'équation est **sans second membre** (ou « à membre nul »).
- Sinon, $f(x)$ est le **second membre**.

---

## 1. Équation sans second membre : $y' + ay = 0$

**Solution générale :**

$$y(x) = C\,e^{-ax}, \qquad C \in \mathbb{R}$$

**Exemple :** $y' = 3y$ s'écrit $y' - 3y = 0$, donc $y(x) = C\,e^{3x}$.

---

## 2. Équation avec second membre constant : $y' + ay = b$

**Étape 1 : solution particulière constante.** Si $y$ est constante ($y' = 0$), l'équation devient $ay = b$, donc :

$$y_p(x) = \frac{b}{a} \quad (a \neq 0)$$

**Étape 2 : solution générale.** On ajoute la solution sans second membre :

$$y(x) = C\,e^{-ax} + \frac{b}{a}$$

**Exemple :** $y' + y = 4$ donne $y_p = 4$ et $y(x) = C\,e^{-x} + 4$.

---

## 3. Second membre polynomial ou exponentiel

Il faut **deviner la forme** de la solution particulière, puis trouver ses coefficients en la remplaçant dans l'équation.

| Second membre $f(x)$ | Forme de $y_p$ à essayer |
|---|---|
| Nombre constant $b$ | $y_p = K$ |
| Polynôme de degré 1, $px + q$ | $y_p = Px + Q$ |
| Exponentielle $k\,e^{mx}$ | $y_p = K\,e^{mx}$ |

**Exemple :** $y' + y = 3x + 1$. On cherche $y_p = Px + Q$, donc $y_p' = P$. En remplaçant : $P + Px + Q = 3x + 1$, d'où $P = 3$ et $Q = -2$. Donc $y_p = 3x - 2$ et $y(x) = C\,e^{-x} + 3x - 2$.

---

## 4. Méthode générale en 4 étapes

1. **Écrire l'équation** sous la forme $y' + ay = f(x)$.
2. **Résoudre l'équation sans second membre** $y' + ay = 0$ : on obtient $y_h = C\,e^{-ax}$.
3. **Trouver une solution particulière** $y_p$ (constante, polynomiale ou exponentielle selon $f$).
4. **Solution générale :** $y = y_h + y_p$.

---

## 5. Solution particulière et condition initiale

La solution générale contient une constante $C$. Une **condition initiale** $y(x_0) = y_0$ permet de trouver la solution **particulière** unique.

**Exemple :** $y' + 2y = 4$ avec $y(0) = 1$.
- $y_p = 2$, donc $y(x) = C\,e^{-2x} + 2$.
- $y(0) = C + 2 = 1$, donc $C = -1$.
- Solution particulière : $y(x) = 2 - e^{-2x}$.

---

## Résumé

- **Solution générale** : $y = y_h + y_p$, avec une constante $C$.
- **Solution particulière** : la solution obtenue après avoir fixé $C$ avec une condition initiale.
- **Vérification** : remplacer $y$ et $y'$ dans l'équation pour contrôler le résultat.
