---
sidebar_position: 6
description:
slug: tp/05
---

# 05 - ANTLR Lexer et Parser

## Grammaires avec ANTLR4
À partir de ce TP, on va utiliser ANTLR pour l’analyse du texte. ANTLR (Another Tool For Language Recognition) est un outil pour generer des analyseurs (parsers) qui permettent le traitement, l’exécution et la traduction du code. On va employer ANTLR pour la partie de front-end de notre compilateur.

Pour les grammaires indépendantes du contexte, ANTLR utilise des fichiers `.g4`. Pour écrire une grammaire, il faut créer un fichier avec le même nom que la grammaire que vous souhaitez définir. 

### Terminaux
En ANTLR, on peut même utiliser des productions pour décrire les terminaux. Dans ce cas, le corps de la production doit contenir que des terminaux. On va identifier les terminaux avec des noms qui commencent avec des lettres **MAJUSCULES** (On vous conseile d’utiliser que des majuscules pour les terminaux, pour pouvoir les distinguer plus facilement). D’habitude, on trouve les définitions des terminaux à la fin de la grammaire.

```antlr4
  INTEGER: (-)?[0-9]+ ;  //un terminal pour représenter les nombres entières
  WHITESPACE: ' ' ; //un terminal pour représenter les espaces blancs
  VARIABLE_NAME: [a-zA-Z]+ //un terminal pour représenter les noms des variables
```

### Règles

On va identifier les non-terminaux avec des lettres **minuscules**.

:::warning
En ANTLR, on **ne peut pas avoir des productions avec la même tête**. Ce qu’on peut faire, c’est de mettre les deux corps dans un seul et de les séparer avec l’opérateur `|`.
:::

```antlr4
  assignment: VARIABLE_NAME '=' INTEGER ; //une règle pour représenter une affectation
  
  //une règles pour représenter une expression d'addition
  addition: addition '+' INTEGER
          | INTEGER
          ;
```

### Grammaires
Prenons la grammaire précedante et essayons de l’écrire avec ANTLR.

:::warning
La grammaire sera un peu différente, à cause du fait qu’en ANTLR on ne peut pas utiliser la chaîne vide. Alors, pour ne pas nous eloigner de l’exemple, S va commencer
par la valeur `01`.
:::

La grammaire devient: 

```antlr4
grammar demo;

ZERO: '0';
ONE: '1'; 
p : s '+'s;
s : ZERO s ONE  
  | ZERO ONE; 
```