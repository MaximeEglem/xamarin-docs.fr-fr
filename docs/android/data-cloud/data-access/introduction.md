---
title: Introduction au stockage des données sur Android
ms.prod: xamarin
ms.assetid: FDAC0771-4749-4758-865A-F1BD190CA54B
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 03/28/2017
ms.openlocfilehash: 42af02d2ed2a679d89425257d92f03a3764675ce
ms.sourcegitcommit: 797597d902330652195931dec9ac3e0cc00792c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/20/2018
ms.locfileid: "31646987"
---
# <a name="introduction"></a>Introduction

## <a name="when-to-use-a-database"></a>Quand utiliser une base de données

Alors qu’augmentent les capacités de stockage et le traitement des appareils mobiles, des téléphones et tablettes toujours être en décalage leurs équivalents de bureau et portables. Pour cette raison, il est important de prendre le temps de planifier l’architecture de stockage de données de votre application plutôt que de simplement une base de données est la bonne tout le temps de réponse. Il existe différentes options, selon les exigences de l’autres, telles que :

-  **Préférences** – Android offre un mécanisme intégré pour stocker des paires clé-valeur simples de données. Si vous stockez les paramètres utilisateur simple ou les petits éléments de données (par exemple, les informations de personnalisation) ensuite utiliser des fonctionnalités natives de la plateforme pour le stockage de ce type d’information.
-  **Fichiers texte** – l’entrée d’utilisateur ou des caches de téléchargé le contenu (par exemple). HTML) peut être stockée directement sur le système de fichiers. Utilisez une convention d’affectation de noms de fichier appropriée pour vous aider à organiser les fichiers et de rechercher des données.
-  **Sérialiser des fichiers de données** – objets peuvent être rendue persistante en tant que XML ou JSON sur le système de fichiers. Le .NET framework inclut des bibliothèques de sérialisation et désérialisation des objets. Utilisez les noms appropriés pour organiser les fichiers de données.
-  **Base de données** : moteur de base de données SQLite l’est disponible sur la plateforme Android et utiles pour le stockage structuré de données dont vous avez besoin pour interroger, trier ou manipuler. Stockage de base de données est adapté aux listes de données avec de nombreuses propriétés.
-  **Fichiers image** – bien qu’il soit possible de stocker des données binaires dans la base de données sur un appareil mobile, il est recommandé de les stocker directement dans le système de fichiers. Si nécessaire, vous pouvez stocker les noms de fichiers dans une base de données pour associer l’image avec d’autres données. Lorsque vous traitez des images de grande taille ou un grand nombre d’images, il est conseillé de planifier une stratégie de mise en cache qui supprime les fichiers que vous n’avez plus besoin afin d’éviter la consommation d’espace de stockage de tous les utilisateurs.

Si une base de données est le mécanisme de stockage approprié pour votre application, le reste de ce document explique comment utiliser SQLite sur la plateforme de Xamarin.

## <a name="advantages-of-using-a-database"></a>Avantages de l’utilisation d’une base de données

Il existe un certain nombre d’avantages à l’aide d’une base de données SQL dans votre application mobile :

-  Bases de données SQL permettent un stockage efficace des données structurées.
-  Données spécifiques peuvent être extraits avec des requêtes complexes.
-  Résultats de la requête peuvent être triées.
-  Résultats de la requête peuvent être agrégées.
-  Aux développeurs des compétences de base de données peuvent utiliser leurs connaissances pour concevoir le code d’accès aux données et de la base de données.
-  Le modèle de données à partir du composant serveur d’une application connectée peut être réutilisée (en totalité ou en partie) dans l’application mobile.


## <a name="sqlite-database-engine"></a>Moteur de base de données SQLite

SQLite est un moteur de base de données open source qui a été arrêté par Google pour leur plateforme mobile. Le moteur de base de données SQLite est intégré pour les deux systèmes d’exploitation et il n’existe aucun travail supplémentaire pour les développeurs de tirer parti de celui-ci. SQLite est adapté au développement mobile multiplateforme, car :

-  Le moteur de base de données est petite, rapidement et facilement portable.
-  Une base de données est stockée dans un seul fichier, qui est facile à gérer sur des appareils mobiles.
-  Le format de fichier est facile à utiliser sur plusieurs plateformes : si 32 ou 64 bits et les systèmes de big - endian ou little-endian.
-  Il implémente la plupart du SQL92 standard.


SQLite est conçu pour être petite et rapide, il existe certaines restrictions sur son utilisation :

-  Une syntaxe de jointure externe n’est pas pris en charge.
-  Changement de nom de table uniquement et ADDCOLUMN sont pris en charge. Vous ne pouvez effectuer d’autres modifications à votre schéma.
-  Les vues sont en lecture seule.


Vous pouvez en savoir plus sur SQLite sur le site Web - [SQLite.org](http://SQLite.org) - cependant toutes les informations que vous devez utiliser SQLite avec Xamarin sont contenues dans ce document et associé les exemples. Le moteur de base de données SQLite a été pris en charge dans Android depuis 2 Android.
Bien que non couvert dans ce chapitre, SQLite est également disponible pour une utilisation sur Windows Phone et des applications Windows.

## <a name="windows-and-windows-phone"></a>Windows et Windows Phone

SQLite peut également être utilisé sur les plateformes Windows, bien que ces plateformes ne sont pas traités dans ce document.
En savoir plus en le [Tasky](~/cross-platform/app-fundamentals/building-cross-platform-applications/case-study-tasky.md) et [Tasky Pro](~/cross-platform/app-fundamentals/building-cross-platform-applications/case-study-tasky.md) études de cas et passez en revue [blog de Tim Heuer](http://timheuer.com/blog/archive/2012/06/28/seeding-your-metro-style-app-with-sqlite-database.aspx).


## <a name="related-links"></a>Liens associés

- [DataAccess Basic (exemple)](https://github.com/xamarin/mobile-samples/tree/master/DataAccess/Basic)
- [DataAccess avancé (exemple)](https://github.com/xamarin/mobile-samples/tree/master/DataAccess/Advanced)
- [Recettes de données Android](https://developer.xamarin.com/recipes/android/data/)
- [Accès aux données de Xamarin.Forms](~/xamarin-forms/app-fundamentals/databases.md)
