---
uid: mvc/overview/getting-started/introduction/getting-started
title: Erste Schritte mit ASP.NET MVC 5 | Microsoft-Dokumentation
author: Rick-Anderson
description: 'Hinweis: Eine aktualisierte Version dieses Tutorials ist hier mithilfe von Visual Studio 2015 verfügbar. Das neue Tutorial verwendet die ASP.NET Core MVC 6, die viele Improvem bereitstellt...'
ms.author: riande
ms.date: 05/28/2015
ms.assetid: f3d8adbe-55e7-4fd4-84a8-7155bc45c676
msc.legacyurl: /mvc/overview/getting-started/introduction/getting-started
msc.type: authoredcontent
ms.openlocfilehash: 8417be945e16ed99e655f628134c9190429f1d67
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838025"
---
<a name="getting-started-with-aspnet-mvc-5"></a><span data-ttu-id="c56ad-104">Erste Schritte mit ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="c56ad-104">Getting Started with ASP.NET MVC 5</span></span>
====================
<span data-ttu-id="c56ad-105">durch [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="c56ad-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE [consider RP](../../../../includes/razor.md)]

 <span data-ttu-id="c56ad-106">Dieses Tutorial vermittelt Ihnen die Grundlagen zum Erstellen einer ASP.NET MVC 5 Web-app mit [Visual Studio 2017](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="c56ad-106">This tutorial will teach you the basics of building an ASP.NET MVC 5 web app using [Visual Studio 2017](https://www.visualstudio.com/).</span></span> <span data-ttu-id="c56ad-107">Letzte Quelle Tutorial befindet sich auf [GitHub](https://github.com/aspnet/Docs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie)</span><span class="sxs-lookup"><span data-stu-id="c56ad-107">Final Source for tutorial located on [GitHub](https://github.com/aspnet/Docs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie)</span></span>


 <span data-ttu-id="c56ad-108">In diesem Tutorial wurde von geschrieben [Scott Guthrie](https://weblogs.asp.net/scottgu/) (twitter-[ @scottgu ](https://twitter.com/scottgu) ), [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [ @shanselman ](https://twitter.com/shanselman) ) , und [Rick Anderson](https://twitter.com/RickAndMSFT) ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) )</span><span class="sxs-lookup"><span data-stu-id="c56ad-108">This tutorial was written by [Scott Guthrie](https://weblogs.asp.net/scottgu/) (twitter[@scottgu](https://twitter.com/scottgu) ), [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](https://twitter.com/shanselman) ), and [Rick Anderson](https://twitter.com/RickAndMSFT) ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )</span></span>

 <span data-ttu-id="c56ad-109">Sie benötigen ein Azure-Konto auf diese app in Azure bereit:</span><span class="sxs-lookup"><span data-stu-id="c56ad-109">You need an Azure account to deploy this app to Azure:</span></span>

 - <span data-ttu-id="c56ad-110">Sie können [öffnen Sie ein Azure-Konto kostenlos](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) – Sie erhalten ein Guthaben zum Ausprobieren Zahlungspflichtiger Azure-Dienste nutzen können, und auch nach dem sie verwendet werden, bis können Sie das Konto behalten und kostenlose Azure-Dienste.</span><span class="sxs-lookup"><span data-stu-id="c56ad-110">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
 - <span data-ttu-id="c56ad-111">Sie können [MSDN-abonnentenvorteile aktivieren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -Ihr MSDN-Abonnement ein monatliches Guthaben, die Sie für zahlungspflichtige Azure-Dienste verwenden können.</span><span class="sxs-lookup"><span data-stu-id="c56ad-111">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>


## <a name="getting-started"></a><span data-ttu-id="c56ad-112">Erste Schritte</span><span class="sxs-lookup"><span data-stu-id="c56ad-112">Getting Started</span></span>

<span data-ttu-id="c56ad-113">Zunächst installieren und Ausführen von [Visual Studio 2017](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="c56ad-113">Start by installing and running [Visual Studio 2017](https://www.visualstudio.com/).</span></span>

<span data-ttu-id="c56ad-114">Visual Studio ist eine IDE oder der integrierten Entwicklungsumgebung.</span><span class="sxs-lookup"><span data-stu-id="c56ad-114">Visual Studio is an IDE, or integrated development environment.</span></span> <span data-ttu-id="c56ad-115">Wie Sie Microsoft Word zum Schreiben von Dokumenten verwenden, verwenden Sie eine IDE, um Anwendungen zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="c56ad-115">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="c56ad-116">In Visual Studio ein, es gibt eine Liste entlang des unteren mit verschiedenen verfügbaren Optionen für Sie.</span><span class="sxs-lookup"><span data-stu-id="c56ad-116">In Visual Studio there's a list along the bottom showing various options available to you.</span></span> <span data-ttu-id="c56ad-117">Es gibt auch ein Menü, das eine andere Möglichkeit, Aufgaben in der IDE bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="c56ad-117">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="c56ad-118">(Z. B. anstelle **neues Projekt** aus der **starten** Seite können Sie das Menü und auswählen **Datei** &gt; **neues Projekt**.)</span><span class="sxs-lookup"><span data-stu-id="c56ad-118">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>


![](getting-started/_static/image1.png)  


## <a name="creating-your-first-application"></a><span data-ttu-id="c56ad-119">Erstellen Ihrer ersten Anwendung</span><span class="sxs-lookup"><span data-stu-id="c56ad-119">Creating Your First Application</span></span>

<span data-ttu-id="c56ad-120">Klicken Sie auf **neues Projekt**, wählen Sie dann Visual C# -Code auf der linken Seite, klicken Sie dann **Web** und wählen Sie dann **ASP.NET-Webanwendung ((.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="c56ad-120">Click **New Project**, then select Visual C# on the left, then **Web** and then select **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="c56ad-121">Benennen Sie das Projekt "MvcMovie", und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="c56ad-121">Name your project "MvcMovie" and then click **OK**.</span></span>

![](getting-started/_static/image2.png)

<span data-ttu-id="c56ad-122">In der **neues ASP.NET-Projekt** Dialogfeld klicken Sie auf **MVC** , und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="c56ad-122">In the **New ASP.NET Project** dialog, click **MVC** and then click **OK**.</span></span>

![](getting-started/_static/image3.png)

<span data-ttu-id="c56ad-123">Visual Studio verwendet eine Standardvorlage für das ASP.NET MVC-Projekt, das Sie gerade erstellt haben, müssen Sie eine funktionierende Anwendung jetzt ohne Benutzereingriff.</span><span class="sxs-lookup"><span data-stu-id="c56ad-123">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="c56ad-124">Dies ist eine einfache "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="c56ad-124">This is a simple "Hello World!"</span></span> <span data-ttu-id="c56ad-125">Projekt, und es ist ein guter Ausgangspunkt, um Ihre Anwendung zu starten.</span><span class="sxs-lookup"><span data-stu-id="c56ad-125">project, and it's a good place to start your application.</span></span>

![](getting-started/_static/image4.png)

<span data-ttu-id="c56ad-126">Klicken Sie auf F5, um mit dem Debuggen beginnen.</span><span class="sxs-lookup"><span data-stu-id="c56ad-126">Click F5 to start debugging.</span></span> <span data-ttu-id="c56ad-127">F5 wird in Visual Studio zu [IIS Express](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) , und führen Sie Ihre Web-app.</span><span class="sxs-lookup"><span data-stu-id="c56ad-127">F5 causes Visual Studio to start [IIS Express](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) and run your web app.</span></span> <span data-ttu-id="c56ad-128">Visual Studio klicken Sie dann einen Browser und Startseite der Anwendung wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="c56ad-128">Visual Studio then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="c56ad-129">Beachten Sie, dass mit dem Text die Adressleiste des Browsers `localhost:port#` und nicht etwas wie `example.com`.</span><span class="sxs-lookup"><span data-stu-id="c56ad-129">Notice that the address bar of the browser says `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="c56ad-130">Der Grund dafür ist `localhost` verweist immer auf Ihre eigenen lokalen Computer, die in diesem Fall die Anwendung ausgeführt wird Sie gerade erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="c56ad-130">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="c56ad-131">Wenn Visual Studio ein Webprojekt ausgeführt wird, wird ein zufälliger Port für den Webserver verwendet.</span><span class="sxs-lookup"><span data-stu-id="c56ad-131">When Visual Studio runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="c56ad-132">In der folgenden Abbildung ist die Nummer des Ports 1234.</span><span class="sxs-lookup"><span data-stu-id="c56ad-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="c56ad-133">Wenn Sie die Anwendung ausführen, sehen Sie eine andere Portnummer an.</span><span class="sxs-lookup"><span data-stu-id="c56ad-133">When you run the application, you'll see a different port number.</span></span>

![](getting-started/_static/image5.png)

<span data-ttu-id="c56ad-134">Anwendungstelemetriedaten bietet dieser Standardvorlage Seiten "Home", "Wenden Sie sich an" und "über.</span><span class="sxs-lookup"><span data-stu-id="c56ad-134">Right out of the box this default template gives you Home, Contact and About pages.</span></span> <span data-ttu-id="c56ad-135">In der Abbildung oben zeigt nicht an die **Startseite**, **zu** und **wenden Sie sich an** Links.</span><span class="sxs-lookup"><span data-stu-id="c56ad-135">The image above doesn't show the **Home**, **About** and **Contact** links.</span></span> <span data-ttu-id="c56ad-136">Je nach Größe Ihres Browserfensters müssen Sie auf das Symbol "berichtsnavigation", um die folgenden Links finden Sie unter.</span><span class="sxs-lookup"><span data-stu-id="c56ad-136">Depending on the size of your browser window, you might need to click the navigation icon to see these links.</span></span>

![](getting-started/_static/image6.png)  

<span data-ttu-id="c56ad-137">Die Anwendung liefert auch Support, um die Registrierung und Anmeldung.</span><span class="sxs-lookup"><span data-stu-id="c56ad-137">The application also provides support to register and log in.</span></span> <span data-ttu-id="c56ad-138">Der nächste Schritt besteht, zu ändern, wie diese Anwendung funktioniert, und erfahren etwas zu ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="c56ad-138">The next step is to change how this application works and learn a little bit about ASP.NET MVC.</span></span> <span data-ttu-id="c56ad-139">Schließen Sie die ASP.NET MVC-Anwendung, und Ändern von Code.</span><span class="sxs-lookup"><span data-stu-id="c56ad-139">Close the ASP.NET MVC application and let's change some code.</span></span>

<span data-ttu-id="c56ad-140">Eine Liste der aktuellen Lernprogramme, finden Sie unter [MVC Artikel empfohlen](../mvc-learning-sequence.md).</span><span class="sxs-lookup"><span data-stu-id="c56ad-140">For a list of current tutorials, see [MVC recommended articles](../mvc-learning-sequence.md).</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="c56ad-141">Finden Sie unter dieser App in Azure ausführen</span><span class="sxs-lookup"><span data-stu-id="c56ad-141">See this App Running on Azure</span></span>

<span data-ttu-id="c56ad-142">Möchten Sie die fertige Website als live-Web-app ausgeführt wird, finden Sie unter?</span><span class="sxs-lookup"><span data-stu-id="c56ad-142">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="c56ad-143">Sie können eine vollständige Version der app beim Azure-Konto bereitstellen, indem Sie einfach die folgende Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="c56ad-143">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](https://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?repository=https://github.com/aspnet/Docs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie&amp;WT.mc_id=deploy_azure_aspnet)

<span data-ttu-id="c56ad-144">Sie benötigen ein Azure-Konto zum Bereitstellen dieser Lösung in Azure.</span><span class="sxs-lookup"><span data-stu-id="c56ad-144">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="c56ad-145">Wenn Sie nicht bereits über ein Konto verfügen, müssen Sie die folgenden Optionen aus:</span><span class="sxs-lookup"><span data-stu-id="c56ad-145">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="c56ad-146">[Öffnen Sie ein Azure-Konto kostenlos](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) – Sie erhalten ein Guthaben zum Ausprobieren Zahlungspflichtiger Azure-Dienste nutzen können, und auch nach dem sie verwendet werden, bis können Sie das Konto behalten und kostenlose Azure-Dienste.</span><span class="sxs-lookup"><span data-stu-id="c56ad-146">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="c56ad-147">[MSDN-abonnentenvorteile aktivieren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -Ihr MSDN-Abonnement ein monatliches Guthaben, die Sie für zahlungspflichtige Azure-Dienste verwenden können.</span><span class="sxs-lookup"><span data-stu-id="c56ad-147">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c56ad-148">Nächste</span><span class="sxs-lookup"><span data-stu-id="c56ad-148">Next</span></span>](adding-a-controller.md)
