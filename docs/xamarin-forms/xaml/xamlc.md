---
title: Compilation XAML dans Xamarin.Forms
description: Cet article explique comment XAML peut être éventuellement compilé directement en langage intermédiaire (IL) avec le compilateur XAML de Xamarin.Forms (XAMLC).
ms.prod: xamarin
ms.assetid: 9A2D10A6-5DFC-485F-A75A-2F7B98314025
ms.technology: xamarin-forms
author: charlespetzold
ms.author: chape
ms.date: 07/02/2018
ms.openlocfilehash: b828e62ef1037bf47a2ae5fb303fbf8fcace6549
ms.sourcegitcommit: 6e955f6851794d58334d41f7a550d93a47e834d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38997131"
---
# <a name="xaml-compilation-in-xamarinforms"></a>Compilation XAML dans Xamarin.Forms

_XAML peut être éventuellement compilé directement en langage intermédiaire (IL) avec le compilateur XAML (XAMLC)._

XAMLC offre un certain nombre d’avantages :

- Il effectue une vérification au moment de la compilation du code XAML et informe l’utilisateur des erreurs rencontrées.
- Il supprime une partie du temps de chargement et d’instanciation pour les éléments XAML.
- Il permet de réduire la taille de fichier de l’assembly final en n’incluant plus les fichiers .xaml.

XAMLC est désactivé par défaut pour assurer la compatibilité descendante. Il peut être activé au niveau de l’assembly et la classe en ajoutant le `XamlCompilation` attribut.

L’exemple de code suivant illustre l’activation de XAMLC au niveau de l’assembly :

```csharp
using Xamarin.Forms.Xaml;
...
[assembly: XamlCompilation (XamlCompilationOptions.Compile)]
namespace PhotoApp
{
  ...
}
```

Dans cet exemple, la vérification de tous les XAML contenue dans l’assembly lors de la compilation se fera, avec des erreurs XAML signalés au moment de la compilation plutôt que d’exécution. Par conséquent, le `assembly` de préfixe pour le `XamlCompilation` attribut spécifie que l’attribut s’applique à la totalité de l’assembly.

L’exemple de code suivant illustre l’activation de XAMLC au niveau de la classe :

```csharp
using Xamarin.Forms.Xaml;
...
[XamlCompilation (XamlCompilationOptions.Compile)]
public class HomePage : ContentPage
{
  ...
}
```

Dans cet exemple, lors de la compilation la vérification de le XAML pour la `HomePage` classe sera effectuée et erreurs signalés comme faisant partie du processus de compilation.

> [!NOTE]
> Le `XamlCompilation` attribut et la `XamlCompilationOptions` énumération se trouvent dans le `Xamarin.Forms.Xaml` espace de noms, qui doit être importé à les utiliser.


## <a name="related-links"></a>Liens associés

- [XamlCompilation](xref:Xamarin.Forms.Xaml.XamlCompilationAttribute)
- [XamlCompilationOptions](xref:Xamarin.Forms.Xaml.XamlCompilationOptions)
