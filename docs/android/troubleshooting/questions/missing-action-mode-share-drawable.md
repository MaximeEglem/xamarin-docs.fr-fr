---
title: "Android.Support.v7.AppCompat - aucune ressource trouvée qui correspond au nom donné : attr 'android : actionModeShareDrawable'"
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: 5814069C-FC43-41DE-B5A5-024D05E59929
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 03/09/2018
ms.openlocfilehash: 07655587642c3e1aa94d035e76f6f6758340546d
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/04/2018
ms.locfileid: "30774894"
---
# <a name="androidsupportv7appcompat---no-resource-found-that-matches-the-given-name-attr-androidactionmodesharedrawable"></a>Android.Support.v7.AppCompat - aucune ressource trouvée qui correspond au nom donné : attr 'android : actionModeShareDrawable'

1. Assurez-vous que vous téléchargez extras plus récente, ainsi que le Android 5.0 (API 21) SDK via le Gestionnaire de kit de développement logiciel Android.

2. Assurez-vous que vous compilez votre application avec compileSdkVersion définie sur 21. Vous pouvez éventuellement définir la targetSdkVersion 21 ainsi.

3. Si vous avez besoin d’une version antérieure, telles que les API 19, téléchargez la version respective figure dans la page Nuget :

[https://www.nuget.org/packages/Xamarin.Android.Support.v7.AppCompat/](https://www.nuget.org/packages/Xamarin.Android.Support.v7.AppCompat/)

*Remarque*: Si vous installez manuellement ce via la Console du Gestionnaire de Package, assurez-vous que vous installez également la même version de Xamarin.Android.Support.v4

[https://www.nuget.org/packages/Xamarin.Android.Support.v4/](https://www.nuget.org/packages/Xamarin.Android.Support.v4/)

Référence de dépassement de capacité de pile : [http://stackoverflow.com/questions/26431676/appcompat-v721-0-0-no-resource-found-that-matches-the-given-name-attr-andro](http://stackoverflow.com/questions/26431676/appcompat-v721-0-0-no-resource-found-that-matches-the-given-name-attr-andro)

## <a name="see-also"></a>Voir aussi

- [Quels packages Android SDK dois-je installer ?](~/android/troubleshooting/questions/install-android-sdk-packages.md)

