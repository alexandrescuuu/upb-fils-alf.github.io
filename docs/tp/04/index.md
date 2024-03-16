---
sidebar_position: 5
description: Définir les langages de programmation
slug: tp/04
---

# 04 - Grammaires indépendantes de contexte

## Introduction
Dans les TPs précédents, on a appris comment concevoir des modèles pour decrire des chaînes de caractères. Aujourd’hui, on va voir un outil pour définir des règles pour les langages de programmation. Cet outil s’appelle **une grammaire**.

Plus précisément, on va étudier les grammaires indépendantes de contexte. De manière informelle, on dit qu’elles posent **des règles récursives** sur l’ordre dans laquelle se trouvent les jétons dans un langage de programmation et la structure des instructions. Observez qu’on étudie les grammaires à partir des langages qu’elles décrivent.

## Définitions
Du point de vue mathématique, on definit une grammaire indépendante de contexte comme un tuple composé par:
- un ensemble fini de symboles à partir desquels on compose les chaînes du langage défini. On appelle cet ensemble les **terminaux**;
- un ensemble fini de **variables**, ou **non-terminaux** (ou catégories syntaxiques), qui sont décrites en utilisant les terminaux ou d’autres variables;
- une variable qui représent le langage défini par la grammaire, qu’on appelle **symbole de début**;
- un ensemble fini de **règles** (ou **productions**) qui représentent la définition récursive du langage. Chaque production contient: 
  - une variable définie par la production (appelée **la tête de la production**- elle se trouve dans la partie gauche de la production)
  - le symbole de production
  - une chaîne de zéro ou plusieurs terminaux et variables (appelée **le corps de la production**) qui représente un moyen de décrire la variable située dans la tête de la production. Cette chaîne peut aussi être une **expression régulière** construite en utilisant les variables et les terminaux.

### Exemple
Pour definir un langage qui accepte les expréssions des sommes entre deux nombres contenant des 0 consécutives suivis par des 1 consécutives:
$$
  P \rightarrow S + S \tag{1}
$$
$$
  S \rightarrow 0S1 \tag{2}
$$
$$
  S \rightarrow \epsilon  \tag{3}
$$
Dans cet exemple, il y a:
- les terminaux: $$\{+, 0, 1\}$$
- les non-terminaux: $$\{P, S\}$$
- le symbole de début: $$P$$ 
- trois productions $(1), (2), (3)$

Chaînes acceptées:
- `00001111+0011`
- `01+0011`
- `+01`
- `+`

:::warning
  Même si vous voyez l’opérateur arithmétique '+', sachez qu’ici il ne s’agit pas de l’addition! On parle strictement des chaînes de caractères, donc on a besoin exactement du caractère '+'.
:::


## Exercices
1. Ouvrez les fichiers du laboratoire. Dans `TP04/ex1.g4`, completez les `TODO` pour écrire une grammaire qui reconnaît une instruction de déclaration d'une variable, ayant la syntaxe suivante:
```c
  <nom_du_type> <nom_de_la_variable> ;

  //Exemples:
  int a;
  char b23;
  long mnop1;
```
Où:
- le nom du type est l'un des options suivantes: `int`, `long`, `bool`, `char`
- le nom de la variable est une chaîne qui peut contenir des lettres et des nombres, mais ne peut pas commencer avec un nombre

:::warning
  Faites attention aux `;`. Ils doivent toujours apparaître dans la déclaration!
:::

2. Ouvrez les fichiers du laboratoire. Dans `TP04/ex2.g4`, completez les `TODO` pour écrire une grammaire qui reconnaît des expréssions mathématiques avec des nombres entières et des noms de variables.

3. Ouvrez les fichiers du laboratoire. Dans `TP04/ex3.g4`, combinez les deux grammaires des exercices précédents pour obtenir une grammaire qui accepte les instructions suivantes:
```c
  //déclaration d'une variable
  <nom_du_type> <nom_de_la_variable> ;
```

```c
  //attribution d'une expression avec des nombres entières à une variable
  <nom_de_la_variable> = <expression> ;

  //Exemple:
  ab = 3;
  x = 3 + 2 * 7;
```

```c
  //déclaration d'une variable avec une attribution
  <nom_du_type> <nom_de_la_variable> = <expression>;

  //Exemple:
  int y = -78;
  long a8 = 123;
```

4. (Bonus) Écrivez une grammaire sur l’alphabet $\Set{a, b}$ qui accepte les chaînes contenant $m$ apparitions de 'a' et $n$ apparitions de 'b', avec $m>n$.

## Bibliographie
1. *Introduction to Automata Theory, Languages and Computation - 3rd edition*- Chapitre 5.1.1-5.1.2
2. *Compilers: Principles, Techniques & Tools - 2nd Edition* - Chapitre 2.2.1 