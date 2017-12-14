---
uid: webhooks/receiving/receivers
title: "Récepteurs d’ASP.NET WebHooks | Documents Microsoft"
author: rick-anderson
description: "Récepteurs d’ASP.NET WebHooks"
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2012
ms.topic: article
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.technology: 
ms.prod: .net-framework
ms.openlocfilehash: 8c42db4056dd7a6ef77c7bcbc0eca3b5bf7c87e9
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2017
---
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="c6adf-103">Récepteurs d’ASP.NET WebHooks</span><span class="sxs-lookup"><span data-stu-id="c6adf-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="c6adf-104">Réception de WebHooks dépend de qui est l’expéditeur.</span><span class="sxs-lookup"><span data-stu-id="c6adf-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="c6adf-105">Il existe parfois des étapes supplémentaires que l’inscription d’un WebHook vérifier que l’abonné est réellement à l’écoute.</span><span class="sxs-lookup"><span data-stu-id="c6adf-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="c6adf-106">Certains WebHooks fournissent un modèle de pousser à tirer où la requête HTTP POST contient uniquement une référence pour les informations d’événement qui est ensuite être récupérés séparément.</span><span class="sxs-lookup"><span data-stu-id="c6adf-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="c6adf-107">Fréquence à laquelle le modèle de sécurité varie légèrement.</span><span class="sxs-lookup"><span data-stu-id="c6adf-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="c6adf-108">L’objectif de Microsoft ASP.NET WebHooks est plus simple et plus cohérente pour rattacher votre API sans perdre beaucoup de temps à déterminer comment gérer une variante particulière de WebHooks.</span><span class="sxs-lookup"><span data-stu-id="c6adf-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="c6adf-109">Un récepteur de WebHook est responsable de l’acceptation et la vérification de WebHooks à partir d’un expéditeur particulier.</span><span class="sxs-lookup"><span data-stu-id="c6adf-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="c6adf-110">Un récepteur de WebHook peut prendre en charge un nombre quelconque de WebHooks, chacune avec sa propre configuration.</span><span class="sxs-lookup"><span data-stu-id="c6adf-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="c6adf-111">Par exemple, le récepteur GitHub WebHook peut accepter des WebHooks à partir de n’importe quel nombre de dépôts GitHub.</span><span class="sxs-lookup"><span data-stu-id="c6adf-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="c6adf-112">URI du récepteur WebHook</span><span class="sxs-lookup"><span data-stu-id="c6adf-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="c6adf-113">En installant Microsoft ASP.NET WebHooks, vous obtenez un contrôleur de WebHook général qui accepte les requêtes de WebHook à partir d’un nombre très flexible de services.</span><span class="sxs-lookup"><span data-stu-id="c6adf-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="c6adf-114">Lorsqu’une demande arrive, il choisit le récepteur approprié que vous avez installés pour gérer un expéditeur WebHook.</span><span class="sxs-lookup"><span data-stu-id="c6adf-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="c6adf-115">L’URI de ce contrôleur est l’URI du WebHook qui vous inscrivez auprès du service et du formulaire :</span><span class="sxs-lookup"><span data-stu-id="c6adf-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="c6adf-116">Pour des raisons de sécurité, les différents destinataires WebHook nécessitent que l’URI est un *https* URI et dans certains cas, il doit également contenir un paramètre de requête supplémentaire qui est utilisé pour garantir que seul le destinataire prévu peut envoyer des WebHooks à l’URI ci-dessus .</span><span class="sxs-lookup"><span data-stu-id="c6adf-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="c6adf-117">Le  *<receiver>*  composant est le nom du destinataire, par exemple *github* ou *slack*.</span><span class="sxs-lookup"><span data-stu-id="c6adf-117">The *<receiver>* component is the name of the receiver, for example *github* or *slack*.</span></span>

<span data-ttu-id="c6adf-118">Le *{id}* est un identificateur facultatif qui peut servir à identifier une configuration de récepteur WebHook particulière.</span><span class="sxs-lookup"><span data-stu-id="c6adf-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="c6adf-119">Cela peut servir à inscrire le WebHooks N avec un récepteur spécifique.</span><span class="sxs-lookup"><span data-stu-id="c6adf-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="c6adf-120">Par exemple, les URI suivants de trois utilisable pour vous inscrire à trois WebHooks indépendants :</span><span class="sxs-lookup"><span data-stu-id="c6adf-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="c6adf-121">L’installation d’un récepteur de WebHook</span><span class="sxs-lookup"><span data-stu-id="c6adf-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="c6adf-122">Pour recevoir le WebHooks à l’aide de Microsoft ASP.NET WebHooks, vous d’abord installez le package Nuget pour l’ou les fournisseurs de que vous souhaitez recevoir des WebHooks à partir WebHook.</span><span class="sxs-lookup"><span data-stu-id="c6adf-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="c6adf-123">Les packages Nuget sont nommés [Microsoft.AspNet.WebHooks.Receivers.*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) où la dernière partie indique le service de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="c6adf-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="c6adf-124">Exemple :</span><span class="sxs-lookup"><span data-stu-id="c6adf-124">For example</span></span>

<span data-ttu-id="c6adf-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) fournit la prise en charge pour la réception de WebHooks à partir de GitHub et [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) fournit la prise en charge pour la réception des WebHooks généré par ASP. NET WebHooks.</span><span class="sxs-lookup"><span data-stu-id="c6adf-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="c6adf-126">Prêtes à l’emploi, vous pouvez trouver la prise en charge pour l’échange, GitHub, MailChimp, PayPal, Pusher, force de vente, la marge, Stripe, Trello et WordPress, mais il est possible de prendre en charge de n’importe quel nombre d’autres fournisseurs.</span><span class="sxs-lookup"><span data-stu-id="c6adf-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="c6adf-127">Configuration d’un récepteur de WebHook</span><span class="sxs-lookup"><span data-stu-id="c6adf-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="c6adf-128">Les récepteurs de WebHook sont configurés via la [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) l’interface et les implémentations de cette interface particuliers peuvent être inscrit à l’aide de n’importe quel modèle d’injection de dépendance.</span><span class="sxs-lookup"><span data-stu-id="c6adf-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="c6adf-129">L’implémentation par défaut utilise les paramètres d’Application qui peut être défini dans le fichier Web.config, ou, si vous utilisez des applications Web Azure, peut être défini via la [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c6adf-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![Paramètres de l’application Azure](_static/AzureAppSettings.png)

<span data-ttu-id="c6adf-131">Le format pour les clés de paramètre d’Application est la suivante :</span><span class="sxs-lookup"><span data-stu-id="c6adf-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="c6adf-132">La valeur est une liste séparée par des virgules des valeurs correspondant à la *{id}* valeurs pour lesquelles WebHooks ont été enregistrées, par exemple :</span><span class="sxs-lookup"><span data-stu-id="c6adf-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="c6adf-133">L’initialisation d’un récepteur de WebHook</span><span class="sxs-lookup"><span data-stu-id="c6adf-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="c6adf-134">Les récepteurs de WebHook sont initialisés en les enregistrant, généralement dans le *WebApiConfig* classe statique, par exemple :</span><span class="sxs-lookup"><span data-stu-id="c6adf-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

```csharp
namespace WebHookReceivers
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            // Load receivers
            config.InitializeReceiveGitHubWebHooks();
        }
    }
}
```