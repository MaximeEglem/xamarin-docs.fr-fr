---
title: Distribution ad hoc pour les applications Xamarin.iOS
description: Ce document présente les techniques de distribution ad hoc principalement utilisées pour tester des applications Xamarin.iOS auprès d’un large groupe de personnes.
ms.prod: xamarin
ms.assetid: 3B621CAD-103C-478A-97C3-829015F48D1A
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/19/2017
ms.openlocfilehash: 0907c3bcca9e0955e5ad9f8ed48adac03202cbaa
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34784801"
---
# <a name="ad-hoc-distribution-for-xamarinios-apps"></a>Distribution ad hoc pour les applications Xamarin.iOS

_Ce document présente une vue d’ensemble des techniques de distribution ad hoc principalement utilisées pour tester des applications Xamarin.iOS auprès d’un large groupe de personnes._

Une fois l’application Xamarin.iOS développée, la prochaine étape du cycle de vie du développement du logiciel consiste à la distribuer aux utilisateurs pour qu’ils la testent.

iTunes Connect permet de gérer les tests d’application. Vous trouverez une description plus complète dans le guide [TestFlight](~/ios/deploy-test/testflight.md). Toutefois, pour les membres du programme Developer Enterprise d’Apple n’ayant pas accès à iTunes Connect, la distribution *ad hoc* est la meilleure méthode pour tester ces applications.

Les utilisateurs peuvent tester les applications Xamarin.iOS via la distribution *ad hoc*, laquelle est disponible à travers les programmes Developer et Developer Enterprise d’Apple. Elle permet de tester jusqu’à 100 appareils iOS.

La distribution ad hoc a l’avantage de ne pas nécessiter l’approbation de l’App Store. De plus, vous pouvez l’installer par voie hertzienne à partir d’un serveur web ou via iTunes. Elle est toutefois limitée à **100** appareils par adhésion annuelle, aussi bien pour le développement que pour la distribution. De plus, vous devez ajouter ces appareils manuellement dans le Member Center en fonction de leur UDID. Pour plus d’informations sur l’ajout d’appareils, consultez le guide [Provisionnement des appareils](~/ios/get-started/installation/device-provisioning/manual-provisioning.md#adddevice).

Pour permettre le bon fonctionnement de la distribution ad hoc, les applications doivent être provisionnées à l’aide d’un *profil de provisionnement* ad hoc, qui contient les informations sur le code de signature, ainsi que l’identité de l’application et des appareils pouvant installer l’application.

Ce guide fournit des informations sur le provisionnement pour une distribution ad hoc, ainsi que des informations sur la distribution d’une application Xamarin.iOS.

<a name="setup" />

## <a name="setting-up-for-distribution"></a>Configuration de la distribution

Même si vous comptez publier une application Xamarin.iOS pour un déploiement interne, à des fins de test, vous devez créer un profil de provisionnement de distribution ad hoc spécifique. Ce profil permet à une application d’être publiée avec une signature numérique pour qu’elle puisse être installée sur un appareil iOS.

La section suivante décrit comment configurer un certificat de distribution et un profil de provisionnement de distribution.

> [!NOTE]
> Seuls les agents et les administrateurs d’équipe peuvent créer des certificats de distribution et des profils d’approvisionnement.

<a name="createcertificate" />

## <a name="create-a-distribution-certificate"></a>Créer un certificat de distribution


1. Accédez à la section *Certificates, Identifiers & Profiles* (Certificats, identificateurs et profils) du Member Center du programme Developer d’Apple.
2. Sous *Certificates*, sélectionnez **Production**.
3. Cliquez sur le bouton **+** pour créer un certificat.
4. Sous le titre *Production*, sélectionnez **In-House and Ad Hoc (Interne et ad hoc)**, ou **App Store and Ad Hoc (App Store et ad hoc)**, en fonction de votre abonnement au programme :

  [![](ad-hoc-distribution-images/cert-first-small.png "Sélectionner In-House and Ad Hoc (Interne et ad hoc) ou App Store and Ad Hoc (App Store et ad hoc)")](ad-hoc-distribution-images/cert-first-large.png#lightbox)

5. Cliquez sur Continue, puis suivez les instructions permettant de créer une demande de signature de certificat via Trousseaux d’accès :

  [![](ad-hoc-distribution-images/createcertmanually02.png "Créer une demande de signature de certificat via l’accès au trousseau")](ad-hoc-distribution-images/createcertmanually02.png#lightbox)

6. Une fois la demande de signature de certificat créée, cliquez sur Continue, puis chargez-la sur le Member Center :

  [![](ad-hoc-distribution-images/createcertmanually03.png "Charger la demande de signature de certificat sur le Member Center")](ad-hoc-distribution-images/createcertmanually03.png#lightbox)

7. Cliquez sur Generate pour créer un certificat.
8. Pour finir, téléchargez le certificat rempli, puis double-cliquez sur le fichier pour l’installer.
9. À ce stade, le certificat doit être installé sur la machine, mais vous devrez peut-être [actualiser vos profils](~/ios/get-started/installation/device-provisioning/manual-provisioning.md#download) pour vérifier qu’ils sont visibles dans Xcode.

Sinon, il est possible de demander un certificat via la boîte de dialogue Preferences de Xcode. Pour ce faire, suivez les étapes ci-dessous :

1.   Sélectionnez votre équipe, puis cliquez sur **Gérer des certificats...** : [![](ad-hoc-distribution-images/selectteam.png "Sélection de l’équipe")](ad-hoc-distribution-images/selectteam.png#lightbox)

2.   Cliquez ensuite sur le bouton **Plus (+)** et sélectionnez **iOS App Store** : [![](ad-hoc-distribution-images/selectcert.png "Sélection d’iOS App Store")](ad-hoc-distribution-images/selectcert.png#lightbox)

<a name="createprofile" />

## <a name="create-a-distribution-provisioning-profile"></a>Créer un profil d’approvisionnement de distribution

<a name="createappid" />

### <a name="create-an-app-id"></a>Créer un ID d’application
Comme pour tout profil de provisionnement que vous créez, un ID d’application est nécessaire pour identifier l’application à distribuer sur l’appareil de l’utilisateur. Si vous ne l’avez pas déjà créé, suivez les étapes ci-dessous pour en créer un :


1. Dans [Apple Developer Center](https://developer.apple.com/account/overview.action), accédez à la section *Certificates, Identifiers & Profiles* (Certificats, identificateurs et profils). Sélectionnez **App IDs** sous **Identifiers**.
2. Cliquez sur le bouton **+**, puis indiquez un **Name (Nom)** qui identifie l’application sur le portail.
3. Le préfixe d’application doit déjà être défini à l’aide de votre ID d’équipe. Il est impossible de le changer. Sélectionnez un ID d’application explicite ou avec des caractères génériques, puis entrez un ID de bundle au format DNS inversé, par exemple :
    - **Explicite** : `com.[DomainName].[AppName]`
    - **Avec des caractères génériques** : `com.[DomainName].*`
4. Sélectionnez les [services d’application](~/ios/get-started/installation/device-provisioning/manual-provisioning.md#appservices) nécessaires à votre application.
5. Cliquez sur le bouton **Continue** et suivez les instructions affichées à l’écran pour créer l’ID d’application.

Une fois que vous avez les composants nécessaires pour créer un profil de distribution, suivez les étapes ci-dessous pour le créer :

1. Retournez au portail de provisionnement Apple, puis sélectionnez **Provisionnement > Distribution** :  [![](ad-hoc-distribution-images/distribute01.png "Sélectionnez Provisionnement > Distribution")](ad-hoc-distribution-images/distribute01.png#lightbox)

2. Cliquez sur le bouton **+** et sélectionnez le type **Ad hoc** en tant que profil de distribution à créer :

    [![](ad-hoc-distribution-images/distribute02.png "Créer un type de distribution ad hoc")](ad-hoc-distribution-images/distribute02.png#lightbox)

3. Cliquez sur le bouton **Continue**, puis dans la liste déroulante, sélectionnez l’ID d’application pour lequel vous souhaitez créer un profil de distribution :

    [![](ad-hoc-distribution-images/distribute03.png "Sélectionner l’ID d’application dans la liste déroulante")](ad-hoc-distribution-images/distribute03.png#lightbox)

4. Cliquez sur le bouton **Continue**, puis sélectionnez le certificat de distribution nécessaire pour signer l’application :

    [![](ad-hoc-distribution-images/distribute04.png "Sélectionner le certificat de distribution nécessaire pour signer l’application")](ad-hoc-distribution-images/distribute04.png#lightbox)

6. Cliquez sur le bouton **Continue**, puis entrez un **Name (Nom)** pour le nouveau profil de distribution :

    [![](ad-hoc-distribution-images/distribute06.png "Entrer un nom pour le nouveau profil de distribution")](ad-hoc-distribution-images/distribute06.png#lightbox)

7. Cliquez sur le bouton **Generate** pour créer le profil et finaliser le processus.

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio pour Mac](#tab/vsmac)

Vous devrez peut-être quitter Visual Studio pour Mac et obliger Xcode à actualiser sa liste d’identités de signature et de profils de provisionnement disponibles (en suivant les instructions de la section [Téléchargement des profils et des certificats dans Xcode](~/ios/get-started/installation/device-provisioning/manual-provisioning.md#download)) pour qu’un nouveau profil de distribution soit disponible dans Visual Studio pour Mac.

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Vous devrez peut-être quitter Visual Studio et obliger Xcode (sur le Mac de l’hôte de build) à actualiser sa liste d’identités de signature et de profils de provisionnement disponibles (en suivant les instructions de la section [Téléchargement des profils et des certificats dans Xcode](~/ios/get-started/installation/device-provisioning/manual-provisioning.md#download)) pour qu’un nouveau profil de distribution soit disponible dans Visual Studio.

-----

<a name="selectprofile" />

## <a name="selecting-a-distribution-profile-in-a-xamarinios-project"></a>Sélection d’un profil de distribution dans un projet Xamarin.iOS

Une fois que vous êtes prêt à effectuer une build finale d’une application Xamarin.iOS, sélectionnez le profil de distribution créé ci-dessus.

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio pour Mac](#tab/vsmac)

 Dans Visual Studio pour Mac, effectuez les tâches suivantes :

1. Dans l’**Explorateur de solutions**, double-cliquez sur le nom du projet pour l’ouvrir et le modifier.
2. Sélectionnez **Signature du bundle iOS**, ainsi que le type de build dans la liste déroulante **Configuration** :

    ![](ad-hoc-distribution-images/releasexs01.png "Sélectionner le type de build dans la liste déroulante Configuration")
3. Dans la plupart des cas, les options **Identité de signature** et **Profil de provisionnement** peuvent garder leurs valeurs par défaut **Automatique**. Visual Studio pour Mac choisit le profil approprié en fonction de l’identificateur de bundle dans Info.plist :

    ![](ad-hoc-distribution-images/releasexs02.png "Identité de signature et profil de provisionnement avec la valeur par défaut Automatique")
4. Le cas échéant, sélectionnez l’identité de signature et le profil de distribution (créé ci-dessus) dans les listes déroulantes :

    ![](ad-hoc-distribution-images/releasexs03.png "Sélectionner l’identité de signature et le profil de distribution")
5. Cliquez sur le bouton **OK** pour enregistrer les changements.

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)
 Dans Visual Studio, effectuez les tâches suivantes :

1. Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le nom du projet, puis sélectionnez **Propriétés** pour l’ouvrir et le modifier.
2. Sélectionnez **Signature du bundle iOS**, ainsi que le type de build dans la liste déroulante **Configuration** :

    ![](ad-hoc-distribution-images/releasevs01.png "Sélectionner le type de build dans la liste déroulante Configuration")
3. Dans la plupart des cas, les options **Identité de signature** et **Profil de provisionnement** peuvent garder leurs valeurs par défaut **Automatique**. Visual Studio choisit le profil approprié en fonction de l’identificateur de bundle dans Info.plist :

    ![](ad-hoc-distribution-images/releasevs02.png "Identité de signature et profil de provisionnement avec la valeur par défaut Automatique")
4. Le cas échéant, sélectionnez l’identité de signature et le profil de distribution (créé ci-dessus) dans les listes déroulantes :

    ![](ad-hoc-distribution-images/releasevs03.png "Sélectionner l’identité de signature et le profil de distribution")
5. Enregistrez les changements apportés aux propriétés du projet.

-----

<a name="adhoc" />

## <a name="ad-hoc-distribution"></a>Distribution ad hoc

Bien que [TestFlight](~/ios/deploy-test/testflight.md) soit couramment utilisé pour le test et la distribution de versions bêta, il fait partie d’iTunes Connect et n’est donc pas accessible aux membres du programme **Developer Enterprise** d’Apple.

La distribution ad hoc permet aux développeurs de tester des applications bêta sur un large éventail d’appareils quand iTunes n’est pas une option. La distribution ad hoc fonctionne de la même manière que la distribution en interne. Elle nécessite la création d’un fichier IPA, qui peut ensuite être distribué par voie hertzienne ou manuellement via iTunes.

<a name="IPA_Creation" />

### <a name="ipa-support-for-ad-hoc-deployment"></a>Prise en charge du fichier IPA pour le déploiement ad hoc

Une fois les applications provisionnées, elles peuvent être placées dans un paquet appelé fichier *IPA*. Il s’agit d’un fichier zip qui contient l’application, ainsi que des métadonnées et des icônes supplémentaires. Le fichier IPA permet d’ajouter une application localement à iTunes pour qu’elle puisse être synchronisée directement sur un appareil inclus dans le profil de provisionnement.

Pour plus d’informations sur la création d’un fichier IPA, consultez le guide [Prise en charge de fichier IPA](~/ios/deploy-test/app-distribution/ipa-support.md).

## <a name="summary"></a>Récapitulatif

Cet article a décrit les mécanismes de distribution ad hoc, lesquels sont nécessaires au test des applications Xamarin.iOS.


## <a name="related-links"></a>Liens associés

- [Distribution sur l’App Store](~/ios/deploy-test/app-distribution/app-store-distribution/index.md)
- [Distribution en interne](~/ios/deploy-test/app-distribution/in-house-distribution.md)
- [Fichier iTunesMetadata.plist](~/ios/deploy-test/app-distribution/itunesmetadata.md)
- [Prise en charge IPA](~/ios/deploy-test/app-distribution/ipa-support.md)
