---
title: Touch dans Android
ms.prod: xamarin
ms.assetid: 405A1FA0-4EFA-4AEB-B672-F36307B9CF16
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 03/01/2018
ms.openlocfilehash: f1ccc86a20cb441bfdda864b8c7e263a691f5ab7
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/04/2018
ms.locfileid: "30767490"
---
# <a name="touch-in-android"></a>Touch dans Android

Beaucoup comme iOS, Android crée un objet qui contient les données sur l’interaction physique de l’utilisateur avec l’écran &ndash; un `Android.View.MotionEvent` objet. Cet objet contient des données telles que l’action est effectuée, où a eu des fonctions tactiles placer la pression nécessaire a été appliquée, etc. A `MotionEvent` objet décompose le déplacement dans les valeurs suivantes :

-  Un code d’action qui décrit le type de mouvement, telles que les fonctions tactiles initiale, la fonction tactile déplacement entre l’écran ou la fin de l’interaction tactile.

-  Un ensemble de valeurs d’axe qui décrit la position de la `MotionEvent` et d’autres propriétés de mouvement comme où les fonctions tactiles a eu lieu, lorsque les fonctions tactiles a eu lieu et la quantité de pression a été utilisée.
   Les valeurs d’axe peuvent différer en fonction de l’appareil, afin de la liste précédente ne décrit pas toutes les valeurs d’axe.


Le `MotionEvent` objet sera passé à une méthode appropriée dans une application. Il existe trois façons pour une application Xamarin.Android répondre à un événement tactile :

-  *Affecter un gestionnaire d’événements `View.Touch`*  - le `Android.Views.View` classe a un `EventHandler<View.TouchEventArgs>` les applications qui peuvent affecter un gestionnaire à. Ce comportement est normal .NET.

-  *Mise en œuvre `View.IOnTouchListener`*  -Instances de cette interface peuvent être attribués à un objet de vue à l’aide de la vue. `SetOnListener` méthode. Ceci est fonctionnellement équivalent à l’affectation d’un gestionnaire d’événements pour le `View.Touch` événement. S’il existe une logique commune ou partagée nécessitant plusieurs vues différentes lorsqu’ils sont touchées, il sera plus efficace de créer une classe et implémenter cette méthode à to affecter chaque vue son propre gestionnaire d’événements.

-  *Substituer `View.OnTouchEvent`*  -toutes les vues dans une sous-classe Android `Android.Views.View`. Lorsqu’une vue est couvertes, Android appellera la `OnTouchEvent` et lui passer un `MotionEvent` comme paramètre.


> [!NOTE]
> Tous les périphériques Android prend en charge les écrans tactiles. 

Ajout de la balise suivante à votre fichier manifeste entraîne Google Play pour affichage uniquement votre application à ces appareils sont tactile :

```xml
<uses-configuration android:reqTouchScreen="finger" />
```

## <a name="gestures"></a>Mouvements

Un mouvement est une forme dessiné sur l’écran tactile. Un mouvement peut avoir un ou plusieurs traits, chaque tracé constituée d’une séquence de points, créé par un autre point de contact avec l’écran. Android peut prendre en charge différents types de mouvements, à partir d’une simple fling sur l’écran des mouvements complexes qui impliquent tactiles.

Android fournit le `Android.Gestures` espace de noms en particulier pour la gestion et la réponse aux mouvements. Au cœur de tous les mouvements est une classe spéciale appelée `Android.Gestures.GestureDetector`. Comme son nom l’indique, cette classe pour écouter de mouvements et d’événements en fonction de `MotionEvents` fournie par le système d’exploitation.

Pour implémenter un détecteur de mouvement, une activité doit instancier un `GestureDetector` classe et fournir une instance de `IOnGestureListener`, comme illustré par l’extrait de code suivant :

```csharp
GestureOverlayView.IOnGestureListener myListener = new MyGestureListener();
_gestureDetector = new GestureDetector(this, myListener);
```

Une activité doit également implémenter l’OnTouchEvent et transmettez le MotionEvent au détecteur de mouvement. L’extrait de code suivant montre un exemple :

```csharp
public override bool OnTouchEvent(MotionEvent e)
{
    // This method is in an Activity
    return _gestureDetector.OnTouchEvent(e);
}
```

Lorsqu’une instance de `GestureDetector` identifie un mouvement d’intérêt, il avertit l’activité ou l’application en déclenchant un événement ou via un rappel fourni par `GestureDetector.IOnGestureListener`.
Cette interface fournit six méthodes pour les mouvements différents :

-  *OnDown* -appelée lorsqu’un clic se produit, mais n’est pas libéré.

-  *OnFling* -appelée lorsqu’un fling se produit et fournit des données sur la touche de début et de fin qui a déclenché l’événement.

-  *OnLongPress* -appelée lorsqu’une pression sur une longue se produit.

-  *OnScroll* -appelé lorsque survient un événement de défilement.

-  *OnShowPress* - appelée après une OnDown s’est produite et un déplacement ou des événements n’a pas été effectuée.

-  *OnSingleTapUp* -appelée lorsqu’un seul clic se produit.


Dans de nombreux cas les applications peuvent uniquement être intéressées par un sous-ensemble des mouvements. Dans ce cas, les applications doivent étendre la classe GestureDetector.SimpleOnGestureListener et substituer les méthodes qui correspondent aux événements qui les intéressent.

## <a name="custom-gestures"></a>Mouvements personnalisés

Mouvements sont un excellent moyen pour les utilisateurs à interagir avec une application. Les API que nous avons vu jusqu'à présent suffiraient pour des gestes simples, mais il peuvent s’avérer un peu onéreux pour les mouvements plus complexes. Pour faciliter les mouvements plus compliqués, Android fournit un autre ensemble de l’API dans l’espace de noms Android.Gestures qui facilite la partie de la charge associée à des mouvements personnalisés.

### <a name="creating-custom-gestures"></a>Création des mouvements personnalisés

Depuis Android 1.6, le Kit de développement logiciel Android est fourni avec une application préinstallée sur l’émulateur de générateur de mouvements. Cette application permet à un développeur créer des mouvements prédéfinis qui peuvent être incorporés dans une application. La capture d’écran suivante montre un exemple de générateur de mouvements :

[![Capture d’écran de générateur de mouvements avec des mouvements de l’exemple](touch-in-android-images/image11.png)](touch-in-android-images/image11.png#lightbox)

Une version améliorée de cette application appelée outil de mouvement sont accessibles Google Play. Outil de mouvement est très similaire à un générateur de mouvements, sauf qu’elle vous permet de tester les mouvements après que qu’ils ont été créés. Cette capture d’écran suivante montre le Générateur de mouvements :

[![Capture d’écran de mouvement outil avec des mouvements de l’exemple](touch-in-android-images/image12.png)](touch-in-android-images/image12.png#lightbox)

Outil de mouvement est un peu plus utile pour créer des mouvements personnalisés car elle permet les mouvements à tester leur création et est facilement disponible via Google Play.

Outil de mouvement vous permet de que créer un mouvement en dessinant sur l’écran et l’attribution d’un nom. Une fois les mouvements sont créés, ils sont enregistrés dans un fichier binaire sur la carte SD de votre appareil. Ce fichier doit être récupéré à partir de l’appareil et empaquetées avec une application dans le dossier /Resources/raw. Ce fichier peut être récupéré à partir de l’émulateur à l’aide de la passerelle du débogage Android. L’exemple suivant montre la copie du fichier à partir d’un canal Galaxy dans le répertoire de ressources d’une application :

```shell
$ adb pull /storage/sdcard0/gestures <projectdirectory>/Resources/raw
```

Une fois que vous avez extrait le fichier, il doit être empaqueté avec votre application dans le répertoire /Resources/raw. Le moyen le plus simple d’utiliser ce fichier de mouvement est à charger le fichier dans un GestureLibrary, comme indiqué dans l’extrait de code suivant :

```csharp
GestureLibary myGestures = GestureLibraries.FromRawResources(this, Resource.Raw.gestures);
if (!myGestures.Load())
{
    // The library didn't load, so close the activity.
    Finish();
}
```

### <a name="using-custom-gestures"></a>À l’aide des mouvements personnalisés

Pour qu’il reconnaisse les mouvements personnalisés dans une activité, il doit avoir un objet Android.Gesture.GestureOverlay ajouté à sa disposition. L’extrait de code suivant montre comment ajouter par programmation un GestureOverlayView à une activité :

```csharp
GestureOverlayView gestureOverlayView = new GestureOverlayView(this);
gestureOverlayView.AddOnGesturePerformedListener(this);
SetContentView(gestureOverlayView);
```

L’extrait de code XML suivant montre comment ajouter de façon déclarative un GestureOverlayView :

```xml
<android.gesture.GestureOverlayView
    android:id="@+id/gestures"
    android:layout_width="match_parent "
    android:layout_height="match_parent" />
```

Le `GestureOverlayView` a plusieurs événements qui seront déclenchés pendant le processus de dessin d’un mouvement. L’événement plus intéressante est `GesturePeformed`. Cet événement est déclenché lorsque l’utilisateur a terminé le dessin leurs mouvements.

Lorsque cet événement est déclenché, l’activité de demande un `GestureLibrary` pour essayer de correspondre le mouvement créés par l’utilisateur avec l’un des mouvements par l’outil de mouvement. `GestureLibrary` Retourne une liste d’objets de prédiction.

Chaque objet de prédiction contient un score et le nom de l’un des mouvements dans le `GestureLibrary`. Plus le score, plus le mouvement nommé dans la prédiction correspond à du mouvement dessiné par l’utilisateur.
En règle générale, résultats inférieures à 1.0 sont considérés comme des correspondances médiocres.

Le code suivant montre un exemple de mise en correspondance un mouvement :

```csharp
private void GestureOverlayViewOnGesturePerformed(object sender, GestureOverlayView.GesturePerformedEventArgs gesturePerformedEventArgs)
{
    // In this example _gestureLibrary was instantiated in OnCreate
    IEnumerable<Prediction> predictions = from p in _gestureLibrary.Recognize(gesturePerformedEventArgs.Gesture)
    orderby p.Score descending
    where p.Score > 1.0
    select p;
    Prediction prediction = predictions.FirstOrDefault();

    if (prediction == null)
    {
        Log.Debug(GetType().FullName, "Nothing matched the user's gesture.");
        return;
    }

    Toast.MakeText(this, prediction.Name, ToastLength.Short).Show();
}
```

Cela fait, vous devez avoir une compréhension montrant comment utiliser les mouvements tactiles et dans une application Xamarin.Android. Nous maintenant passer à une procédure pas à pas et afficher tous les concepts dans un exemple d’application fonctionnel.



## <a name="related-links"></a>Liens associés

- [Android Touch Démarrer (exemple)](https://developer.xamarin.com/samples/monodroid/ApplicationFundamentals/Touch_start)
- [Android Touch finale (exemple)](https://developer.xamarin.com/samples/monodroid/ApplicationFundamentals/Touch_final)
