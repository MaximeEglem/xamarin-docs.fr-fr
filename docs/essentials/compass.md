---
title: 'Xamarin.Essentials : boussole'
description: Ce document décrit la classe Compass dans Xamarin.Essentials, ce qui vous permet d’analyser le titre du Nord magnétique.
ms.assetid: BF85B0C3-C686-43D9-811A-07DCAF8CDD86
author: jamesmontemagno
ms.author: jamont
ms.date: 05/04/2018
ms.openlocfilehash: 63818014a9b3bdbef479055cbbcfbf8d348080fc
ms.sourcegitcommit: 72450a6a29599fa133ff4f16fb0b1f443d89f9dc
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37080459"
---
# <a name="xamarinessentials-compass"></a>Xamarin.Essentials : boussole

![Version préliminaire de NuGet](~/media/shared/pre-release.png)

Le **boussole** classe vous permet d’analyser le titre du Nord magnétique.

## <a name="using-compass"></a>À l’aide de boussole

Ajoutez une référence à Xamarin.Essentials dans votre classe :

```csharp
using Xamarin.Essentials;
```

La fonctionnalité de boussole fonctionne en appelant le `Start` et `Stop` méthodes pour écouter les modifications apportées à la boussole. Toutes les modifications sont envoyées par le biais de la `ReadingChanged` événement. Voici un exemple :

```csharp
public class CompassTest
{
    // Set speed delay for monitoring changes.
    SensorSpeed speed = SensorSpeed.Ui;

    public CompassTest()
    {
        // Register for reading changes, be sure to unsubscribe when finished
        Compass.ReadingChanged += Compass_ReadingChanged;
    }

    void Compass_ReadingChanged(CompassChangedEventArgs e)
    {
        var data = e.Reading;
        Console.WriteLine($"Reading: {data.HeadingMagneticNorth} degrees");
        // Process Heading Magnetic North
    }

    public void ToggleCompass()
    {
        try
        {
            if (Compass.IsMonitoring)
              Compass.Stop();
            else
              Compass.Start(speed);
        }
        catch (FeatureNotSupportedException fnsEx)
        {
            // Feature not supported on device
        }
        catch (Exception ex)
        {
            // Some other exception has occured
        }
    }
}
```

## <a name="sensor-speedxrefxamarinessentialssensorspeed"></a>[Vitesse de capteur.](xref:Xamarin.Essentials.SensorSpeed)

- **Plus rapide** : obtenir les données de capteur aussi rapidement que possible (ne pas retourne toujours sur le thread d’interface utilisateur).
- **Jeu** – taux approprié pour les jeux (ne pas retourne toujours sur le thread d’interface utilisateur).
- **Normal** – taux par défaut approprié pour les modifications d’orientation de l’écran.
- **L’interface utilisateur** – taux approprié pour l’interface utilisateur générale.

Si votre gestionnaire d’événements n’est pas garanti pour s’exécuter sur le thread d’interface utilisateur et si le Gestionnaire d’événements doit accéder aux éléments d’interface utilisateur, utilisez la [ `MainThread.BeginInvokeOnMainThread` ](main-thread.md) méthode à exécuter ce code sur le thread d’interface utilisateur.

## <a name="platform-implementation-specifics"></a>Caractéristiques d’implémentation de plate-forme

# <a name="androidtabandroid"></a>[Android](#tab/android)

Android ne fournit pas d’une API pour la récupération de l’en-tête boussole. Nous allons utiliser l’accéléromètre et magnétomètre pour calculer l’en-tête Nord magnétique, ce qui est recommandé par Google. 

Dans de rares cas, vous peut-être voir des résultats incohérents, car les capteurs besoin d’être étalonné, ce qui implique le déplacement de votre appareil dans un mouvement figure-8. La meilleure façon de faire cela doit ouvrir des cartes de Google, cliquez sur le point de votre emplacement, puis sélectionnez **étalonner boussole**.

Sachez qui exécutent plusieurs capteurs à partir de votre application en même temps peut ajuster la vitesse de capteur.

--------------

## <a name="api"></a>API

- [Code source boussole](https://github.com/xamarin/Essentials/tree/master/Xamarin.Essentials/Compass)
- [Documentation de l’API boussole](xref:Xamarin.Essentials.Compass)
