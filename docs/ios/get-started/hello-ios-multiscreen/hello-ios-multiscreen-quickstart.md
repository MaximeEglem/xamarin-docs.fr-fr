---
title: Hello.iOS multi-écran - Démarrage rapide
description: Ce document montre comment étendre l’exemple d’application Phoneword pour ajouter un deuxième écran. Il décrit model-view-controller, la navigation iOS et d’autres concepts clés du développement iOS.
ms.topic: quickstart
ms.prod: xamarin
ms.assetid: d72e6230-c9ee-4bee-90ec-877d256821aa
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 12/02/2016
ms.openlocfilehash: 469032dc7caa46c6a89b350dc37bc9a93366066a
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34785669"
---
# <a name="hello-ios-multiscreen--quickstart"></a>Hello.iOS multi-écran - Démarrage rapide

Cette partie de la procédure pas à pas permet d’ajouter un deuxième écran à l’application Phoneword pour afficher l’historique des numéros de téléphone appelés avec l’application. L’application finale propose un deuxième écran qui affiche l’historique des appels, comme l’illustre la capture d’écran suivante :

 [![](hello-ios-multiscreen-quickstart-images/00.png "L’application finale a un deuxième écran qui affiche l’historique des appels, comme l’illustre cette capture d’écran")](hello-ios-multiscreen-quickstart-images/00.png#lightbox)

La partie [En profondeur](~/ios/get-started/hello-ios-multiscreen/hello-ios-multiscreen-deepdive.md) complémentaire reprend l’application générée et aborde l’architecture, la navigation et d’autres nouveaux concepts iOS rencontrés en chemin.

 <a name="Requirements" />

## <a name="requirements"></a>Configuration requise

Ce guide reprend là où le document Hello, iOS s’est arrêté et nécessite d’avoir terminé la partie [Hello, iOS - Démarrage rapide](~/ios/get-started/hello-ios/index.md). La version complète de l’application Phoneword peut être téléchargée à partir de l’[exemple Hello, iOS](https://developer.xamarin.com/samples/monotouch/Hello_iOS/).

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio pour Mac](#tab/vsmac)

## <a name="walkthrough"></a>Procédure pas à pas

Cette procédure pas à pas permet d’ajouter un écran d’historique des appels à notre application **Phoneword**.


1. Ouvrez l’application **Phoneword** dans Visual Studio pour Mac. Si besoin, vous pouvez télécharger l’application Phoneword complète à partir du guide de [procédure pas à pas Hello, iOS](~/ios/get-started/hello-ios/index.md) [ici](https://developer.xamarin.com/samples/monotouch/Hello_iOS/).


2. Ouvrez le fichier **Main.storyboard** à partir du **Panneau Solutions** :

  ![](hello-ios-multiscreen-quickstart-images/02new.png "Main.storyboard dans le concepteur iOS")


3. Faites glisser un **contrôleur de navigation** depuis la **boîte à outils** dans l’aire de conception (Vous devrez peut-être effectuer un zoom arrière pour que tout tienne dans l’aire de conception !) :

  ![](hello-ios-multiscreen-quickstart-images/03new.png "Faire glisser un contrôleur de navigation depuis la boîte à outils dans l’aire de conception")


4. Faites glisser le **Segue sans source** (la flèche grise à gauche du contrôleur d’affichage unique) vers le **contrôleur de navigation** pour modifier le point de départ de l’application :

  ![](hello-ios-multiscreen-quickstart-images/04new.png "Faire glisser le Segue sans source vers le contrôleur de Navigation pour modifier le point de départ de l’application")


5. Sélectionnez le **contrôleur d’affichage racine** existant en cliquant sur la barre inférieure, puis appuyez sur **Supprimer** pour le supprimer de l’aire de conception.
Ensuite, déplacez la scène **Phoneword** à côté du **contrôleur de navigation** :

  ![](hello-ios-multiscreen-quickstart-images/05new.png "Déplacer la scène Phoneword à côté du contrôleur de navigation")


6. Définissez **ViewController** en tant que **contrôleur d’affichage racine** du contrôleur de navigation. Appuyez sur la touche **Ctrl** et cliquez à l’intérieur du **contrôleur de navigation**. Une ligne bleue doit apparaître. Ensuite, tout en maintenant enfoncée la touche **Ctrl**, faites glisser le curseur depuis le **contrôleur de navigation** jusqu’à la scène **Phoneword** et relâchez la touche. Cette opération est appelée _Ctrl+Faire glisser_ :

 ![](hello-ios-multiscreen-quickstart-images/06.png "Faire glisser le curseur depuis le contrôleur de navigation jusqu’à la scène Phoneword et relâcher")


7. Depuis le menu, affectez à la relation la valeur **Racine** :

  ![](hello-ios-multiscreen-quickstart-images/07new.png "Définition de la relation sur Racine")

  **ViewController** est maintenant le **contrôleur d’affichage racine du contrôleur de navigation :**

  ![](hello-ios-multiscreen-quickstart-images/08.png "ViewController est maintenant le contrôleur d’affichage racine du contrôleur de navigation")


8. Double-cliquez sur la barre de **titre** de l’écran **Phoneword** et remplacez le **titre** par **Phoneword** :

  ![](hello-ios-multiscreen-quickstart-images/09.png "Remplacer le titre par Phoneword")


9. Faites glisser un **bouton** à partir de la **boîte à outils** et placez-le sous le **bouton d’appel**. Faites glisser les poignées pour que le nouveau **bouton** ait la même largeur que le **bouton d’appel** :

  ![](hello-ios-multiscreen-quickstart-images/10new.png "Définir la même largeur que celle du bouton d’appel pour le nouveau bouton")


10. Dans le **Panneau Propriétés**, modifiez le **Nom** du bouton **CallHistoryButton** et remplacez le **Titre** par **Historique des appels** :

  ![](hello-ios-multiscreen-quickstart-images/11new.png "Remplacer le nom du bouton par CallHistoryButton et remplacer le titre par Historique des appels")


11. Créez l’écran **Historique des appels**. À partir de la **boîte à outils**, faites glisser un **contrôleur d’affichage Table** dans l’aire de conception :

 ![](hello-ios-multiscreen-quickstart-images/12new.png "Faire glisser un contrôleur d’affichage Table dans l’aire de conception")


12. Ensuite, sélectionnez le **contrôleur d’affichage Table** en cliquant sur la barre noire située au bas de la scène. Dans le **Panneau Propriétés**, remplacez la classe du **contrôleur d’affichage Table** par `CallHistoryController` et appuyez sur **Entrée** :

  ![](hello-ios-multiscreen-quickstart-images/13new.png "Remplacer la classe du contrôleur d’affichage Table par CallHistoryController")

  Le concepteur iOS génère une classe de stockage personnalisée appelée `CallHistoryController` pour gérer la hiérarchie d’affichage de contenu de cet écran.
  Le fichier **CallHistoryController.cs** s’affiche dans le **Panneau Solutions** :

  ![](hello-ios-multiscreen-quickstart-images/14new.png "Le fichier CallHistoryController.cs s’affiche dans le Panneau Solutions")


13. Double-cliquez sur le fichier **CallHistoryController.cs** pour l’ouvrir et remplacez son contenu par le code suivant :

  ```csharp
  using System;
  using Foundation;
  using UIKit;
  using System.Collections.Generic;

  namespace Phoneword_iOS
  {
      public partial class CallHistoryController : UITableViewController
      {
          public List<string> PhoneNumbers { get; set; }

          static NSString callHistoryCellId = new NSString ("CallHistoryCell");

          public CallHistoryController (IntPtr handle) : base (handle)
          {
              TableView.RegisterClassForCellReuse (typeof(UITableViewCell), callHistoryCellId);
              TableView.Source = new CallHistoryDataSource (this);
              PhoneNumbers = new List<string> ();
          }

          class CallHistoryDataSource : UITableViewSource
          {
              CallHistoryController controller;

              public CallHistoryDataSource (CallHistoryController controller)
              {
                  this.controller = controller;
              }

              public override nint RowsInSection (UITableView tableView, nint section)
              {
                  return controller.PhoneNumbers.Count;
              }

              public override UITableViewCell GetCell (UITableView tableView, NSIndexPath indexPath)
              {
                  var cell = tableView.DequeueReusableCell (CallHistoryController.callHistoryCellId);

                  int row = indexPath.Row;
                  cell.TextLabel.Text = controller.PhoneNumbers [row];
                  return cell;
              }
          }
      }
  }
  ```

  Enregistrez l’application (**⌘ + S**) et générez-la (**⌘ + B**) pour vérifier l’absence d’erreurs.


14. Créez un _Segue_ (une transition) entre la scène **Phoneword** et la scène **Historique des appels**.
  Dans la **scène Phoneword**, sélectionnez le **bouton d’historique des appels**, puis en maintenant la touche Ctrl enfoncée, faites glisser le curseur depuis le **bouton** vers la scène **Historique des appels** :

  ![](hello-ios-multiscreen-quickstart-images/15.png "Maintenir la touche Ctrl enfoncée et faire glisser le curseur depuis le bouton vers le scène Historique des appels")

  Dans le menu **Action Segue**, sélectionnez **Afficher**

  Le concepteur iOS ajoute un Segue entre les deux scènes :

  ![](hello-ios-multiscreen-quickstart-images/17new.png "Segue entre les deux scènes")


15. Ajoutez un **titre** au **contrôleur d’affichage Table** en sélectionnant la barre noire située au bas de la scène et en remplaçant le **titre du contrôleur d’affichage** par **Historique des appels** dans le **Panneau Propriétés** :

  ![](hello-ios-multiscreen-quickstart-images/18new.png "Remplacer le titre du contrôleur d’affichage par Historique des appels dans le Panneau Propriétés")

16. Lorsque l’application est exécutée, le **bouton d’historique des appels** ouvre l’écran **Historique des appels**, mais l’affichage Table est vide, car il n’y pas de code permettant de mémoriser et afficher les numéros de téléphone.

  Cette application enregistre les numéros de téléphone sous la forme d’une liste de chaînes.

  Ajoutez une directive `using` pour `System.Collections.Generic` en haut de **ViewController** :

  ```csharp
  using System.Collections.Generic;
  ```



17. Modifiez la classe `ViewController` avec le code suivant :

    ```csharp
    using System;
    using System.Collections.Generic;
    using Foundation;
    using UIKit;

    namespace Phoneword_iOS
    {
      public partial class ViewController : UIViewController
      {
        string translatedNumber = "";

        public List<string> PhoneNumbers { get; set; }

        protected ViewController(IntPtr handle) : base(handle)
        {
          //initialize list of phone numbers called for Call History screen
          PhoneNumbers = new List<string>();
        }

        public override void ViewDidLoad()
        {
          base.ViewDidLoad();
          // Perform any additional setup after loading the view, typically from a nib.

          TranslateButton.TouchUpInside += (object sender, EventArgs e) => {
            // Convert the phone number with text to a number
            // using PhoneTranslator.cs
            translatedNumber = PhoneTranslator.ToNumber(
              PhoneNumberText.Text);

            // Dismiss the keyboard if text field was tapped
            PhoneNumberText.ResignFirstResponder();

            if (translatedNumber == "")
            {
              CallButton.SetTitle("Call ", UIControlState.Normal);
              CallButton.Enabled = false;
            }
            else
            {
              CallButton.SetTitle("Call " + translatedNumber,
                UIControlState.Normal);
              CallButton.Enabled = true;
            }
          };

          CallButton.TouchUpInside += (object sender, EventArgs e) => {

            //Store the phone number that we're dialing in PhoneNumbers
            PhoneNumbers.Add(translatedNumber);

            // Use URL handler with tel: prefix to invoke Apple's Phone app...
            var url = new NSUrl("tel:" + translatedNumber);

            // otherwise show an alert dialog
            if (!UIApplication.SharedApplication.OpenUrl(url))
            {
              var alert = UIAlertController.Create("Not supported", "Scheme 'tel:' is not supported on this device", UIAlertControllerStyle.Alert);
              alert.AddAction(UIAlertAction.Create("Ok", UIAlertActionStyle.Default, null));
              PresentViewController(alert, true, null);
            }
          };
        }

        public override void PrepareForSegue(UIStoryboardSegue segue, NSObject sender)
        {
          base.PrepareForSegue(segue, sender);

          // set the View Controller that’s powering the screen we’re
          // transitioning to

          var callHistoryContoller = segue.DestinationViewController as CallHistoryController;

          //set the Table View Controller’s list of phone numbers to the
          // list of dialed phone numbers

          if (callHistoryContoller != null)
          {
            callHistoryContoller.PhoneNumbers = PhoneNumbers;
          }
        }
      }
    }
    ```


Quelques éléments méritent votre attention
  * La variable `translatedNumber` a été déplacée depuis la méthode `ViewDidLoad` vers une _variable de niveau de classe_.
  * Le code de **CallButton** a été modifié pour ajouter les numéros composés à la liste des numéros de téléphone en appelant `PhoneNumbers.Add(translatedNumber)`
  * La méthode `PrepareForSegue` a été ajoutée

  Enregistrez et générez l’application pour vérifier qu’il n’y a pas d’erreurs.

20. Appuyez sur le bouton **Démarrer** pour lancer l’application dans le **simulateur iOS** :

  ![](hello-ios-multiscreen-quickstart-images/19.png "Appuyer sur le bouton Démarrer pour lancer l’application dans le simulateur iOS")


Félicitations ! Vous avez terminé votre première application Xamarin.iOS multi-écran.

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

## <a name="walkthrough"></a>Procédure pas à pas

Cette procédure pas à pas permet d’ajouter un écran d’historique des appels à notre application **Phoneword**.


1. Ouvrez l’application **Phoneword** dans Visual Studio. Si besoin, téléchargez l’[application Phoneword complète](https://developer.xamarin.com/samples/monotouch/Hello_iOS/) à partir du guide de [procédure pas à pas Hello, iOS](~/ios/get-started/hello-ios/index.md). N’oubliez pas qu’il est nécessaire de se connecter à un [Mac](~/ios/get-started/installation/windows/connecting-to-mac/index.md) pour utiliser le concepteur iOS et le simulateur iOS.


2. Commencez par modifier l’interface utilisateur. Ouvrez le fichier **Main.storyboard** depuis l’**Explorateur de solutions**, en vérifiant que **Afficher en tant que** a la valeur _iPhone 6_ :

  ![](hello-ios-multiscreen-quickstart-images/image1.png "Main.storyboard dans le concepteur iOS")


3. Faites glisser un **contrôleur de navigation** depuis la **boîte à outils** dans l’aire de conception :

  ![](hello-ios-multiscreen-quickstart-images/image2.png "Faire glisser un contrôleur de navigation depuis la boîte à outils dans l’aire de conception")


4. Faites glisser le **Segue sans source** (la flèche grise à gauche de la scène **Phoneword**) depuis la scène **Phoneword** vers le **contrôleur de navigation** pour modifier le point de départ de l’application :

  ![](hello-ios-multiscreen-quickstart-images/image3.png "Faire glisser le Segue sans source vers le contrôleur de Navigation pour modifier le point de départ de l’application")


5. Sélectionnez le **contrôleur d’affichage racine** en cliquant sur la barre noire, puis appuyez sur **Supprimer** pour le supprimer de l’aire de conception.
  Ensuite, déplacez la scène **Phoneword** à côté du **contrôleur de navigation** :

  ![](hello-ios-multiscreen-quickstart-images/image4.png "Déplacer la scène Phoneword à côté du contrôleur de navigation")


6. Définissez **ViewController** en tant que `Root View Controller` du contrôleur de navigation. Appuyez sur la touche **Ctrl** et cliquez à l’intérieur du **contrôleur de navigation**. Une ligne bleue doit apparaître. Ensuite, tout en maintenant enfoncée la touche **Ctrl**, faites glisser le curseur depuis le **contrôleur de navigation** jusqu’à la scène **Phoneword** et relâchez la touche. Cette opération est appelée _Ctrl+Faire glisser_ :

  ![](hello-ios-multiscreen-quickstart-images/image5.png "Faire glisser le curseur depuis le contrôleur de navigation jusqu’à la scène Phoneword et relâcher")


7. Depuis le menu, affectez à la relation la valeur **Racine** :

  ![](hello-ios-multiscreen-quickstart-images/image6.png "Affecter à la relation la valeur Racine")

  **ViewController** est maintenant le **contrôleur d’affichage racine de notre contrôleur de navigation.**


8. Double-cliquez sur la barre de **titre** de l’écran **Phoneword** et remplacez le **titre** par **Phoneword** :

  ![](hello-ios-multiscreen-quickstart-images/image7.png "Remplacer le titre par Phoneword")


9. Faites glisser un **bouton** à partir de la **boîte à outils** et placez-le sous le **bouton d’appel**. Faites glisser les poignées pour que le nouveau **bouton** ait la même largeur que le **bouton d’appel** :

  ![](hello-ios-multiscreen-quickstart-images/image8.png "Définir la même largeur que celle du bouton d’appel pour le nouveau bouton")


10. Dans le **volet Propriétés**, remplacez le **nom** du **bouton** par `CallHistoryButton` et remplacez le **titre** par **Historique des appels** :

  ![](hello-ios-multiscreen-quickstart-images/image9.png "Remplacer le nom du bouton par CallHistoryButton et le titre par Historique des appels")


11. Créez l’écran **Historique des appels**. À partir de la **boîte à outils**, faites glisser un **contrôleur d’affichage Table** dans l’aire de conception :

  ![](hello-ios-multiscreen-quickstart-images/image10.png "Faire glisser un contrôleur d’affichage Table dans l’aire de conception")


12. Sélectionnez le **contrôleur d’affichage Table** en cliquant sur la barre noire située au bas de la scène. Dans le **volet Propriétés**, remplacez la classe du **contrôleur d’affichage Table** par `CallHistoryController` et appuyez sur **Entrée** :

  ![](hello-ios-multiscreen-quickstart-images/image11.png "Remplacer la classe du contrôleur d’affichage Table par CallHistoryController")

  Le concepteur iOS génère une classe de stockage personnalisée appelée `CallHistoryController` pour gérer la hiérarchie d’affichage de contenu de cet écran.
  Le fichier **CallHistoryController.cs** s’affiche dans l’**Explorateur de solutions** :

  ![](hello-ios-multiscreen-quickstart-images/image12.png "Le fichier CallHistoryController.cs s’affiche dans l’Explorateur de solutions")


13. Double-cliquez sur le fichier **CallHistoryController.cs** pour l’ouvrir et remplacez son contenu par le code suivant :

        using System;
        using Foundation;
        using UIKit;
        using System.Collections.Generic;

        namespace Phoneword
        {
            public partial class CallHistoryController : UITableViewController
            {
                public List<String> PhoneNumbers { get; set; }

                static NSString callHistoryCellId = new NSString ("CallHistoryCell");

                public CallHistoryController (IntPtr handle) : base (handle)
                {
                    TableView.RegisterClassForCellReuse (typeof(UITableViewCell), callHistoryCellId);
                    TableView.Source = new CallHistoryDataSource (this);
                    PhoneNumbers = new List<string> ();
                }

                class CallHistoryDataSource : UITableViewSource
                {
                    CallHistoryController controller;

                    public CallHistoryDataSource (CallHistoryController controller)
                    {
                        this.controller = controller;
                    }

                    // Returns the number of rows in each section of the table
                    public override nint RowsInSection (UITableView tableView, nint section)
                    {
                        return controller.PhoneNumbers.Count;
                    }

                    public override UITableViewCell GetCell (UITableView tableView, NSIndexPath indexPath)
                    {
                        var cell = tableView.DequeueReusableCell (CallHistoryController.callHistoryCellId);

                        int row = indexPath.Row;
                        cell.TextLabel.Text = controller.PhoneNumbers [row];
                        return cell;
                    }
                }
            }
        }

  Enregistrez l’application et générez-la pour vérifier l’absence d’erreurs. Vous pouvez ignorer les avertissements de génération pour le moment.


14. Créez un _Segue_ (une transition) entre la scène **Phoneword** et la scène **Historique des appels**.
  Dans la **scène Phoneword**, sélectionnez le **bouton d’historique des appels**, puis **en maintenant la touche Ctrl enfoncée, faites glisser** le curseur depuis le **bouton** vers la scène **Historique des appels** :

  ![](hello-ios-multiscreen-quickstart-images/image13.png "Maintenir la touche Ctrl enfoncée et faire glisser le curseur depuis le bouton vers le scène Historique des appels")

  Dans le menu **Action Segue**, sélectionnez **Afficher** :

  ![](hello-ios-multiscreen-quickstart-images/image14.png "Sélectionner Afficher comme type de Segue")

  Le concepteur iOS ajoute un Segue entre les deux scènes :

  ![](hello-ios-multiscreen-quickstart-images/image15.png "Segue entre les deux scènes")


15. Ajoutez un **titre** au **contrôleur d’affichage Table** en sélectionnant la barre noire située au bas de la scène et en remplaçant **Contrôleur d’affichage > Titre** par **Historique des appels** dans le **volet Propriétés** :

  ![](hello-ios-multiscreen-quickstart-images/image16.png "Remplacer le titre du contrôleur d’affichage par Historique des appels")


16. Lorsque l’application est exécutée, le **bouton d’historique des appels** ouvre l’écran **Historique des appels**, mais l’affichage Table est vide, car il n’y pas de code permettant de mémoriser et afficher les numéros de téléphone.

  Cette application enregistre les numéros de téléphone sous la forme d’une liste de chaînes.

  Ajoutez une directive `using` pour `System.Collections.Generic` en haut de **ViewController** :

        using System.Collections.Generic;

17. Modifiez la classe `ViewController` avec le code suivant :

    ```csharp
    using System;
    using System.Collections.Generic;
    using Foundation;
    using UIKit;

    namespace Phoneword_iOS
    {
      public partial class ViewController : UIViewController
      {
        string translatedNumber = "";

        public List<string> PhoneNumbers { get; set; }

        protected ViewController(IntPtr handle) : base(handle)
        {
          //initialize list of phone numbers called for Call History screen
          PhoneNumbers = new List<string>();
        }

        public override void ViewDidLoad()
        {
          base.ViewDidLoad();
          // Perform any additional setup after loading the view, typically from a nib.

          TranslateButton.TouchUpInside += (object sender, EventArgs e) => {
            // Convert the phone number with text to a number
            // using PhoneTranslator.cs
            translatedNumber = PhoneTranslator.ToNumber(
              PhoneNumberText.Text);

            // Dismiss the keyboard if text field was tapped
            PhoneNumberText.ResignFirstResponder();

            if (translatedNumber == "")
            {
              CallButton.SetTitle("Call ", UIControlState.Normal);
              CallButton.Enabled = false;
            }
            else
            {
              CallButton.SetTitle("Call " + translatedNumber,
                UIControlState.Normal);
              CallButton.Enabled = true;
            }
          };

          CallButton.TouchUpInside += (object sender, EventArgs e) => {

            //Store the phone number that we're dialing in PhoneNumbers
            PhoneNumbers.Add(translatedNumber);

            // Use URL handler with tel: prefix to invoke Apple's Phone app...
            var url = new NSUrl("tel:" + translatedNumber);

            // otherwise show an alert dialog
            if (!UIApplication.SharedApplication.OpenUrl(url))
            {
              var alert = UIAlertController.Create("Not supported", "Scheme 'tel:' is not supported on this device", UIAlertControllerStyle.Alert);
              alert.AddAction(UIAlertAction.Create("Ok", UIAlertActionStyle.Default, null));
              PresentViewController(alert, true, null);
            }
          };
        }

        public override void PrepareForSegue(UIStoryboardSegue segue, NSObject sender)
        {
          base.PrepareForSegue(segue, sender);

          // set the View Controller that’s powering the screen we’re
          // transitioning to

          var callHistoryContoller = segue.DestinationViewController as CallHistoryController;

          //set the Table View Controller’s list of phone numbers to the
          // list of dialed phone numbers

          if (callHistoryContoller != null)
          {
            callHistoryContoller.PhoneNumbers = PhoneNumbers;
          }
        }
      }
    }
    ```

Quelques éléments méritent votre attention
  * La variable `translatedNumber` a été déplacée depuis la méthode `ViewDidLoad` vers une _variable de niveau de classe_.
  * Le code de **CallButton** a été modifié pour ajouter les numéros composés à la liste des numéros de téléphone en appelant `PhoneNumbers.Add(translatedNumber)`
  * La méthode `PrepareForSegue` a été ajoutée

  Enregistrez et générez l’application pour vérifier qu’il n’y a pas d’erreurs.

  Enregistrez et générez l’application pour vérifier qu’il n’y a pas d’erreurs.


20. Appuyez sur le bouton **Démarrer** pour lancer l’application dans le **simulateur iOS** :

  ![](hello-ios-multiscreen-quickstart-images/19.png "Premier écran de l’exemple d’application")


Félicitations ! Vous avez terminé votre première application Xamarin.iOS multi-écran.


-----

L’application peut à présent gérer la navigation à l’aide de Segues de Storyboard et dans le code. Le moment est maintenant venu d’éplucher les outils découverts et les compétences acquises tout au long du guide [Hello, iOS multi-écran - En profondeur](~/ios/get-started/hello-ios-multiscreen/hello-ios-multiscreen-deepdive.md).


## <a name="related-links"></a>Liens associés

- [Hello, iOS (exemple)](https://developer.xamarin.com/samples/monotouch/Hello_iOS/)
- [Lignes directrices de l’interface utilisateur iOS](http://developer.apple.com/library/ios/#documentation/UserExperience/Conceptual/MobileHIG/Introduction/Introduction.html)
- [Portail de provisionnement iOS](https://developer.apple.com/ios/manage/overview/index.action)
