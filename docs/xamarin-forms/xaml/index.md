---
title: Application XAML eXtensible Markup Language)
description: XAML est un langage de balisage déclaratif qui peut être utilisé pour définir les interfaces utilisateur. L’interface utilisateur est défini dans un fichier XML à l’aide de la syntaxe XAML, le comportement d’exécution est définie dans un fichier code-behind distinct.
ms.prod: xamarin
ms.assetid: CD30EECC-8AC1-4CF5-A4FE-348420A6231E
ms.technology: xamarin-forms
author: charlespetzold
ms.author: chape
ms.date: 06/18/2018
ms.openlocfilehash: c040c12829708418d0a705b8e9f930989900c678
ms.sourcegitcommit: 7a89735aed9ddf89c855fd33928915d72da40c2d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36209425"
---
# <a name="extensible-application-markup-language-xaml"></a>Application XAML eXtensible Markup Language)

_XAML est un langage de balisage déclaratif qui peut être utilisé pour définir les interfaces utilisateur. L’interface utilisateur est défini dans un fichier XML à l’aide de la syntaxe XAML, le comportement d’exécution est définie dans un fichier code-behind distinct._

> [!VIDEO https://youtube.com/embed/H6UOrSyhTEE]

**Faire évoluer 2016 : Devenir un maître de XAML**

> [!NOTE]
> Essayer la [XAML Standard Preview](standard/index.md)

<a name="xaml" />

## <a name="xaml-basicsxaml-basicsindexmd"></a>[Notions de base XAML](xaml-basics/index.md)

XAML permet aux développeurs de définir les interfaces utilisateur dans les applications de Xamarin.Forms à l’aide de balisage plutôt que du code. XAML n’est jamais nécessaire dans un programme de Xamarin.Forms, mais il est compatible avec les outils et est souvent plus cohérente visuellement et plus concise que le code équivalent. XAML est particulièrement bien adapté pour une utilisation avec l’architecture d’application Model-View-ViewModel (MVVM) populaires : code XAML qui définit la vue qui est liée au code de ViewModel par le biais des liaisons de données basée sur XAML.

## <a name="xaml-compilationxamlcmd"></a>[Compilation XAML](xamlc.md)

XAML peut être éventuellement compilé directement en langage intermédiaire (IL) avec le compilateur XAML (XAMLC). Cet article explique comment utiliser XAMLC et ses avantages.

## <a name="xaml-previewerxaml-previewermd"></a>[Générateur d’aperçu XAML](xaml-previewer.md)

Le [XAML aperçu](~/xamarin-forms/xaml/xaml-previewer.md) lors 2016 évoluer de Xamarin est disponible pour le test dans le canal Alpha.

## <a name="xaml-namespacesnamespacesmd"></a>[Espaces de noms XAML](namespaces.md)

XAML utilise le `xmlns` attribut XML pour les déclarations d’espace de noms. Cet article présente la syntaxe d’espace de noms XAML et montre comment déclarer un espace de noms XAML pour un type d’accès.

## <a name="xaml-markup-extensionsmarkup-extensionsindexmd"></a>[Extensions de balisage XAML](markup-extensions/index.md)

Le code XAML inclut des extensions de balisage pour la définition des attributs à des valeurs ou objets au-delà de ce qui peut être exprimé avec des chaînes simples. Ceux-ci incluent le référencement de constantes, les propriétés statiques et les champs, les dictionnaires de ressources et des liaisons de données.

## <a name="field-modifiersfield-modifiersmd"></a>[Modificateurs de champ](field-modifiers.md)

Le `x:FieldModifier` attribut namespace Spécifie le niveau d’accès pour les champs générés pour les éléments XAML nommés.

## <a name="passing-argumentspassing-argumentsmd"></a>[Passage d’arguments](passing-arguments.md)

XAML peut être utilisé pour passer des arguments pour les constructeurs par défaut ou aux méthodes de fabrique. Cet article décrit à l’aide d’attributs XAML qui peuvent être utilisés pour passer des arguments aux constructeurs, pour appeler des méthodes de fabrique et pour spécifier le type d’argument générique.

## <a name="bindable-propertiesbindable-propertiesmd"></a>[Propriétés pouvant être liées](bindable-properties.md)

Dans Xamarin.Forms, les fonctionnalités des common language runtime (CLR) sont étendue par les propriétés pouvant être liées. Une propriété est un type spécial de propriété, où la valeur de propriété est suivie par le système de propriétés de Xamarin.Forms. Cet article présente les propriétés pouvant être liées et montre comment créer et les utiliser.

## <a name="attached-propertiesattached-propertiesmd"></a>[Propriétés jointes](attached-properties.md)

Une propriété jointe est un type spécial de propriété pouvant être liée, définie dans une classe mais est associé à d’autres objets et reconnaissable dans XAML en tant qu’attribut qui contient une classe et un nom de propriété séparés par un point. Cet article fournit une introduction aux propriétés jointes et montre comment créer et les utiliser.

## <a name="resource-dictionariesresource-dictionariesmd"></a>[Dictionnaires de ressources](resource-dictionaries.md)

Ressources XAML sont des définitions d’objets qui peuvent être utilisés plusieurs fois. A [ `ResourceDictionary` ](https://developer.xamarin.com/api/type/Xamarin.Forms.ResourceDictionary/) permet aux ressources d’être définis dans un emplacement unique et réutilisées dans une application de Xamarin.Forms. Cet article explique comment créer et utiliser un `ResourceDictionary`et comment fusionner `ResourceDictionary` dans un autre.
