---
title: Prise en main Xamarin.Essentials
description: Xamarin.Essentials fournit une API multi-plateforme unique qui fonctionne avec n’importe quel iOS, Android ou UWP application qui sont accessibles à partir de partagée code quelle que soit la façon dont l’interface utilisateur est créé.
ms.assetid: B2669C48-B659-4854-BD80-FEB0E876F5B9
author: jamesmontemagno
ms.author: jamont
ms.date: 05/04/2018
ms.openlocfilehash: a42086f70eb81a761358655b3effb9f8f934c8d4
ms.sourcegitcommit: 3f2737f8abf9b855edf060474aa222e973abda3f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37067286"
---
# <a name="get-started-with-xamarinessentials"></a>Prise en main Xamarin.Essentials

![Version préliminaire de NuGet](~/media/shared/pre-release.png)

Xamarin.Essentials fournit une API multi-plateforme unique qui fonctionne avec n’importe quel iOS, Android ou UWP application qui sont accessibles à partir de partagée code quelle que soit la façon dont l’interface utilisateur est créé.

## <a name="platform-support"></a>Prise en charge de plateforme

Xamarin.Essentials prend en charge les plates-formes et les systèmes d’exploitation suivants :

| Plateforme | Version |
| --- | --- |
| Android | 4.4 (API 19) ou une version ultérieure |
| iOS |supérieur ou égal à 10,0 |
| UWP | 10.0.16299.0 ou une version ultérieure |

## <a name="installation"></a>Installation

Xamarin.Essentials est disponible sous forme de package NuGet qui peut être ajouté à un projet nouveau ou existant à l’aide de Visual Studio.

1. Téléchargez et installez [Visual Studio](http://visualstudio.com) avec la [Visual Studio tools pour Xamarin](~/cross-platform/get-started/installation/index.md).

2. Ouvrez un projet existant ou créez un nouveau projet à l’aide du modèle application vide sous **Visual Studio c#** (Android, iPhone et iPad ou Cross-Platform). **Important**: si l’ajout à un projet UWP Vérifiez la Build 16299 ou une version ultérieure est définie dans les propriétés du projet.

3. Ajouter le **Xamarin.Essentials** package NuGet pour chaque projet :

    # <a name="visual-studiotabwindows"></a>[Visual Studio](#tab/windows)

    Dans le panneau de configuration de l’Explorateur de solutions, cliquez avec le bouton droit sur le nom de la solution et sélectionnez **gérer les Packages NuGet**. Recherchez **Xamarin.Essentials** et installez le package dans **tous les** projets, y compris les bibliothèques Android, iOS, UWP et .NET Standard.

    > [!TIP]
    > Vérifiez le **inclure la version préliminaire** zone lors de la [ **Xamarin.Essentials** NuGet](https://www.nuget.org/packages/Xamarin.Essentials) est en version préliminaire.

    # <a name="visual-studio-for-mactabmacos"></a>[Visual Studio pour Mac](#tab/macos)

    Dans le panneau de configuration de l’Explorateur de solutions, cliquez avec le bouton droit sur le nom du projet et sélectionnez **Ajouter > ajouter des Packages NuGet...** . Recherchez **Xamarin.Essentials** et installez le package dans **tous les** projets, y compris les bibliothèques Android, iOS et .NET Standard.

    > [!TIP]
    > Vérifiez le **afficher les packages de la version préliminaire** zone lors de la [ **Xamarin.Essentials** NuGet](https://www.nuget.org/packages/Xamarin.Essentials) est en version préliminaire.

    -----

4. Ajouter une référence à Xamarin.Essentials dans n’importe quelle classe c# pour référencer l’API.

    ```csharp
    using Xamarin.Essentials;
    ```

5. Xamarin.Essentials requiert le programme d’installation spécifique à la plateforme :

    # <a name="androidtabandroid"></a>[Android](#tab/android)

    Xamarin.Essentials prend en charge une version minimale Android 4.4, correspondant au niveau de l’API 19, mais la version Android cible pour la compilation doit être 8.1, correspondant au niveau de l’API 27. (Dans Visual Studio, ces deux versions sont définies dans la boîte de dialogue Propriétés du projet pour le projet Android, dans l’onglet manifeste Android. Dans Visual Studio pour Mac, elles sont définies dans la boîte de dialogue Options du projet pour le projet Android, dans l’onglet Application Android.) 
    
    Xamarin.Essentials installe la version 27.0.2 des bibliothèques Xamarin.Android.Support dont il a besoin. Toutes les autres bibliothèques Xamarin.Android.Support nécessaires à votre application doivent également être mis à jour vers la version 27.0.2 à l’aide du Gestionnaire de package NuGet. Toutes les bibliothèques Xamarin.Android.Support utilisés par votre application doivent être identiques et doit être au moins la version 27.0.2. Reportez-vous à la [page Résolution des problèmes](troubleshooting.md) si vous rencontrez des problèmes d’ajout de Xamarin.Essentials NuGet ou la mise à jour NuGets dans votre solution.

    Dans le projet Android `MainLauncher` ou n’importe quel `Activity` qui est lancé Xamarin.Essentials doivent être initialisés dans le `OnCreate` méthode :

    ```csharp
    Xamarin.Essentials.Platform.Init(this, bundle);
    ```

    Pour gérer les autorisations d’exécution sur Android, Xamarin.Essentials doit recevoir les `OnRequestPermissionsResult`. Ajoutez le code suivant à tous les `Activity` classes :

    ```csharp
    public override void OnRequestPermissionsResult(int requestCode, string[] permissions, [GeneratedEnum] Android.Content.PM.Permission[] grantResults)
    {
        Xamarin.Essentials.Platform.OnRequestPermissionsResult(requestCode, permissions, grantResults);

        base.OnRequestPermissionsResult(requestCode, permissions, grantResults);
    }
    ```

    # <a name="iostabios"></a>[iOS](#tab/ios)

    Aucune configuration supplémentaire n’est requise.

    # <a name="uwptabuwp"></a>[UWP](#tab/uwp)

    Aucune configuration supplémentaire n’est requise.

    -----

6. Suivez les [Xamarin.Essentials guides](index.md) qui permettent de copier et coller des extraits de code pour chaque fonctionnalité.

## <a name="other-resources"></a>Autres ressources

Nous vous recommandons des développeurs à une visite de Xamarin [mise en route avec le développement Xamarin](~/cross-platform/getting-started/index.md).

Visitez le [Xamarin.Essentials GitHub référentiel](http://github.com/xamarin/Essentials) voir actuel du code, nouveautés à venir ensuite, exécutez les exemples, source et de fermer l’espace de stockage. Contributions de la Communauté sont les bienvenus !

Parcourir le [documentation de l’API](xref:Xamarin.Essentials) pour toutes les fonctionnalités de Xamarin.Essentials.
