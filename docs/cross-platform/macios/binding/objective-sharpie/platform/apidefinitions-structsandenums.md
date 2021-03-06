---
title: ApiDefinitions & StructsAndEnums fichiers
description: Ce document décrit les fichiers ApiDefinitions.cs et StructsAndEnums.cs objectif Sharpie génère. Ces fichiers sont ensuite utilisés pour accéder au code Objective-C à partir de c#.
ms.prod: xamarin
ms.assetid: AC2087C0-BA54-46D8-B70C-6972941C8F73
author: asb3993
ms.author: amburns
ms.date: 03/29/2017
ms.openlocfilehash: df8d4508db14116a5b36e893f161ac891d58dc46
ms.sourcegitcommit: ec50c626613f2f9af51a9f4a52781129bcbf3fcb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37855180"
---
# <a name="apidefinitions--structsandenums-files"></a>ApiDefinitions & StructsAndEnums fichiers

Lorsque l’objectif Sharpie s’est exécutée correctement, il génère `Binding/ApiDefinitions.cs` et `Binding/StructsAndEnums.cs` fichiers.
Ces deux fichiers sont ajoutés à un projet de liaison dans Visual Studio pour Mac ou passées directement à la `btouch` ou `bmac` outils pour produire la liaison finale.

Dans *certains* cas ces fichiers générés peuvent suffire, mais le plus souvent le développeur devra modifier manuellement ces fichiers pour résoudre les problèmes qui ne peuvent pas être gérées automatiquement par l’outil (par exemple, ces indicateurs générés avec un [ `Verify` attribut](~/cross-platform/macios/binding/objective-sharpie/platform/verify.md)).

Parmi les étapes suivantes :

- **Ajustement de noms**: parfois, vous souhaitez ajuster les noms des méthodes et des classes pour faire correspondre les instructions de conception de .NET Framework.
- **Méthodes ou propriétés**: l’heuristique utilisée par objectif Sharpie parfois sélectionnent une méthode soit transformé en une propriété. À ce stade, vous pouvez décider s’il s’agit du comportement souhaité ou non.
- **Raccorder des événements**: vous pouvez lier vos classes avec vos classes de délégué et générer automatiquement des événements pour ceux.
- **Raccorder les Notifications**: il n’est pas possible d’extraire le contrat d’API de notifications à partir des fichiers d’en-tête pure, cette opération nécessite un aller-retour vers la documentation de l’API. Si vous souhaitez que les notifications fortement typées, vous devez mettre à jour le résultat.
- **API collecte**: À ce stade, vous pouvez choisir de fournir des constructeurs supplémentaires, ajoutez les méthodes (pour permettre la syntaxe d’initialisation sur construction c#), la surcharge d’opérateur et implémenter vos propres interfaces sur le fichier de définitions supplémentaires.

Consultez le [une API de liaison](~/cross-platform/macios/binding/objective-c-libraries.md) description pour voir comment ces fichiers s’intègrent dans le processus de liaison, comme illustré dans le diagramme ci-dessous :

![](apidefinitions-structsandenums-images/binding-flowchart.png "Le processus de liaison est illustré dans ce diagramme")

Reportez-vous à la [référence des Types de liaison](~/cross-platform/macios/binding/binding-types-reference.md) pour plus d’informations sur le contenu de ces fichiers.

## <a name="related-links"></a>Liens associés

- [Cours de l’Université de Xamarin : Génération d’une bibliothèque de liaisons Objective-C](https://university.xamarin.com/classes/track/all#building-an-objective-c-bindings-library)
- [Xamarin University cours : Générer une bibliothèque de liaisons Objective-C avec Sharpie objectif](https://university.xamarin.com/classes/track/all#build-an-objective-c-bindings-library-with-objective-sharpie)
