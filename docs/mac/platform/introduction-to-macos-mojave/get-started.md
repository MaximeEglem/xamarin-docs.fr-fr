---
title: Mise en route avec macOS Mojave
description: Ce document décrit comment préparer le jusqu'à build macOS applications Mojave avec Xamarin.Mac. Il explique comment télécharger Xcode 10 et mettre à jour de Visual Studio pour Mac.
ms.prod: xamarin
ms.assetid: E9A7B68A-E164-4C5C-86AC-B2A3E7A30DA1
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 07/08/2018
ms.openlocfilehash: 213f1feb53abf4a4eb00ae0d65c312eaaec95614
ms.sourcegitcommit: 12d48cdf99f0d916536d562e137d0e840d818fa1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2018
ms.locfileid: "39615364"
---
# <a name="getting-started-with-macos-mojave"></a>Mise en route avec macOS Mojave

![Preview](~/media/shared/preview.png)

> [!WARNING]
> MacOS de Xamarin prise en charge Mojave est actuellement en version préliminaire, ce qui signifie qu’il peut contenir des bogues, s’il n’est pas complet et peut changer.
> Utilisez-le pour l’expérimentation uniquement. 

Ce document décrit comment préparer le jusqu'à build macOS applications Mojave avec Xamarin.Mac. Il explique comment télécharger Xcode 10 et mettre à jour de Visual Studio pour Mac.

## <a name="download-and-install"></a>Téléchargez et installez

1. **Installer la dernière version bêta de Xcode 10** – les développeurs d’Apple inscrits peuvent télécharger et installer la dernière version du 10 Xcode à partir de la [portail des développeurs Apple](https://developer.apple.com/download/).

2. **Exécuter Xcode 10** – 10 de Xcode exécuter avant la mise à jour et d’exécuter Visual Studio pour Mac ; il installe des outils qui nécessite de Xamarin.

3. **Mettre à jour de Visual Studio pour Mac** : suivez les instructions de la [release blog](https://releases.xamarin.com/preview-release-xcode-10-beta-5/) pour installer la version préliminaire de Xamarin.

4. _(facultatif)_  **Installer la dernière version de mise à jour bêta macOS Mojave sur votre Mac** : permet de tester des applications Xamarin.Mac qui utilisent nouvellement introduites macOS Mojave API, inscrit peut de développeurs Apple [télécharger](https://developer.apple.com/download/) et installer le dernière macOS Mojave developer bêta.

   > [!TIP]
   > Même si votre application n’utilise pas de n’importe quel nouveau macOS Mojave API, veillez à le générer avec le Kit de développement logiciel Mojave macOS et testez-le pour vous assurer que tout fonctionne comme prévu. Si une application n’appelle pas les nouvelles API, vous pouvez le recompiler avec le Kit de développement logiciel Mojave macOS et le tester sans mise à niveau du système d’exploitation de votre Mac.
   >
   > Avant la mise à niveau de votre Mac à macOS Mojave pour générer et tester des applications Xamarin.Mac qui appellent le nouveau macOS Mojave API :
   >
   > - Lecture [notes de publication d’Apple](https://developer.apple.com/download/) pour la mise à jour du système d’exploitation.
   > - Lire l’aperçu Xamarin [mise en production de billet de blog](https://releases.xamarin.com/preview-release-xcode-10-beta-5/).

## <a name="related-links"></a>Liens connexes

- [Télécharger Xcode 10](https://developer.apple.com/download/)
- Aperçu de Xamarin [mise en production de billet de blog](https://releases.xamarin.com/preview-release-xcode-10-beta-5/)
