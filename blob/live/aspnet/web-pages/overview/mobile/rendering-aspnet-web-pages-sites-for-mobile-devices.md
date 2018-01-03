---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: "Rendern von ASP.NET Web-Seiten (Razor)-Websites für Mobile Geräte | Microsoft Docs"
author: tfitzmac
description: "Dieser Artikel beschreibt, wie Seiten in einer ASP.NET Web Pages (Razor) Standort zu erstellen, die auf mobilen Geräten ordnungsgemäß gerendert werden. Sie lernen: Vorgehensweise Sie..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/17/2014
ms.topic: article
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: 08b714eb2ffaefc7c7e2e5c9a7428106b231e5b7
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/10/2017
---
<a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a><span data-ttu-id="44069-104">Rendern von ASP.NET Web Pages (Razor)-Websites für Mobile Geräte</span><span class="sxs-lookup"><span data-stu-id="44069-104">Rendering ASP.NET Web Pages (Razor) Sites for Mobile Devices</span></span>
====================
<span data-ttu-id="44069-105">durch [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="44069-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="44069-106">Dieser Artikel beschreibt, wie Seiten in einer ASP.NET Web Pages (Razor) Standort zu erstellen, die auf mobilen Geräten ordnungsgemäß gerendert werden.</span><span class="sxs-lookup"><span data-stu-id="44069-106">This article describes how to create pages in an ASP.NET Web Pages (Razor) site that will render appropriately on mobile devices.</span></span>
> 
> <span data-ttu-id="44069-107">Lernen Sie:</span><span class="sxs-lookup"><span data-stu-id="44069-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="44069-108">Wie Sie eine Benennungskonvention zu verwenden, um anzugeben, dass eine Seite, die speziell für mobile Geräte entwickelt wurde.</span><span class="sxs-lookup"><span data-stu-id="44069-108">How to use a naming convention to specify that a page is designed specifically for mobile devices.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="44069-109">In diesem Lernprogramm verwendeten Versionen der Software</span><span class="sxs-lookup"><span data-stu-id="44069-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="44069-110">ASP.NET Web Pages (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="44069-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="44069-111">Dieses Lernprogramm funktioniert auch mit ASP.NET Web Pages 2.</span><span class="sxs-lookup"><span data-stu-id="44069-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<span data-ttu-id="44069-112">ASP.NET Web Pages können Sie benutzerdefinierte zeigt zum Rendern von Inhalt auf Mobile oder anderen Geräten zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="44069-112">ASP.NET Web Pages lets you create custom displays for rendering content on mobile or other devices.</span></span>

<span data-ttu-id="44069-113">Die einfachste Möglichkeit zum Erstellen von gerätespezifischen-Seite in einer ASP.NET Web Pages-Website wird mit einem Dateibenennung Muster wie folgt: *FileName.* *Mobile**cshtml*.</span><span class="sxs-lookup"><span data-stu-id="44069-113">The simplest way to create device-specific page in an ASP.NET Web Pages site is by using a file-naming pattern like this: *FileName.**Mobile**.cshtml*.</span></span> <span data-ttu-id="44069-114">Sie können zwei Versionen einer Seite erstellen (z. B. eines Namens *MyFile.cshtml* und dasjenige mit dem Namen *MyFile.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="44069-114">You can create two versions of a page (for example, one named *MyFile.cshtml* and one named *MyFile.Mobile.cshtml*).</span></span> <span data-ttu-id="44069-115">Zur Laufzeit, wenn ein mobiles Gerät anfordert *MyFile.cshtml*, ASP.NET rendert den Inhalt von *MyFile.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="44069-115">At run time, when a mobile device requests *MyFile.cshtml*, ASP.NET renders the content from *MyFile.Mobile.cshtml*.</span></span> <span data-ttu-id="44069-116">Andernfalls *MyFile.cshtml* gerendert wird.</span><span class="sxs-lookup"><span data-stu-id="44069-116">Otherwise, *MyFile.cshtml* is rendered.</span></span>

<span data-ttu-id="44069-117">Das folgende Beispiel zeigt, wie mobile Rendering durch Hinzufügen einer Inhaltsseite für mobile Geräte aktivieren.</span><span class="sxs-lookup"><span data-stu-id="44069-117">The following example shows how to enable mobile rendering by adding a content page for mobile devices.</span></span> <span data-ttu-id="44069-118">*Page1.cshtml* enthält Inhalte sowie eine navigationsrandleiste.</span><span class="sxs-lookup"><span data-stu-id="44069-118">*Page1.cshtml* contains content plus a navigation sidebar.</span></span> <span data-ttu-id="44069-119">*Page1.Mobile.cshtml* den gleichen Inhalt enthält, lässt aber die Randleiste.</span><span class="sxs-lookup"><span data-stu-id="44069-119">*Page1.Mobile.cshtml* contains the same content, but omits the sidebar.</span></span>

1. <span data-ttu-id="44069-120">Erstellen Sie in einer ASP.NET Web Pages-Website, eine Datei namens *Page1.cshtml* , und Ersetzen Sie den aktuellen Inhalt durch Folgendes Markup.</span><span class="sxs-lookup"><span data-stu-id="44069-120">In an ASP.NET Web Pages site, create a file named *Page1.cshtml* and replace the current content with following markup.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. <span data-ttu-id="44069-121">Erstellen Sie eine Datei mit dem Namen *Page1.Mobile.cshtml* , und Ersetzen Sie den vorhandenen Inhalt durch Folgendes Markup.</span><span class="sxs-lookup"><span data-stu-id="44069-121">Create a file named *Page1.Mobile.cshtml* and replace the existing content with the following markup.</span></span> <span data-ttu-id="44069-122">Beachten Sie, dass die mobile Version der Seite im Abschnitt Navigation besser Rendern auf einen kleineren Bildschirm wird ausgelassen.</span><span class="sxs-lookup"><span data-stu-id="44069-122">Notice that the mobile version of the page omits the navigation section for better rendering on a smaller screen.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. <span data-ttu-id="44069-123">Führen Sie einen Desktopbrowser, und navigieren Sie zu *Page1.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="44069-123">Run a desktop browser and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="44069-124">![Mobilesites 1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="44069-124">![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span></span>
4. <span data-ttu-id="44069-125">Führen Sie einen mobilen Browser (oder einen Emulator für mobile Geräte), und navigieren Sie zu *Page1.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="44069-125">Run a mobile browser (or a mobile device emulator) and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="44069-126">(Beachten Sie, die Sie kein *.mobile.*</span><span class="sxs-lookup"><span data-stu-id="44069-126">(Notice that you do not include *.mobile.*</span></span> <span data-ttu-id="44069-127">als Teil der URL). Obwohl die Anforderung ist *Page1.cshtml*, rendert ASP.NET *Page1.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="44069-127">as part of the URL.) Even though the request is to *Page1.cshtml*, ASP.NET renders *Page1.Mobile.cshtml*.</span></span>

    ![Mobilesites 2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="44069-129">Um mobiler Seiten zu testen, können Sie einen Mobilgerät-Simulator aus, der auf einem desktop-Computer ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="44069-129">To test mobile pages, you can use a mobile device simulator that runs on a desktop computer.</span></span> <span data-ttu-id="44069-130">Mit diesem Tool können Sie die Webseiten zu testen, wie sie auf mobilen Geräten aussehen würde (d. h. in der Regel mit einer wesentlich kleineren anzeigen Bereich).</span><span class="sxs-lookup"><span data-stu-id="44069-130">This tool lets you test web pages as they would look on mobile devices (that is, typically with a much smaller display area).</span></span> <span data-ttu-id="44069-131">Ein Beispiel für einen Simulator ist die [Benutzer-Agent Switcher Add-on](http://addons.mozilla.org/en-us/firefox/addon/user-agent-switcher/) für Mozilla Firefox, dem können Sie die verschiedenen mobile Browsern aus einer desktop-Version von Firefox emulieren.</span><span class="sxs-lookup"><span data-stu-id="44069-131">One example of a simulator is the [User Agent Switcher add-on](http://addons.mozilla.org/en-us/firefox/addon/user-agent-switcher/) for Mozilla Firefox, which lets you emulate various mobile browsers from a desktop version of Firefox.</span></span>


<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="44069-132">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="44069-132">Additional Resources</span></span>


<span data-ttu-id="44069-133">[Windows Phone-Emulator](https://msdn.microsoft.com/en-us/library/ff402563(v=VS.92).aspx)</span><span class="sxs-lookup"><span data-stu-id="44069-133">[Windows Phone Emulator](https://msdn.microsoft.com/en-us/library/ff402563(v=VS.92).aspx)</span></span>