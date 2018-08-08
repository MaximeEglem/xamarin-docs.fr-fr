---
title: Dessiner un cercle Simple dans SkiaSharp
description: Cet article explique les principes fondamentaux du dessin SkiaSharp, y compris le canevas et paint, dans les applications de Xamarin.Forms et illustre ceci avec l’exemple de code.
ms.prod: xamarin
ms.technology: xamarin-skiasharp
ms.assetid: E3A4E373-F65D-45C8-8E77-577A804AC3F8
author: charlespetzold
ms.author: chape
ms.date: 03/10/2017
ms.openlocfilehash: e06a1310fad01da11c8d8b115df504cc19426344
ms.sourcegitcommit: 12d48cdf99f0d916536d562e137d0e840d818fa1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2018
ms.locfileid: "39615221"
---
# <a name="drawing-a-simple-circle-in-skiasharp"></a>Dessiner un cercle Simple dans SkiaSharp

_Découvrez les principes fondamentaux de dessin SkiaSharp, y compris le canevas et paint_

Cet article présente les concepts du dessin de graphiques dans Xamarin.Forms à l’aide de SkiaSharp, y compris la création un `SKCanvasView` objet pour héberger la gestion des graphiques le `PaintSurface` événement et à l’aide un `SKPaint` objet pour spécifier la couleur et autres dessins attributs.

Le [ **SkiaSharpFormsDemos** ](https://developer.xamarin.com/samples/xamarin-forms/SkiaSharpForms/Demos/) programme contient des exemples de code pour cette série d’articles de SkiaSharp. La première page est autorisée à utiliser **cercle Simple** et appelle la classe de page [ `SimpleCirclePage` ](https://github.com/xamarin/xamarin-forms-samples/blob/master/SkiaSharpForms/Demos/Demos/SkiaSharpFormsDemos/Basics/SimpleCirclePage.cs). Ce code montre comment dessiner un cercle dans le centre de la page avec un rayon de 100 pixels. Le contour du cercle est rouge, et l’intérieur du cercle est bleu.

![](circle-images/circleexample.png "Un cercle bleu surlignée en rouge")

Le [ `SimpleCirle` ](https://github.com/xamarin/xamarin-forms-samples/blob/master/SkiaSharpForms/Demos/Demos/SkiaSharpFormsDemos/Basics/SimpleCirclePage.cs) dérive de la classe de page `ContentPage` et contient deux `using` directives pour les espaces de noms SkiaSharp :

```csharp
using SkiaSharp;
using SkiaSharp.Views.Forms;
```

Le constructeur suivant de la classe crée un [ `SKCanvasView` ](https://developer.xamarin.com/api/type/SkiaSharp.Views.Forms.SKCanvasView/) d’objet, attache un gestionnaire pour la [ `PaintSurface` ](https://developer.xamarin.com/api/event/SkiaSharp.Views.Forms.SKCanvasView.PaintSurface/) événements et définit le `SKCanvasView` objet en tant que le contenu de la page :

```csharp
public SimpleCirclePage()
{
    Title = "Simple Circle";

    SKCanvasView canvasView = new SKCanvasView();
    canvasView.PaintSurface += OnCanvasViewPaintSurface;
    Content = canvasView;
}
```

Le `SKCanvasView` occupe toute la zone de contenu de la page. Vous pouvez également combiner une `SKCanvasView` avec autres Xamarin.Forms `View` dérivés, comme vous le verrez dans d’autres exemples.

Le `PaintSurface` Gestionnaire d’événements est où vous effectuez toutes les votre dessin. Cette méthode est appelée en général plusieurs fois pendant l’exécution de votre programme, afin qu’il doit mettre à jour toutes les informations nécessaires pour recréer les graphismes s’afficher :

```csharp
void OnCanvasViewPaintSurface(object sender, SKPaintSurfaceEventArgs args)
{
    ...
}

```

Le [ `SKPaintSurfaceEventArgs` ](https://developer.xamarin.com/api/type/SkiaSharp.Views.Forms.SKPaintSurfaceEventArgs/) objet qui accompagne l’événement a deux propriétés :

- [`Info`](https://developer.xamarin.com/api/property/SkiaSharp.Views.Forms.SKPaintSurfaceEventArgs.Info/) de type [`SKImageInfo`](https://developer.xamarin.com/api/type/SkiaSharp.SKImageInfo/)
- [`Surface`](https://developer.xamarin.com/api/property/SkiaSharp.Views.Forms.SKPaintSurfaceEventArgs.Surface/) de type [`SKSurface`](https://developer.xamarin.com/api/type/SkiaSharp.SKSurface/)

Le `SKImageInfo` structure contient des informations sur la surface de dessin, plus important encore, il est la largeur et hauteur en pixels. Le `SKSurface` objet représente la surface de dessin. Dans ce programme, la surface de dessin est un écran vidéo, mais dans d’autres programmes un `SKSurface` objet peut également représenter une bitmap qui vous permet de dessiner sur SkiaSharp.

La propriété la plus importante de `SKSurface` est [ `Canvas` ](https://developer.xamarin.com/api/property/SkiaSharp.SKSurface.Canvas/) de type [ `SKCanvas` ](https://developer.xamarin.com/api/type/SkiaSharp.SKCanvas/). Cette classe est un contexte qui permet d’effectuer le dessin proprement dit de dessin des graphiques. Le `SKCanvas` objet encapsule un état graphique qui inclut les transformations graphiques et le découpage.

Voici un départ typique d’un `PaintSurface` Gestionnaire d’événements :

```csharp
void OnCanvasViewPaintSurface(object sender, SKPaintSurfaceEventArgs args)
{
    SKImageInfo info = args.Info;
    SKSurface surface = args.Surface;
    SKCanvas canvas = surface.Canvas;

    canvas.Clear();
    ...
}

```

Le [ `Clear` ](https://developer.xamarin.com/api/member/SkiaSharp.SKCanvas.Clear()/) méthode efface la zone de dessin avec une couleur transparente. Une surcharge vous permet de spécifier une couleur d’arrière-plan pour la zone de dessin.

L’objectif ici consiste à tracer un cercle rouge rempli en bleu. Étant donné que cette image de graphique particulier contient deux couleurs différentes, la tâche doit être effectuée en deux étapes. La première étape consiste à dessiner le contour du cercle. Pour spécifier la couleur et autres caractéristiques de la ligne, vous créez et initialisez une [ `SKPaint` ](https://developer.xamarin.com/api/type/SkiaSharp.SKPaint/) objet :

```csharp
void OnCanvasViewPaintSurface(object sender, SKPaintSurfaceEventArgs args)
{
    ...
    SKPaint paint = new SKPaint
    {
        Style = SKPaintStyle.Stroke,
        Color = Color.Red.ToSKColor(),
        StrokeWidth = 25
    };
    ...
}
```

Le [ `Style` ](https://developer.xamarin.com/api/property/SkiaSharp.SKPaint.Style/) propriété indique que vous souhaitez *stroke* une ligne (dans ce cas, le contour du cercle) au lieu de *remplissage* l’intérieur. Les trois membres de le [ `SKPaintStyle` ](https://developer.xamarin.com/api/type/SkiaSharp.SKPaintStyle/) énumération sont les suivantes :

- [`Fill`](https://developer.xamarin.com/api/field/SkiaSharp.SKPaintStyle.Fill/)
- [`Stroke`](https://developer.xamarin.com/api/field/SkiaSharp.SKPaintStyle.Stroke/)
- [`StrokeAndFill`](https://developer.xamarin.com/api/field/SkiaSharp.SKPaintStyle.StrokeAndFill/)

La valeur par défaut est `Fill`. La troisième option permet de tracer la ligne et de remplir l’intérieur de la même couleur.

Définir le [ `Color` ](https://developer.xamarin.com/api/property/SkiaSharp.SKPaint.Color/) propriété une valeur de type [ `SKColor` ](https://developer.xamarin.com/api/type/SkiaSharp.SKColor/). Vous pouvez notamment créer un `SKColor` valeur est en convertissant un Xamarin.Forms `Color` valeur un `SKColor` valeur à l’aide de la méthode d’extension [ `ToSKColor` ](https://developer.xamarin.com/api/member/SkiaSharp.Views.Forms.Extensions.ToSKColor/p/Xamarin.Forms.Color/). Le [ `Extensions` ](https://developer.xamarin.com/api/type/SkiaSharp.Views.Forms.Extensions/) classe dans le `SkiaSharp.Views.Forms` espace de noms inclut d’autres méthodes qui convertissent entre les valeurs de Xamarin.Forms et SkiaSharp.

Le [ `StrokeWidth` ](https://developer.xamarin.com/api/property/SkiaSharp.SKPaint.StrokeWidth/) propriété indique l’épaisseur de la ligne. Ici, il est défini sur 25 pixels.

Que vous utilisez `SKPaint` objet sur lequel dessiner le cercle :

```csharp
void OnCanvasViewPaintSurface(object sender, SKPaintSurfaceEventArgs args)
{
    ...
    canvas.DrawCircle(info.Width / 2, info.Height / 2, 100, paint);
    ...
}
```

Coordonnées sont spécifiées par rapport à l’angle supérieur gauche de la surface d’affichage. X coordonne augmentation à droite et l’augmentation de coordonnées Y pour descendre. Dans la discussion à propos des graphiques, souvent la notation mathématique (x, y) est utilisée pour désigner un point. Le point (0, 0) est l’angle supérieur gauche de la surface d’affichage et est souvent appelé la *origine*.

Les deux premiers arguments de `DrawCircle` indiquent les coordonnées X et Y du centre du cercle. Celles-ci sont affectées de moitié la largeur et la hauteur de la surface d’affichage pour placer le centre du cercle dans le centre de la surface d’affichage. Le troisième argument spécifie le rayon du cercle et le dernier argument est le `SKPaint` objet.

Pour remplir l’intérieur du cercle, vous pouvez modifier deux propriétés de la `SKPaint` objet et appelez `DrawCircle` à nouveau. Ce code montre également une autre façon d’obtenir un `SKColor` valeur parmi de nombreux champs de la [ `SKColors` ](https://developer.xamarin.com/api/type/SkiaSharp.SKColors/) structure :

```csharp
void OnCanvasViewPaintSurface(object sender, SKPaintSurfaceEventArgs args)
{
    ...
    paint.Style = SKPaintStyle.Fill;
    paint.Color = SKColors.Blue;
    canvas.DrawCircle(args.Info.Width / 2, args.Info.Height / 2, 100, paint);
}
```
Cette fois-ci, le `DrawCircle` appel remplit le cercle à l’aide des nouvelles propriétés de la `SKPaint` objet.

Voici le programme en cours d’exécution sur iOS, Android et la plateforme Windows universelle :

[![](circle-images/simplecircle-small.png "Capture d’écran triple de la page Simple cercle")](circle-images/simplecircle-large.png#lightbox "Triple capture d’écran de la page de cercle Simple")

Lorsque vous exécutez le programme vous-même, vous pouvez activer le téléphone ou le simulateur sur le côté pour voir comment le graphique est redessiné. Chaque fois que le graphique doit être redessiné, le `PaintSurface` Gestionnaire d’événements est appelé à nouveau.

Un `SKPaint` objet n’est guère plus qu’une collection de propriétés de dessin graphics. Ces objets sont très légers. Vous pouvez réutiliser `SKPaint` objets que ce programme, ou vous pouvez créer plusieurs `SKPaint` objets pour différentes combinaisons des propriétés de dessin. Vous pouvez créer et initialiser ces objets en dehors de la `PaintSurface` Gestionnaire d’événements et vous pouvez les enregistrer en tant que champs dans votre classe de page.

Bien que la largeur du contour du cercle est spécifiée comme 25 pixels &mdash; ou un quart du rayon du cercle &mdash; il semble être plus étroit, et il existe une bonne raison pour cela : la moitié de la largeur de la ligne est masquée par le cercle bleu. Les arguments de la `DrawCircle` méthode définissent les coordonnées géométriques abstraites d’un cercle. L’intérieur de bleu est dimensionné à cette dimension au pixel le plus proche, mais le contour de 25 pixels de large rapproche du cercle géométrique &mdash; la moitié de l’intérieur et l’autre moitié à l’extérieur.

L’exemple suivant dans le [l’intégration avec Xamarin.Forms](~/xamarin-forms/user-interface/graphics/skiasharp/basics/integration.md) article montre visuellement.


## <a name="related-links"></a>Liens associés

- [API de SkiaSharp](https://developer.xamarin.com/api/root/SkiaSharp/)
- [SkiaSharpFormsDemos (exemple)](https://developer.xamarin.com/samples/xamarin-forms/SkiaSharpForms/Demos/)
