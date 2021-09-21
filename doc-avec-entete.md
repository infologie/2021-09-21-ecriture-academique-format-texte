---
title: L’écriture académique au format texte
author: Arthur Perret (Université Bordeaux Montaigne)
date: 21/09/2021
lang: fr-FR
documentclass: scrartcl
colorlinks: true
---

# L'auteur {-}

Doctorant à l'université [Bordeaux Montaigne](https://www.u-bordeaux-montaigne.fr/fr/index.html), laboratoire [MICA](https://mica.u-bordeaux-montaigne.fr), axe [E3D](https://mica.u-bordeaux-montaigne.fr/e3d/). Je contribue au programme de recherche ANR [HyperOtlet](https://hyperotlet.hypotheses.org/le-projet). Je suis actuellement ATER à l'[IUT Bordeaux Montaigne](https://www.iut.u-bordeaux-montaigne.fr). Je participe aussi à l'organisation des journées d'étude [Reticulum](http://reticulum.info) et du groupe de discussion [Inachevé d'imprimer](https://inacheve-dimprimer.net). J'ai fait mes études de master à l'[Enssib](https://www.enssib.fr), où certains enseignants ([Éric Guichard](http://barthes.enssib.fr), [Antoine Fauchié](https://www.quaternum.net)) m'ont fait découvrir des outils d'écriture académique au format texte (LaTeX, Markdown, Pandoc). J'alimente depuis quelques années [un site](https://www.arthurperret.fr) avec mes recherches. Je rédige actuellement ma thèse sur Paul Otlet.

# Traitement de texte

Un traitement de texte est un outil polyvalent ; par conséquent, il tend souvent vers l’usine à gaz et s'avère gourmand en ressources (énergie, mémoire). Ancré dans le paradigme de l’imprimé, il est fondamentalement inadapté à la communication via le Web. Son modèle économique (en tout pas pour les logiciels propriétaires) est de moins en moins avantageux pour le consommateur (abonnement). Ses formats sont soit complètement fermés (`.doc`) soit difficiles à utiliser via d’autres outils (`.docx`).

# Format texte

Le format texte constitue une alternative au traitement de texte, sans pour autant le remplacer totalement.

## Définition

En informatique, au niveau le plus fondamental, tout est exprimé dans un alphabet numérique binaire : 0 et 1. Un format, c'est une convention qui établit la correspondance entre une certaine succession de 0 et de 1, et quelque chose d'autre : par exemple une couleur, ou une lettre de l'alphabet, ou la position d'un pixel sur un écran. L'expression « format texte » désigne une catégorie de formats pour lesquels le contenu en binaire des fichiers encode des caractères textuels.

<!-- Exemple du fichier image. Exemple du fichier texte. Pourquoi on peut ouvrir un fichier image dans un éditeur de texte (et ce qu'on constate) et pas un fichier texte dans une visualiseuse d'images. -->

Le format texte a des avantages inhérents : légèreté, pérennité, interopérabilité, choix. Il fonde une offre logicielle variée, qui comprend aussi bien des plateformes intégrées alternatives à Google Docs que des systèmes modulaires bricolés avec des logiciels libres. Surtout, il existe des styles d’interface différents pour le format texte : on a le choix de travailler en WYSIWYG ou non.

## Format texte et formats pour traitement de texte

Le format `.doc` est uniquement binaire, on ne peut l'utiliser qu'avec un traitement de texte. Le format `.docx` lui est comparable au `.zip`, c'est en fait un répertoire compressé qui contient des fichiers au format texte, balisés en XML ; on peut les ouvrir dans un éditeur de texte mais concrètement ils sont destinés à être interprétés par la machine, pas par l'humain.

## Implications de l'utilisation du format texte

L'utilisation du format texte n'est pas plus ou moins simple que celle du traitement de texte, elle occasionne plutôt ce que j'appellerais un déplacement des efforts cognitifs. L'interface textuelle lève l'ambiguïté entre fond et forme. Conséquence : on a plus de temps de cerveau disponible pour élaborer le fond, mais on va devoir monter en compétence d'écriture et d’automatisation, notamment pour gérer la forme (via des styles, des modèles).

Deux principales difficultés entourent le format texte. Premièrement, son utilisation nécessite un changement de culture technique, un apprentissage. Deuxièmement, sa pratique rentre en conflit avec les habitudes prises par notre entourage (collègues, industries diverses comme par exemple l’édition).

Sur ce deuxième point notamment, les solutions logicielles qui permettraient de faciliter la collaboration autour du format texte ne sont pas entièrement satisfaisantes. Il existe des solutions d’écriture collaborative synchrone reposant sur des formats ouverts, par exemple [HackMD](https://hackmd.io) [^1] ; il existe même des plateformes dédiées à l'écriture académique, comme [Authorea](https://www.authorea.com/users/332544-arthur-perret). Mais le fait est que ces outils manquent de fonctionnalités (ex : HackMD ne facilite pas spécifiquement des besoins comme les citations) ou bien complexifient considérablement des processus qui pourraient être beaucoup plus simples (ex : les citations dans Authorea).

[^1]: Voir également [CodiMD](https://codimd.math.cnrs.fr), version ouverte proposée par l'équipe de HackMD, et [HedgeDoc](https://hedgedoc.org), une copie du projet gérée par une communauté bénévole.

## Principaux formats

- Balisage « lourd » : [XML](https://fr.wikipedia.org/wiki/Extensible_Markup_Language), [HTML](https://fr.wikipedia.org/wiki/Hypertext_Markup_Language), [LaTeX](https://fr.wikipedia.org/wiki/LaTeX)…
- Balisage « léger » : [Markdown](https://fr.wikipedia.org/wiki/Markdown), [AsciiDoc](https://fr.wikipedia.org/wiki/AsciiDoc), [Org](https://fr.wikipedia.org/wiki/Org-mode)…

En fait, ce sont des écosystèmes, avec des cultures techniques et des traditions différentes :

- LaTeX : publication scientifique ;
- HTML, Markdown : rédaction Web ;
- XML, Asciidoc : rédaction technique ;
- Org-mode : organisation personnelle (notes, tâches, projets) via logiciel libre (Linux, Emacs) ;

Ce qui ne veut pas dire que les usages sont prescrits. Mais la philosophie du format influence la pratique.

# Pandoc

[Pandoc](https://pandoc.org) est un convertisseur entre formats textuels. Le créateur de Pandoc est [John MacFarlane](https://johnmacfarlane.net), professeur de philosophie à Berkeley.

Pandoc définit également une variante de Markdown qui peut servir de source à tous les autres formats d'export. Cette variante, le [Pandoc Markdown](https://pandoc.org/MANUAL.html#pandocs-markdown), inclut des fonctionnalités liées à l’écriture académique. Ceci en fait un logiciel extrêmement utile lorsqu'on veut pratiquer le format texte en contexte académique et coexister pacifiquement avec les traitements de texte.

## L’écosystème Pandoc

Pandoc peut être utilisé de manière autonome. Mais il peut aussi être utilisé via des scripts qui facilitent son automatisation, comme [Pandoc Scholar](https://pandoc-scholar.github.io), [Manubot](https://manubot.org/), [Pandocomatic](https://heerdebeer.org/Software/markdown/pandocomatic/). Pandoc est au cœur du fonctionnement de certains éditeurs de texte, comme [PanWriter](https://panwriter.com), [Fidus Writer](https://www.fiduswriter.org/how-it-works/), [Zettlr](https://zettlr.com), [Stylo](https://stylo.huma-num.fr). Enfin, l'intégration de Pandoc à certains éditeurs de texte populaires (Vim, Emacs, Sublime, Atom, VS Code…) est disponible via des [extensions](https://github.com/jgm/pandoc/wiki/Pandoc-Extras#editors), et son intégration à certains grands écosystèmes de programmation existe également : Pandoc est utilisé par exemple par le format [R Markdown](https://rmarkdown.rstudio.com) (R) et dans les carnets [Jupyter](https://jupyter.org) (Python).

Ces ressources et bien d'autres sont listées sur le wiki [Pandoc Extras](https://github.com/jgm/pandoc/wiki/Pandoc-Extras).

## Apprendre à utiliser Pandoc

Il existe des cours permettant de découvrir simultanément Markdown et Pandoc :

- [Élaboration et conversion de documents avec Markdown et Pandoc](https://www.jdbonjour.ch/cours/markdown-pandoc/)
- [Rédaction durable avec Pandoc et Markdown](https://programminghistorian.org/fr/lecons/redaction-durable-avec-pandoc-et-markdown)

Une fois cette première étape passée, la principale ressource pour continuer à apprendre à utiliser Pandoc est [le manuel](https://pandoc.org/MANUAL.html). Ce long document constitue une mine d'or inépuisable.

De nombreuses ressources traitent des différents usages spécialisés de Pandoc. J'ai publié moi-même quelques retours d'expérience sur mon site. Une simple recherche « pandoc + type d'utilisation » permet généralement de trouver rapidement des billets de blog contenant des exemples et des solutions.

# Critique du format texte

Les outils autour du format texte ont des défauts, mais certains critiquent aussi le format texte lui-même.

[Adam Hyde](https://www.adamhyde.net), fondateur de [Coko](https://coko.foundation), suggérait [récemment](https://www.adamhyde.net/markdown-definition/) que les auteurs n'ont pas nécessairement envie d'apprendre à écrire du code source, si on s'accorde à définir ainsi Markdown par exemple. Hyde est plutôt partisan d'outils fondés sur le format texte mais avec des interfaces d'écriture WYSIWYG.

Et par ailleurs, les partisans du format texte ont parfois une posture anti-traitement de texte caricaturale qui me paraît contre-productive, car elle favorise la réduction de la question à une querelle de chapelles, avec une radicalisation des positions qui ne peut que nuire à la diffusion de nouvelles pratiques. Ainsi, certaines critiques virulentes de Word nous reviennent désormais en boomerang sous la forme d'une opposition de principe au format texte. Il me paraît urgent de désamorcer ces conflits stériles.
