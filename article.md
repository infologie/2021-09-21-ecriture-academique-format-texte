---
title: Cosma, un logiciel de visualisation de graphe documentaire
author: Arthur Perret, Olivier Le Deuff, Clément Borel, Guillaume Brioudes
date: mai 2021
lang: fr-FR
documentclass: scrartcl
colorlinks: true
number-sections: true
abstract: "Nous présentons Cosma, un logiciel de visualisation de graphe documentaire pensé pour fonctionner en complémentarité avec les logiciels de prise de notes interreliées. Cosma contribue à ouvrir l'information experte en permettant de l'élaborer dans un format pérenne et de la communiquer sous une forme qui donne pleinement accès à des outils heuristiques : sa spécificité est d'exporter en un seul fichier les données et l'interface pour les explorer. Cosma est un logiciel libre, interopérable et documenté qui laisse un degré de contrôle élevé à l'utilisateur. Cosma nous permet également de mobiliser les notions de documentation hypertextuelle et de graphe documentaire pour traiter du rapport entre hypertexte et théories de l'organisation des connaissances."
keywords: [card, graph, documentation, hypertext, heuristics]
---

# Introduction

Nous constatons depuis deux décennies environ la montée en popularité d'une nouvelle catégorie d'outils de création, de gestion et de partage d'information : les logiciels de prise de notes interreliées. Ces logiciels se démarquent des solutions de prise de notes associées à la bureautique classique et aux terminaux mobiles, comme Evernote ou OneNote, par le fait qu'ils facilitent la création de véritables bases documentaires hypertextuelles. Cependant, ils ne sont pas issus de la culture documentaire ni encyclopédique : ce ne sont ni des bases de données relationnelles, ni des wikis. Ces outils se focalisent avant tout sur la saisie, qui doit être riche en fonctionnalités tout en générant le moins de friction possible. Quelques exemples : Roam Research, Notion, Zettlr, Obsidian.

Ces outils intéressent directement les secteurs sur lesquels nous travaillons : information scientifique et technique, documentation savante, intelligence grise et renseignement de sources ouvertes (en anglais *open source intelligence*, OSINT). En effet, ces secteurs sont confrontés à une interconnexion complexe qui affecte aussi bien l'élaboration de l'information (circuler, trouver, comparer, manipuler) que sa communication (expliquer, prouver, partager, réutiliser). Un outillage *ad hoc* est alors nécessaire. L'intérêt des bases de données relationnelles et des technologies du Web sémantique est bien connu. Les logiciels de prise de notes interreliées représentent un autre type de solution, axée sur l'hypertexte et sa représentation graphique sous forme de réseau. Ces outils s'appuient notamment sur les avancées des technologies du Web et des langages de balisage pour proposer des capacités d'édition, de publication et de conservation de l'information.

Ces outils représentent une opportunité à examiner pour nos secteurs informationnels mais ils ne satisfont pas encore à leurs exigences. En effet, nos secteurs requièrent des solutions complètes, c'est-à-dire qui combinent les techniques classiques de la documentation et des systèmes d'information (classement, indexation, recherche) aux techniques liées à l'hypertexte (liens, sémantique) et aux techniques graphiques (représentation, visualisation, design). Peu de logiciels présentent toutes ces facettes : ce sont des écosystèmes d'outils qui permettent d'aller en ce sens, grâce aux logiques d'interopérabilité et de modularité. Or ce type d'écosystème n'existe pas encore pour la prise de notes interreliées. Les logiciels les plus riches en fonctionnalités manquent d'interopérabilité, et réciproquement. Dans cet article, nous présentons Cosma [@perret2021a], un logiciel conçu pour pallier ce manque.

# Caractéristiques

## Description générale

Cosma est un logiciel de visualisation de graphe documentaire. Il permet de représenter des notes interreliées sous la forme d’un réseau interactif dans une interface web. Cosma n'est pas lui-même un logiciel de prise de notes : il est pensé pour fonctionner en complémentarité avec ces logiciels et nécessite que les notes soient structurées suivant un format bien précis.

La plupart des outils de visualisation concentrent leurs fonctionnalités dans une application à interface graphique, à partir de laquelle il est possible d'exporter des données structurées ou des images statiques. Cosma inverse cette logique : la partie application, surnommée **cosmographe**, est un simple formulaire de création, et c'est l'export, un fichier HTML surnommé **cosmoscope**, qui constitue la véritable interface de visualisation. Ce fichier autonome contient un graphe interactif, des outils de navigation interne (index, moteur de recherche, filtres) et le texte intégral des fiches ; il inclut aussi les données sources au format JSON et peut être utilisé hors connexion.

Cosma est conçu pour laisser un degré élevé de contrôle à ses utilisateurs. Premièrement, il n'intervient pas dans la gestion et l'édition des notes. Deuxièmement, de nombreux éléments d'interface sont personnalisables : algorithme de dessin de réseau, couleurs des nœuds, tracé des liens, raccourcis. Troisièmement, des enrichissements documentaires (métadonnées) et sémantiques (qualification des liens) sont possibles et se font par des mécanismes génériques : l'utilisateur est libre d'appliquer les typologies et ontologies de son choix. Et quatrièmement, Cosma est un logiciel libre : le code est public, son développement est documenté, il est accessible et réutilisable gratuitement sous licence MIT. Le travail peut ainsi être évalué, archivé et continué par d'autres.

## Format des données

Les logiciels de prise de notes interreliées combinent différentes normes d'écriture, auxquelles ils apportent parfois des variations ; ceci leur permet de créer des fonctionnalités mais diminue l'interopérabilité, voire crée des effets de verrouillage passif (*soft lock*) des utilisateurs. Par exemple, la syntaxe des liens suit généralement la forme wiki (doubles crochets) mais la cible des liens n'est pas gérée de la même manière par tous les logiciels : certains utilisent un système d'identifiant unique (URI), tandis que d'autres utilisent les titres des notes ; dans le second cas, les fichiers gagnent en lisibilité mais le système perd en robustesse, et les utilisateurs dépendent du logiciel pour assurer la maintenance des données. Les aspects les moins développés de ces normes d'écriture concernent les métadonnées et la sémantique : très peu de techniques documentaires sont mises en œuvre au-delà de l'indexation par mots-clés.

Cosma prend en compte ces différentes problématiques. Le format prescrit est composé de normes existantes avec le moins de modifications possibles, afin d'accroître l'interopérabilité du logiciel. Nous avons repris l'approche des logiciels de type Zettelkasten, avec un URI à 14 chiffres qui correspond à l'horodatage de la création du fichier. Enfin, le logiciel est capable de représenter visuellement des catégories de notes mais aussi de liens, ce qui constitue un enrichissement documentaire et sémantique significatif.

| Élément | Norme utilisée dans Cosma |
|:--------|:---------------------------|
| Texte | Markdown |
| Métadonnées | YAML |
| Liens | Syntaxe de type wiki (doubles crochets) |
| Cible des liens | Identifiant unique (URI) |
| Qualification des liens | Syntaxe de type XML (préfixe et deux-points) |

: Tableau 1. Format de données utilisé par Cosma

## Usages

Cosma s'inscrit dans la tradition de la fiche érudite [@bert2017], dont il réaffirme la pertinence au sein du paradigme informationnel actuel [@ledeuff2019c]. La fiche peut être mise en œuvre de plusieurs façons. C'est d'abord une question de volume et de périmètre : une collection de fiches peut prendre la forme d'un lexique thématique resserré (centaine de documents) ou d'une vaste documentation (de la centaine au millier de documents) ; il peut s'agir d'un produit fini réalisé dans le cadre d'un projet, proche du dossier, ou bien d'une documentation personnelle destinée à croître sur plusieurs années.

C'est ensuite une question d'usages, et Cosma est conçu avec deux usages principaux en tête. Premièrement, l'outil doit apporter des capacités d'analyse et de synthèse lors de l'élaboration de l'information. Les notes interreliées fonctionnent alors comme partenaire de réflexion et d'écriture, une pratique inspirée notamment par le sociologue allemand Niklas Luhmann et popularisée sous le nom de Zettelkasten [@luhmann1992]. Deuxièmement, l'outil doit permettre de montrer, démontrer et expliquer. La visualisation des fiches sous forme de graphe constitue un support de communication, de médiation de l'information, dans une démarche pédagogique ou journalistique par exemple.

Le partage d'une visualisation s'accompagne parfois des données sous une forme structurée et réutilisable. Cosma adopte cette pratique en exportant les données textuelles et relationnelles des fiches sous la forme d'une section en JSON dans le fichier cosmoscope. Cependant, nous souhaitons aller plus loin et partager plus généralement des *capacités heuristiques*. La visualisation n'est qu'un outil parmi d'autres ; François Dagognet inclut le graphe dans une « triade épistémologique » de « dispositifs élémentaires et heuristiques » qui comprend aussi le mot et la classe [@dagognet1999, 87-88]. L'export de Cosma (le cosmoscope) inclut ainsi les fonctionnalités classiques d'une interface exploratoire (recherche, index, tri, filtres), qui s'appuient sur le travail de terminologie et de classification réalisé pour l'élaboration des fiches ; il inclut aussi des fonctionnalités hypertextuelles comme les liens et rétroliens dans chaque fiche.

Cette approche correspond à une tendance. Depuis quelques années, les dispositifs de publication font l'objet de recherches visant à les transformer en de véritables « outils de la réflexion » [*tools for thought*, @matuschak2019], qui tendent vers le document exécutable ou « document-instrument » [@otlet1934, 429]. Par exemple, les *notebooks* ou carnets numériques programmables sont des dispositifs qui mêlent écriture et éléments interactifs reproductibles ; ils requièrent néanmoins un environnement de développement (IDE) dédié pour être utilisés. Cosma poursuit le même objectif, avec une plus grande portabilité puisque le cosmoscope ne nécessite qu'un navigateur Internet ; ceci permet d'accroître la portée de l'outil et du travail informationnel dont il fait la médiation.

# Épistémologie

À travers Cosma, la prise de notes interreliées constitue un terrain pour réfléchir à la terminologie et mettre à l'épreuve de nouveaux concepts. Nous parlons ainsi de documentation hypertextuelle pour désigner l'objet que constitue une collection de fiches, et de graphe documentaire pour la structure de cet objet.

Les graphes documentaires constituent une catégorie générique émergente, qui englobe et dépasse d'autres formes plus connues comme les cartographies relationnelles (réseaux d'acteurs) et heuristiques (réseaux hiérarchiques de concepts). Thibaut Arribe définit « graphe documentaire » à l'échelle intra-documentaire comme représentation de la structure des fragments du document [@arribe2014, 29] et à l'échelle inter-documentaire comme graphe orienté de documents rééditorialisés [@arribe2014, 210]. Dans cette deuxième acception, graphe documentaire désigne simplement des documents interreliés. Les outils de prise de notes qui nous concernent ici rentrent donc dans cette catégorie.

Les graphes documentaires sont distincts des graphes de connaissance, lesquels sont assimilables à des ontologies [@bergman2019]. Les graphes de connaissance sont fondés sur les métadonnées, tandis que les graphes documentaires sont fondés sur les documents. Le Web sémantique a popularisé la notion de graphe de connaissance mais son coût technique reste élevé : les modèles (RDF, *property graphs*) sont complexes et les outils nécessitent une formation importante ; par conséquent les tableurs et bases de données relationnelles restent beaucoup plus utilisés. Par contraste, les graphes documentaires sont plus faciles à mettre en œuvre car ils procèdent de l'hypertexte.

L'enjeu représenté par Cosma est de développer un outillage qui tire parti de cette interconnexion facilitée. Ce faisant, un certain nombre d'apports épistémologiques sont envisageables. D'abord, il s'agit d'obtenir à la fois une vision globale (macro), intermédiaire (méso) et détaillée (micro) de la complexité informationnelle. Ensuite, il s'agit de contribuer à populariser certaines potentialités de l'hypertexte, comme les rétroliens, ouvrant de nouvelles possibilités de circulation. Enfin, il s'agit de puiser dans les outils de la théorie des graphes, dont l'utilité a été démontrée par le champ de l'analyse des réseaux, et dont l'application à l'organisation des connaissances pourrait être explorée au-delà des ontologies.

# Bibliographie

