---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
title: "Remplissage dynamique d’un contrôle (VB) | Documents Microsoft"
author: wenz
description: "Le contrôle DynamicPopulate dans les outils de contrôle ASP.NET AJAX appelle un service web (ou une méthode de page) et remplit la valeur obtenue dans un contrôle cible t..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 27305347-7b5d-4519-97b7-197a357e7f6e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: ec0b6d429f3eb4a7243201c2a91adde462cf6345
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2017
---
<a name="dynamically-populating-a-control-vb"></a><span data-ttu-id="d0d23-103">Remplissage dynamique d’un contrôle (VB)</span><span class="sxs-lookup"><span data-stu-id="d0d23-103">Dynamically Populating a Control (VB)</span></span>
====================
<span data-ttu-id="d0d23-104">par [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="d0d23-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="d0d23-105">[Télécharger le Code](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip) ou [télécharger le PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="d0d23-105">[Download Code](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)</span></span>

> <span data-ttu-id="d0d23-106">Le contrôle DynamicPopulate dans les outils de contrôle ASP.NET AJAX appelle un service web (ou une méthode de page) et remplit la valeur obtenue dans un contrôle cible dans la page, sans une actualisation de la page.</span><span class="sxs-lookup"><span data-stu-id="d0d23-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span>


## <a name="overview"></a><span data-ttu-id="d0d23-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="d0d23-107">Overview</span></span>

<span data-ttu-id="d0d23-108">Le `DynamicPopulate` contrôle dans la boîte à outils de contrôle ASP.NET AJAX appelle un service web (ou une méthode de page) et remplit la valeur obtenue dans un contrôle cible dans la page, sans une actualisation de la page.</span><span class="sxs-lookup"><span data-stu-id="d0d23-108">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="d0d23-109">Ce didacticiel montre comment le configurer.</span><span class="sxs-lookup"><span data-stu-id="d0d23-109">This tutorial shows how to set this up.</span></span>

## <a name="steps"></a><span data-ttu-id="d0d23-110">Étapes</span><span class="sxs-lookup"><span data-stu-id="d0d23-110">Steps</span></span>

<span data-ttu-id="d0d23-111">Vous devez tout d’abord, Service Web ASP.NET qui implémente la méthode à être appelée par `DynamicPopulate`.</span><span class="sxs-lookup"><span data-stu-id="d0d23-111">First of all, you need an ASP.NET Web Service which implements the method to be called by `DynamicPopulate`.</span></span> <span data-ttu-id="d0d23-112">La classe de service web requiert le `ScriptService` attribut qui est défini dans `Microsoft.Web.Script.Services`; sinon ASP.NET AJAX ne peut pas créer le proxy JavaScript côté client pour le service web, qui à son tour, est requis par `DynamicPopulate`.</span><span class="sxs-lookup"><span data-stu-id="d0d23-112">The web service class requires the `ScriptService` attribute which is defined within `Microsoft.Web.Script.Services`; otherwise ASP.NET AJAX cannot create the client-side JavaScript proxy for the web service which in turn is required by `DynamicPopulate`.</span></span>

<span data-ttu-id="d0d23-113">La méthode web doit attendre un argument de type chaîne, appelée `contextKey`, étant donné que le `DynamicPopulate` contrôle envoie une partie des informations de contexte à chaque appel de service web.</span><span class="sxs-lookup"><span data-stu-id="d0d23-113">The web method must expect one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="d0d23-114">Le service web suivant retourne la date actuelle dans un format représenté par le `contextKey` argument :</span><span class="sxs-lookup"><span data-stu-id="d0d23-114">The following web service returns the current date in a format represented by the `contextKey` argument:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample1.aspx)]

<span data-ttu-id="d0d23-115">Le service web est ensuite enregistré en tant que `DynamicPopulate.vb.asmx`.</span><span class="sxs-lookup"><span data-stu-id="d0d23-115">The web service is then saved as `DynamicPopulate.vb.asmx`.</span></span> <span data-ttu-id="d0d23-116">Vous pouvez également implémenter la `getDate()` méthode comme méthode de page dans la page ASP.NET avec la `DynamicPopulate` contrôle.</span><span class="sxs-lookup"><span data-stu-id="d0d23-116">Alternatively, you could implement the `getDate()` method as a page method within the actual ASP.NET page with the `DynamicPopulate` control.</span></span>

<span data-ttu-id="d0d23-117">Dans l’étape suivante, créez un nouveau fichier ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d0d23-117">In the next step, create a new ASP.NET file.</span></span> <span data-ttu-id="d0d23-118">Comme toujours, la première étape consiste à inclure le `ScriptManager` dans la page en cours de chargement de la bibliothèque ASP.NET AJAX et faire le travail de la boîte à outils de contrôle :</span><span class="sxs-lookup"><span data-stu-id="d0d23-118">As always, the first step is to include the `ScriptManager` in the current page to load the ASP.NET AJAX library and to make the Control Toolkit work:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample2.aspx)]

<span data-ttu-id="d0d23-119">Ensuite, ajoutez un contrôle label (par exemple à l’aide du contrôle HTML portant le même nom, ou le &lt; `asp:Label`  / &gt; contrôle web) qui affichera ultérieurement le résultat de l’appel de service web.</span><span class="sxs-lookup"><span data-stu-id="d0d23-119">Then, add a label control (for instance using the HTML control of the same name, or the &lt;`asp:Label` /&gt; web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample3.aspx)]

<span data-ttu-id="d0d23-120">Un bouton HTML (comme un contrôle HTML, étant donné que nous ne nécessitent pas d’une publication sur le serveur) sera ensuite être utilisé pour déclencher l’alimentation dynamique :</span><span class="sxs-lookup"><span data-stu-id="d0d23-120">An HTML button (as an HTML control, since we do not require a postback to the server) will then be used to trigger the dynamic population:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample4.aspx)]

<span data-ttu-id="d0d23-121">Enfin, nous devons le `DynamicPopulateExtender` contrôle pour associer les choses.</span><span class="sxs-lookup"><span data-stu-id="d0d23-121">Finally, we need the `DynamicPopulateExtender` control to wire things up.</span></span> <span data-ttu-id="d0d23-122">Les attributs suivants seront définis (en dehors de celles évidents, `ID` et `runat` = `"server"`) :</span><span class="sxs-lookup"><span data-stu-id="d0d23-122">The following attributes will be set (apart from the obvious ones, `ID` and `runat`=`"server"`):</span></span>

- <span data-ttu-id="d0d23-123">`TargetControlID`où placer le résultat de l’appel de service web</span><span class="sxs-lookup"><span data-stu-id="d0d23-123">`TargetControlID` where to put the result from the web service call</span></span>
- <span data-ttu-id="d0d23-124">`ServicePath`chemin d’accès au service web (omettre si vous souhaitez utiliser une méthode de page)</span><span class="sxs-lookup"><span data-stu-id="d0d23-124">`ServicePath` path to the web service (omit if you want to use a page method)</span></span>
- <span data-ttu-id="d0d23-125">`ServiceMethod`nom de la méthode web ou d’une méthode de page</span><span class="sxs-lookup"><span data-stu-id="d0d23-125">`ServiceMethod` name of the web method or page method</span></span>
- <span data-ttu-id="d0d23-126">`ContextKey`informations de contexte à envoyer au service web</span><span class="sxs-lookup"><span data-stu-id="d0d23-126">`ContextKey` context information to be sent to the web service</span></span>
- <span data-ttu-id="d0d23-127">`PopulateTriggerControlID`élément qui déclenche l’appel de service web</span><span class="sxs-lookup"><span data-stu-id="d0d23-127">`PopulateTriggerControlID` element which triggers the web service call</span></span>
- <span data-ttu-id="d0d23-128">`ClearContentsDuringUpdate`s’il faut vider l’élément cible lors de l’appel de service web</span><span class="sxs-lookup"><span data-stu-id="d0d23-128">`ClearContentsDuringUpdate` whether to empty the target element during the web service call</span></span>

<span data-ttu-id="d0d23-129">Comme vous pouvez le voir, le contrôle requiert des informations mais tout la mise en place est assez simple.</span><span class="sxs-lookup"><span data-stu-id="d0d23-129">As you can see, the control requires some information but putting everything into place is quite straight-forward.</span></span> <span data-ttu-id="d0d23-130">Voici le balisage de la `DynamicPopulateExtender` contrôle dans le scénario en cours :</span><span class="sxs-lookup"><span data-stu-id="d0d23-130">Here is the markup for the `DynamicPopulateExtender` control in the current scenario:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample5.aspx)]

<span data-ttu-id="d0d23-131">Exécutez la page ASP.NET dans le navigateur, puis cliquez sur le bouton ; vous recevez la date actuelle au format de mois-jour-année.</span><span class="sxs-lookup"><span data-stu-id="d0d23-131">Run the ASP.NET page in the browser and click on the button; you will receive the current date in month-day-year format.</span></span>


<span data-ttu-id="d0d23-132">[![Un clic sur le bouton récupère la date à partir du serveur](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d0d23-132">[![A click on the button retrieves the date from the server](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="d0d23-133">Un clic sur le bouton récupère la date à partir du serveur ([cliquez pour afficher l’image en taille réelle](dynamically-populating-a-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="d0d23-133">A click on the button retrieves the date from the server ([Click to view full-size image](dynamically-populating-a-control-vb/_static/image3.png))</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="d0d23-134">[Précédent](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
[Suivant](dynamically-populating-a-control-using-javascript-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="d0d23-134">[Previous](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
[Next](dynamically-populating-a-control-using-javascript-code-vb.md)</span></span>