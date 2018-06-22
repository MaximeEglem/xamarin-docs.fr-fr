---
title: Fichier IPA est de 0 octet
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: 376BBA27-8694-4E63-9976-BF60349D42D8
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/21/2017
ms.openlocfilehash: 40799d0b8b051459145f51671ae7f6143db9635a
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/04/2018
ms.locfileid: "30777783"
---
# <a name="ipa-file-is-0-bytes"></a>Fichier IPA est de 0 octet

> [!IMPORTANT]
> Ce problème a été résolu dans les versions récentes de Xamarin. Toutefois, si le problème se produit sur la dernière version du logiciel, veuillez soumettre un [nouveau bogue](~/cross-platform/troubleshooting/questions/howto-file-bug.md) avec votre contrôle de version complet intégral et les informations de la sortie de journal de build.



A des problèmes connus dans les versions précédentes de Xamarin qui peut entraîner le fichier IPA sur Windows à 0 octet. 

### <a name="fixed-in-xamarin-for-visual-studio-311584"></a>Fixe dans Xamarin pour Visual Studio 3.11.584 
- [Bogue 24416 - configuration de génération « Ad Hoc » à partir de la ligne de commande ne pas copier IPA le fichier dans Windows](https://bugzilla.xamarin.com/show_bug.cgi?id=24416)
- [Bogue 24417 - modification « propriétés du projet -> iOS IPA Options -> nom du Package « évite IPA soient copiées vers Windows](https://bugzilla.xamarin.com/show_bug.cgi?id=24417)
- [Bogue 29822 - [XVS.iOS 3.11] la définition « Build » du nombre différent de « Version » numéro causes IPA ne pas à copier vers Windows](https://bugzilla.xamarin.com/show_bug.cgi?id=29822)

### <a name="fixed-in-xamarin-for-visual-studio-410496"></a>Fixe dans Xamarin pour Visual Studio 4.1.0.496
- [Bogue 27989 - afficher le fichier ipa sur Échec de serveur de Build si le nom de l’Assembly ne correspond pas le nom du projet](https://bugzilla.xamarin.com/show_bug.cgi?id=27989)
