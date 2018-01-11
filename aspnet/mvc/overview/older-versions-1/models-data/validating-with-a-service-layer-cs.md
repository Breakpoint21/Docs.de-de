---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
title: "Überprüfen mit einer Dienstebene (c#) | Microsoft Docs"
author: StephenWalther
description: "Erfahren Sie, wie Ihre Validierungslogik aus Ihrer Controlleraktionen und in einer separaten Dienstebene zu verschieben. In diesem Lernprogramm Stephen Walther wird erläutert, wie Sie..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: 4eabc535-b8a1-43f5-bb99-cfeb86db0fca
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: f36301aef4377c6c00cb4fc33dbc5c57b1c426a9
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/10/2017
---
<a name="validating-with-a-service-layer-c"></a><span data-ttu-id="1afa1-104">Überprüfen mit einer Dienstebene (c#)</span><span class="sxs-lookup"><span data-stu-id="1afa1-104">Validating with a Service Layer (C#)</span></span>
====================
<span data-ttu-id="1afa1-105">durch [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="1afa1-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="1afa1-106">Erfahren Sie, wie Ihre Validierungslogik aus Ihrer Controlleraktionen und in einer separaten Dienstebene zu verschieben.</span><span class="sxs-lookup"><span data-stu-id="1afa1-106">Learn how to move your validation logic out of your controller actions and into a separate service layer.</span></span> <span data-ttu-id="1afa1-107">In diesem Lernprogramm wird Stephen Walther erläutert, wie Sie eine Spitze Trennung von Anliegen beibehalten können, indem die Dienstebene aus Ihrer Controller Layer isolieren.</span><span class="sxs-lookup"><span data-stu-id="1afa1-107">In this tutorial, Stephen Walther explains how you can maintain a sharp separation of concerns by isolating your service layer from your controller layer.</span></span>


<span data-ttu-id="1afa1-108">Das Ziel dieses Lernprogramms ist eine Methode zum Ausführen der Überprüfung in einer ASP.NET MVC-Anwendung beschreiben.</span><span class="sxs-lookup"><span data-stu-id="1afa1-108">The goal of this tutorial is to describe one method of performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="1afa1-109">In diesem Lernprogramm erfahren Sie, wie Ihre Validierungslogik aus Ihrem Domänencontroller und in einer separaten Dienstebene zu verschieben.</span><span class="sxs-lookup"><span data-stu-id="1afa1-109">In this tutorial, you learn how to move your validation logic out of your controllers and into a separate service layer.</span></span>

## <a name="separating-concerns"></a><span data-ttu-id="1afa1-110">Trennung von Anliegen</span><span class="sxs-lookup"><span data-stu-id="1afa1-110">Separating Concerns</span></span>

<span data-ttu-id="1afa1-111">Bei der Erstellung einer ASP.NET MVC-Anwendung sollten Sie Ihre Datenbanklogik nicht innerhalb der Controlleraktionen platzieren.</span><span class="sxs-lookup"><span data-stu-id="1afa1-111">When you build an ASP.NET MVC application, you should not place your database logic inside your controller actions.</span></span> <span data-ttu-id="1afa1-112">Mischen Ihre Datenbank und Controller-Logik macht Ihre Anwendung schwieriger, die im Zeitverlauf.</span><span class="sxs-lookup"><span data-stu-id="1afa1-112">Mixing your database and controller logic makes your application more difficult to maintain over time.</span></span> <span data-ttu-id="1afa1-113">Es wird empfohlen, dass Sie alle Ihre Datenbanklogik in einer separaten Repository Ebene platzieren.</span><span class="sxs-lookup"><span data-stu-id="1afa1-113">The recommendation is that you place all of your database logic in a separate repository layer.</span></span>

<span data-ttu-id="1afa1-114">Auflisten von 1 enthält beispielsweise ein einfaches Repository mit dem Namen der ProductRepository.</span><span class="sxs-lookup"><span data-stu-id="1afa1-114">For example, Listing 1 contains a simple repository named the ProductRepository.</span></span> <span data-ttu-id="1afa1-115">Die Produkt-Repository enthält alle Datenzugriffscode für die Anwendung.</span><span class="sxs-lookup"><span data-stu-id="1afa1-115">The product repository contains all of the data access code for the application.</span></span> <span data-ttu-id="1afa1-116">Die Liste enthält auch die IProductRepository-Schnittstelle, die das Produkt Repository implementiert.</span><span class="sxs-lookup"><span data-stu-id="1afa1-116">The listing also includes the IProductRepository interface that the product repository implements.</span></span>

<span data-ttu-id="1afa1-117">**1 – Models\ProductRepository.cs auflisten**</span><span class="sxs-lookup"><span data-stu-id="1afa1-117">**Listing 1 -- Models\ProductRepository.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample1.cs)]

<span data-ttu-id="1afa1-118">Der Controller im Codebeispiel 2 verwendet die Repository-Ebene für die Aktionen hinsichtlich der Index() und der Create()-.</span><span class="sxs-lookup"><span data-stu-id="1afa1-118">The controller in Listing 2 uses the repository layer in both its Index() and Create() actions.</span></span> <span data-ttu-id="1afa1-119">Beachten Sie, dass dieser Domänencontroller keine Datenbanklogik enthält.</span><span class="sxs-lookup"><span data-stu-id="1afa1-119">Notice that this controller does not contain any database logic.</span></span> <span data-ttu-id="1afa1-120">Erstellen eine Repository-Ebene können Sie eine klare Trennung von Anliegen zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="1afa1-120">Creating a repository layer enables you to maintain a clean separation of concerns.</span></span> <span data-ttu-id="1afa1-121">Controller für datenflusskontrolllogik von Anwendung verantwortlich sind, und das Repository ist für Datenzugriffslogik zuständig.</span><span class="sxs-lookup"><span data-stu-id="1afa1-121">Controllers are responsible for application flow control logic and the repository is responsible for data access logic.</span></span>

<span data-ttu-id="1afa1-122">**Auflisten von 2 – Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="1afa1-122">**Listing 2 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample2.cs)]

## <a name="creating-a-service-layer"></a><span data-ttu-id="1afa1-123">Erstellen einer Dienstebene</span><span class="sxs-lookup"><span data-stu-id="1afa1-123">Creating a Service Layer</span></span>

<span data-ttu-id="1afa1-124">Deshalb datenflusskontrolllogik von Anwendung gehört, in einem Controller und darauf von Datenzugriffslogik gehört, in einem Repository.</span><span class="sxs-lookup"><span data-stu-id="1afa1-124">So, application flow control logic belongs in a controller and data access logic belongs in a repository.</span></span> <span data-ttu-id="1afa1-125">In diesem Fall, in dem nehmen Sie Ihre Validierungslogik?</span><span class="sxs-lookup"><span data-stu-id="1afa1-125">In that case, where do you put your validation logic?</span></span> <span data-ttu-id="1afa1-126">Eine Möglichkeit besteht darin, platzieren Sie die Validierungslogik in einem *Dienstschicht*.</span><span class="sxs-lookup"><span data-stu-id="1afa1-126">One option is to place your validation logic in a *service layer*.</span></span>

<span data-ttu-id="1afa1-127">Eine Dienstebene ist eine zusätzliche Ebene in einer ASP.NET MVC-Anwendung, die Kommunikation zwischen einem Controller und Repository-Ebene vermittelt.</span><span class="sxs-lookup"><span data-stu-id="1afa1-127">A service layer is an additional layer in an ASP.NET MVC application that mediates communication between a controller and repository layer.</span></span> <span data-ttu-id="1afa1-128">Die Dienstebene enthält Geschäftslogik.</span><span class="sxs-lookup"><span data-stu-id="1afa1-128">The service layer contains business logic.</span></span> <span data-ttu-id="1afa1-129">Insbesondere enthält die Validierungslogik.</span><span class="sxs-lookup"><span data-stu-id="1afa1-129">In particular, it contains validation logic.</span></span>

<span data-ttu-id="1afa1-130">Beispielsweise verfügt die Product-Dienstebene auflisten 3 eine CreateProduct()-Methode.</span><span class="sxs-lookup"><span data-stu-id="1afa1-130">For example, the product service layer in Listing 3 has a CreateProduct() method.</span></span> <span data-ttu-id="1afa1-131">Die CreateProduct()-Methode ruft die ValidateProduct()-Methode, um ein neues Produkt zu überprüfen, bevor das Produkt mit der Produkt-Repository übergeben.</span><span class="sxs-lookup"><span data-stu-id="1afa1-131">The CreateProduct() method calls the ValidateProduct() method to validate a new product before passing the product to the product repository.</span></span>

<span data-ttu-id="1afa1-132">**3 – Models\ProductService.cs auflisten**</span><span class="sxs-lookup"><span data-stu-id="1afa1-132">**Listing 3 - Models\ProductService.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample3.cs)]

<span data-ttu-id="1afa1-133">Der Product-Controller wurde aktualisiert, 4 auflisten, die Dienstebene anstelle der Repository-Ebene verwendet.</span><span class="sxs-lookup"><span data-stu-id="1afa1-133">The Product controller has been updated in Listing 4 to use the service layer instead of the repository layer.</span></span> <span data-ttu-id="1afa1-134">Die Controller-Schicht kommuniziert mit der Dienstebene.</span><span class="sxs-lookup"><span data-stu-id="1afa1-134">The controller layer talks to the service layer.</span></span> <span data-ttu-id="1afa1-135">Die Dienstebene kommuniziert mit der Repository-Ebene.</span><span class="sxs-lookup"><span data-stu-id="1afa1-135">The service layer talks to the repository layer.</span></span> <span data-ttu-id="1afa1-136">Jede Ebene weist eine separaten Verantwortung.</span><span class="sxs-lookup"><span data-stu-id="1afa1-136">Each layer has a separate responsibility.</span></span>

<span data-ttu-id="1afa1-137">**4 – Controllers\ProductController.cs auflisten**</span><span class="sxs-lookup"><span data-stu-id="1afa1-137">**Listing 4 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample4.cs)]

<span data-ttu-id="1afa1-138">Beachten Sie, dass der Product-Dienst in der Product-Controller-Konstruktor erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="1afa1-138">Notice that the product service is created in the product controller constructor.</span></span> <span data-ttu-id="1afa1-139">Wenn der Product-Dienst erstellt wird, wird das Modellzustandswörterbuch an den Dienst übergeben.</span><span class="sxs-lookup"><span data-stu-id="1afa1-139">When the product service is created, the model state dictionary is passed to the service.</span></span> <span data-ttu-id="1afa1-140">Der Product-Dienst verwendet den Modellzustand Validierung Fehlermeldungen an den Controller zurückgesendet.</span><span class="sxs-lookup"><span data-stu-id="1afa1-140">The product service uses model state to pass validation error messages back to the controller.</span></span>

## <a name="decoupling-the-service-layer"></a><span data-ttu-id="1afa1-141">Trennen die Dienstebene</span><span class="sxs-lookup"><span data-stu-id="1afa1-141">Decoupling the Service Layer</span></span>

<span data-ttu-id="1afa1-142">Wir konnten nicht den Controller- und Dienst Ebenen in einen Bezug zu isolieren.</span><span class="sxs-lookup"><span data-stu-id="1afa1-142">We have failed to isolate the controller and service layers in one respect.</span></span> <span data-ttu-id="1afa1-143">Der Controller und die Dienst-Ebenen, kommunizieren über Modellstatus.</span><span class="sxs-lookup"><span data-stu-id="1afa1-143">The controller and service layers communicate through model state.</span></span> <span data-ttu-id="1afa1-144">Das heißt, hat die Dienstebene eine Abhängigkeit auf eine bestimmte Funktion von ASP.NET MVC-Framework.</span><span class="sxs-lookup"><span data-stu-id="1afa1-144">In other words, the service layer has a dependency on a particular feature of the ASP.NET MVC framework.</span></span>

<span data-ttu-id="1afa1-145">Wir möchten die Dienstebene aus unserem Controller Ebene so weit wie möglich zu isolieren.</span><span class="sxs-lookup"><span data-stu-id="1afa1-145">We want to isolate the service layer from our controller layer as much as possible.</span></span> <span data-ttu-id="1afa1-146">Theoretisch sollten wir die Dienstebene mit jedem Typ der Anwendung und nicht nur eine ASP.NET MVC-Anwendung verwenden können.</span><span class="sxs-lookup"><span data-stu-id="1afa1-146">In theory, we should be able to use the service layer with any type of application and not only an ASP.NET MVC application.</span></span> <span data-ttu-id="1afa1-147">In der Zukunft, wir möchten eine WPF-Front-End für die Anwendung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="1afa1-147">For example, in the future, we might want to build a WPF front-end for our application.</span></span> <span data-ttu-id="1afa1-148">Es sollte eine Möglichkeit zum Entfernen der Abhängigkeit von ASP.NET MVC Modellzustand aus unserem Dienstschicht gefunden.</span><span class="sxs-lookup"><span data-stu-id="1afa1-148">We should find a way to remove the dependency on ASP.NET MVC model state from our service layer.</span></span>

<span data-ttu-id="1afa1-149">Auflisten von 5 wurde die Dienstebene aktualisiert, sodass der Modellzustand nicht mehr verwendet.</span><span class="sxs-lookup"><span data-stu-id="1afa1-149">In Listing 5, the service layer has been updated so that it no longer uses model state.</span></span> <span data-ttu-id="1afa1-150">Stattdessen wird jede Klasse, die IValidationDictionary-Schnittstelle implementiert.</span><span class="sxs-lookup"><span data-stu-id="1afa1-150">Instead, it uses any class that implements the IValidationDictionary interface.</span></span>

<span data-ttu-id="1afa1-151">**Auflisten von 5 – Models\ProductService.cs (entkoppelt)**</span><span class="sxs-lookup"><span data-stu-id="1afa1-151">**Listing 5 - Models\ProductService.cs (decoupled)**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample5.cs)]

<span data-ttu-id="1afa1-152">Auflisten von 6 ist die IValidationDictionary-Schnittstelle definiert.</span><span class="sxs-lookup"><span data-stu-id="1afa1-152">The IValidationDictionary interface is defined in Listing 6.</span></span> <span data-ttu-id="1afa1-153">Diese einfache Schnittstelle verfügt über eine einzelne Methode und eine einzelne Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="1afa1-153">This simple interface has a single method and a single property.</span></span>

<span data-ttu-id="1afa1-154">**6 – Models\IValidationDictionary.cs auflisten**</span><span class="sxs-lookup"><span data-stu-id="1afa1-154">**Listing 6 - Models\IValidationDictionary.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample6.cs)]

<span data-ttu-id="1afa1-155">Die Klasse in 7 auflisten, mit dem Namen der Klasse ModelStateWrapper implementiert die IValidationDictionary-Schnittstelle.</span><span class="sxs-lookup"><span data-stu-id="1afa1-155">The class in Listing 7, named the ModelStateWrapper class, implements the IValidationDictionary interface.</span></span> <span data-ttu-id="1afa1-156">Sie können die ModelStateWrapper-Klasse instanziieren, indem eine Modellzustandswörterbuch an den Konstruktor übergeben.</span><span class="sxs-lookup"><span data-stu-id="1afa1-156">You can instantiate the ModelStateWrapper class by passing a model state dictionary to the constructor.</span></span>

<span data-ttu-id="1afa1-157">**Auflisten von 7 - Models\ModelStateWrapper.cs**</span><span class="sxs-lookup"><span data-stu-id="1afa1-157">**Listing 7 - Models\ModelStateWrapper.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample7.cs)]

<span data-ttu-id="1afa1-158">Schließlich verwendet der aktualisierte Controller in 8 Auflisten der ModelStateWrapper beim Erstellen von der Dienstebene in seinem Konstruktor.</span><span class="sxs-lookup"><span data-stu-id="1afa1-158">Finally, the updated controller in Listing 8 uses the ModelStateWrapper when creating the service layer in its constructor.</span></span>

<span data-ttu-id="1afa1-159">**Auflisten von 8 - Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="1afa1-159">**Listing 8 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample8.cs)]

<span data-ttu-id="1afa1-160">Mithilfe der IValidationDictionary können Schnittstelle und die Klasse ModelStateWrapper wir unsere Dienstebene aus unserem Controller Ebene vollständig zu isolieren.</span><span class="sxs-lookup"><span data-stu-id="1afa1-160">Using the IValidationDictionary interface and the ModelStateWrapper class enables us to completely isolate our service layer from our controller layer.</span></span> <span data-ttu-id="1afa1-161">Die Dienstebene ist nicht mehr Modellstatus abhängig.</span><span class="sxs-lookup"><span data-stu-id="1afa1-161">The service layer is no longer dependent on model state.</span></span> <span data-ttu-id="1afa1-162">Sie können eine beliebige Klasse übergeben, die um die Dienstebene der IValidationDictionary-Schnittstelle implementiert.</span><span class="sxs-lookup"><span data-stu-id="1afa1-162">You can pass any class that implements the IValidationDictionary interface to the service layer.</span></span> <span data-ttu-id="1afa1-163">Beispielsweise kann eine WPF-Anwendung die IValidationDictionary-Schnittstelle mit einer einfachen Auflistungsklasse implementieren.</span><span class="sxs-lookup"><span data-stu-id="1afa1-163">For example, a WPF application might implement the IValidationDictionary interface with a simple collection class.</span></span>

## <a name="summary"></a><span data-ttu-id="1afa1-164">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="1afa1-164">Summary</span></span>

<span data-ttu-id="1afa1-165">Das Ziel dieses Lernprogramms wurde ein Verfahren zur Ausführung der Validierung in ASP.NET MVC-Anwendung zu besprechen.</span><span class="sxs-lookup"><span data-stu-id="1afa1-165">The goal of this tutorial was to discuss one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="1afa1-166">In diesem Lernprogramm haben Sie gelernt, wie Sie alle Ihre Validierungslogik aus Ihrem Domänencontroller und in einer separaten Dienstebene zu verschieben.</span><span class="sxs-lookup"><span data-stu-id="1afa1-166">In this tutorial, you learned how to move all of your validation logic out of your controllers and into a separate service layer.</span></span> <span data-ttu-id="1afa1-167">Außerdem haben Sie gelernt, die Dienstebene aus Ihrer Controller Layer zu isolieren, indem Sie eine ModelStateWrapper-Klasse erstellen.</span><span class="sxs-lookup"><span data-stu-id="1afa1-167">You also learned how to isolate your service layer from your controller layer by creating a ModelStateWrapper class.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="1afa1-168">[Zurück](validating-with-the-idataerrorinfo-interface-cs.md)
[Weiter](validation-with-the-data-annotation-validators-cs.md)</span><span class="sxs-lookup"><span data-stu-id="1afa1-168">[Previous](validating-with-the-idataerrorinfo-interface-cs.md)
[Next](validation-with-the-data-annotation-validators-cs.md)</span></span>