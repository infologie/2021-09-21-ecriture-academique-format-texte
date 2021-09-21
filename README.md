# L’écriture académique au format texte – Démonstration

Ce dépôt contient les ressources liées à la formation « L’écriture académique au format texte » organisée par l'Urfist de Bordeaux et animée par Arthur Perret le 21/09/2021. [Cliquez ici pour consulter le support de la formation.](https://www.arthurperret.fr/2021-09-21-ecriture-academique-format-texte.html) La partie « Démo » du support est reprise ci-dessous.

## Préparation

[Cliquez ici pour récupérer les fichiers de la démo.](https://github.com/infologie/2021-09-21-ecriture-academique-format-texte)

Lancez un terminal et déplacez-vous à l'endroit où vous avez mis ces fichiers. Par exemple, si les fichiers sont dans un répertoire `démo` sur votre Bureau dans macOS :

```
cd /Users/ici-votre-login/Desktop/démo
```

## Conversion simple

L'ordre des options n'a pas d'importance. Les commandes ci-dessous sont rédigées de manière à mimer le processus de conversion : on dit à Pandoc de prendre un fichier et de le convertir en un autre fichier.

Conversion dans un format pour traitement de texte :

```
pandoc doc-simple.md -o doc-simple.docx
```

Conversion en HTML :

```
pandoc doc-simple.md -o doc-simple.html
```

Conversion en PDF (nécessite d'[installer une distribution LaTeX](https://fr.wikibooks.org/wiki/LaTeX/Installer_LaTeX)) :

```
pandoc doc-simple.md -o doc-simple.pdf
```

Très vite, on va ajouter des options aux commandes Pandoc, qui ne tiennent plus toujours sur une ligne. Dans le reste du document, les commandes sont donc présentées autrement : le fichier à convertir occupe la dernière ligne, et il y a un retour à la ligne entre chaque option. Or un retour à la ligne (touche entrée) dans un terminal déclenche l'exécution de la commande ; s'il intervenait au milieu de la commande `pandoc`, celle-ci n'aurait pas l'effet escompté. Solution : on ajoute une barre oblique inverse avant un retour à la ligne pour signaler que ce dernier ne doit pas être pris en compte par le terminal. On peut alors copier et coller en bloc une commande de plusieurs lignes puis appuyer sur Entrée pour l'exécuter.

```
pandoc \
  -o doc-simple.docx \
  doc-simple.md 
```

## Options

Exemple (ajout d'une feuille de styles CSS à un export HTML) :

```
pandoc \
  --css=styles.css \
  --standalone \
  -o doc-simple.html \
  doc-simple.md
```

## Métadonnées

Le fichier `doc-avec-entete.md` commence par un en-tête au format [YAML](https://fr.wikipedia.org/wiki/YAML). On peut y inclure des métadonnées qui seront utilisées quelque soit le format d'export :

```yaml
title: L’écriture académique au format texte
author: Arthur Perret (Université Bordeaux Montaigne)
date: 21/09/2021
lang: fr-FR
```

On peut aussi inclure des options qui seront utilisées en fonction du format :

```yaml
documentclass: scrartcl
colorlinks: true
```

Les métadonnées peuvent être stockées dans un fichier séparé, auquel cas il faut l'indiquer dans la commande `pandoc` :

```
pandoc \
  --metadata-file=metadonnees.yml \
  --css=styles.css \
  --standalone \
  -o doc-sans-entete.html \
  doc-avec-entete-separe.md
```

## Modèles par défaut et personnalisation

Pandoc utilise un modèle par défaut pour chaque format. [Cliquez ici pour les consulter](https://github.com/jgm/pandoc-templates). Ils sont construits pour vous permettre de modifier l'export via des options, qu'elles soient dans l'en-tête de votre fichier Markdown ou dans la commande Pandoc utilisée pour le convertir. Lorsque la personnalisation voulue est plus poussée, il est possible de récupérer un modèle par défaut, le modifier et l'utiliser pour la conversion.

Mettez vos templates dans le dossier utilisateur de Pandoc afin qu'ils soient utilisés automatiquement.

> Sur les systèmes type Unix et macOS, il s'agira du sous-répertoire `pandoc` du répertoire de données de l'utilisateur, par défaut, `$HOME/.local/share`. Si ce répertoire n'existe pas et que `$HOME/.pandoc` existe, il sera utilisé (pour la rétro-compatibilité). Sous Windows, le répertoire de données utilisateur par défaut est `C:\Users\USERNAME\AppData\Roaming\pandoc`. Vous pouvez trouver le répertoire de données utilisateur par défaut sur votre système en saisissant `pandoc --version` dans un terminal. Les fichiers de données placés dans ce répertoire (par exemple, `reference.odt`, `reference.docx`, `epub.css`, `templates`) remplaceront les valeurs par défaut normales de pandoc.

Prenons un exemple. LaTeX est un système modulaire, c'est-à-dire que beaucoup de fonctionnalités sont disponibles sous formes de modules appelés « paquets » (en anglais *packages*) et peuvent être utilisées à la carte en fonction de vos besoins. En ajoutant une ligne contenant

`\usepackage{ici le nom du paquet}`

dans l'en-tête d'un document LaTeX ou dans un modèle de document LaTeX, cela ajoute la fonctionnalité correspondante au moment de la compilation en PDF.

Le template LaTeX par défaut de Pandoc peut être contrôlé via des options. Ainsi, si vous ajoutez une ligne contenant

`fontfamily: times`

dans l'en-tête de votre fichier Markdown, l'export PDF utilisera le paquet `times`, ce qui modifie la police du document. Ceci repose sur le template LaTeX, sans que vous ayiez eu à modifier ce dernier.

Mais parfois, il faut modifier le template. Dans les classes de document LaTeX KOMA-Script, plus adaptées aux normes typographiques européennes que les classes par défaut, plusieurs polices sont utilisées dans un même document (souvent une police sans empattements pour les titres, et avec empattements pour le corps du texte). On peut vouloir utiliser une famille de polices comme IBM Plex. Or l'option `fontfamily` ne fonctionnera pas, car on ne peut déclarer qu'un paquet avec, et on ne peut pas utiliser plusieurs fois une même option en YAML. La solution est d'ajouter les lignes suivantes au modèle LaTeX par défaut de Pandoc :

```latex
\usepackage{plex-serif}
\usepackage{plex-sans}
\usepackage{plex-mono}
```

Dans le fichier `template.latex` fourni, cette modification a été effectuée (lignes 39-41).

```
pandoc \
  --template=template.latex \
  --number-sections \
  -o doc-sans-entete.pdf \
  doc-avec-entete.md
```

## Citations

Pandoc accepte plusieurs formats de données bibliographiques. Les principaux utilisés dans l'écosystème Pandoc sont le BibTeX et le CSL JSON.

```
pandoc \
  --citeproc \
  --bibliography=references.bib \
  --csl=styles.csl \
  -o article.pdf \
  article.md
```

Zotero propose [un répertoire en ligne](https://www.zotero.org/styles) de fichiers de styles bibliographiques.

