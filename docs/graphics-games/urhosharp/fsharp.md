---
title: 'Programmation UrhoSharp avec F #'
description: 'Ce document décrit comment créer une simple application hello world UrhoSharp avec F # dans Visual Studio pour Mac.'
ms.prod: xamarin
ms.assetid: F976AB09-0697-4408-999A-633977FEFF64
author: charlespetzold
ms.author: chape
ms.date: 03/29/2017
ms.openlocfilehash: 430c4eca7c6dbd7107692246b70ff93bafa44d01
ms.sourcegitcommit: b56b3f906d2c05a3f1be219ef41be8b79e519b8e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/25/2018
ms.locfileid: "39241832"
---
# <a name="programming-urhosharp-with-f"></a>Programmation UrhoSharp avec F #

UrhoSharp peut être programmé avec F # avec les mêmes bibliothèques et concepts utilisés par les programmeurs c#. Le [à l’aide de UrhoSharp](~/graphics-games/urhosharp/using.md) article donne une vue d’ensemble du moteur UrhoSharp et doivent être lues avant cet article.

Telles que de nombreuses bibliothèques origine dans le monde de C++, de nombreuses fonctions de UrhoSharp retournent des valeurs booléennes ou des entiers indiquant la réussite ou l’échec. Vous devez utiliser `|> ignore` pour ignorer ces valeurs.

Le [exemple de programme](https://github.com/xamarin/recipes/tree/master/Recipes/cross-platform/urho/urho-fsharp/HelloWorldUrhoFsharp) est un « Hello World » pour UrhoSharp à partir de F #.

## <a name="creating-an-empty-project"></a>Création d’un projet vide

Il n’existe aucun modèle F # pour UrhoSharp encore disponible, par conséquent, pour créer votre propre projet UrhoSharp que vous pouvez démarrer avec la [exemple](https://github.com/xamarin/recipes/tree/master/Recipes/cross-platform/urho/urho-fsharp/HelloWorldUrhoFsharp) ou procédez comme suit :

1. À partir de Visual Studio pour Mac, créer un nouveau **Solution**. Choisissez **iOS > application > application avec affichage unique** et sélectionnez **F #** comme langage d’implémentation. 
1. Supprimer le **Main.storyboard** fichier. Ouvrir le **Info.plist** fichier puis, dans le **iPhone / iPod des informations de déploiement** volet, supprimer le `Main` chaîne dans le **Interface principale** liste déroulante.
1. Supprimer le **ViewController.fs** également le fichier.

## <a name="building-hello-world-in-urho"></a>Création de Hello World dans Urho

Vous êtes maintenant prêt à commencer à définir les classes de votre jeu. Au minimum, vous devez définir une sous-classe de `Urho.Application` et substituer sa `Start` (méthode). Pour créer ce fichier, avec le bouton droit sur votre projet F #, choisissez **ajouter un nouveau fichier...**  et ajoutez une classe F # vide à votre projet. Le nouveau fichier sera ajouté à la fin de la liste des fichiers dans votre projet, mais vous devez faire glisser afin qu’il apparaisse *avant* il est utilisé dans **AppDelegate.fs**.

1. Ajoutez une référence au package NuGet de Urho.
1. À partir d’un projet existant de Urho, copier les répertoires (grandes) **CoreData /** et **données /** dans votre projet **ressources /** directory. Dans votre projet F #, cliquez sur le **ressources** dossier et utilisez **ajouter / ajouter un dossier existant** pour ajouter tous ces fichiers à votre projet.

Structure de votre projet doit maintenant ressembler à :

![](fsharp-images/solutionpane.png "La structure de projet doit maintenant ressembler à")

Définir votre classe qui vient d’être créé comme un sous-type de `Urho.Application` et substituer sa `Start` méthode :

```fsharp
namespace HelloWorldUrho1

open Urho
open Urho.Gui
open Urho.iOS

type HelloWorld(o : ApplicationOptions) =
    inherit Urho.Application(o) 

override this.Start() = 
        let cache = this.ResourceCache
        let helloText = new Text()

        helloText.Value <- "Hello World from Urho3D, Mono, and F#"
        helloText.HorizontalAlignment <- HorizontalAlignment.Center
        helloText.VerticalAlignment <- VerticalAlignment.Center

        helloText.SetColor (new Color(0.f, 1.f, 0.f))
        let f = cache.GetFont("Fonts/Anonymous Pro.ttf")

        helloText.SetFont(f, 30) |> ignore
                  
        this.UI.Root.AddChild(helloText)
            
```

Le code est très simple. Il utilise le `Urho.Gui.Text` classe pour afficher une chaîne alignée au centre avec une certaine taille de police et de couleur. 

Avant ce code peut s’exécuter, cependant, UrhoSharp doit être initialisé. 

Ouvrez le fichier AppDelegate.fs et modifiez le `FinishedLaunching` méthode comme suit :

```fsharp
namespace HelloWorldUrho1

open System
open UIKit
open Foundation
open Urho
open Urho.iOS

[<Register ("AppDelegate")>]
type AppDelegate () =
    inherit UIApplicationDelegate ()

    override this.FinishedLaunching (app, options) =
        let o = ApplicationOptions.Default
     
        let g = new HelloWorld(o)
        g.Run() |> ignore
       
        true
```

Le `ApplicationOptions.Default` fournit les options par défaut pour une application en mode paysage. Transmettre `ApplicationOptions` au constructeur par défaut pour votre `Application` sous-classe (Notez que lorsque vous avez défini le `HelloWorld` classe, la ligne `inherit Application(o)` appelle le constructeur de classe de base). 

Le `Run` méthode de votre `Application` lance le programme. Il est défini comme retournant un `int`, ce qui peut être transmis à `ignore`. 

Le programme résultant doit ressembler à :

![](fsharp-images/helloworldfsharp.png "Le programme résultant doit ressembler à")








## <a name="related-links"></a>Liens associés

- [Rechercher sur GitHub (exemple)](https://github.com/xamarin/recipes/tree/master/Recipes/cross-platform/urho/urho-fsharp/HelloWorldUrhoFsharp)
