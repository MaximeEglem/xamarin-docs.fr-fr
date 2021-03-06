---
title: Résumé du chapitre 2. Anatomie d’une application
description: 'Création d’applications mobiles avec Xamarin.Forms : résumé du chapitre 2. Anatomie d’une application'
ms.prod: xamarin
ms.technology: xamarin-forms
ms.assetid: 8764EB7D-8331-4CF7-9BE1-26D0DEE9E0BB
author: charlespetzold
ms.author: chape
ms.date: 07/17/2018
ms.openlocfilehash: fe6a8c3d17cf1fe6f489f6425bbdaa3cd30f390a
ms.sourcegitcommit: 8555a4dd1a579b2206f86c867125ee20fbc3d264
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39156678"
---
# <a name="summary-of-chapter-2-anatomy-of-an-app"></a>Résumé du chapitre 2. Anatomie d’une application

> [!NOTE] 
> Notes sur cette page indiquent des zones où Xamarin.Forms est différente de la matière présentée dans le livre.

Dans une application Xamarin.Forms, les objets qui occupent l’espace sur l’écran sont appelés *éléments visuels*, il est encapsulé par le [ `VisualElement` ](xref:Xamarin.Forms.VisualElement) classe. Éléments visuels peuvent être divisées en trois catégories correspondant à ces classes :

- [Page](xref:Xamarin.Forms.Page)
- [Disposition](xref:Xamarin.Forms.Layout)
- [Affichage](xref:Xamarin.Forms.View)

Un `Page` dérivé occupe tout l’écran, ou presque tout l’écran. Souvent, l’enfant d’une page est un `Layout` dérivé pour organiser les éléments visuels enfants. Les enfants de la `Layout` peut être autre `Layout` classes ou `View` dérivés (souvent appelé *éléments*), qui sont des objets familiers tels que le texte, images bitmap, curseurs, boutons, zones de liste et ainsi de suite.

Ce chapitre montre comment créer une application en se concentrant sur la [ `Label` ](xref:Xamarin.Forms.Label), qui est le `View` dérivée qui affiche du texte.

## <a name="say-hello"></a>Saluez

Sur la plateforme Xamarin est installée, vous pouvez créer une solution Xamarin.Forms dans Visual Studio ou Visual Studio pour Mac. Le [ **Hello** ](https://github.com/xamarin/xamarin-forms-book-samples/tree/master/Chapter02/Hello) solution utilise une bibliothèque de classes Portable pour le code commun. 

> [!NOTE] 
> Bibliothèques de classes portables ont été remplacés par des bibliothèques .NET Standard. Exemples de code à partir de l’ouvrage a été converti pour utiliser les bibliothèques .NET standard.

Cet exemple montre une solution Xamarin.Forms créée dans Visual Studio sans aucune modification. La solution se compose de six projets :

- [**Hello**](https://github.com/xamarin/xamarin-forms-book-samples/tree/master/Chapter02/Hello/Hello/Hello), une bibliothèque de classes Portable (PCL) partagés par les autres projets
- [**Hello.Droid**](https://github.com/xamarin/xamarin-forms-book-samples/tree/master/Chapter02/Hello/Hello/Hello.Droid), un projet d’application pour Android
- [**Hello.iOS**](https://github.com/xamarin/xamarin-forms-book-samples/tree/master/Chapter02/Hello/Hello/Hello.iOS), un projet d’application pour iOS
- [**Hello.UWP**](https://github.com/xamarin/xamarin-forms-book-samples/tree/master/Chapter02/Hello/Hello/Hello.UWP), un projet d’application pour la plateforme Windows universelle (Windows 10 et Windows 10 Mobile)
- [**Hello.Windows**](https://github.com/xamarin/xamarin-forms-book-samples/tree/master/Chapter02/Hello/Hello/Hello.Windows), un projet d’application pour Windows 8.1
- [**Hello.WinPhone**](https://github.com/xamarin/xamarin-forms-book-samples/tree/master/Chapter02/Hello/Hello/Hello.WinPhone), un projet d’application pour Windows Phone 8.1

> [!NOTE] 
> Xamarin.Forms ne gère plus de Windows 8.1, Windows Phone 8.1 ou Windows 10 Mobile, mais les applications Xamarin.Forms s’exécutent sur le bureau Windows 10. 

Vous pouvez apporter l’une de ces projets d’application du projet de démarrage, puis générer et exécuter le programme sur un appareil ou un simulateur.

Dans la plupart de vos programmes de Xamarin.Forms, vous ne modifient les projets d’application. Souvent, ils restent minuscules stubs simplement pour lancer le programme. La majeure partie de votre objectif sera de la bibliothèque commune à toutes les applications.

## <a name="inside-the-files"></a>Dans les fichiers

Les éléments visuels affichés par le **Hello** programme sont définis dans le constructeur de la [ `App` ](https://github.com/xamarin/xamarin-forms-book-samples/blob/master/Chapter02/Hello/Hello/Hello/App.cs) classe. `App` dérive de la classe Xamarin.Forms [ `Application` ](xref:Xamarin.Forms.Application).

> [!NOTE] 
> Les modèles de solution Visual Studio pour Xamarin.Forms créent une page avec un fichier XAML. XAML n’est pas abordé dans cet ouvrage jusqu'à [chapitre 7](chapter07.md).

Le **références** section de la **Hello** projet PCL inclut les assemblys Xamarin.Forms suivants :

- **Xamarin.Forms.Core**
- **Xamarin.Forms.Xaml**
- **Xamarin.Forms.Platform**

Le **références** sections des projets de cinq application incluent des assemblys supplémentaires qui s’appliquent à chaque plate-forme :

- **Xamarin.Forms.Platform.Android**
- **Xamarin.Forms.Platform.iOS**
- **Xamarin.Forms.Platform.UWP**
- **Xamarin.Forms.Platform.WinRT**
- **Xamarin.Forms.Platform.WinRT.Tablet**
- **Xamarin.Forms.Platform.WinRT.Phone**

> [!NOTE] 
> Le **références** sections de ces projets répertorient ne sont plus les assemblys. Au lieu de cela, le fichier projet contient un **PackageReference** étiquettes référençant le package Xamarin.Forms NuGet. Le **références** section dans les listes de Visual Studio le **Xamarin.Forms** package plutôt que les assemblys Xamarin.Forms. 

Chacun des projets d’application contient un appel à la méthode statique `Forms.Init` méthode dans le `Xamarin.Forms` espace de noms. Ce code initialise la bibliothèque Xamarin.Forms. Une version différente de `Forms.Init` est défini pour chaque plateforme. Vous trouverez les appels à cette méthode dans les classes suivantes :

- iOS : [`AppDelegate`](https://github.com/xamarin/xamarin-forms-book-samples/blob/master/Chapter02/Hello/Hello/Hello.iOS/AppDelegate.cs)
- Android : [`MainActivity`](https://github.com/xamarin/xamarin-forms-book-samples/blob/master/Chapter02/Hello/Hello/Hello.Droid/MainActivity.cs)
- UWP : [ `App` (classe), `OnLaunched` (méthode)](https://github.com/xamarin/xamarin-forms-book-samples/blob/master/Chapter02/Hello/Hello/Hello.Droid/MainActivity.cs)

En outre, chaque plateforme doit instancier la `App` classe emplacement dans la bibliothèque partagée. Cela se produit dans un appel à `LoadApplication` dans les classes suivantes :

- iOS : [`AppDelegate`](https://github.com/xamarin/xamarin-forms-book-samples/blob/master/Chapter02/Hello/Hello/Hello.iOS/AppDelegate.cs)
- Android : [`MainActivity`](https://github.com/xamarin/xamarin-forms-book-samples/blob/master/Chapter02/Hello/Hello/Hello.Droid/MainActivity.cs)
- UWP : [`MainPage`](https://github.com/xamarin/xamarin-forms-book-samples/blob/master/Chapter02/Hello/Hello/Hello.UWP/MainPage.xaml.cs)

Sinon, ces projets d’application sont des programmes de « ne rien faire » normal.

## <a name="pcl-or-sap"></a>Bibliothèque de classes portable ou SAP ?

Il est possible de créer une solution Xamarin.Forms avec le code commun dans une bibliothèque de classes Portable (PCL) ou un projet de ressource partagé (SAP). Pour créer une solution SAP, sélectionnez l’option partagé dans Visual Studio. Le [ **HelloSap** ](https://github.com/xamarin/xamarin-forms-book-samples/tree/master/Chapter02/HelloSap) solution montre le modèle SAP sans aucune modification.

> [!NOTE] 
> Bibliothèques de classes portables a été remplacée par des bibliothèques .NET Standard. Exemples de code à partir de l’ouvrage a été converti pour utiliser les bibliothèques .NET standard. Sinon, les bibliothèques .NET Standard et de bibliothèque de classes portable sont conceptuellement très similaires.

Les regroupements d’approche de bibliothèque tous les courantes de code dans un projet de bibliothèque référencé par les projets d’application de plateforme. Avec l’approche SAP, le code commun existe dans tous les projets d’application de plateforme efficacement et est partagé entre eux.

La plupart des développeurs Xamarin.Forms préfère l’approche de la bibliothèque. Dans cet ouvrage, la plupart des solutions utilisent une bibliothèque. Ceux qui utilisent SAP incluent un **Sap** suffixe du nom de projet.

L’approche SAP le code dans le projet partagé permet d’exécuter un code différent pour les différentes plateformes à l’aide de directives de préprocesseur c# (`#if`, #`elif`, et `#endif`) avec ces prédéfinis des identificateurs :

- iOS : `__IOS__`
- Android : `__ANDROID__`
- UWP : `WINDOWS_UWP`

Dans une bibliothèque partagée, vous pouvez déterminer la plateforme que vous exécutez lors de l’exécution, comme vous le verrez plus loin dans ce chapitre.

## <a name="labels-for-text"></a>Étiquettes de texte

Le [ **Greetings** ](https://github.com/xamarin/xamarin-forms-book-samples/tree/master/Chapter02/Greetings) solution montre comment ajouter un nouveau fichier c# à la **Greetings** projet. Ce fichier définit une classe nommée `GreetingsPage` qui dérive de `ContentPage`. Dans cet ouvrage, la plupart des projets contiennent une seule `ContentPage` dérivé dont le nom est le nom du projet avec le suffixe `Page` ajouté.

Le `GreetingsPage` constructeur instancie un [ `Label` ](xref:Xamarin.Forms.Label) vue, qui est la vue Xamarin.Forms qui affiche du texte. Le [ `Text` ](xref:Xamarin.Forms.Label.Text) propriété est définie sur le texte affiché par le `Label`. Ce programme définit la `Label` à la `Content` propriété du `ContentPage`. Le constructeur de la `App` classe instancie ensuite `GreetingsPage` et lui affecte son `MainPage` propriété.

Le texte est affiché dans le coin supérieur gauche de la page. Sur iOS, cela signifie qu’il chevauche barre d’état de la page. Il existe plusieurs solutions à ce problème :

### <a name="solution-1-include-padding-on-the-page"></a>Solution 1. Inclure la marge intérieure dans la page

Définir un [ `Padding` ](xref:Xamarin.Forms.Page.Padding) propriété sur la page. `Padding` est de type [ `Thickness` ](xref:Xamarin.Forms.Thickness), une structure avec quatre propriétés :

- [`Left`](xref:Xamarin.Forms.Thickness.Left)
- [`Top`](xref:Xamarin.Forms.Thickness.Top)
- [`Right`](xref:Xamarin.Forms.Thickness.Right)
- [`Bottom`](xref:Xamarin.Forms.Thickness.Bottom)

`Padding` définit une zone à l’intérieur d’une page où le contenu est exclu. Cela permet la `Label` pour éviter le remplacement de la barre d’état iOS.

### <a name="solution-2-include-padding-just-for-ios-sap-only"></a>Solution 2. Inclure la marge intérieure simplement pour iOS (SAP uniquement)

Définir une propriété « Marge » uniquement sur iOS à l’aide d’un SAP avec une directive de préprocesseur c#. Cela est illustré dans le [ **GreetingsSap** ](https://github.com/xamarin/xamarin-forms-book-samples/tree/master/Chapter02/GreetingsSap) solution.

### <a name="solution-3-include-padding-just-for-ios-pcl-or-sap"></a>Solution 3. Inclure la marge intérieure simplement pour iOS (bibliothèque de classes portable ou SAP)

Dans la version de Xamarin.Forms utilisé pour le livre, un `Padding` propriété spécifique à iOS dans une bibliothèque de classes portable ou une SAP peut être sélectionnée à l’aide de la [ `Device.OnPlatform` ](xref:Xamarin.Forms.Device.OnPlatform(System.Action,System.Action,System.Action,System.Action)) ou [ `Device.OnPlatform<T>` ](xref:Xamarin.Forms.Device.OnPlatform*) méthode statique. Ces méthodes sont désormais déconseillés.

Le `Device.OnPlatform` méthodes sont utilisées pour exécuter du code de plateforme spécifique ou pour sélectionner les valeurs spécifiques à la plateforme. En interne, elles rendent utilisent le [ `Device.OS` ](xref:Xamarin.Forms.Device.OS) en lecture seule propriété statique, qui retourne un membre de la [ `TargetPlatform` ](xref:Xamarin.Forms.TargetPlatform) énumération :

- [`iOS`](xref:Xamarin.Forms.TargetPlatform.iOS)
- [`Android`](xref:Xamarin.Forms.TargetPlatform.Android)
- [`Windows`](xref:Xamarin.Forms.TargetPlatform.Windows) pour les appareils UWP.

Le `Device.OnPlatform` méthodes, le `Device.OS` propriété et le `TargetPlatform` énumération sont tous maintenant déconseillé. Au lieu de cela, utilisez le [ `Device.RuntimePlatform` ](xref:Xamarin.Forms.Device.RuntimePlatform) propriété et comparer le `string` retourner de valeur avec les champs statiques suivantes :

- [`iOS`](xref:Xamarin.Forms.Device.iOS), la chaîne « iOS »
- [`Android`](xref:Xamarin.Forms.Device.Android), la chaîne « Android »
- [`UWP`](xref:Xamarin.Forms.Device.UWP), la chaîne « UWP », qui fait référence à la plateforme Windows universelle

Le [ `Device.Idiom` ](xref:Xamarin.Forms.Device.Idiom) propriété en lecture seule statique est liée. Cela retourne un membre de la [ `TargetIdiom` ](xref:Xamarin.Forms.TargetIdiom), ce qui a ces membres :

- [`Desktop`](xref:Xamarin.Forms.TargetIdiom.Desktop)
- [`Tablet`](xref:Xamarin.Forms.TargetIdiom.Tablet)
- [`Phone`](xref:Xamarin.Forms.TargetIdiom.Phone)
- [`Unsupported`](xref:Xamarin.Forms.TargetIdiom.Unsupported) n’est pas utilisé

Pour iOS et Android, la limite entre `Tablet` et `Phone` est une largeur de portrait de 600 unités. Pour la plateforme Windows, `Desktop` indique une application UWP s’exécutant sous Windows 10, et `Phone` indique une application UWP s’exécutant sous Windows 10 application.

## <a name="solution-3a-set-margin-on-the-label"></a>3 a de solution. Définir la marge sur l’étiquette

Le [ `Margin` ](xref:Xamarin.Forms.View.Margin) propriété a été introduite trop tard pour être inclus dans le livre, mais il est également de type `Thickness` et vous pouvez le définir sur le `Label` pour définir une zone en dehors de la vue qui est incluse dans le calcul de la disposition de la vue.

Le `Padding` propriété est disponible uniquement sur [ `Layout` ](xref:Xamarin.Forms.Layout) et [ `Page` ](xref:Xamarin.Forms.Page) dérivés. Le `Margin` propriété n’est disponible sur tous les [ `View` ](xref:Xamarin.Forms.View) dérivés.

## <a name="solution-4-center-the-label-within-the-page"></a>Solution 4. Centrer l’étiquette dans la page

Vous pouvez centrer le `Label` au sein de la `Page` (ou le placer dans un des huit autres endroits) en définissant le [ `HorizontalOptions` ](xref:Xamarin.Forms.View.HorizontalOptions) et [ `VerticalOptions` ](xref:Xamarin.Forms.View.VerticalOptions) propriétés de la `Label` une valeur de type [ `LayoutOptions` ](xref:Xamarin.Forms.LayoutOptions). Le `LayoutOptions` structure définit deux propriétés :

- Un [ `Alignment` ](xref:Xamarin.Forms.LayoutOptions.Alignment) propriété de type [ `LayoutAlignment` ](xref:Xamarin.Forms.LayoutAlignment), une énumération avec quatre membres : [ `Start` ](xref:Xamarin.Forms.LayoutAlignment.Start), ce qui signifie que gauche ou supérieur en fonction de la orientation, [ `Center` ](xref:Xamarin.Forms.LayoutAlignment.Center), [ `End` ](xref:Xamarin.Forms.LayoutAlignment.End), ce qui signifie que le droit ou inférieur selon l’orientation, et [ `Fill` ](xref:Xamarin.Forms.LayoutAlignment.Fill).

- Un [ `Expands` ](xref:Xamarin.Forms.LayoutOptions.Expands) propriété de type `bool`.

Généralement ces propriétés ne sont pas utilisées directement. Au lieu de cela, les combinaisons de ces deux propriétés sont fournies par huit propriétés en lecture seule statiques de type `LayoutOptions`:

- [`LayoutOptions.Start`](xref:Xamarin.Forms.LayoutOptions.Start)
- [`LayoutOptions.Center`](xref:Xamarin.Forms.LayoutOptions.Center)
- [`LayoutOptions.End`](xref:Xamarin.Forms.LayoutOptions.End)
- [`LayoutOptions.Fill`](xref:Xamarin.Forms.LayoutOptions.Fill)
- [`LayoutOptions.StartAndExpand`](xref:Xamarin.Forms.LayoutOptions.StartAndExpand)
- [`LayoutOptions.CenterAndExpand`](xref:Xamarin.Forms.LayoutOptions.CenterAndExpand)
- [`LayoutOptions.EndAndExpand`](xref:Xamarin.Forms.LayoutOptions.EndAndExpand)
- [`LayoutOptions.FillAndExpand`](xref:Xamarin.Forms.LayoutOptions.FillAndExpand)

`HorizontalOptions` et `VerticalOptions` sont des propriétés les plus importantes dans la disposition de Xamarin.Forms et sont décrits plus en détail dans [ **chapitre 4. Défilement de la pile**](chapter04.md).

Voici le résultat avec la `HorizontalOptions` et `VerticalOptions` propriétés de `Label` toutes deux définies sur `LayoutOptions.Center`:

[![Triple capture d’écran du programme de greetings](images/ch02fg05-small.png "horizontalement et verticalement centré étiqueter")](images/ch02fg05-large.png#lightbox "étiqueter de centré horizontalement et verticalement")

## <a name="solution-5-center-the-text-within-the-label"></a>Solution 5. Centrer le texte dans l’étiquette

Vous pouvez également centrer le texte (ou placez-le dans les huit autres emplacements sur la page) en définissant le [ `HorizontalTextAlignment` ](xref:Xamarin.Forms.Label.HorizontalTextAlignment) et [ `VerticalTextAlignment` ](xref:Xamarin.Forms.Label.VerticalTextAlignment) propriétés de `Label` à un membre de la [ `TextAlignment` ](xref:Xamarin.Forms.TextAlignment) énumération :

- [`Start`](xref:Xamarin.Forms.TextAlignment.Start), signification gauche ou supérieur (selon l’orientation)
- [`Center`](xref:Xamarin.Forms.TextAlignment.Center)
- [`End`](xref:Xamarin.Forms.TextAlignment.End), ce qui signifie qu’à droite ou en bas (selon l’orientation)

Ces deux propriétés sont définies uniquement par `Label`, tandis que le `HorizontalAlignment` et `VerticalAlignment` propriétés sont définies par `View` et héritée par toutes les `View` dérivés. Les résultats visuels peuvent sembler similaires, mais ils sont très différents, comme illustré dans le chapitre suivant.

## <a name="related-links"></a>Liens connexes

- [Chapitre 2, texte intégral (PDF)](https://download.xamarin.com/developer/xamarin-forms-book/XamarinFormsBook-Ch02-Apr2016.pdf)
- [Exemples de chapitre 2](https://github.com/xamarin/xamarin-forms-book-samples/tree/master/Chapter02)
- [Exemples de chapitre 2 F #](https://github.com/xamarin/xamarin-forms-book-samples/tree/master/Chapter02/FS)
- [Bien démarrer avec Xamarin.Forms](~/xamarin-forms/get-started/index.md)
