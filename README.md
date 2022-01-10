# Emplois du temps en LaTeX [[dépôt git](https://github.com/ktzanev/planning) et [site web](https://ktzanev.github.io/planning)]

Ce dépôt décrit l'utilisation du style [planning.sty](planning.sty) pour dessiner l'emploi du temps d'une formation.

## Exemples disponibles :

- Le planning du L2 Math pour 2020/21 sous format [pdf](L2S2-Planning-2020-2021.pdf) et la source [tex](L2S2-Planning-2020-2021.tex).
- Le planning du M1 CAPES pour 2020/21 sous format [pdf](CAPES-Planning-2020-2021.pdf) et la source [tex](CAPES-Planning-2020-2021.tex).
- Le planning du M1 Math pour 2020/21 sous format [pdf](M1-Planning-2020-2021.pdf) et la source [tex](M1-Planning-2020-2021.tex).

## Récupération des sources

Vous pouvez récupérer les sources sous format [zip](https://github.com/ktzanev/planning/archive/master.zip).
Ou vous pouvez cloner ce dépôt avec la commande :

```shell
> git clone https://github.com/ktzanev/planning.git .
```

## Utilisation

Cette bibliothèque est basée sur `tikz` est par conséquent la configuration se fait via des styles `tikz` :
```latex
\tikzset{
  largeur du planning = 21cm,
  hauteur du planning = 17cm,
  largeur du nom du jour = 4cm,
  largeur du nom du groupe = 1cm,
  hauteur du deplacement vertical des heures = 4mm,
  nombre de jours = 5,
  nombre d'heures=11, % nombre d'heures par jour
  heure du debut=8,
  nombre de groupes=3,
}
```
Il y a aussi les style optionnels
- `etiquette jour`, le style des `node` qui affiche les noms des jours,
- `etiquette groupe`, le style des `node` qui affiche les numéros des groupes,
- `etiquette heure`, le style des `node` qui affiche les heures,
- `etiquette demi-heure`, le style des `node` qui affiche les demi-heures,
- `ligne jour`, la style des lignes horizontales qui séparent les jours (ainsi que les bords horizontaux),
- `ligne groupe`, la style des lignes horizontales qui séparent les groupes,
- `ligne heure`, la style des lignes verticales des heures,
- `ligne demi-heure`, la style des lignes verticales des demi-heures,
- `lignes verticales`, la style des autres lignes verticales (ainsi que les bords verticaux).

Ainsi par exemple pour ne pas afficher la ligne séparatrice des groupes on peut faire
```latex
\tikzset{
  ligne groupe/.style = {draw=none}
}
```

Il y a essentiellement deux environnements `planning` et `module` et une commande `creneau`:

```latex
\tikzset{
  cours/.style={
    titre/.append style={echelle=1.05, align=center},
    sur-titre/.append style={echelle=.85},
    sous-titre/.append style={echelle=.7},
    line width=.7pt,
  }
}
\begin{planning}[screen colors 1]
  \begin{module}{M41}{Analyse}
    \creneau[cours]{Cours \numeromodule}{\titremodule}{salle M1-DLVP}{mardi}{1/1}{10:15-11:45}
  \end{module}
\end{planning}
```

- L'environnement `planning` produit une image `tikz`.
- L'environnement `module`
  - définir les macros `\numeromodule` et `\titremodule`
  - fixe la couleur automatiquement
  - permet de modifier les paramètres par défaut, comme `[nombre de groupes=2]`.

### La commande `\creneau`

- Le premier paramètre est optionnel et il détermine le style (couleurs, épaisseurs des lignes, tailles des polices).
- Les trois paramètres suivants sont le « sur-titre » (qui est souvent le type d'enseignement), le « titre » (qui est souvent le nom du module) et le « sous-titre » (qui est souvent la salle).
- Les deux paramètres suivants, la journée et le groupe, détermine la position verticale et la hauteur du créneau dessiné.
- Le dernier paramètre, les horaires, détermine la position horizontale et la largeur du créneau.

Le paramètre du groupe peut prendre plusieurs formes :
- La forme `{k-l/m}` indique qu'il s'agit d'un créneau qui concerne les groupes de `k` à `l` parmi `m` groupes (= nombre de zones horizontales d'une journée).
- Le plus souvent le paramètre `l` est omis, et dans ce cas il est remplacé par `k`. Ainsi par exemple `{2/3}` indique le groupe 2 parmi 3.
- si le paramètre `m` est omis, comme dans `{1}`, alors le nombre de groupes par défaut est utilisé. Le nombre de groupes par défaut est fixé avec le style `nombre de groupes` qui peut être utilisé de façon globale ou dans un module particulier.

### Les styles de `\creneau`

Il y a deux style utilitaires pour les créneaux :
- `echelle` qui détermine la taille (relative) de la police utilisé. Par exemple `echelle=0.84` ;
- `plus haut` qui permet de monter (ou descendre) les textes (titre, sur/sous-titre). Par exemple `plus haut=1mm`.

### Les raccourcies

Pour faciliter l'écriture il est judicieux de définir des commandes « raccourcies » comme

```latex
% \cours{jour}{08:00-10:00}{amphi}
\newcommand{\cours}[3]{
  \creneau[cours]{Cours \numeromodule}{\titremodule}{#3}{#1}{1/1}{#2}
}
```

Ainsi après on peut utiliser
```latex
  \begin{module}{M41}{Analyse}
    \cours{mardi}{10:15-11:45}{salle M1-DLVP}
  \end{module}
```
### Les couleurs

Il y 3 thèmes de couleurs qui peuvent être sélectionnés avec `screen colors 1`, `screen colors 2` et `screen colors 3` (ce dernier est par défaut).

Il y a aussi un thème de couleurs en niveaux de gris (destiné à l'impression) : `print colors`.

Pour redéfinir la couleur du troisième module il suffit de faire par exemple :

```latex
\colorlet{module3}{red}
```

### Questions fréquentes

La page [FAQ](faq.md) contient des réponses à des questions particulières.
