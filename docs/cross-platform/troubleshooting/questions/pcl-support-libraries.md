---
title: Comment puis-je afficher les bibliothèques sont prises en charge dans une bibliothèque de classes portable ?
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: 14FF03BD-AF41-4DB1-B307-2349C13DE7E4
author: asb3993
ms.author: amburns
ms.date: 07/27/2018
ms.openlocfilehash: 7e1017baf7daed68b5e55319a9ce13a4a2df5f2e
ms.sourcegitcommit: aa9b9b203ab4cd6a6b4fd51e27d865e2abf582c1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/30/2018
ms.locfileid: "39351468"
---
# <a name="how-can-i-view-what-libraries-are-supported-in-a-pcl"></a>Comment puis-je afficher les bibliothèques sont prises en charge dans une bibliothèque de classes portable ?

- Vous trouverez une vue d’ensemble des différentes fonctionnalités prises en charge par les différentes plateformes de bibliothèque de classes portable cible sous le *fonctionnalités prises en charge* partie de cette page : [https://docs.microsoft.com/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library](https://docs.microsoft.com/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library)

- Une autre option consiste à utiliser le [Analyseur de portabilité .NET](https://visualstudiogallery.msdn.microsoft.com/1177943e-cfb7-4822-a8a6-e56c7905292b) afin d’évaluer si votre bibliothèque existante peut être converti en un profil de bibliothèque de classes portable.

- Une troisième possibilité consiste à parcourir le contenu du profil réel que vous pouvez utiliser. À l’aide de profil 78 par exemple, vous pouvez accéder ici : `C:\Program Files (x86)\Reference Assemblies\Microsoft\Framework\.NETPortable\v4.5\Profile\Profile78\` et afficher tous les assemblys qu’il contient.

Quelle que soit la méthode choisie, veuillez Notez que certaines fonctionnalités doit être téléchargé via NuGet et la bibliothèque Microsoft BCL.
