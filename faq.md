# FAQ

## Que peut-on faire avec les styles ?

On peut paramétrer (présque) tout : les couleurs, les épaisseurs des lignes, les tailles des polices, les décalages (horizontaux et vérticaux)...

## Pour changer un style où il faut mettre la commande ?

- Pour changer un style qui concerne tout le planning on peut le mettre soit dans la commande `\tikzset` :
```tex
\tikzset{
  nombre de groupes=3
}
```
soit juste après `\begin{planning}` :
```tex
\begin{planning}[nombre de groupes=3]
```
- Pour changer un style qui concerne tous les créneaux d'un module il faut le mettre juste après `\begin{module}` :
```tex
\begin{module}{M44}{Géométrie}[nombre de groupes=3]
```
- Pour changer un style d'un créneau particulier il faut le mettre juste après `\creneau`, ou si vous avez créé des raccourcis comme `\cours` ou `\td`, juste après cette commande :
```tex
\td[echelle=.84, plus haut=1mm]{enseignants}{lundi}{08:00-10:00}{nom salle}
```

## Comment changer plusieurs styles à la fois ?

Il suffit de séparer les styles par des virgules. Par exemple pour changer les couleurs du titre et du sous-titre d'un module on peut faire :

```tex
\begin{module}{M44}{Géométrie}[
    titre/.append style={text=red},
    sous-titre/.append style={text=blue}
  ]
```

## Comment changer la taille d'une police ?

La taille des polices (titre, sous-titre, sur-titre) s'adapte en fonction du nombre de groupes. Pour changer la taille de toutes les polices vous pouvez utiliser le style `echelle`. 
```tex
\creneau[echelle=1.1]{sur-titre}{titre}{sous-titre}{lundi}{1/1}{08:00-10:00}
```
Pour changer la taille d'une seule des polices vous pouvez rajouter le style `scale` à la police en question. Par exemple pour changer la taille du titre :
```tex
\creneau[titre/.append style={scale=0.9}]{sur-titre}{titre}{sous-titre}{lundi}{1/1}{08:00-10:00}
```

En réalité, `echelle=X` rajoute `scale=X` aux trois styles `sur-titre`, `titre` et `sous-titre`. 

## Comment décaler vers le haut les textes dans un créneau ?

Pour décaler tous les textes dans un créneau vous pouvez utiliser le style `plus haut`. Par exemple pour décaler de 1 mm :
```tex
\creneau[plus haut=1mm]{sur-titre}{titre}{sous-titre}{lundi}{1/1}{08:00-10:00}
```
En réalité il suffit de monter le titre, car le sous-titre et le sur-titre sont positionnés relativement au titre. Pour monter le titre il suffit de rajouter au style `titre` le style `yshift` (ici « shift » signifié « décalage » et « y » est pour « verticale »). Ainsi, par exemple, pour monter de 7 pt au lieu de faire `plus haut=7pt` on peut faire aussi :
```tex
titre/.append style={yshift=7pt}
```
