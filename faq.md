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
\td[sous-titre/.append style={echelle=.84}]{enseignants}{lundi}{08:00-10:00}{nom salle}
```

## Comment changer plusieurs styles à la fois ?

Il suffit de séparer les styles par des virgules, comme :

```tex
\begin{module}{M44}{Géométrie}[titre/.append style={yshift=7mm}, sous-titre/.append style={scale=1.2}]
```
ou
```tex
\begin{module}{M44}{Géométrie}[
    titre/.append style={yshift=7mm},
    sous-titre/.append style={scale=1.2}
  ]
```

## Comment changer la taille d'une police ?

Pour changer la taille d'une police vous pouvez utiliser le style `echelle` (qui s'adapte en fonction du nombre de groupes) ou le plus standard `scale`. Ces styles peuvent être rajoutés aux styles du texte en question :
- Pour changer la taille du sous-titre (qui contient souvent la salle) on peut faire :
```tex
\td[sous-titre/.append style={scale=1.2}]{enseignants}{lundi}{08:00-10:00}{nom salle}
```

## Comment décaler vers le haut les textes dans un créneau ?

Pour décaler tous les textes dans un créneau il suffit de monter le titre, car le sous-titre et le sur-titre sont positionnés relativement au titre. Pour monter le titre il suffit de rajouter au style `titre` le style `yshift` (ici « shift » signifié « décalage » et « y » est pour « verticale »). Ainsi par exemple pour monter de 7 mm :
```tex
titre/.append style={yshift=7mm}
```
