---
title: Navigation hiérarchique
description: Cet article montre comment utiliser la classe NavigationPage pour effectuer la navigation dans une pile de dernier entré, premier sorti (LIFO) pages.
ms.prod: xamarin
ms.assetid: C8A5EEFF-5A3B-4163-838A-147EE3939FAA
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 07/10/2017
ms.openlocfilehash: f8f8f9b4e5755e8b1707178fef633321b64e4e94
ms.sourcegitcommit: 6e955f6851794d58334d41f7a550d93a47e834d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38994674"
---
# <a name="hierarchical-navigation"></a>Navigation hiérarchique

_La classe NavigationPage fournit une expérience de navigation hiérarchique où l’utilisateur est en mesure de parcourir les pages, ascendante et descendante, comme vous le souhaitez. La classe implémente la navigation comme une pile dernier entré, premier sorti (LIFO) des objets de la Page. Cet article montre comment utiliser la classe NavigationPage pour effectuer la navigation dans une pile de pages._

Cet article aborde les rubriques suivantes :

- [Navigation entre les](#Performing_Navigation) : création de la page racine, en exécutant un push de pages à la pile de navigation, dépilant les pages à partir de la pile de navigation et animer des transitions de page.
- [Passage de données lors de la navigation](#Passing_Data_when_Navigating) : passer des données via un constructeur de page et un `BindingContext`.
- [Manipulation de la pile de navigation](#Manipulating_the_Navigation_Stack) : manipulation de la pile en insérant ou en supprimant des pages.

## <a name="overview"></a>Vue d'ensemble

Pour passer d’une page à l’autre, une application envoie une nouvelle page dans la pile de navigation, où elle devient la page active, comme illustré dans le diagramme suivant :

![](hierarchical-images/pushing.png "Envoi d’une Page vers la pile de Navigation")

Pour revenir à la page précédente, l’application dépile la page actuelle à partir de la pile de navigation, et la nouvelle page tout en haut devient la page active, comme illustré dans le diagramme suivant :

![](hierarchical-images/popping.png "Dépilé une Page à partir de la pile de Navigation")

Méthodes de navigation exposées par le [ `Navigation` ](xref:Xamarin.Forms.VisualElement.Navigation) propriété sur n’importe quel [ `Page` ](xref:Xamarin.Forms.Page) les types dérivés. Ces méthodes permettent de transmettre des pages dans la pile de navigation, aux pages pop à partir de la pile de navigation et pour effectuer des manipulations de la pile.

<a name="Performing_Navigation" />

## <a name="performing-navigation"></a>Navigation entre les

Dans la navigation hiérarchique, la classe [`NavigationPage`](xref:Xamarin.Forms.NavigationPage) est utilisée pour parcourir une pile d’objets [`ContentPage`](xref:Xamarin.Forms.ContentPage). Les captures d’écran suivantes montrent les principaux composants de la `NavigationPage` sur chaque plateforme :

![](hierarchical-images/navigationpage-components.png "Composants NavigationPage")

La disposition d’un [ `NavigationPage` ](xref:Xamarin.Forms.NavigationPage) dépend de la plateforme :

- Sur iOS, une barre de navigation est présente en haut de la page qui affiche un titre, et qui a un *retour* bouton retourne à la page précédente.
- Sur Android, une barre de navigation est présente en haut de la page qui affiche un titre, une icône, et un *retour* bouton retourne à la page précédente. L’icône est définie dans le `[Activity]` attribut décore le `MainActivity` classe dans le projet spécifique à la plateforme Android.
- Sur la plateforme Windows universelle, une barre de navigation est présente en haut de la page qui affiche un titre.

Sur toutes les plateformes, la valeur de la [ `Page.Title` ](xref:Xamarin.Forms.Page.Title) propriété s’affiche sous le titre de la page.

> [!NOTE]
> Il est recommandé qu’un `NavigationPage` doit être rempli avec `ContentPage` instances uniquement.

### <a name="creating-the-root-page"></a>Création de la Page racine

La première page ajoutée à une pile de navigation est appelée la page *racine* de l’application et l’exemple de code suivant illustre le déroulement de l’opération :

```csharp
public App ()
{
  MainPage = new NavigationPage (new Page1Xaml ());
}
```

Cela entraîne le `Page1Xaml` [ `ContentPage` ](xref:Xamarin.Forms.ContentPage) instance à être envoyée à la pile de navigation, où elle devient la page active et la page racine de l’application. Ceci est illustré dans les captures d’écran suivante :

![](hierarchical-images/mainpage.png "Page de la racine de la pile de Navigation")

> [!NOTE]
> Le [ `RootPage` ](xref:Xamarin.Forms.NavigationPage.RootPage) propriété d’un [ `NavigationPage` ](xref:Xamarin.Forms.NavigationPage) instance permet d’accéder à la première page de la pile de navigation.

### <a name="pushing-pages-to-the-navigation-stack"></a>Envoyer des Pages à la pile de Navigation

Pour accéder à `Page2Xaml`, il est nécessaire d’appeler le [ `PushAsync` ](xref:Xamarin.Forms.NavigationPage.PushAsync*) méthode sur le [ `Navigation` ](xref:Xamarin.Forms.VisualElement.Navigation) propriété de la page active, comme illustré dans l’exemple de code suivant :

```csharp
async void OnNextPageButtonClicked (object sender, EventArgs e)
{
  await Navigation.PushAsync (new Page2Xaml ());
}
```

L’instance de `Page2Xaml` est ainsi envoyée dans la pile de navigation, où elle devient la page active. Ceci est illustré dans les captures d’écran suivante :

![](hierarchical-images/secondpage.png "Page placé sur la pile de Navigation")

Lorsque le [ `PushAsync` ](xref:Xamarin.Forms.NavigationPage.PushAsync*) méthode est appelée, les événements suivants se produisent :

- L’appel de la page `PushAsync` a son [ `OnDisappearing` ](xref:Xamarin.Forms.Page.OnDisappearing) remplacement appelé.
- La page cible de la navigation a son [ `OnAppearing` ](xref:Xamarin.Forms.Page.OnAppearing) remplacement appelé.
- Le `PushAsync` tâche se termine.

Toutefois, l’ordre exact dans lequel ces événements se produisent est dépendant de la plate-forme. Pour plus d’informations, consultez [chapitre 24](https://developer.xamarin.com/r/xamarin-forms/book/chapter24.pdf) du livre de Xamarin.Forms de Petzold.

> [!NOTE]
> Les appels à la [ `OnDisappearing` ](xref:Xamarin.Forms.Page.OnDisappearing) et [ `OnAppearing` ](xref:Xamarin.Forms.Page.OnAppearing) remplacements ne peut pas être traités comme indications garanties de navigation entre les pages. Par exemple, sur iOS, le `OnDisappearing` override est appelée sur la page active lorsque l’application se termine.

### <a name="popping-pages-from-the-navigation-stack"></a>Exécution de type POP Pages à partir de la pile de Navigation

La page active peut être retirée de la pile de navigation en appuyant sur le bouton *Précédent* sur l’appareil, qu’il s’agisse d’un bouton physique sur l’appareil ou d’un bouton à l’écran.

Pour revenir par programmation à la page d’origine, l’instance de `Page2Xaml` doit appeler la méthode [`PopAsync`](xref:Xamarin.Forms.NavigationPage.PopAsync), comme illustré dans l’exemple de code suivant :

```csharp
async void OnPreviousPageButtonClicked (object sender, EventArgs e)
{
  await Navigation.PopAsync ();
}
```

L’instance de `Page2Xaml` est ainsi retirée de la pile de navigation, et la nouvelle page tout en haut devient la page active. Lorsque le [ `PopAsync` ](xref:Xamarin.Forms.NavigationPage.PopAsync) méthode est appelée, les événements suivants se produisent :

- L’appel de la page `PopAsync` a son [ `OnDisappearing` ](xref:Xamarin.Forms.Page.OnDisappearing) remplacement appelé.
- A la page ne soit retournée à son [ `OnAppearing` ](xref:Xamarin.Forms.Page.OnAppearing) remplacement appelé.
- La `PopAsync` retourne la tâche.

Toutefois, l’ordre exact dans lequel ces événements se produisent est dépendant de la plate-forme. Pour plus d’informations, consultez [chapitre 24](https://developer.xamarin.com/r/xamarin-forms/book/chapter24.pdf) du livre de Xamarin.Forms de Petzold.

Ainsi que [ `PushAsync` ](xref:Xamarin.Forms.NavigationPage.PushAsync*) et [ `PopAsync` ](xref:Xamarin.Forms.NavigationPage.PopAsync) méthodes, le [ `Navigation` ](xref:Xamarin.Forms.VisualElement.Navigation) propriété de chaque page fournit également un [ `PopToRootAsync` ](xref:Xamarin.Forms.NavigationPage.PopToRootAsync) (méthode), ce qui est illustré dans l’exemple de code suivant :

```csharp
async void OnRootPageButtonClicked (object sender, EventArgs e)
{
  await Navigation.PopToRootAsync ();
}
```

Cette méthode affiche toutes les valeurs sauf la racine [ `Page` ](xref:Xamarin.Forms.Page) la pile de navigation, ce qui rend donc la page racine de l’application de la page active.

### <a name="animating-page-transitions"></a>Animer des Transitions de Page

Le [ `Navigation` ](xref:Xamarin.Forms.VisualElement.Navigation) propriété de chaque page fournit également substituée push et pop méthodes qui incluent un `boolean` paramètre qui contrôle s’il faut afficher une animation de la page lors de la navigation, comme illustré dans le code suivant exemple :

```csharp
async void OnNextPageButtonClicked (object sender, EventArgs e)
{
  // Page appearance not animated
  await Navigation.PushAsync (new Page2Xaml (), false);
}

async void OnPreviousPageButtonClicked (object sender, EventArgs e)
{
  // Page appearance not animated
  await Navigation.PopAsync (false);
}

async void OnRootPageButtonClicked (object sender, EventArgs e)
{
  // Page appearance not animated
  await Navigation.PopToRootAsync (false);
}
```

Définition de la `boolean` paramètre `false` désactive l’animation de transition de page, tout en affectant au paramètre `true` permet l’animation de transition de page, si elle est prise en charge par la plateforme sous-jacente. Toutefois, les méthodes push et pop qui ne disposent pas de ce paramètre activent l’animation par défaut.

<a name="Passing_Data_when_Navigating" />

## <a name="passing-data-when-navigating"></a>Passage de données lors de la navigation

Il est parfois nécessaire pour une page passer des données lors de la navigation vers une autre page. Deux techniques permettant d’accomplir cela transmettez des données via un constructeur de page et en définissant la nouvelle page [ `BindingContext` ](xref:Xamarin.Forms.BindableObject.BindingContext) aux données. Chaque maintenant nous aborderons tour.

### <a name="passing-data-through-a-page-constructor"></a>Passage de données via un constructeur de Page

La technique la plus simple pour transmettre des données vers une autre page lors de la navigation est via un paramètre de constructeur de page, qui est indiqué dans l’exemple de code suivant :

```csharp
public App ()
{
  MainPage = new NavigationPage (new MainPage (DateTime.Now.ToString ("u")));
}
```

Ce code crée un `MainPage` d’une instance, en passant la date et heure actuelles au format ISO8601, qui est encapsulé dans un [ `NavigationPage` ](xref:Xamarin.Forms.NavigationPage) instance.

Le `MainPage` instance reçoit les données via un paramètre de constructeur, comme indiqué dans l’exemple de code suivant :

```csharp
public MainPage (string date)
{
  InitializeComponent ();
  dateLabel.Text = date;
}
```

Les données sont ensuite affichées dans la page en définissant le [ `Label.Text` ](xref:Xamarin.Forms.Label.Text) propriété, comme indiqué dans les captures d’écran suivante :

![](hierarchical-images/passing-data-constructor.png "Données passées via un constructeur de Page")

### <a name="passing-data-through-a-bindingcontext"></a>Passage de données via un objet BindingContext

Une autre approche pour transmettre des données vers une autre page lors de la navigation est en définissant la nouvelle page [ `BindingContext` ](xref:Xamarin.Forms.BindableObject.BindingContext) aux données, comme indiqué dans l’exemple de code suivant :

```csharp
async void OnNavigateButtonClicked (object sender, EventArgs e)
{
  var contact = new Contact {
    Name = "Jane Doe",
    Age = 30,
    Occupation = "Developer",
    Country = "USA"
  };

  var secondPage = new SecondPage ();
  secondPage.BindingContext = contact;
  await Navigation.PushAsync (secondPage);
}
```

Ce code définit le [ `BindingContext` ](xref:Xamarin.Forms.BindableObject.BindingContext) de la `SecondPage` l’instance à la `Contact` de l’instance, puis accède à la `SecondPage`.

Le `SecondPage` utilise ensuite la liaison de données pour afficher le `Contact` instance des données, comme indiqué dans l’exemple de code XAML suivant :

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="PassingData.SecondPage"
             Title="Second Page">
    <ContentPage.Content>
        <StackLayout HorizontalOptions="Center" VerticalOptions="Center">
            <StackLayout Orientation="Horizontal">
                <Label Text="Name:" HorizontalOptions="FillAndExpand" />
                <Label Text="{Binding Name}" FontSize="Medium" FontAttributes="Bold" />
            </StackLayout>
            ...
            <Button x:Name="navigateButton" Text="Previous Page" Clicked="OnNavigateButtonClicked" />
        </StackLayout>
    </ContentPage.Content>
</ContentPage>
```

L’exemple de code suivant montre comment la liaison de données peut être effectuée en c# :

```csharp
public class SecondPageCS : ContentPage
{
  public SecondPageCS ()
  {
    var nameLabel = new Label {
      FontSize = Device.GetNamedSize (NamedSize.Medium, typeof(Label)),
      FontAttributes = FontAttributes.Bold
    };
    nameLabel.SetBinding (Label.TextProperty, "Name");
    ...
    var navigateButton = new Button { Text = "Previous Page" };
    navigateButton.Clicked += OnNavigateButtonClicked;

    Content = new StackLayout {
      HorizontalOptions = LayoutOptions.Center,
      VerticalOptions = LayoutOptions.Center,
      Children = {
        new StackLayout {
          Orientation = StackOrientation.Horizontal,
          Children = {
            new Label{ Text = "Name:", FontSize = Device.GetNamedSize (NamedSize.Medium, typeof(Label)), HorizontalOptions = LayoutOptions.FillAndExpand },
            nameLabel
          }
        },
        ...
        navigateButton
      }
    };
  }

  async void OnNavigateButtonClicked (object sender, EventArgs e)
  {
    await Navigation.PopAsync ();
  }
}
```

Les données sont ensuite affichées dans la page par une série de [ `Label` ](xref:Xamarin.Forms.Label) des contrôles, comme indiqué dans les captures d’écran suivante :

![](hierarchical-images/passing-data-bindingcontext.png "Données passées via un objet BindingContext")

Pour plus d’informations sur la liaison de données, consultez [Notions de base de la liaison de données](~/xamarin-forms/xaml/xaml-basics/data-binding-basics.md).

<a name="Manipulating_the_Navigation_Stack" />

## <a name="manipulating-the-navigation-stack"></a>Manipulation de la pile de Navigation

Le [ `Navigation` ](xref:Xamarin.Forms.VisualElement.Navigation) propriété expose un [ `NavigationStack` ](xref:Xamarin.Forms.INavigation.NavigationStack) propriété à partir de laquelle les pages dans la pile de navigation peuvent être obtenus. Tandis que Xamarin.Forms gère l’accès à la pile de navigation, le `Navigation` propriété fournit le [ `InsertPageBefore` ](xref:Xamarin.Forms.INavigation.InsertPageBefore*) et [ `RemovePage` ](xref:Xamarin.Forms.INavigation.RemovePage*) méthodes pour manipuler la pile en insérant pages ou en les supprimant.

Le [ `InsertPageBefore` ](xref:Xamarin.Forms.INavigation.InsertPageBefore*) méthode insère une page spécifiée dans la pile de navigation avant une page existante spécifiée, comme indiqué dans le diagramme suivant :

![](hierarchical-images/insert-page-before.png "Insertion d’une Page dans la pile de Navigation")

Le [ `RemovePage` ](xref:Xamarin.Forms.INavigation.RemovePage*) méthode supprime la page spécifiée à partir de la pile de navigation, comme illustré dans le diagramme suivant :

![](hierarchical-images/remove-page.png "Suppression d’une Page à partir de la pile de Navigation")

Ces méthodes permettent une expérience de navigation personnalisés, tels que le remplacement d’une page de connexion avec une nouvelle page, en suivant une connexion réussie. L’exemple de code suivant illustre ce scénario :

```csharp
async void OnLoginButtonClicked (object sender, EventArgs e)
{
  ...
  var isValid = AreCredentialsCorrect (user);
  if (isValid) {
    App.IsUserLoggedIn = true;
    Navigation.InsertPageBefore (new MainPage (), this);
    await Navigation.PopAsync ();
  } else {
    // Login failed
  }
}

```

Condition que les informations d’identification sont correctes, le `MainPage` instance est insérée dans la pile de navigation avant la page active. Le [ `PopAsync` ](xref:Xamarin.Forms.NavigationPage.PopAsync) méthode supprime ensuite la page actuelle à partir de la pile de navigation, avec le `MainPage` instance devient la page active.

## <a name="summary"></a>Récapitulatif

Cet article vous a montré comment utiliser le [ `NavigationPage` ](xref:Xamarin.Forms.NavigationPage) classe pour effectuer la navigation dans une pile de pages. Cette classe fournit une expérience de navigation hiérarchique où l’utilisateur est en mesure de parcourir les pages, ascendante et descendante, comme vous le souhaitez. La classe implémente la navigation comme une pile d’objets [`Page`](xref:Xamarin.Forms.Page) LIFO (dernier entré, premier sorti).


## <a name="related-links"></a>Liens associés

- [Navigation entre les pages](https://developer.xamarin.com/r/xamarin-forms/book/chapter24.pdf)
- [Hiérarchique (exemple)](https://developer.xamarin.com/samples/xamarin-forms/Navigation/Hierarchical/)
- [PassingData (exemple)](https://developer.xamarin.com/samples/xamarin-forms/Navigation/PassingData/)
- [LoginFlow (exemple)](https://developer.xamarin.com/samples/xamarin-forms/Navigation/LoginFlow/)
- [Comment créer une connexion dans le flux d’écran dans les exemples Xamarin.Forms (vidéo Xamarin University)](http://xamarinuniversity.blob.core.windows.net/lightninglectures/CreateASignIn.zip)
- [Comment créer une connexion dans le flux d’écran dans Xamarin.Forms (vidéo Xamarin University)](https://university.xamarin.com/lightninglectures/how-to-create-a-sign-in-screen-flow-in-xamarinforms)
- [NavigationPage](xref:Xamarin.Forms.NavigationPage)
