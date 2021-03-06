---
title: Utilisation de SkiaSharp dans Xamarin.Forms
description: SkiaSharp est un système de graphismes 2D pour .NET et le moteur de graphiques Skia open source qui est largement utilisé dans les produits Google pour c#. Ce guide explique comment utiliser SkiaSharp pour les graphismes 2D dans vos applications Xamarin.Forms.
ms.prod: xamarin
ms.assetid: 2C348BEA-81DF-4794-8857-EB1DFF5E11DB
author: charlespetzold
ms.author: chape
ms.date: 09/11/2017
ms.openlocfilehash: f7d97b798bf2a5a75af0731a665fe212491a6516
ms.sourcegitcommit: 12d48cdf99f0d916536d562e137d0e840d818fa1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2018
ms.locfileid: "39615871"
---
# <a name="using-skiasharp-in-xamarinforms"></a>Utilisation de SkiaSharp dans Xamarin.Forms

_Utiliser SkiaSharp pour les graphismes 2D dans vos applications Xamarin.Forms_

SkiaSharp est un système de graphismes 2D pour .NET et le moteur de graphiques Skia open source qui est largement utilisé dans les produits Google pour c#. Vous pouvez utiliser SkiaSharp dans vos applications Xamarin.Forms pour dessiner le texte, les bitmaps et les graphiques à vecteurs 2D. Consultez le [dessin 2D](~/graphics-games/skiasharp/index.md) guide pour plus d’informations générales sur la bibliothèque SkiaSharp et certains autres didacticiels.

Ce guide suppose que vous êtes familiarisé avec la programmation de Xamarin.Forms.

> [!VIDEO https://channel9.msdn.com/Events/Xamarin/Xamarin-University-Presents-Webinar-Series/SkiaSharp-Graphics-for-XamarinForms/player]

**Séminaire Web : Les SkiaSharp pour Xamarin.Forms**

## <a name="skiasharp-preliminaries"></a>Prérequis de SkiaSharp

SkiaSharp pour Xamarin.Forms est empaqueté sous forme de package NuGet. Une fois que vous avez créé une solution Xamarin.Forms dans Visual Studio ou Visual Studio pour Mac, vous pouvez utiliser le Gestionnaire de package NuGet pour rechercher le **SkiaSharp.Views.Forms** empaqueter et ajoutez-le à votre solution. Si vous cochez la **références** section de chaque projet après l’ajout de SkiaSharp, vous pouvez voir que divers **SkiaSharp** bibliothèques ont été ajoutées à chacun des projets dans la solution.

Si votre application Xamarin.Forms cible iOS, utilisez la page de propriétés de projet pour modifier la cible de déploiement minimum à iOS 8.0.

Dans n’importe quelle page c# qui utilise SkiaSharp, vous souhaiterez incluent un `using` directive pour le [ `SkiaSharp` ](https://developer.xamarin.com/api/namespace/SkiaSharp/) espace de noms qui englobe tous les SkiaSharp classes, structures et énumérations que vous allez utiliser dans vos graphiques la programmation. Il vous faudra également un `using` directive pour le [ `SkiaSharp.Views.Forms` ](https://developer.xamarin.com/api/namespace/SkiaSharp.Views.Forms/) espace de noms pour les classes spécifiques à Xamarin.Forms. Il s’agit un beaucoup plus petit espace de noms, avec la classe la plus importante étant [ `SKCanvasView` ](https://developer.xamarin.com/api/type/SkiaSharp.Views.Forms.SKCanvasView/). Cette classe dérive de Xamarin.Forms `View` classe et héberge votre sortie graphique de SkiaSharp.

> [!IMPORTANT]
> Le `SkiaSharp.Views.Forms` espace de noms contient également un `SKGLView` classe qui dérive de `View` mais utilise OpenGL pour le rendu de graphiques. Pour des raisons de simplicité, la limite de ce guide lui-même pour `SKCanvasView`, mais l’utilisation `SKGLView` au lieu de cela est assez semblable.

## <a name="skiasharp-drawing-basicsbasicsindexmd"></a>[Principes de base de dessin SkiaSharp](basics/index.md)

Certaines des figures graphique la plus simple, que vous pouvez dessiner avec SkiaSharp sont des rectangles, des ovales et des cercles. Dans l’affichage de ces chiffres, vous allez découvrir les coordonnées SkiaSharp, tailles et couleurs.

## <a name="skiasharp-lines-and-pathspathsindexmd"></a>[Lignes et chemins d’accès SkiaSharp](paths/index.md)

Un chemin d’accès de graphiques est une série de lignes droites connectées et de courbes. Chemins d’accès peuvent être tracés rempli, ou les deux. Cette rubrique comprend de nombreux aspects du dessin au trait, y compris les extrémités de trait et jointures et en pointillés et les lignes en pointillés, mais bloque les géométries de courbe.

## <a name="skiasharp-transformstransformsindexmd"></a>[Transformations SkiaSharp](transforms/index.md)

Transformations permettent aux objets de graphiques d’être uniformément traduite, mis à l’échelle, pivoté ou décalées. Cet article montre également comment vous pouvez utiliser une matrice 3 x 3 transformation standard pour créer des transformations non affines et appliquer des transformations aux chemins d’accès.

## <a name="skiasharp-curves-and-pathscurvesindexmd"></a>[Courbes et chemins d’accès SkiaSharp](curves/index.md)

L’exploration des chemins d’accès se poursuit avec l’ajout des courbes à des objets de chemin d’accès et d’exploiter les autres fonctionnalités puissantes de chemin d’accès. Vous verrez comment vous pouvez spécifier un chemin d’accès complet dans une chaîne de texte concis, comment utiliser les effets de chemin d’accès et comment aller dans les profondeurs de chemin d’accès.

## <a name="skiasharp-bitmapsbitmapsindexmd"></a>[Bitmaps SkiaSharp](bitmaps/index.md)

Les images bitmap sont des tableaux rectangulaires de bits correspondent aux pixels de périphérique d’affichage. Cette série d’articles montre comment charger, enregistrer, afficher, créer, dessiner sur, animer et accéder aux bits de bitmaps de SkiaSharp.

## <a name="related-links"></a>Liens associés

- [API de SkiaSharp](https://developer.xamarin.com/api/root/SkiaSharp/)
- [SkiaSharpFormsDemos (exemple)](https://developer.xamarin.com/samples/xamarin-forms/SkiaSharpForms/Demos/)
- [SkiaSharp avec Xamarin.Forms webinaire (vidéo)](https://channel9.msdn.com/Events/Xamarin/Xamarin-University-Presents-Webinar-Series/SkiaSharp-Graphics-for-XamarinForms)
