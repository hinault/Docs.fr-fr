---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: "Affichant la vidéo dans ASP.NET Web Pages (Razor) Site | Documents Microsoft"
author: tfitzmac
description: "Ce chapitre explique comment afficher la vidéo dans un ASP.NET Web Pages avec la page de syntaxe Razor."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: 0e1849fb780908b55520d8108e2227d046759987
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2017
---
<a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="4307e-103">Affichant la vidéo dans un Site de Pages (Razor) Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4307e-103">Displaying Video in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="4307e-104">par [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="4307e-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="4307e-105">Cet article explique comment utiliser un lecteur vidéo (multimédia) dans un site Web ASP.NET Web Pages (Razor) pour permettre aux utilisateurs d’afficher les vidéos qui sont stockés sur le site.</span><span class="sxs-lookup"><span data-stu-id="4307e-105">This article explains how to use a video (media) player in an ASP.NET Web Pages (Razor) website to let users view videos that are stored on the site.</span></span> <span data-ttu-id="4307e-106">ASP.NET Web Pages avec syntaxe Razor vous permet de lire le disque mémoire Flash (*.swf*), Media Player (*.wmv*) et Silverlight (*.xap*) vidéos.</span><span class="sxs-lookup"><span data-stu-id="4307e-106">ASP.NET Web Pages with Razor syntax lets you play Flash (*.swf*), Media Player (*.wmv*), and Silverlight (*.xap*) videos.</span></span>
> 
> <span data-ttu-id="4307e-107">Ce que vous allez apprendre :</span><span class="sxs-lookup"><span data-stu-id="4307e-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="4307e-108">Comment choisir un lecteur vidéo.</span><span class="sxs-lookup"><span data-stu-id="4307e-108">How to choose a video player.</span></span>
> - <span data-ttu-id="4307e-109">Comment ajouter une vidéo à une page web.</span><span class="sxs-lookup"><span data-stu-id="4307e-109">How to add video to a web page.</span></span>
> - <span data-ttu-id="4307e-110">Comment définir les attributs de lecteur vidéo.</span><span class="sxs-lookup"><span data-stu-id="4307e-110">How to set video player attributes.</span></span>
> 
> <span data-ttu-id="4307e-111">Il s’agit de Razor ASP.NET pages fonctionnalités introduites dans l’article :</span><span class="sxs-lookup"><span data-stu-id="4307e-111">These are the ASP.NET Razor pages features introduced in the article:</span></span>
> 
> - <span data-ttu-id="4307e-112">Le `Video` helper.</span><span class="sxs-lookup"><span data-stu-id="4307e-112">The `Video` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="4307e-113">Versions du logiciel utilisées dans le didacticiel</span><span class="sxs-lookup"><span data-stu-id="4307e-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="4307e-114">Pages Web ASP.NET (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="4307e-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="4307e-115">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="4307e-115">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="4307e-116">Ce didacticiel fonctionne également avec WebMatrix 3.</span><span class="sxs-lookup"><span data-stu-id="4307e-116">This tutorial also works with WebMatrix 3.</span></span>


## <a name="introduction"></a><span data-ttu-id="4307e-117">Introduction</span><span class="sxs-lookup"><span data-stu-id="4307e-117">Introduction</span></span>

<span data-ttu-id="4307e-118">Vous pouvez souhaiter afficher une vidéo sur votre site.</span><span class="sxs-lookup"><span data-stu-id="4307e-118">You might want to display a video on your site.</span></span> <span data-ttu-id="4307e-119">Une manière de procéder consiste à lier à un site qui a déjà la vidéo, comme YouTube.</span><span class="sxs-lookup"><span data-stu-id="4307e-119">One way to do that is to link to a site that already has the video, like YouTube.</span></span> <span data-ttu-id="4307e-120">Si vous souhaitez incorporer une vidéo à partir de ces sites directement dans vos propres pages, vous pouvez généralement obtenir le balisage HTML à partir du site et copiez-le dans votre page.</span><span class="sxs-lookup"><span data-stu-id="4307e-120">If you want to embed a video from these sites directly in your own pages, you can usually get HTML markup from the site and then copy it into your page.</span></span> <span data-ttu-id="4307e-121">Par exemple, l’exemple suivant montre comment incorporer un YouTube vidéo :</span><span class="sxs-lookup"><span data-stu-id="4307e-121">For example, the following example shows how to embed a YouTube video:</span></span>

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

<span data-ttu-id="4307e-122">Si vous souhaitez lire une vidéo qui se trouve sur votre site Web (et non sur un site de partage de vidéo public), vous ne peut pas lier directement à l’aide du balisage incorporé comme suit.</span><span class="sxs-lookup"><span data-stu-id="4307e-122">If you want to play a video that's on your own website (not on a public video-sharing site), you can't directly link to it using embedded markup like this.</span></span> <span data-ttu-id="4307e-123">Toutefois, vous pouvez lire des vidéos à partir de votre site à l’aide de la `Video` assistance, qui restitue un lecteur multimédia directement dans une page.</span><span class="sxs-lookup"><span data-stu-id="4307e-123">However, you can play videos from your site by using the `Video` helper, which renders a media player directly in a page.</span></span>

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a><span data-ttu-id="4307e-124">Choix d’un lecteur vidéo</span><span class="sxs-lookup"><span data-stu-id="4307e-124">Choosing a Video Player</span></span>

<span data-ttu-id="4307e-125">Il existe un grand nombre de formats pour les fichiers vidéo, et chaque format nécessite généralement un autre lecteur et une manière différente pour configurer le lecteur.</span><span class="sxs-lookup"><span data-stu-id="4307e-125">There are lots of formats for video files, and each format typically requires a different player and a different way to configure the player.</span></span> <span data-ttu-id="4307e-126">Dans les pages ASP.NET Razor, vous pouvez lire une vidéo dans une page web à l’aide de la `Video` helper.</span><span class="sxs-lookup"><span data-stu-id="4307e-126">In ASP.NET Razor pages, you can play a video in a web page using the `Video` helper.</span></span> <span data-ttu-id="4307e-127">Le `Video` helper simplifie le processus d’incorporation de vidéos dans une page web, car il génère automatiquement le `object` et `embed` des éléments HTML qui sont normalement utilisés pour ajouter une vidéo à la page.</span><span class="sxs-lookup"><span data-stu-id="4307e-127">The `Video` helper simplifies the process of embedding videos in a web page because it automatically generates the `object` and `embed` HTML elements that are normally used to add video to the page.</span></span>

<span data-ttu-id="4307e-128">Le `Video` helper prend en charge les lecteurs multimédias suivants :</span><span class="sxs-lookup"><span data-stu-id="4307e-128">The `Video` helper supports the following media players:</span></span>

- <span data-ttu-id="4307e-129">Adobe Flash</span><span class="sxs-lookup"><span data-stu-id="4307e-129">Adobe Flash</span></span>
- <span data-ttu-id="4307e-130">Windows MediaPlayer</span><span class="sxs-lookup"><span data-stu-id="4307e-130">Windows MediaPlayer</span></span>
- <span data-ttu-id="4307e-131">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="4307e-131">Microsoft Silverlight</span></span>

### <a name="the-flash-player"></a><span data-ttu-id="4307e-132">Le lecteur Flash</span><span class="sxs-lookup"><span data-stu-id="4307e-132">The Flash Player</span></span>

<span data-ttu-id="4307e-133">Le `Flash` lecteur de la `Video` assistance vous permettent de lire des vidéos Flash (*.swf* fichiers) dans une page web.</span><span class="sxs-lookup"><span data-stu-id="4307e-133">The `Flash` player of the `Video` helper let you play Flash videos (*.swf* files) in a web page.</span></span> <span data-ttu-id="4307e-134">Au minimum, vous devez fournir un chemin d’accès au fichier vidéo.</span><span class="sxs-lookup"><span data-stu-id="4307e-134">At a minimum, you have to provide a path to the video file.</span></span> <span data-ttu-id="4307e-135">Si vous spécifiez rien d’autre que le chemin d’accès, le lecteur utilise les valeurs par défaut qui sont définies par la version actuelle de Flash.</span><span class="sxs-lookup"><span data-stu-id="4307e-135">If you specify nothing but the path, the player uses default values that are set by the current version of Flash.</span></span> <span data-ttu-id="4307e-136">Les paramètres par défaut sont :</span><span class="sxs-lookup"><span data-stu-id="4307e-136">Typical default settings are:</span></span>

- <span data-ttu-id="4307e-137">La vidéo est affichée à l’aide de la largeur de la valeur par défaut et sa hauteur et sans une couleur d’arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="4307e-137">The video is displayed using its default width and height and without a background color.</span></span>
- <span data-ttu-id="4307e-138">La vidéo est lue automatiquement lors de la charge de la page.</span><span class="sxs-lookup"><span data-stu-id="4307e-138">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="4307e-139">Les boucles de la vidéo en continu jusqu'à ce qu’il est arrêté de manière explicite.</span><span class="sxs-lookup"><span data-stu-id="4307e-139">The video loops continuously until it's explicitly stopped.</span></span>
- <span data-ttu-id="4307e-140">La vidéo est mis à l’échelle pour afficher l’intégralité de la vidéo, au lieu de rognage pour s’ajuster à une taille spécifique.</span><span class="sxs-lookup"><span data-stu-id="4307e-140">The video is scaled to show all of the video, rather than cropping the video to fit a specific size.</span></span>
- <span data-ttu-id="4307e-141">La vidéo est lue dans une fenêtre.</span><span class="sxs-lookup"><span data-stu-id="4307e-141">The video plays in a window.</span></span>

### <a name="the-mediaplayer-player"></a><span data-ttu-id="4307e-142">Le lecteur MediaPlayer</span><span class="sxs-lookup"><span data-stu-id="4307e-142">The MediaPlayer Player</span></span>

<span data-ttu-id="4307e-143">Le `MediaPlayer` lecteur de la `Video` assistance vous permet de lire les vidéos Windows Media (*.wmv* fichiers), Windows Media audio (*.wma* fichiers) et MP3 (*.mp3* les fichiers) dans une page web.</span><span class="sxs-lookup"><span data-stu-id="4307e-143">The `MediaPlayer` player of the `Video` helper lets you play Windows Media videos (*.wmv* files), Windows Media audio (*.wma* files), and MP3 (*.mp3* files) in a web page.</span></span> <span data-ttu-id="4307e-144">Vous devez inclure le chemin d’accès du fichier multimédia à lire ; tous les autres paramètres sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="4307e-144">You must include path of the media file to play; all other parameters are optional.</span></span> <span data-ttu-id="4307e-145">Si vous spécifiez uniquement un chemin d’accès, le lecteur utilise les paramètres par défaut définies par la version actuelle de MediaPlayer, telle que :</span><span class="sxs-lookup"><span data-stu-id="4307e-145">If you specify only a path, the player uses default settings set by the current version of MediaPlayer, such as:</span></span>

- <span data-ttu-id="4307e-146">La vidéo est affichée à l’aide de la largeur de la valeur par défaut et sa hauteur.</span><span class="sxs-lookup"><span data-stu-id="4307e-146">The video is displayed using its default width and height.</span></span>
- <span data-ttu-id="4307e-147">La vidéo est lue automatiquement lors de la charge de la page.</span><span class="sxs-lookup"><span data-stu-id="4307e-147">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="4307e-148">La vidéo est lue une fois (elle ne de boucle).</span><span class="sxs-lookup"><span data-stu-id="4307e-148">The video plays once (it doesn't loop).</span></span>
- <span data-ttu-id="4307e-149">Le lecteur affiche l’ensemble des contrôles dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4307e-149">The player displays the full set of controls in the user interface.</span></span>
- <span data-ttu-id="4307e-150">La vidéo est lue une fenêtre.</span><span class="sxs-lookup"><span data-stu-id="4307e-150">The video plays in in a window.</span></span>

### <a name="the-silverlight-player"></a><span data-ttu-id="4307e-151">Le lecteur Silverlight</span><span class="sxs-lookup"><span data-stu-id="4307e-151">The Silverlight Player</span></span>

<span data-ttu-id="4307e-152">Le `Silverlight` lecteur de la `Video` assistance vous permet de lire la vidéo Windows Media (*.wmv* fichiers), Windows Media Audio (*.wma* fichiers) et MP3 (*.mp3* fichiers).</span><span class="sxs-lookup"><span data-stu-id="4307e-152">The `Silverlight` player of the `Video` helper lets you play Windows Media Video (*.wmv* files), Windows Media Audio (*.wma* files), and MP3 (*.mp3* files).</span></span> <span data-ttu-id="4307e-153">Vous devez définir le paramètre de chemin d’accès pointe vers un package d’application basée sur Silverlight (*.xap* fichier).</span><span class="sxs-lookup"><span data-stu-id="4307e-153">You must set the path parameter to point to a Silverlight-based application package (*.xap* file).</span></span> <span data-ttu-id="4307e-154">Vous devez également définir les paramètres de largeur et hauteur.</span><span class="sxs-lookup"><span data-stu-id="4307e-154">You also must set the width and height parameters.</span></span> <span data-ttu-id="4307e-155">Tous les autres paramètres sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="4307e-155">All other parameters are optional.</span></span> <span data-ttu-id="4307e-156">Lorsque vous utilisez le lecteur Silverlight pour la vidéo, si vous affectez uniquement les paramètres requis, le lecteur Silverlight affiche la vidéo sans une couleur d’arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="4307e-156">When you use the Silverlight player for video, if you set only the required parameters, the Silverlight player displays the video without a background color.</span></span>

> [!NOTE]
> <span data-ttu-id="4307e-157">Dans le cas où vous ne connaissez pas déjà Silverlight : le *.xap* fichier est un fichier compressé qui contient des instructions de mise en page dans un *.xaml* de fichiers, le code managé dans des assemblys et des ressources facultatives.</span><span class="sxs-lookup"><span data-stu-id="4307e-157">In case you don't already know Silverlight: the *.xap* file is a compressed file that contains layout instructions in a *.xaml* file, managed code in assemblies, and optional resources.</span></span> <span data-ttu-id="4307e-158">Vous pouvez créer un *.xap* fichier dans Visual Studio en tant qu’un projet d’application Silverlight.</span><span class="sxs-lookup"><span data-stu-id="4307e-158">You can create a *.xap* file in Visual Studio as a Silverlight application project.</span></span>


<span data-ttu-id="4307e-159">Le `Silverlight` lecteur vidéo utilise à la fois les paramètres que vous fournissez pour le lecteur et les paramètres qui sont fournis dans le *.xap* fichier.</span><span class="sxs-lookup"><span data-stu-id="4307e-159">The `Silverlight` video player uses both the settings that you provide for the player and the settings that are provided in the *.xap* file.</span></span>

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a><span data-ttu-id="4307e-160">Types MIME</span><span class="sxs-lookup"><span data-stu-id="4307e-160">MIME Types</span></span>
> 
> <span data-ttu-id="4307e-161">Lorsqu’un navigateur télécharge un fichier, le navigateur permet de s’assurer que le type de fichier correspond au type MIME spécifié pour le document qui est rendu.</span><span class="sxs-lookup"><span data-stu-id="4307e-161">When a browser downloads a file, the browser makes sure that the file type matches the MIME type that's specified for the document that's being rendered.</span></span> <span data-ttu-id="4307e-162">Le type MIME est le type de contenu de type ou le support d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="4307e-162">The MIME type is the content type or media type of a file.</span></span> <span data-ttu-id="4307e-163">Le `Video` assistance utilise les types MIME suivants :</span><span class="sxs-lookup"><span data-stu-id="4307e-163">The `Video` helper uses the following MIME types:</span></span>
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`


<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a><span data-ttu-id="4307e-164">Lecture de vidéos de Flash (.swf)</span><span class="sxs-lookup"><span data-stu-id="4307e-164">Playing Flash (.swf) Videos</span></span>

<span data-ttu-id="4307e-165">Cette procédure vous montre comment lire une vidéo Flash nommée *sample.swf*.</span><span class="sxs-lookup"><span data-stu-id="4307e-165">This procedure shows you how to play a Flash video named *sample.swf*.</span></span> <span data-ttu-id="4307e-166">La procédure suppose que vous avez sélectionné un dossier nommé *Media* sur votre site et que le *.swf* fichier se trouve dans ce dossier.</span><span class="sxs-lookup"><span data-stu-id="4307e-166">The procedure assumes that you've got a folder named *Media* on your site and that the *.swf* file is in that folder.</span></span>

1. <span data-ttu-id="4307e-167">Ajoutez la bibliothèque de programmes d’assistance ASP.NET Web à votre site Web, comme décrit dans [programmes d’assistance de l’installation dans un Site de Pages Web ASP.NET](https://go.microsoft.com/fwlink/?LinkId=252372), si vous n’avez pas déjà ajouté.</span><span class="sxs-lookup"><span data-stu-id="4307e-167">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="4307e-168">Dans le site Web, ajoutez une page et nommez-le *FlashVideo.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="4307e-168">In the website, add a page and name it *FlashVideo.cshtml*.</span></span>
3. <span data-ttu-id="4307e-169">Ajoutez le balisage suivant à la page :</span><span class="sxs-lookup"><span data-stu-id="4307e-169">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. <span data-ttu-id="4307e-170">Exécutez la page dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="4307e-170">Run the page in a browser.</span></span> <span data-ttu-id="4307e-171">(Assurez-vous que la page est sélectionnée dans le **fichiers** espace de travail avant de l’exécuter.) La page s’affiche et la vidéo est lue automatiquement.</span><span class="sxs-lookup"><span data-stu-id="4307e-171">(Make sure the page is selected in the **Files** workspace before you run it.) The page is displayed and the video plays automatically.</span></span> 

    <span data-ttu-id="4307e-172">![[image] ] (10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")</span><span class="sxs-lookup"><span data-stu-id="4307e-172">![[image]](10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")</span></span>

<span data-ttu-id="4307e-173">Vous pouvez définir le `quality` paramètre pour une vidéo Flash à `low`, `autolow`, `autohigh`, `medium`, `high`, et `best`:</span><span class="sxs-lookup"><span data-stu-id="4307e-173">You can set the `quality` parameter for a Flash video to `low`, `autolow`, `autohigh`, `medium`, `high`, and `best`:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

<span data-ttu-id="4307e-174">Vous pouvez modifier la disque mémoire Flash vidéo est lue à une taille spécifique à l’aide de le `scale` paramètre que vous pouvez définir pour les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4307e-174">You can change the Flash video to play at a specific size using the `scale` parameter, which you can set to the following:</span></span>

- <span data-ttu-id="4307e-175">`showall`.</span><span class="sxs-lookup"><span data-stu-id="4307e-175">`showall`.</span></span> <span data-ttu-id="4307e-176">Cela rend la vidéo complète visible tout en conservant les proportions d’origine.</span><span class="sxs-lookup"><span data-stu-id="4307e-176">This makes the entire video visible while maintaining the original aspect ratio.</span></span> <span data-ttu-id="4307e-177">Toutefois, vous pouvez obtenir des bordures de chaque côté.</span><span class="sxs-lookup"><span data-stu-id="4307e-177">However, you might end up with borders on each side.</span></span>
- <span data-ttu-id="4307e-178">`noorder`.</span><span class="sxs-lookup"><span data-stu-id="4307e-178">`noorder`.</span></span> <span data-ttu-id="4307e-179">Cela met à l’échelle la vidéo tout en conservant les proportions d’origine, mais il peut être tronqué.</span><span class="sxs-lookup"><span data-stu-id="4307e-179">This scales the video while maintaining the original aspect ratio, but it might be cropped.</span></span>
- <span data-ttu-id="4307e-180">`exactfit`.</span><span class="sxs-lookup"><span data-stu-id="4307e-180">`exactfit`.</span></span> <span data-ttu-id="4307e-181">Cela rend la vidéo complète visible sans conserver les proportions d’origine, mais la distorsion peut se produire.</span><span class="sxs-lookup"><span data-stu-id="4307e-181">This makes the entire video visible without preserving the original aspect ratio, but distortion may occur.</span></span>

<span data-ttu-id="4307e-182">Si vous ne spécifiez pas un `scale` paramètre, la vidéo complète sera visible et les proportions d’origine est conservée sans découpage.</span><span class="sxs-lookup"><span data-stu-id="4307e-182">If you don't specify a `scale` parameter, the entire video will be visible and the original aspect ratio will be maintained without any cropping.</span></span> <span data-ttu-id="4307e-183">L’exemple suivant montre comment utiliser le `scale` paramètre :</span><span class="sxs-lookup"><span data-stu-id="4307e-183">The following example shows how to use the `scale` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

<span data-ttu-id="4307e-184">Le lecteur Flash prend en charge un paramètre nommé de mode vidéo `windowMode`.</span><span class="sxs-lookup"><span data-stu-id="4307e-184">The Flash player supports a video mode setting named `windowMode`.</span></span> <span data-ttu-id="4307e-185">Vous pouvez définir cette option `window`, `opaque`, et `transparent`.</span><span class="sxs-lookup"><span data-stu-id="4307e-185">You can set this to `window`, `opaque`, and `transparent`.</span></span> <span data-ttu-id="4307e-186">Par défaut, le `windowMode` a la valeur `window`, qui affiche la vidéo dans une fenêtre distincte sur la page web.</span><span class="sxs-lookup"><span data-stu-id="4307e-186">By default, the `windowMode` is set to `window`, which displays the video in a separate window on the web page.</span></span> <span data-ttu-id="4307e-187">Le `opaque` paramètre masque tout derrière la vidéo sur la page web.</span><span class="sxs-lookup"><span data-stu-id="4307e-187">The `opaque` setting hides everything behind the video on the web page.</span></span> <span data-ttu-id="4307e-188">Le `transparent` paramètre permet l’arrière-plan de la page web dans la vidéo, en supposant que n’importe quelle partie de la vidéo est transparente.</span><span class="sxs-lookup"><span data-stu-id="4307e-188">The `transparent` setting lets the background of the web page show through the video, assuming any part of the video is transparent.</span></span>

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a><span data-ttu-id="4307e-189">Lecture MediaPlayer (*.wmv*) vidéos</span><span class="sxs-lookup"><span data-stu-id="4307e-189">Playing MediaPlayer (*.wmv*) Videos</span></span>

<span data-ttu-id="4307e-190">La procédure suivante vous montre comment lire une vidéo de la fenêtre support nommée *sample.wmv* qui se trouve dans le *Media* dossier.</span><span class="sxs-lookup"><span data-stu-id="4307e-190">The following procedure shows you how to play a Window Media video named *sample.wmv* that's in the *Media* folder.</span></span>

1. <span data-ttu-id="4307e-191">Ajoutez la bibliothèque de programmes d’assistance ASP.NET Web à votre site Web, comme décrit dans [programmes d’assistance de l’installation dans un Site de Pages Web ASP.NET](https://go.microsoft.com/fwlink/?LinkId=252372), si vous n’avez pas encore.</span><span class="sxs-lookup"><span data-stu-id="4307e-191">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="4307e-192">Créer une nouvelle page nommée *MediaPlayerVideo.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="4307e-192">Create a new page named *MediaPlayerVideo.cshtml*.</span></span>
3. <span data-ttu-id="4307e-193">Ajoutez le balisage suivant à la page :</span><span class="sxs-lookup"><span data-stu-id="4307e-193">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. <span data-ttu-id="4307e-194">Exécutez la page dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="4307e-194">Run the page in a browser.</span></span> <span data-ttu-id="4307e-195">La vidéo charge et lit automatiquement.</span><span class="sxs-lookup"><span data-stu-id="4307e-195">The video loads and plays automatically.</span></span> 

    <span data-ttu-id="4307e-196">![[image] ] (10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")</span><span class="sxs-lookup"><span data-stu-id="4307e-196">![[image]](10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")</span></span>

<span data-ttu-id="4307e-197">Vous pouvez définir `playCount` vers un entier qui indique combien de fois pour lire la vidéo automatiquement :</span><span class="sxs-lookup"><span data-stu-id="4307e-197">You can set `playCount` to an integer that indicates how many times to play the video automatically:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

<span data-ttu-id="4307e-198">Le `uiMode` paramètre vous permet de spécifier les contrôles qui apparaissent dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4307e-198">The `uiMode` parameter lets you specify which controls show up in the user interface.</span></span> <span data-ttu-id="4307e-199">Vous pouvez définir `uiMode` à `invisible`, `none`, `mini`, ou `full`.</span><span class="sxs-lookup"><span data-stu-id="4307e-199">You can set `uiMode` to `invisible`, `none`, `mini`, or `full`.</span></span> <span data-ttu-id="4307e-200">Si vous ne spécifiez pas un `uiMode` paramètre, la vidéo sera affiché avec la fenêtre d’état, de recherche de la barre, contrôler les boutons et les contrôles de volume en plus de la fenêtre de la vidéo.</span><span class="sxs-lookup"><span data-stu-id="4307e-200">If you don't specify a `uiMode` parameter, the video will be displayed with the status window, seek bar, control buttons, and volume controls in addition to the video window.</span></span> <span data-ttu-id="4307e-201">Ces contrôles affichera également si vous utilisez le lecteur pour lire un fichier audio.</span><span class="sxs-lookup"><span data-stu-id="4307e-201">These controls will also be displayed if you use the player to play an audio file.</span></span> <span data-ttu-id="4307e-202">Voici un exemple montrant comment utiliser le `uiMode` paramètre :</span><span class="sxs-lookup"><span data-stu-id="4307e-202">Here's an example of how to use the `uiMode` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

<span data-ttu-id="4307e-203">Par défaut, audio est activé lorsque la vidéo est lue.</span><span class="sxs-lookup"><span data-stu-id="4307e-203">By default, audio is on when the video plays.</span></span> <span data-ttu-id="4307e-204">Vous pouvez désactiver l’audio en définissant le `mute` valeur true au paramètre :</span><span class="sxs-lookup"><span data-stu-id="4307e-204">You can mute the audio by setting the `mute` parameter to true:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

<span data-ttu-id="4307e-205">Vous pouvez contrôler le niveau audio de la vidéo MediaPlayer en définissant le `volume` paramètre à une valeur comprise entre 0 et 100.</span><span class="sxs-lookup"><span data-stu-id="4307e-205">You can control the audio level of the MediaPlayer video by setting the `volume` parameter to a value between 0 and 100.</span></span> <span data-ttu-id="4307e-206">La valeur par défaut est 50.</span><span class="sxs-lookup"><span data-stu-id="4307e-206">The default value is 50.</span></span> <span data-ttu-id="4307e-207">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="4307e-207">Here's an example:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a><span data-ttu-id="4307e-208">Lecture de vidéos de Silverlight</span><span class="sxs-lookup"><span data-stu-id="4307e-208">Playing Silverlight Videos</span></span>

<span data-ttu-id="4307e-209">Cette procédure vous montre comment lire une vidéo de contenu dans un Silverlight *.xap* page se trouve dans un dossier nommée *Media*.</span><span class="sxs-lookup"><span data-stu-id="4307e-209">This procedure shows you how to play video contained in a Silverlight *.xap* page that's in a folder named *Media*.</span></span>

1. <span data-ttu-id="4307e-210">Ajoutez la bibliothèque de programmes d’assistance ASP.NET Web à votre site Web, comme décrit dans [programmes d’assistance de l’installation dans un Site de Pages Web ASP.NET](https://go.microsoft.com/fwlink/?LinkId=252372), si vous n’avez pas encore.</span><span class="sxs-lookup"><span data-stu-id="4307e-210">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already .</span></span>
2. <span data-ttu-id="4307e-211">Créer une nouvelle page nommée *SilverlightVideo.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="4307e-211">Create a new page named *SilverlightVideo.cshtml*.</span></span>
3. <span data-ttu-id="4307e-212">Ajoutez le balisage suivant à la page :</span><span class="sxs-lookup"><span data-stu-id="4307e-212">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. <span data-ttu-id="4307e-213">Exécutez la page dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="4307e-213">Run the page in a browser.</span></span> 

    <span data-ttu-id="4307e-214">![[image] ] (10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")</span><span class="sxs-lookup"><span data-stu-id="4307e-214">![[image]](10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="4307e-215">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4307e-215">Additional Resources</span></span>


<span data-ttu-id="4307e-216">[Vue d’ensemble de Silverlight](https://msdn.microsoft.com/en-us/library/bb404700(VS.95).aspx)</span><span class="sxs-lookup"><span data-stu-id="4307e-216">[Silverlight Overview](https://msdn.microsoft.com/en-us/library/bb404700(VS.95).aspx)</span></span>

[<span data-ttu-id="4307e-217">Attributs de balise d’objet et incorporer un périphérique flash</span><span class="sxs-lookup"><span data-stu-id="4307e-217">Flash OBJECT and EMBED tag attributes</span></span>](http://kb2.adobe.com/cps/127/tn_12701.html)

<span data-ttu-id="4307e-218">[Les balises PARAM de kit de développement logiciel Windows Media Player 11](https://msdn.microsoft.com/en-us/library/aa392321(VS.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="4307e-218">[Windows Media Player 11 SDK PARAM Tags](https://msdn.microsoft.com/en-us/library/aa392321(VS.85).aspx)</span></span>