---
title: Xamarin.Mac – Documentation connexe
description: 'Ce document fournit des liens vers de la documentation pertinente pour les développeurs Xamarin.Mac : documentation Xamarin.iOS, Centre de développement Mac d’Apple et divers guides pas à pas qui décrivent comment générer des interfaces utilisateur avec Xamarin.Mac.'
ms.prod: xamarin
ms.assetid: 0a282c58-1c37-4f73-8440-85de2daf454a
ms.technology: xamarin-mac
author: bradumbaugh
ms.author: brumbaug
ms.date: 12/02/2016
ms.openlocfilehash: 1bef756d89a92d082bd5ee29e18047bc4bed2498
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34792526"
---
# <a name="xamarinmac--related-documentation"></a>Xamarin.Mac – Documentation connexe

En plus de la section Mac de [developer.xamarin.com](~/mac/get-started/index.md) il existe trois sources de documentation intéressantes qui peuvent également s’avérer utiles sur les questions liées à Xamarin.Mac :

- [**Documentation Xamarin.iOS**](~/ios/get-started/index.md) : Pour de nombreuses API (principalement en dehors d’AppKit/UIKit), il n’existe que des différences minimes entre les versions iOS et macOS. Dans certains cas où une API iOS donnée porte le nom `UIFoo`, une API similaire nommée `NSFoo` se trouve sur macOS. Ces exemples figurent généralement déjà dans C#.

- **[Mac Dev Center](https://developer.apple.com/devcenter/mac/) d’Apple** : Très souvent, un exemple des API à appeler en Objective-C peut être directement converti en C#. Pour plus d’informations sur la procédure à suivre, consultez [Présentation des API Mac](~/mac/app-fundamentals/mac-apis.md).

- [**Dépassement de capacité de la pile**](http://stackoverflow.com/) : Ressource idéale pour des questions simples et isolées telles que [« Comment développer automatiquement tous les nœuds dans un NSOutlineView »](http://stackoverflow.com/questions/519751/nsoutlineview-auto-expand-all-nodes). Ces exemples figurent souvent dans Objective-C et doivent être convertis en C#, mais il existe un sous-ensemble de réponses dans C#.

## <a name="user-interface"></a>Interface utilisateur

Quand il utilise C# et .NET dans une application Xamarin.Mac, le développeur a accès aux mêmes contrôles d’interface utilisateur qu’un développeur travaillant dans *Objective-C* et *Xcode*. Comme Xamarin.Mac s’intègre directement à Xcode, le développeur peut utiliser _Interface Builder_ de Xcode pour créer et gérer les interfaces utilisateur d’une application (ou éventuellement pour les créer directement en code C#).

Les guides ci-dessous donnent des informations détaillées sur l’utilisation des éléments macOS dans une application Xamarin.Mac :

- [Fenêtres](~/mac/user-interface/window.md)
- [Boîtes de dialogue](~/mac/user-interface/dialog.md)
- [Alertes](~/mac/user-interface/alert.md)
- [Menus](~/mac/user-interface/menu.md)
- [Barres d’outils](~/mac/user-interface/toolbar.md)
- [Vues Table](~/mac/user-interface/table-view.md)
- [Modes Plan](~/mac/user-interface/outline-view.md)
- [Listes de sources](~/mac/user-interface/source-list.md)
