---
title: Utilisation de watchOS tailles d’écran de Xamarin
description: Ce document décrit l’utilisation des différentes tailles d’écran watchOS. Il présente le Concepteur d’Interface, le simulateur, watchOS watchOS et ressources d’image.
ms.prod: xamarin
ms.assetid: 840DF939-2F59-4ABA-87D8-92AAC8A92BC4
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/17/2017
ms.openlocfilehash: 30866c70879950acd8f43fd5880b1b24ba127fa4
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34790709"
---
# <a name="working-with-watchos-screen-sizes-in-xamarin"></a>Utilisation de watchOS tailles d’écran de Xamarin

Apple Watch est disponible dans les deux tailles d’écran :

- **38mm**
  - nombre de pixels logiques 136 x 170 (272 x 340 physiques pixels)

- **42mm**
  - 156 x 195 pixels logiques (312 x 390 physiques pixels).

Taille de l’écran doit tenir compte lors de la conception et le test de vos applications.

## <a name="watchos-interface-designer"></a>watchOS Interface Designer

Par défaut, Visual Studio pour Mac concepteur affichera regarder contrôleurs d’interface à **Any Apple Watch**.

![](screen-sizes-images/screen-any-sml.png "Les contrôleurs d’interface concepteur affiche espion à n’importe quel Apple Watch")

Utilisez le menu de taille pour modifier et afficher un aperçu de votre plan conceptuel à une des tailles d’écran disponibles : **38mm** ou **42mm**:

![](screen-sizes-images/screen-menu-sml.png "Sélection de la taille de 38 ou 42mm")

La taille d’écran supérieure parfois restituera contenu qui serait tronquée/masqué sur l’écran de petite taille.
Veillez à tester dans les deux tailles.


### <a name="interface-design"></a>Conception d'interfaces

Votre application doit afficher le même contenu dans l’écran, quelle que soit la taille et il doit développer ou réduire des éléments comme il convient. Dans Visual Studio pour Mac générateur, dans l’inspecteur de l’attribut, vous devez utiliser **relatif au conteneur** ou **taille pour ajuster le contenu** , plutôt que des tailles fixes.

![](screen-sizes-images/sizeattributepanel-sml.png "Utilisez Relative au conteneur ou taille pour ajuster le contenu, plutôt que des tailles fixes")

Étant donné que l’écran de surveillance est entourée d’un cadre noir, en fournissant la marge intérieure autour de votre interface n’est pas recommandée. Permettent d’éléments reposent sur le bord de l’écran et laisser le panneau forment une bordure naturelle autour de l’application.


## <a name="watchos-simulator"></a>watchOS simulateur

Lorsque test sur le simulateur, vous pouvez facilement basculer entre les tailles d’écran de deux à l’aide de la **matériel > appareil** menu.

![](screen-sizes-images/simulator.png "Le simulateur peut basculer entre les tailles d’écran de deux à l’aide du menu du périphérique matériel")


## <a name="image-resources"></a>Ressources image

Vous devez utiliser plusieurs composants de l’image si un seul élément multimédia ne recherche pas bon pour différentes tailles. Les catalogues asset image permettent distincts pour chaque taille :

![](screen-sizes-images/images-xcassets.png "Éditeur de catalogue asset image")

```csharp
// specify the asset name, the correct size will automatically be loaded
staticImage.SetImage(UIImage.FromBundle("Walkway"));
```

Ou bien, utilisez le code pour déterminer la taille d’écran et de charger des images complètement :

```csharp
bool large = WKInterfaceDevice.CurrentDevice.ScreenBounds.Size.Width > 136.0;
// Load image depending on screen size
using (var image = UIImage.FromBundle (large ? "42mm-Walkway" : "38mm-Walkway"))
{
   myImage.SetImage (image);

}
```

En savoir plus sur à l’aide de la [contrôle image](~/ios/watchos/user-interface/image.md).



## <a name="related-links"></a>Liens associés

- [Introduction à watchOS 3](~/ios/watchos/platform/introduction-to-watchos3/index.md)
