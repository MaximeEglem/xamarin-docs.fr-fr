---
title: 'Xamarin.Essentials : accéléromètre'
description: La classe Accelerometer dans Xamarin.Essentials vous permet de surveiller le capteur de l’accéléromètre de l’appareil, qui indique l’accélération de l’appareil dans un espace tridimensionnel.
ms.assetid: 97883573-F0D9-4854-AC7C-A654814401C5
author: jamesmontemagno
ms.author: jamont
ms.date: 05/04/2018
ms.openlocfilehash: 53e7ca70184270662d27043387da836ad44432fe
ms.sourcegitcommit: 47709db4d115d221e97f18bc8111c95723f6cb9b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/13/2018
ms.locfileid: "40184426"
---
# <a name="xamarinessentials-accelerometer"></a>Xamarin.Essentials : accéléromètre

![Préversion NuGet](~/media/shared/pre-release.png)

La classe **Accelerometer** vous permet de surveiller le capteur de l’accéléromètre de l’appareil, qui indique l’accélération de l’appareil dans un espace tridimensionnel.

## <a name="using-accelerometer"></a>Utilisation de l’accéléromètre

Ajoutez une référence à Xamarin.Essentials dans votre classe :

```csharp
using Xamarin.Essentials;
```

La fonctionnalité de l’accéléromètre fonctionne en appelant les méthodes `Start` et `Stop` qui permettent d’écouter les changements d’accélération. Tous les changements sont renvoyés via l’événement `ReadingChanged`. Voici un exemple d’utilisation :

```csharp

public class AccelerometerTest
{
    // Set speed delay for monitoring changes.
    SensorSpeed speed = SensorSpeed.UI;

    public AccelerometerTest()
    {
        // Register for reading changes, be sure to unsubscribe when finished
        Accelerometer.ReadingChanged += Accelerometer_ReadingChanged;
    }

    void Accelerometer_ReadingChanged(object sender, AccelerometerChangedEventArgs e)
    {
        var data = e.Reading;
        Console.WriteLine($"Reading: X: {data.Acceleration.X}, Y: {data.Acceleration.Y}, Z: {data.Acceleration.Z}");
        // Process Acceleration X, Y, and Z
    }

    public void ToggleAccelerometer()
    {
        try
        {
            if (Accelerometer.IsMonitoring)
              Accelerometer.Stop();
            else
              Accelerometer.Start(speed);
        }
        catch (FeatureNotSupportedException fnsEx)
        {
            // Feature not supported on device
        }
        catch (Exception ex)
        {
            // Other error has occurred.
        }
    }
}
```

Les lectures de l’accéléromètre sont retournées en G. G est une unité de force gravitationnelle égale à celle exercée par le champ gravitationnelle de la Terre (9,81 m/s^2).

Le système de coordonnées est défini par rapport à l’écran du téléphone dans son orientation par défaut. Les axes ne sont pas intervertis quand l’orientation de l’écran de l’appareil change.

L’axe des X est horizontal et pointe vers la droite, l’axe des Y est vertical et pointe vers le haut et l’axe Z pointe vers l’extérieur de la face avant de l’écran. Dans ce système, les coordonnées derrière l’écran ont des valeurs Z négatives.

Exemples :

* Lorsque l’appareil est à plat sur une table et est poussé par son côté gauche vers la droite, la valeur d’accélération x est un nombre positive.

* Lorsque l’appareil est à plat sur une table, la valeur de l’accélération est +1.00 G ou (+9,81 m/s^2), qui correspond à l’accélération de l’appareil (0 m/s^2) moins la force de gravité (-9,81 m/s^2) et standardisée en G.

* Lorsque l’appareil est à plat sur une table et est poussé vers le ciel avec une accélération de A m/s^2, la valeur d’accélération est égale à A+9,81, qui correspond à l’accélération de l’appareil (+A m/s^2) moins la force de gravité (-9,81 m/s^2) et standardisée en G.

[!include[](~/essentials/includes/sensor-speed.md)]

## <a name="api"></a>API

- [Code source de l’accéléromètre](https://github.com/xamarin/Essentials/tree/master/Xamarin.Essentials/Accelerometer)
- [Documentation de l’API Accéléromètre](xref:Xamarin.Essentials.Accelerometer)
