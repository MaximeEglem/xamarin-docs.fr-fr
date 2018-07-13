---
title: Convertisseurs de valeur de liaison Xamarin.Forms
description: Cet article explique comment effectuer un cast ou convertir des valeurs au sein d’une liaison de données Xamarin.Forms en implémentant un convertisseur de valeurs (qui est également appelé un convertisseur de liaison ou un convertisseur de valeurs de liaison).
ms.prod: xamarin
ms.assetid: 02B1BBE6-D804-490D-BDD4-8ACED8B70C92
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 01/05/2018
ms.openlocfilehash: 28892692133020de1fa5a6eb007bb3f9bcf2612b
ms.sourcegitcommit: 6e955f6851794d58334d41f7a550d93a47e834d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38997478"
---
# <a name="xamarinforms-binding-value-converters"></a>Convertisseurs de valeur de liaison Xamarin.Forms

Liaisons de données généralement transférer des données à partir d’une propriété source à une propriété cible et dans certains cas à partir de la propriété cible à la propriété source. Ce transfert est simple lorsque les propriétés source et cible sont du même type, ou quand un type peut être converti à l’autre type via une conversion implicite. Lorsque qui n’est pas le cas, une conversion de type doit avoir lieu.

Dans le [ **mise en forme de chaîne** ](string-formatting.md) article, vous avez vu comment vous pouvez utiliser le `StringFormat` propriété d’une liaison de données pour convertir n’importe quel type en une chaîne. Pour les autres types de conversions, vous devez écrire du code spécialisé dans une classe qui implémente le [ `IValueConverter` ](xref:Xamarin.Forms.IValueConverter) interface. (La plateforme Windows universelle contient une classe similaire nommée [ `IValueConverter` ](/uwp/api/Windows.UI.Xaml.Data.IValueConverter/) dans le `Windows.UI.Xaml.Data` espace de noms, mais cela `IValueConverter` est dans le `Xamarin.Forms` espace de noms.) Classes qui implémentent `IValueConverter` sont appelés *convertisseurs de valeur*, mais elles sont également souvent appelées *liaison convertisseurs* ou *liaison des convertisseurs de valeur*.

## <a name="the-ivalueconverter-interface"></a>L’Interface IValueConverter

Supposons que vous souhaitez définir une liaison de données où la propriété source est de type `int` mais la propriété cible est un `bool`. Vous souhaitez que cette liaison de données pour produire un `false` valeur lorsque la source de l’entier est égale à 0, et `true` dans le cas contraire.  

Vous pouvez faire cela avec une classe qui implémente le `IValueConverter` interface :

```csharp
public class IntToBoolConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        return (int)value != 0;
    }

    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
    {
        return (bool)value ? 1 : 0;
    }
}
```

Vous définissez une instance de cette classe pour le [ `Converter` ](xref:Xamarin.Forms.Binding.Converter) propriété de la `Binding` classe ou à la [ `Converter` ](xref:Xamarin.Forms.Xaml.BindingExtension.Converter) propriété de la `Binding` extension de balisage. Cette classe devient partie intégrante de la liaison de données.

Le `Convert` méthode est appelée lorsque les données sont transférées de la source à la cible dans `OneWay` ou `TwoWay` liaisons. Le `value` paramètre est l’objet ou la valeur de la source de liaison de données. La méthode doit retourner une valeur du type de la cible de liaison de données. La méthode illustrée ici casts le `value` paramètre à un `int` puis le compare avec 0 pour un `bool` valeur de retour.

Le `ConvertBack` méthode est appelée lorsque les données sont transférées de la cible à la source dans `TwoWay` ou `OneWayToSource` liaisons. `ConvertBack` effectue la conversion opposée : il suppose la `value` paramètre est un `bool` à partir de la cible et la convertit en un `int` retourner de valeur pour la source.

Si la liaison de données inclut également un `StringFormat` définition, le convertisseur de valeurs est appelé avant que le résultat est mis en forme en tant que chaîne.

Le **activer les boutons** page dans le [ **démonstrations de liaison de données** ](https://developer.xamarin.com/samples/xamarin-forms/DataBindingDemos/) exemple illustre l’utilisation de ce convertisseur de valeur dans une liaison de données. Le `IntToBoolConverter` est instancié dans le dictionnaire de ressources de la page. Il est ensuite référencé avec un `StaticResource` extension de balisage pour définir le `Converter` propriété dans des liaisons de données de deux. Il est très courant pour partager des convertisseurs de données entre plusieurs liaisons de données sur la page :

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:DataBindingDemos"
             x:Class="DataBindingDemos.EnableButtonsPage"
             Title="Enable Buttons">
    <ContentPage.Resources>
        <ResourceDictionary>
            <local:IntToBoolConverter x:Key="intToBool" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <StackLayout Padding="10, 0">
        <Entry x:Name="entry1"
               Text=""
               Placeholder="enter search term"
               VerticalOptions="CenterAndExpand" />

        <Button Text="Search"
                HorizontalOptions="Center"
                VerticalOptions="CenterAndExpand"
                IsEnabled="{Binding Source={x:Reference entry1},
                                    Path=Text.Length,
                                    Converter={StaticResource intToBool}}" />

        <Entry x:Name="entry2"
               Text=""
               Placeholder="enter destination"
               VerticalOptions="CenterAndExpand" />

        <Button Text="Submit"
                HorizontalOptions="Center"
                VerticalOptions="CenterAndExpand"
                IsEnabled="{Binding Source={x:Reference entry2},
                                    Path=Text.Length,
                                    Converter={StaticResource intToBool}}" />
    </StackLayout>
</ContentPage>
```

Si un convertisseur de valeurs est utilisé dans plusieurs pages de votre application, vous pouvez l’instancier dans le dictionnaire de ressources dans le **App.xaml** fichier.

Le **activer les boutons** page montre un commun besoin quand un `Button` effectue une opération basée sur le texte que l’utilisateur tape dans un `Entry` vue. Si rien n’a été tapé dans le `Entry`, la `Button` doit être désactivée. Chaque `Button` contient une liaison de données sur son `IsEnabled` propriété. La source de liaison de données est la `Length` propriété de la `Text` propriété correspondante `Entry`. Si le problème `Length` propriété n’est pas 0, le convertisseur de valeurs retourne `true` et `Button` est activé :

[![Activer les boutons](converters-images/enablebuttons-small.png "activer les boutons")](converters-images/enablebuttons-large.png#lightbox "activer les boutons")

Notez que le `Text` propriété dans chaque `Entry` est initialisé avec une chaîne vide. Le `Text` propriété est `null` par défaut et les données de liaison ne fonctionnera pas dans ce cas.

Certains convertisseurs de valeur sont écrites spécifiquement pour des applications spécifiques, tandis que d’autres sont généralisées. Si vous savez qu’un convertisseur de valeurs servira uniquement dans `OneWay` liaisons, puis le `ConvertBack` méthode peut retourner simplement `null`.

Le `Convert` méthode illustrée ci-dessus implicitement suppose que le `value` argument est de type `int` et la valeur de retour doit être de type `bool`. De même, le `ConvertBack` méthode suppose que le `value` argument est de type `bool` et la valeur de retour est `int`. Si tel n’est pas le cas, une exception runtime se produit.

Vous pouvez écrire des convertisseurs de valeur pour être plus généralisé et pour accepter différents types de données. Le `Convert` et `ConvertBack` méthodes peuvent utiliser le `as` ou `is` opérateurs avec la `value` paramètre, ou vous pouvez appeler `GetType` sur ce paramètre pour déterminer son type et effectuez quelque chose appropriées. Le type attendu de chaque valeur de retour est fourni par le `targetType` paramètre. Parfois, les convertisseurs de valeurs sont utilisées avec des liaisons de données de différents types de cibles ; le convertisseur de valeurs peut utiliser le `targetType` argument pour effectuer une conversion du type correct.

Si la conversion en cours d’exécution est différente pour différentes cultures, utilisez le `culture` paramètre à cet effet. Le `parameter` l’argument de `Convert` et `ConvertBack` est abordée plus loin dans cet article.

## <a name="binding-converter-properties"></a>Propriétés de convertisseur de liaison

Classes de convertisseur de valeur peuvent avoir des propriétés et des paramètres génériques. Ce convertisseur de valeur particulière convertit un `bool` à partir de la source vers un objet de type `T` pour la cible :

```csharp
public class BoolToObjectConverter<T> : IValueConverter
{
    public T TrueObject { set; get; }

    public T FalseObject { set; get; }

    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        return (bool)value ? TrueObject : FalseObject;
    }

    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
    {
        return ((T)value).Equals(TrueObject);
    }
}
```

Le **commutateur indicateurs** page montre comment elle peut être utilisée pour afficher la valeur d’un `Switch` vue. Bien qu’il est courant d’instancier des convertisseurs de valeur en tant que ressources dans un dictionnaire de ressources, cette page montre une alternative : chaque convertisseur de valeurs est instancié entre `Binding.Converter` balises d’élément de propriété. Le `x:TypeArguments` indique l’argument générique, et `TrueObject` et `FalseObject` sont toutes deux définies sur les objets de ce type :

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:DataBindingDemos"
             x:Class="DataBindingDemos.SwitchIndicatorsPage"
             Title="Switch Indicators">
    <ContentPage.Resources>
        <ResourceDictionary>
            <Style TargetType="Label">
                <Setter Property="FontSize" Value="18" />
                <Setter Property="VerticalOptions" Value="Center" />
            </Style>

            <Style TargetType="Switch">
                <Setter Property="VerticalOptions" Value="Center" />
            </Style>
        </ResourceDictionary>
    </ContentPage.Resources>

    <StackLayout Padding="10, 0">
        <StackLayout Orientation="Horizontal"
                     VerticalOptions="CenterAndExpand">
            <Label Text="Subscribe?" />
            <Switch x:Name="switch1" />
            <Label>
                <Label.Text>
                    <Binding Source="{x:Reference switch1}"
                             Path="IsToggled">
                        <Binding.Converter>
                            <local:BoolToObjectConverter x:TypeArguments="x:String"
                                                         TrueObject="Of course!"
                                                         FalseObject="No way!" />
                        </Binding.Converter>
                    </Binding>
                </Label.Text>
            </Label>
        </StackLayout>

        <StackLayout Orientation="Horizontal"
                     VerticalOptions="CenterAndExpand">
            <Label Text="Allow popups?" />
            <Switch x:Name="switch2" />
            <Label>
                <Label.Text>
                    <Binding Source="{x:Reference switch2}"
                             Path="IsToggled">
                        <Binding.Converter>
                            <local:BoolToObjectConverter x:TypeArguments="x:String"
                                                         TrueObject="Yes"
                                                         FalseObject="No" />
                        </Binding.Converter>
                    </Binding>
                </Label.Text>
                <Label.TextColor>
                    <Binding Source="{x:Reference switch2}"
                             Path="IsToggled">
                        <Binding.Converter>
                            <local:BoolToObjectConverter x:TypeArguments="Color"
                                                         TrueObject="Green"
                                                         FalseObject="Red" />
                        </Binding.Converter>
                    </Binding>
                </Label.TextColor>
            </Label>
        </StackLayout>

        <StackLayout Orientation="Horizontal"
                     VerticalOptions="CenterAndExpand">
            <Label Text="Learn more?" />
            <Switch x:Name="switch3" />
            <Label FontSize="18"
                   VerticalOptions="Center">
                <Label.Style>
                    <Binding Source="{x:Reference switch3}"
                             Path="IsToggled">
                        <Binding.Converter>
                            <local:BoolToObjectConverter x:TypeArguments="Style">
                                <local:BoolToObjectConverter.TrueObject>
                                    <Style TargetType="Label">
                                        <Setter Property="Text" Value="Indubitably!" />
                                        <Setter Property="FontAttributes" Value="Italic, Bold" />
                                        <Setter Property="TextColor" Value="Green" />
                                    </Style>                                    
                                </local:BoolToObjectConverter.TrueObject>

                                <local:BoolToObjectConverter.FalseObject>
                                    <Style TargetType="Label">
                                        <Setter Property="Text" Value="Maybe later" />
                                        <Setter Property="FontAttributes" Value="None" />
                                        <Setter Property="TextColor" Value="Red" />
                                    </Style>
                                </local:BoolToObjectConverter.FalseObject>
                            </local:BoolToObjectConverter>
                        </Binding.Converter>
                    </Binding>
                </Label.Style>
            </Label>
        </StackLayout>
    </StackLayout>
</ContentPage>
```

Au cours des trois `Switch` et `Label` paires, l’argument générique a la valeur `Style`et ensemble `Style` objets sont fournis pour les valeurs de `TrueObject` et `FalseObject`. Ces remplacent le style implicit pour `Label` définie dans le dictionnaire de ressources, par conséquent, les propriétés dans ce style sont explicitement affectées à la `Label`. Activation/désactivation du `Switch` provoque le correspondantes `Label` pour refléter la modification :

[![Basculer les indicateurs](converters-images/switchindicators-small.png "basculer les indicateurs")](converters-images/switchindicators-large.png#lightbox "basculer les indicateurs")

Il est également possible d’utiliser [ `Triggers` ](~/xamarin-forms/app-fundamentals/triggers.md) pour implémenter des modifications similaires dans l’interface utilisateur basée sur les autres vues.

## <a name="binding-converter-parameters"></a>Liaison de paramètres de convertisseur

Le `Binding` classe définit un [ `ConverterParameter` ](xref:Xamarin.Forms.Binding.ConverterParameter) propriété et le `Binding` extension de balisage définit également un [ `ConverterParameter` ](xref:Xamarin.Forms.Xaml.BindingExtension.ConverterParameter) propriété. Si cette propriété est définie, la valeur est passée à la `Convert` et `ConvertBack` méthodes en tant que le `parameter` argument. Même si l’instance du convertisseur de valeurs est partagée entre plusieurs liaisons de données, le `ConverterParameter` peut être différent pour effectuer des conversions quelque peu différentes.

L’utilisation de `ConverterParameter` est illustrée par un programme de sélection de couleur. Dans ce cas, le `RgbColorViewModel` a trois propriétés de type `double` nommé `Red`, `Green`, et `Blue` qu’il utilise pour construire un `Color` valeur :

```csharp
public class RgbColorViewModel : INotifyPropertyChanged
{
    Color color;
    string name;

    public event PropertyChangedEventHandler PropertyChanged;

    public double Red
    {
        set
        {
            if (color.R != value)
            {
                Color = new Color(value, color.G, color.B);
            }
        }
        get
        {
            return color.R;
        }
    }

    public double Green
    {
        set
        {
            if (color.G != value)
            {
                Color = new Color(color.R, value, color.B);
            }
        }
        get
        {
            return color.G;
        }
    }

    public double Blue
    {
        set
        {
            if (color.B != value)
            {
                Color = new Color(color.R, color.G, value);
            }
        }
        get
        {
            return color.B;
        }
    }

    public Color Color
    {
        set
        {
            if (color != value)
            {
                color = value;
                PropertyChanged?.Invoke(this, new PropertyChangedEventArgs("Red"));
                PropertyChanged?.Invoke(this, new PropertyChangedEventArgs("Green"));
                PropertyChanged?.Invoke(this, new PropertyChangedEventArgs("Blue"));
                PropertyChanged?.Invoke(this, new PropertyChangedEventArgs("Color"));

                Name = NamedColor.GetNearestColorName(color);
            }
        }
        get
        {
            return color;
        }
    }

    public string Name
    {
        private set
        {
            if (name != value)
            {
                name = value;
                PropertyChanged?.Invoke(this, new PropertyChangedEventArgs("Name"));
            }
        }
        get
        {
            return name;
        }
    }
}
```

Le `Red`, `Green`, et `Blue` plage propriétés comprise entre 0 et 1. Toutefois, vous préférerez peut-être que les composants affichés en tant que valeurs hexadécimales à deux chiffres.

Pour afficher en tant que valeurs hexadécimales dans XAML, ils doivent être multipliées par 255, converties en entier et puis mis en forme avec une spécification de « X2 » dans le `StringFormat` propriété. Les deux premières tâches (multipliant par 255 et la conversion en un entier) peuvent être gérés par le convertisseur de valeurs. Pour rendre le convertisseur de valeurs comme généralisée que possible, le facteur de multiplication peut être spécifié avec le `ConverterParameter` propriété, ce qui signifie qu’il entre dans le `Convert` et `ConvertBack` méthodes en tant que le `parameter` argument :

```csharp
public class DoubleToIntConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        return (int)Math.Round((double)value * GetParameter(parameter));
    }

    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
    {
        return (int)value / GetParameter(parameter);
    }

    double GetParameter(object parameter)
    {
        if (parameter is double)
            return (double)parameter;

        else if (parameter is int)
            return (int)parameter;

        else if (parameter is string)
            return double.Parse((string)parameter);

        return 1;
    }
}
```

Le `Convert` convertit à partir d’un `double` à `int` tout en la multipliant par la `parameter` valeur ; la `ConvertBack` divise l’entier `value` argument par `parameter` et retourne un `double` résultat. (Dans le programme illustré ci-dessous, le convertisseur de valeurs est utilisé uniquement dans le cadre de mise en forme de chaîne, par conséquent, `ConvertBack` n’est pas utilisé.)

Le type de la `parameter` argument est susceptible d’être différents selon que la liaison de données est définie dans le code ou XAML. Si le `ConverterParameter` propriété du `Binding` est défini dans le code, il est susceptible d’être définie sur une valeur numérique :

```csharp
binding.ConverterParameter = 255;
```

Le `ConverterParameter` propriété est de type `Object`, de sorte que le compilateur c# interprète le littéral 255 en tant qu’entier et définit la propriété à cette valeur.

Dans XAML, toutefois, le `ConverterParameter` est susceptible d’être défini comme suit :

```xaml
<Label Text="{Binding Red,
                      Converter={StaticResource doubleToInt},
                      ConverterParameter=255,
                      StringFormat='Red = {0:X2}'}" />
```

Les 255 ressemble à un nombre, mais étant donné que `ConverterParameter` est de type `Object`, l’analyseur XAML traite les 255 sous forme de chaîne.

Pour cette raison, le convertisseur de valeur indiqué ci-dessus inclut un distinct `GetParameter` méthode qui gère des cas pour `parameter` étant de type `double`, `int`, ou `string`.  

Le **sélecteur de couleurs RVB** page instancie `DoubleToIntConverter` dans son dictionnaire de ressources suivant la définition de deux styles implicites :

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:DataBindingDemos"
             x:Class="DataBindingDemos.RgbColorSelectorPage"
             Title="RGB Color Selector">
    <ContentPage.Resources>
        <ResourceDictionary>
            <Style TargetType="Slider">
                <Setter Property="VerticalOptions" Value="CenterAndExpand" />
            </Style>

            <Style TargetType="Label">
                <Setter Property="HorizontalTextAlignment" Value="Center" />
            </Style>

            <local:DoubleToIntConverter x:Key="doubleToInt" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <StackLayout>
        <StackLayout.BindingContext>
            <local:RgbColorViewModel Color="Gray" />
        </StackLayout.BindingContext>

        <BoxView Color="{Binding Color}"
                 VerticalOptions="FillAndExpand" />

        <StackLayout Margin="10, 0">
            <Label Text="{Binding Name}" />

            <Slider Value="{Binding Red}" />
            <Label Text="{Binding Red,
                                  Converter={StaticResource doubleToInt},
                                  ConverterParameter=255,
                                  StringFormat='Red = {0:X2}'}" />

            <Slider Value="{Binding Green}" />
            <Label Text="{Binding Green,
                                  Converter={StaticResource doubleToInt},
                                  ConverterParameter=255,
                                  StringFormat='Green = {0:X2}'}" />

            <Slider Value="{Binding Blue}" />
            <Label>
                <Label.Text>
                    <Binding Path="Blue"
                             StringFormat="Blue = {0:X2}"
                             Converter="{StaticResource doubleToInt}">
                        <Binding.ConverterParameter>
                            <x:Double>255</x:Double>
                        </Binding.ConverterParameter>
                    </Binding>
                </Label.Text>
            </Label>
        </StackLayout>
    </StackLayout>
</ContentPage>    
```

Les valeurs de la `Red` et `Green` propriétés sont affichées avec un `Binding` extension de balisage. Le `Blue` propriété, toutefois, instancie le `Binding` classe afin d’illustrer comment explicite `double` peut avoir la valeur `ConverterParameter` propriété.

Voici le résultat :

[![Sélecteur de couleurs RVB](converters-images/rgbcolorselector-small.png "sélecteur de couleurs RVB")](converters-images/rgbcolorselector-large.png#lightbox "sélecteur de couleurs RVB")


## <a name="related-links"></a>Liens associés

- [Démonstrations de liaison de données (exemple)](https://developer.xamarin.com/samples/xamarin-forms/DataBindingDemos/)
- [Chapitre de liaison de données à partir du livre de Xamarin.Forms](~/xamarin-forms/creating-mobile-apps-xamarin-forms/summaries/chapter16.md)
