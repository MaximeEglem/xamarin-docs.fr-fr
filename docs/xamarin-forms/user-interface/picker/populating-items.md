---
title: Ajout de données à la Collection d’éléments d’un sélecteur
description: La vue de sélecteur est un contrôle pour la sélection d’un élément de texte à partir d’une liste de données. Cet article explique comment remplir un sélecteur de données en l’ajoutant à la collection d’éléments et comment répondre à la sélection d’éléments par l’utilisateur.
ms.prod: xamarin
ms.assetid: 3C840F64-A430-457D-A4B2-3D7AF46F9DBE
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 04/11/2017
ms.openlocfilehash: 8d911108d7d72586a37a3281803eab9c0841f16c
ms.sourcegitcommit: 6e955f6851794d58334d41f7a550d93a47e834d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38997106"
---
# <a name="adding-data-to-a-pickers-items-collection"></a>Ajout de données à la Collection d’éléments d’un sélecteur

_La vue de sélecteur est un contrôle pour la sélection d’un élément de texte à partir d’une liste de données. Cet article explique comment remplir un sélecteur de données en l’ajoutant à la collection d’éléments et comment répondre à la sélection d’éléments par l’utilisateur._

## <a name="populating-a-picker-with-data"></a>Remplissage d’un sélecteur de données

Avant de Xamarin.Forms 2.3.4, le processus pour remplir un [ `Picker` ](xref:Xamarin.Forms.Picker) avec données consistait à ajouter les données à afficher en lecture seule [ `Items` ](xref:Xamarin.Forms.Picker.Items) collection, ce qui est de type `IList<string>`. Chaque élément dans la collection doit être de type `string`. Éléments peuvent être ajoutés dans XAML en initialisant le `Items` propriété avec une liste de `x:String` éléments :

```xaml
<Picker Title="Select a monkey">
  <Picker.Items>
    <x:String>Baboon</x:String>
    <x:String>Capuchin Monkey</x:String>
    <x:String>Blue Monkey</x:String>
    <x:String>Squirrel Monkey</x:String>
    <x:String>Golden Lion Tamarin</x:String>
    <x:String>Howler Monkey</x:String>
    <x:String>Japanese Macaque</x:String>
  </Picker.Items>
</Picker>
```

Le code c# équivalent est indiqué ci-dessous :

```csharp
var picker = new Picker { Title = "Select a monkey" };
picker.Items.Add("Baboon");
picker.Items.Add("Capuchin Monkey");
picker.Items.Add("Blue Monkey");
picker.Items.Add("Squirrel Monkey");
picker.Items.Add("Golden Lion Tamarin");
picker.Items.Add("Howler Monkey");
picker.Items.Add("Japanese Macaque");
```

Outre l’ajout de données à l’aide du `Items.Add` (méthode), données peuvent également être insérées dans la collection à l’aide de la `Items.Insert` (méthode).

## <a name="responding-to-item-selection"></a>Réponse à la sélection de l’élément

Un [ `Picker` ](xref:Xamarin.Forms.Picker) prend en charge la sélection d’un élément à la fois. Lorsqu’un utilisateur sélectionne un élément, le [ `SelectedIndexChanged` ](xref:Xamarin.Forms.Picker.SelectedIndexChanged) se déclenche des événements et le [ `SelectedIndex` ](xref:Xamarin.Forms.Picker.SelectedIndex) propriété est mise à jour vers un entier représentant l’index de l’élément sélectionné dans la liste. Le `SelectedIndex` propriété est un numéro de base zéro indiquant l’élément sélectionné par l’utilisateur. Si aucun élément n’est sélectionné, ce qui est le cas lorsque le `Picker` est tout d’abord créé et initialisé, `SelectedIndex` sera -1.

> [!NOTE]
> Élément de comportement de sélection dans un [ `Picker` ](xref:Xamarin.Forms.Picker) peuvent être personnalisés sur iOS avec un spécifique à la plateforme. Pour plus d’informations, consultez [sélection d’éléments de contrôle de sélecteur de](~/xamarin-forms/platform/platform-specifics/consuming/ios.md#picker_update_mode).

Le code suivant montre l’exemple le `OnPickerSelectedIndexChanged` méthode de gestionnaire d’événements qui est exécutée lorsque la [ `SelectedIndexChanged` ](xref:Xamarin.Forms.Picker.SelectedIndexChanged) se déclenche des événements :

```csharp
void OnPickerSelectedIndexChanged(object sender, EventArgs e)
{
  var picker = (Picker)sender;
  int selectedIndex = picker.SelectedIndex;

  if (selectedIndex != -1)
  {
    monkeyNameLabel.Text = picker.Items[selectedIndex];
  }
}
```

Cette méthode obtient le [ `SelectedIndex` ](xref:Xamarin.Forms.Picker.SelectedIndex) valeur de propriété et utilise la valeur pour récupérer l’élément sélectionné à partir de la [ `Items` ](xref:Xamarin.Forms.Picker.Items) collection. Étant donné que chaque élément de la `Items` collection est un `string`, ils peuvent être affichés en un [ `Label` ](xref:Xamarin.Forms.Label) sans nécessiter un cast.

> [!NOTE]
> Un [ `Picker` ](xref:Xamarin.Forms.Picker) puisse être initialisé pour afficher un élément spécifique en définissant le [ `SelectedIndex` ](xref:Xamarin.Forms.Picker.SelectedIndex) propriété. Toutefois, le `SelectedIndex` propriété doit être définie après l’initialisation de la [ `Items` ](xref:Xamarin.Forms.Picker.Items) collection.

## <a name="summary"></a>Récapitulatif

Le [ `Picker` ](xref:Xamarin.Forms.Picker) vue est un contrôle pour la sélection d’un élément de texte à partir d’une liste de données. Cet article a expliqué comment remplir un `Picker` avec des données en l’ajoutant à la [ `Items` ](xref:Xamarin.Forms.Picker.Items) collection et comment répondre à la sélection d’éléments par l’utilisateur. C’était le processus permettant d’utiliser un `Picker` avant Xamarin.Forms 2.3.4.


## <a name="related-links"></a>Liens associés

- [Démonstration de sélecteur (exemple)](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/PickerDemo/)
- [Picker](xref:Xamarin.Forms.Picker)
