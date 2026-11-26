# Fiche méthode : équations différentielles du premier ordre

## 1. Variables séparables

**Forme :** $y' = f(x)\,g(y)$

**Méthode :**
1. Séparer : $\dfrac{dy}{g(y)} = f(x)\,dx$
2. Intégrer les deux membres : $\displaystyle\int \dfrac{dy}{g(y)} = \int f(x)\,dx + C$
3. Résoudre si possible en $y$.
4. Ne pas oublier les **solutions constantes** $y = y_0$ où $g(y_0) = 0$.

**Exemple :** $y' = xy^2 \Rightarrow -\dfrac{1}{y} = \dfrac{x^2}{2} + C \Rightarrow y = \dfrac{-2}{x^2 + K}$

---

## 2. Équations linéaires d'ordre 1

**Forme :** $y' + a(x)\,y = b(x)$

**Méthode (facteur intégrant) :**
1. Calculer $A(x) = \displaystyle\int a(x)\,dx$ (sans constante).
2. Poser le facteur intégrant $\mu(x) = e^{A(x)}$.
3. Multiplier : $(\mu y)' = \mu\, b$.
4. Intégrer : $y = \dfrac{1}{\mu(x)}\left(\displaystyle\int \mu(x)\,b(x)\,dx + C\right)$.

**Rappel :** la solution générale = solution homogène $y_h = C e^{-A(x)}$ + une solution particulière.

**Exemple :** $y' + 2y = e^x$ a pour solution $y = \dfrac{e^x}{3} + C e^{-2x}$.

---

## 3. Équations de Bernoulli

**Forme :** $y' + a(x)\,y = b(x)\,y^\alpha$, avec $\alpha \neq 0$ et $\alpha \neq 1$

**Méthode :**
1. Poser $z = y^{1-\alpha}$.
2. Vérifier que $z' + (1-\alpha)\,a(x)\,z = (1-\alpha)\,b(x)$ : c'est une équation **linéaire** en $z$.
3. Résoudre en $z$, puis revenir à $y = z^{1/(1-\alpha)}$.

**Piège :** pour $\alpha \neq 1$, ne pas oublier que $y = 0$ est aussi une solution.

---

## 4. Équations homogènes

**Forme :** $y' = f\!\left(\dfrac{y}{x}\right)$

**Méthode :**
1. Poser $u = \dfrac{y}{x}$, donc $y = ux$ et $y' = u + xu'$.
2. Obtenir $x\,u' = f(u) - u$, équation à **variables séparables** en $u$.
3. Résoudre, puis revenir à $y = x\,u(x)$.

**Exemple :** $y' = 1 + \dfrac{y}{x}$ donne $u = \ln|x| + C$, soit $y = x\ln|x| + Cx$.

---

## 5. Équations exactes (bonus)

**Forme :** $M(x,y)\,dx + N(x,y)\,dy = 0$

**Test :** l'équation est exacte si $\dfrac{\partial M}{\partial y} = \dfrac{\partial N}{\partial x}$.

**Méthode :** il existe $F(x,y)$ telle que $\dfrac{\partial F}{\partial x} = M$ et $\dfrac{\partial F}{\partial y} = N$. Les solutions sont données par $F(x,y) = C$.

---

## 6. Problème de Cauchy

Une condition initiale $y(x_0) = y_0$ permet de déterminer la constante $C$ après avoir trouvé la solution générale.

---

## Tableau récapitulatif

| Type | Reconnaître | Méthode principale |
|---|---|---|
| Variables séparables | $y' = f(x)g(y)$ | Séparer et intégrer |
| Linéaire | $y' + a(x)y = b(x)$ | Facteur intégrant $e^{\int a}$ |
| Bernoulli | terme $y^\alpha$ | Substitution $z = y^{1-\alpha}$ |
| Homogène | $y' = f(y/x)$ | Substitution $u = y/x$ |
| Exacte | $M\,dx + N\,dy = 0$ | Potentiel $F$ |
