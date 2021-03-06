---
title: Vue d’ensemble de la distribution d’applications Xamarin.iOS
description: Ce document présente les techniques de distribution disponibles pour les applications Xamarin.iOS, et sert de point de départ vers d’autres documents plus détaillés sur le sujet.
ms.prod: xamarin
ms.assetid: 341D36DB-BB07-FA94-BCC9-5F8C0B18C179
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/18/2017
ms.openlocfilehash: 815277e9a4f9384d92bf17376f426cacd40dbc9f
ms.sourcegitcommit: 7a89735aed9ddf89c855fd33928915d72da40c2d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36209438"
---
# <a name="xamarinios-app-distribution-overview"></a>Vue d’ensemble de la distribution d’applications Xamarin.iOS

_Ce document offre une vue d’ensemble des techniques de distribution disponibles pour les applications Xamarin.iOS, et sert de point de départ vers d’autres documents plus détaillés sur le sujet._

Une fois l’application Xamarin.iOS développée, la prochaine étape du cycle de vie du développement du logiciel consiste à la distribuer aux utilisateurs, comme indiqué dans la section en surbrillance du diagramme ci-dessous :


[![](images/publishingdiagram.png "Une fois l’application iOS développée, la prochaine étape consiste à la distribuer aux utilisateurs, comme indiqué dans la section en surbrillance de ce diagramme")](images/publishingdiagram.png#lightbox)


Apple propose les méthodes suivantes (prises en charge par Xamarin.iOS) pour distribuer une application iOS :

1. [**App Store**](#App_Store_Distribution)
2. [**Interne (Entreprise)**](#In-House_Distribution)
2. [**Ad hoc**](#Ad_Hoc_Distribution)

Dans tous ces scénarios, les applications doivent être provisionnées à l’aide du *profil de provisionnement* approprié. Les profils de provisionnement sont des fichiers qui contiennent les informations sur le code de signature, ainsi que l’identité de l’application et le mécanisme de distribution prévu. Pour la distribution hors App Store, ils contiennent également des informations relatives aux appareils sur lesquels l’application peut être déployée.

<a name="App_Store_Distribution"/>

## <a name="app-store-distribution"></a>Distribution dans l’App Store

> [!IMPORTANT]
> Apple [a indiqué](https://developer.apple.com/news/?id=05072018a) qu’à partir de juillet 2018 toutes les applications et mises à jour envoyées à l’App Store doivent avoir été créées avec le Kit de développement logiciel (SDK) d’iOS 11 et [prendre en charge l’écran de l’iPhone X](~/ios/platform/introduction-to-ios11/updating-your-app/visual-design.md).

Il s’agit de la méthode principalement utilisée pour distribuer des applications iOS aux consommateurs sur des appareils iOS. Toutes les applications soumises à l’App Store nécessitent l’approbation d’Apple.

Les applications sont soumises à l’App Store via un portail appelé *iTunes Connect*. Le guide [Configurer votre application dans iTunes Connect](~/ios/deploy-test/app-distribution/app-store-distribution/itunesconnect.md) fournit des informations supplémentaires sur la configuration et l’utilisation de ce portail pour préparer la publication d’une application Xamarin.iOS dans l’App Store.

Il est important de noter que seuls les développeurs membres du **programme Developer d’Apple** ont accès à iTunes Connect. Les membres du programme **Developer Enterprise d’Apple** n’y ont pas accès.

Pour plus d’informations, visitez le guide [Distribution dans l’App Store](~/ios/deploy-test/app-distribution/app-store-distribution/index.md).

<a name="In-House_Distribution"/>

## <a name="in-house-distribution"></a>Distribution en interne

Parfois appelée *Distribution d’entreprise*, la distribution en interne permet aux membres du **programme Developer Enterprise d’Apple** de distribuer des applications en interne à d’autres membres de la même organisation. La distribution en interne présente l’avantage de ne pas nécessiter une évaluation pour l’App Store et de ne pas limiter le nombre d’appareils sur lesquels une application peut être installée. Toutefois, il est important de noter que les membres du **programme Developer Enterprise d’Apple** n’ont **pas** accès à iTunes Connect, et que le licencié est donc responsable de la distribution de l’application.

Pour plus d’informations sur la préparation et la distribution d’une application en interne, consultez le guide [Distribution en interne](~/ios/deploy-test/app-distribution/in-house-distribution.md).

<a name="Ad_Hoc_Distribution"/>

## <a name="ad-hoc-distribution"></a>Distribution ad hoc

Les utilisateurs peuvent tester les applications Xamarin.iOS via la distribution ad hoc, laquelle est disponible à travers les programmes **Developer** et **Developer Enterprise** d’Apple. Elle permet de tester jusqu’à 100 appareils iOS. Le meilleur cas d’usage pour la distribution ad hoc est celui d’une distribution en entreprise sans iTunes Connect.

Pour plus d’informations sur la préparation et la distribution d’une application en interne, consultez le guide [Distribution ad hoc](~/ios/deploy-test/app-distribution/ad-hoc-distribution.md).

## <a name="summary"></a>Récapitulatif

Cet article a fourni une brève présentation des mécanismes de distribution disponibles pour les applications Xamarin.iOS. Il a présenté l’App Store d’iTunes, les déploiements ad hoc et interne, et a fourni des liens vers des informations plus détaillées.

## <a name="related-links"></a>Liens associés

- [Distribution sur l’App Store](~/ios/deploy-test/app-distribution/app-store-distribution/index.md)
- [Configuration d’une application dans iTunes Connect](~/ios/deploy-test/app-distribution/app-store-distribution/itunesconnect.md)
- [Publication dans l’App Store](~/ios/deploy-test/app-distribution/app-store-distribution/publishing-to-the-app-store.md)
- [Distribution en interne](~/ios/deploy-test/app-distribution/in-house-distribution.md)
- [Distribution ad hoc](~/ios/deploy-test/app-distribution/ad-hoc-distribution.md)
- [Fichier iTunesMetadata.plist](~/ios/deploy-test/app-distribution/itunesmetadata.md)
- [Prise en charge IPA](~/ios/deploy-test/app-distribution/ipa-support.md)
- [Résolution des problèmes](~/ios/deploy-test/troubleshooting.md)
