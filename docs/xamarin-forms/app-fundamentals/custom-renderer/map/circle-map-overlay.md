---
title: Mise en surbrillance d’une zone circulaire sur une carte
description: Cet article explique comment ajouter un segment de recouvrement circulaire à un mappage, pour mettre en surbrillance une zone circulaire de la carte. IOS et Android offrent des API pour l’ajout de la superposition circulaire pour la carte, sur UWP, la superposition est restituée sous la forme d’un polygone.
ms.prod: xamarin
ms.assetid: 6FF8BD15-074E-4E6A-9522-F9E2BE32EF12
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 11/29/2017
ms.openlocfilehash: 3064296d4c78a3342fb27afc971c37a029987e5e
ms.sourcegitcommit: 6e955f6851794d58334d41f7a550d93a47e834d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38998555"
---
# <a name="highlighting-a-circular-area-on-a-map"></a>Mise en surbrillance d’une zone circulaire sur une carte

_Cet article explique comment ajouter un segment de recouvrement circulaire à un mappage, pour mettre en surbrillance une zone circulaire de la carte._

## <a name="overview"></a>Vue d'ensemble

Une superposition est un graphique en couche sur une carte. Superpositions prend en charge le dessin contenu graphique qui s’adapte à la carte, comme elle est redimensionnée. Les captures d’écran suivantes montrent le résultat de l’ajout d’un segment de recouvrement circulaire à un mappage :

![](circle-map-overlay-images/screenshots.png)

Quand un [ `Map` ](xref:Xamarin.Forms.Maps.Map) contrôle est restitué par une application Xamarin.Forms, dans iOS le `MapRenderer` classe est instanciée, ce qui instancie à son tour native `MKMapView` contrôle. Sur la plateforme Android, le `MapRenderer` classe instancie native `MapView` contrôle. Sur la plateforme de Windows universelle (UWP), le `MapRenderer` classe instancie native `MapControl`. Le processus de rendu peut être exploitée pour implémenter les personnalisations spécifiques à la plateforme mappage en créant un convertisseur personnalisé pour un `Map` sur chaque plateforme. Le processus pour effectuer cette opération est la suivante :

1. [Créer](#Creating_the_Custom_Map) une carte personnalisée Xamarin.Forms.
1. [Consommer](#Consuming_the_Custom_Map) la carte personnalisée à partir de Xamarin.Forms.
1. [Personnaliser](#Customizing_the_Map) la carte en créant un convertisseur personnalisé pour la carte sur chaque plateforme.

> [!NOTE]
> [`Xamarin.Forms.Maps`](xref:Xamarin.Forms.Maps) doit être initialisé et configuré avant utilisation. Pour plus d’informations, consultez [`Maps Control`](~/xamarin-forms/user-interface/map.md)

Pour plus d’informations sur la personnalisation d’une carte à l’aide d’un convertisseur personnalisé, consultez [personnalisation d’un code confidentiel de carte](~/xamarin-forms/app-fundamentals/custom-renderer/map/customized-pin.md).

<a name="Creating_the_Custom_Map" />

### <a name="creating-the-custom-map"></a>Création de la carte personnalisée

Créer un `CustomCircle` classe a `Position` et `Radius` propriétés :

```csharp
public class CustomCircle
{
  public Position Position { get; set; }
  public double Radius { get; set; }
}
```

Ensuite, créez une sous-classe de la [ `Map` ](xref:Xamarin.Forms.Maps.Map) (classe), qui ajoute une propriété de type `CustomCircle`:

```csharp
public class CustomMap : Map
{
  public CustomCircle Circle { get; set; }
}
```

<a name="Consuming_the_Custom_Map" />

### <a name="consuming-the-custom-map"></a>Utilisation de la carte personnalisée

Consommer le `CustomMap` contrôle en déclarant une instance de celle-ci dans l’instance de la page XAML :

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:MapOverlay;assembly=MapOverlay"
             x:Class="MapOverlay.MapPage">
    <ContentPage.Content>
        <local:CustomMap x:Name="customMap" MapType="Street" WidthRequest="{x:Static local:App.ScreenWidth}" HeightRequest="{x:Static local:App.ScreenHeight}" />
    </ContentPage.Content>
</ContentPage>
```

Vous pouvez également utiliser le `CustomMap` contrôle en déclarant une instance de celle-ci dans l’instance de page c# :

```csharp
public class MapPageCS : ContentPage
{
    public MapPageCS ()
    {
        var customMap = new CustomMap {
            MapType = MapType.Street,
            WidthRequest = App.ScreenWidth,
            HeightRequest = App.ScreenHeight
        };
        ...
        Content = customMap;
    }
}
```

Initialiser le `CustomMap` contrôler en fonction des besoins :

```csharp
public partial class MapPage : ContentPage
{
  public MapPage ()
  {
    ...
    var pin = new Pin {
      Type = PinType.Place,
      Position = new Position (37.79752, -122.40183),
      Label = "Xamarin San Francisco Office",
      Address = "394 Pacific Ave, San Francisco CA"
    };

    var position = new Position (37.79752, -122.40183);
    customMap.Circle = new CustomCircle {
      Position = position,
      Radius = 1000
    };

    customMap.Pins.Add (pin);
    customMap.MoveToRegion (MapSpan.FromCenterAndRadius (position, Distance.FromMiles (1.0)));
  }
}
```

Ajoute cette initialisation [ `Pin` ](xref:Xamarin.Forms.Maps.Pin) et `CustomCircle` les instances à la carte personnalisée et positionne la vue de la carte avec le [ `MoveToRegion` ](xref:Xamarin.Forms.Maps.Map.MoveToRegion*) (méthode), ce qui modifie la position et le zoom niveau de la carte en créant un [ `MapSpan` ](xref:Xamarin.Forms.Maps.MapSpan) à partir d’un [ `Position` ](xref:Xamarin.Forms.Maps.Position) et un [ `Distance` ](xref:Xamarin.Forms.Maps.Distance).

<a name="Customizing_the_Map" />

### <a name="customizing-the-map"></a>Personnalisation de la carte

Un convertisseur personnalisé doit maintenant être ajouté à chaque projet d’application pour ajouter la superposition circulaire au mappage.

#### <a name="creating-the-custom-renderer-on-ios"></a>Création du convertisseur personnalisé sur iOS

Créer une sous-classe de la `MapRenderer` classe et substituer sa `OnElementChanged` méthode pour ajouter la superposition circulaire :

```csharp
[assembly: ExportRenderer(typeof(CustomMap), typeof(CustomMapRenderer))]
namespace MapOverlay.iOS
{
    public class CustomMapRenderer : MapRenderer
    {
        MKCircleRenderer circleRenderer;

        protected override void OnElementChanged(ElementChangedEventArgs<View> e)
        {
            base.OnElementChanged(e);

            if (e.OldElement != null) {
                var nativeMap = Control as MKMapView;
                if (nativeMap != null) {
                    nativeMap.RemoveOverlays(nativeMap.Overlays);
                    nativeMap.OverlayRenderer = null;
                    circleRenderer = null;
                }
            }

            if (e.NewElement != null) {
                var formsMap = (CustomMap)e.NewElement;
                var nativeMap = Control as MKMapView;
                var circle = formsMap.Circle;

                nativeMap.OverlayRenderer = GetOverlayRenderer;

                var circleOverlay = MKCircle.Circle(new CoreLocation.CLLocationCoordinate2D(circle.Position.Latitude, circle.Position.Longitude), circle.Radius);
                nativeMap.AddOverlay(circleOverlay);
            }
        }
        ...
    }
}

```

Cette méthode effectue la configuration suivante, sous réserve que le convertisseur personnalisé est attaché à un nouvel élément Xamarin.Forms :

- Le `MKMapView.OverlayRenderer` propriété est définie sur un délégué correspondant.
- Le cercle est créé en définissant un statique `MKCircle` objet qui spécifie le centre du cercle et le rayon du cercle en mètres.
- Le cercle est ajouté à la carte en appelant le `MKMapView.AddOverlay` (méthode).

Ensuite, implémentez la `GetOverlayRenderer` méthode pour personnaliser le rendu de la superposition :

```csharp
public class CustomMapRenderer : MapRenderer
{
  MKCircleRenderer circleRenderer;
  ...

  MKOverlayRenderer GetOverlayRenderer(MKMapView mapView, IMKOverlay overlayWrapper)
  {
      if (circleRenderer == null && !Equals(overlayWrapper, null)) {
          var overlay = Runtime.GetNSObject(overlayWrapper.Handle) as IMKOverlay;
          circleRenderer = new MKCircleRenderer(overlay as MKCircle) {
              FillColor = UIColor.Red,
              Alpha = 0.4f
          };
      }
      return circleRenderer;
  }
}
```

#### <a name="creating-the-custom-renderer-on-android"></a>Création du convertisseur personnalisé sur Android

Créer une sous-classe de la `MapRenderer` classe et substituer sa `OnElementChanged` et `OnMapReady` méthodes pour ajouter la superposition circulaire :

```csharp
[assembly: ExportRenderer(typeof(CustomMap), typeof(CustomMapRenderer))]
namespace MapOverlay.Droid
{
    public class CustomMapRenderer : MapRenderer
    {
        CustomCircle circle;

        public CustomMapRenderer(Context context) : base(context)
        {
        }

        protected override void OnElementChanged(Xamarin.Forms.Platform.Android.ElementChangedEventArgs<Xamarin.Forms.Maps.Map> e)
        {
            base.OnElementChanged(e);

            if (e.OldElement != null)
            {
                // Unsubscribe
            }

            if (e.NewElement != null)
            {
                var formsMap = (CustomMap)e.NewElement;
                circle = formsMap.Circle;
                Control.GetMapAsync(this);
            }
        }

        protected override void OnMapReady(Android.Gms.Maps.GoogleMap map)
        {
            base.OnMapReady(map);

            var circleOptions = new CircleOptions();
            circleOptions.InvokeCenter(new LatLng(circle.Position.Latitude, circle.Position.Longitude));
            circleOptions.InvokeRadius(circle.Radius);
            circleOptions.InvokeFillColor(0X66FF0000);
            circleOptions.InvokeStrokeColor(0X66FF0000);
            circleOptions.InvokeStrokeWidth(0);

            NativeMap.AddCircle(circleOptions);
        }
    }
}
```

Le `OnElementChanged` les appels de méthode le `MapView.GetMapAsync` (méthode), qui obtient sous-jacent `GoogleMap` qui est lié à la vue, sous réserve que le convertisseur personnalisé est attaché à un nouvel élément Xamarin.Forms. Une fois le `GoogleMap` instance n’est disponible, le `OnMapReady` méthode sera appelée, où le cercle est créé en instanciant un `CircleOptions` objet qui spécifie le centre du cercle et le rayon du cercle en mètres. Le cercle est ensuite ajouté à la carte en appelant le `NativeMap.AddCircle` (méthode).

#### <a name="creating-the-custom-renderer-on-the-universal-windows-platform"></a>Création du convertisseur personnalisé sur la plateforme Windows universelle

Créer une sous-classe de la `MapRenderer` classe et substituer sa `OnElementChanged` méthode pour ajouter la superposition circulaire :

```csharp
[assembly: ExportRenderer(typeof(CustomMap), typeof(CustomMapRenderer))]
namespace MapOverlay.UWP
{
    public class CustomMapRenderer : MapRenderer
    {
        const int EarthRadiusInMeteres = 6371000;

        protected override void OnElementChanged(ElementChangedEventArgs<Map> e)
        {
            base.OnElementChanged(e);

            if (e.OldElement != null)
            {
                // Unsubscribe
            }
            if (e.NewElement != null)
            {
                var formsMap = (CustomMap)e.NewElement;
                var nativeMap = Control as MapControl;
                var circle = formsMap.Circle;

                var coordinates = new List<BasicGeoposition>();
                var positions = GenerateCircleCoordinates(circle.Position, circle.Radius);
                foreach (var position in positions)
                {
                    coordinates.Add(new BasicGeoposition { Latitude = position.Latitude, Longitude = position.Longitude });
                }

                var polygon = new MapPolygon();
                polygon.FillColor = Windows.UI.Color.FromArgb(128, 255, 0, 0);
                polygon.StrokeColor = Windows.UI.Color.FromArgb(128, 255, 0, 0);
                polygon.StrokeThickness = 5;
                polygon.Path = new Geopath(coordinates);
                nativeMap.MapElements.Add(polygon);
            }
        }
        // GenerateCircleCoordinates helper method (below)
    }
}
```

Cette méthode effectue les opérations suivantes, si le convertisseur personnalisé est attaché à un nouvel élément Xamarin.Forms :

- La position du cercle et radius sont récupérés à partir de la `CustomMap.Circle` propriété et passé à la `GenerateCircleCoordinates` (méthode), qui génère la latitude et longitude coordonnées pour le périmètre du cercle. Vous trouverez ci-dessous le code de cette méthode d’assistance.
- Les coordonnées de périmètre du cercle sont converties en un `List` de `BasicGeoposition` coordonnées.
- Le cercle est créé en instanciant un `MapPolygon` objet. Le `MapPolygon` classe est utilisée pour afficher une forme multipoint sur la carte en définissant son `Path` propriété un `Geopath` objet qui contient les coordonnées de la forme.
- Le polygone est rendu sur la carte en l’ajoutant à la `MapControl.MapElements` collection.


```
List<Position> GenerateCircleCoordinates(Position position, double radius)
{
    double latitude = position.Latitude.ToRadians();
    double longitude = position.Longitude.ToRadians();
    double distance = radius / EarthRadiusInMeteres;
    var positions = new List<Position>();

    for (int angle = 0; angle <=360; angle++)
    {
        double angleInRadians = ((double)angle).ToRadians();
        double latitudeInRadians = Math.Asin(Math.Sin(latitude) * Math.Cos(distance) + Math.Cos(latitude) * Math.Sin(distance) * Math.Cos(angleInRadians));
        double longitudeInRadians = longitude + Math.Atan2(Math.Sin(angleInRadians) * Math.Sin(distance) * Math.Cos(latitude), Math.Cos(distance) - Math.Sin(latitude) * Math.Sin(latitudeInRadians));

        var pos = new Position(latitudeInRadians.ToDegrees(), longitudeInRadians.ToDegrees());
        positions.Add(pos);
    }

    return positions;
}
```

## <a name="summary"></a>Récapitulatif

Cet article a expliqué comment ajouter un segment de recouvrement circulaire à un mappage, pour mettre en surbrillance une zone circulaire de la carte.


## <a name="related-links"></a>Liens associés

- [Ovlerlay carte circulaire (exemple)](https://developer.xamarin.com/samples/xamarin-forms/customrenderers/map/circle/)
- [Personnalisation d’une épingle de carte](~/xamarin-forms/app-fundamentals/custom-renderer/map/customized-pin.md)
- [Xamarin.Forms.Maps](xref:Xamarin.Forms.Maps)
