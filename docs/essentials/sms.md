---
title: 'Xamarin.Essentials : SMS'
description: La classe Sms dans Xamarin.Essentials permet à une application ouvrir l’application de SMS par défaut avec un message à envoyer à un destinataire spécifié.
ms.assetid: 81A757F2-6F2A-458F-B9BE-770ADEBFAB58
author: jamesmontemagno
ms.author: jamont
ms.date: 05/04/2018
ms.openlocfilehash: a93a67b83ea8f435a5e3ad5d26e1d6cbbb7092f7
ms.sourcegitcommit: 632955f8cdb80712abd8dcc30e046cb9c435b922
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38815595"
---
# <a name="xamarinessentials-sms"></a>Xamarin.Essentials : SMS

![Version préliminaire NuGet](~/media/shared/pre-release.png)

Le **Sms** classe permet à une application ouvrir l’application de SMS par défaut avec un message à envoyer à un destinataire spécifié.

## <a name="using-sms"></a>À l’aide de Sms

Ajoutez une référence à Xamarin.Essentials dans votre classe :

```csharp
using Xamarin.Essentials;
```

La fonctionnalité SMS fonctionne en appelant le `ComposeAsync` méthode un `SmsMessage` qui contient le destinataire et le corps du message, qui sont tous deux facultatifs.

```csharp
public class SmsTest
{
    public async Task SendSms(string messageText, string recipient)
    {
        try
        {
            var message = new SmsMessage(messageText, recipient);
            await Sms.ComposeAsync(message);
        }
        catch (FeatureNotSupportedException ex)
        {
            // Sms is not supported on this device.
        }
        catch (Exception ex)
        {
            // Other error has occurred.
        }
    }
}
```

## <a name="api"></a>API

- [Code source de SMS](https://github.com/xamarin/Essentials/tree/master/Xamarin.Essentials/Sms)
- [Documentation de l’API de SMS](xref:Xamarin.Essentials.Sms)
