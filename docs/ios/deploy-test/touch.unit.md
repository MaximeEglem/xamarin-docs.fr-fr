---
title: Tests unitaires d’applications Xamarin.iOS
description: Ce document fournit une vue d’ensemble des tests unitaires d’une application Xamarin.iOS. Il décrit comment créer un projet de tests unitaires et comment écrire et exécuter des tests.
ms.prod: xamarin
ms.assetid: BD959779-3239-79B6-5289-3A9ECDFBD973
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/19/2017
ms.openlocfilehash: ce2b452d50222ac3561dab5b76915b7ae634934b
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34785461"
---
# <a name="unit-testing-xamarinios-apps"></a>Tests unitaires d’applications Xamarin.iOS

Ce document décrit comment créer des tests unitaires pour vos projets Xamarin.iOS.
Les tests unitaires avec Xamarin.iOS s’effectuent à l’aide du framework Touch.Unit. Ce framework contient un outil Test Runner iOS, ainsi qu’une version modifiée de NUnit, appelée [Touch.Unit](https://github.com/xamarin/Touch.Unit), qui fournit un ensemble d’API couramment utilisées pour l’écriture de tests unitaires.

## <a name="setting-up-a-test-project"></a>Configuration d’un projet de tests

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio pour Mac](#tab/vsmac)

Pour configurer un framework pour votre projet de tests unitaires, ajoutez simplement à votre solution un projet de type **Projet de tests unitaires iOS**. Cliquez avec le bouton droit sur votre solution, puis sélectionnez **Ajouter > Ajouter un nouveau projet**. Dans la liste, sélectionnez **iOS > Tests > API unifiée > Projet de tests unitaires iOS** (vous pouvez choisir C# ou F#).

![](touch.unit-images/00.png "Choisir C# ou F#")

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Pour configurer un framework pour votre projet de tests unitaires, ajoutez simplement à votre solution un projet de type **Projet de tests unitaires iOS**. Cliquez avec le bouton droit sur votre solution, puis sélectionnez **Ajouter > Nouveau projet...**. Dans la liste, sélectionnez **Visual C# > iOS > Application de tests unitaires (iOS)**.

![](touch.unit-images/00a.png "Application de tests unitaires (iOS)")

-----

Les étapes précédentes créent un projet de base qui contient un programme Runner simple et qui fait référence au nouvel assembly MonoTouch.NUnitLite. Votre projet doit ressembler à ceci :

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio pour Mac](#tab/vsmac)

![](touch.unit-images/01.png "Projet dans l’Explorateur de solutions")

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

![](touch.unit-images/01a.png "Projet dans l’Explorateur de solutions")

-----

La classe `AppDelegate.cs` contient Test Runner, comme illustré ci-dessous :

```csharp
[Register ("AppDelegate")]
public partial class AppDelegate : UIApplicationDelegate
{
        UIWindow window;
        TouchRunner runner;

        public override bool FinishedLaunching (UIApplication app, NSDictionary options)
        {
                // create a new window instance based on the screen size
                window = new UIWindow (UIScreen.MainScreen.Bounds);
                runner = new TouchRunner (window);

                // register every tests included in the main application/assembly
                runner.Add (System.Reflection.Assembly.GetExecutingAssembly ());

                window.RootViewController = new UINavigationController (runner.GetViewController ());

                // make the window visible
                window.MakeKeyAndVisible ();

                return true;
        }
}
```

## <a name="writing-some-tests"></a>Écriture de tests

Votre environnement de base est en place. Vous pouvez donc commencer à écrire votre première série de tests.

Pour écrire des tests, vous créez des classes auxquelles vous appliquez l’attribut `[TestFixture]`. Dans chaque classe TestFixture, vous devez appliquer l’attribut `[Test]` à chaque méthode devant être appelée par Test Runner. Les fixtures de test peuvent se trouver dans n’importe quel fichier dans votre projet de tests.

Pour démarrer rapidement, sélectionnez **Ajouter/Ajouter un nouveau fichier** et sélectionnez **UnitTests** dans le groupe Xamarin.iOS. Cela ajoute un fichier squelette qui contient un test réussi, un test échoué et un test ignoré, comme illustré ci-dessous :

```csharp
using System;
using NUnit.Framework;

namespace Fixtures {

        [TestFixture]
        public class Tests {

                [Test]
                public void Pass ()
                {
                        Assert.True (true);
                }

                [Test]
                public void Fail ()
                {
                        Assert.False (true);
                }

                [Test]
                [Ignore ("another time")]
                public void Ignore ()
                {
                        Assert.True (false);
                }
        }
}
```

## <a name="running-your-tests"></a>Exécution de vos tests

Pour exécuter ce projet dans votre solution, cliquez dessus avec le bouton droit et sélectionnez **Déboguer l’élément** ou **Exécuter l’élément**.

Test Runner affiche les tests qui sont enregistrés et vous permet de sélectionner individuellement les tests à exécuter.

[![](touch.unit-images/02.png "Liste des tests inscrits")](touch.unit-images/02.png#lightbox) 

[![](touch.unit-images/03.png "Test individuel")](touch.unit-images/03.png#lightbox) 

[![](touch.unit-images/04.png "Résultats de l’exécution")](touch.unit-images/04.png#lightbox)

Vous pouvez exécuter les fixtures de test de votre choix en les sélectionnant dans les vues imbriquées, ou exécuter tous les tests en sélectionnant le bouton « Exécuter tout ». Si vous exécutez le test par défaut, celui-ci est censé inclure un test réussi, un test échoué et un test ignoré. Voici à quoi ressemble le rapport. Vous pouvez accéder directement aux détails des tests ayant échoué pour déterminer la cause de l’échec :

[![](touch.unit-images/05.png "Exemple de rapport")](touch.unit-images/05.png#lightbox) [![](touch.unit-images/05.png "Exemple de rapport")](touch.unit-images/05.png#lightbox) [![](touch.unit-images/05.png "Exemple de rapport")](touch.unit-images/05.png#lightbox)

Vous pouvez également examiner les tests en cours d’exécution et leur état actuel dans la fenêtre Sortie de l’application dans votre environnement IDE.

## <a name="writing-new-tests"></a>Écriture de nouveaux tests

NUnitLite est une version modifiée de NUnit, appelée projet [Touch.Unit](https://github.com/xamarin/Touch.Unit). Il s’agit d’un framework de test léger pour .NET, basé sur les concepts [NUnit](http://nunit.com/) et offrant une partie de ses fonctionnalités.
Il utilise peu de ressources et s’exécute sur les plateformes limitées en ressources, telles que celles utilisées dans les environnements de développement incorporé et mobile. [Découvrez l’API NUnitLite](https://developer.xamarin.com/api/namespace/NUnitLite/) disponible dans Xamarin.iOS. Avec la structure de base fournie par le modèle de test unitaire, les méthodes de la [classe Assert](https://developer.xamarin.com/api/type/NUnit.Framework.Assert/) constituent votre point d’entrée principal.

En plus des méthodes de la classe Assert, la fonctionnalité de test unitaire est partagée par les espaces de noms suivants qui font partie de NUnitLite :

-   [NUnit.Framework](https://developer.xamarin.com/api/namespace/NUnit.Framework/)
-   [NUnit.Constraints](https://developer.xamarin.com/api/namespace/NUnit.Framework.Constraints/)
-   [NUnitLite](https://developer.xamarin.com/api/namespace/NUnitLite/)
-   [NUniteLite.Runner](https://developer.xamarin.com/api/namespace/NUnitLite.Runner/)


Le programme Test Runner spécifique à Xamarin.iOS est documenté ici :

-   [NUnit.UI.TouchRunner](https://developer.xamarin.com/api/type/NUnit.UI.TouchRunner/)
