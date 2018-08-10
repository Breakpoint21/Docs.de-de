---
title: DevOps mit ASP.NET Core und Azure
author: CamSoper
description: Ein Leitfaden, der End-to-End-Anleitungen zum Erstellen einer DevOps-Pipeline für eine in Azure gehostete ASP.NET Core-App bereitstellt.
ms.author: casoper
ms.date: 08/07/2018
uid: azure/devops/index
ms.openlocfilehash: 09ca835e908e81c6f38f9430fb40638ba6dc3350
ms.sourcegitcommit: 29dfe436f54a27fbb4f6494bc639d16c75001fab
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2018
ms.locfileid: "39722537"
---
# <a name="devops-with-aspnet-core-and-azure"></a><span data-ttu-id="74da4-103">DevOps mit ASP.NET Core und Azure</span><span class="sxs-lookup"><span data-stu-id="74da4-103">DevOps with ASP.NET Core and Azure</span></span>

<span data-ttu-id="74da4-104">Willkommen zum Leitfaden für den Azure-Entwicklungslebenszyklus für .NET!</span><span class="sxs-lookup"><span data-stu-id="74da4-104">Welcome to the Azure Development Lifecycle guide for .NET!</span></span> <span data-ttu-id="74da4-105">In diesem Leitfaden werden die grundlegenden Konzepte zum Erstellen eines Entwicklungslebenszyklus für Azure mithilfe von .NET-Tools und -Prozessen vorgestellt.</span><span class="sxs-lookup"><span data-stu-id="74da4-105">This guide introduces the basic concepts of building a development lifecycle around Azure using .NET tools and processes.</span></span> <span data-ttu-id="74da4-106">Nach Abschluss dieses Leitfadens können Sie die Vorteile einer ausgereiften DevOps-Toolkette nutzen.</span><span class="sxs-lookup"><span data-stu-id="74da4-106">After finishing this guide, you'll reap the benefits of a mature DevOps toolchain.</span></span>

## <a name="who-this-guide-is-for"></a><span data-ttu-id="74da4-107">Für wen ist dieser Leitfaden gedacht?</span><span class="sxs-lookup"><span data-stu-id="74da4-107">Who this guide is for</span></span>

<span data-ttu-id="74da4-108">Sie sollten ein erfahrener ASP.NET-Entwickler (auf Ebene 200–300) sein.</span><span class="sxs-lookup"><span data-stu-id="74da4-108">You should be an experienced ASP.NET developer (200-300 level).</span></span> <span data-ttu-id="74da4-109">Sie müssen nicht mit Azure vertraut sein, da dieses Thema in der Einführung behandelt wird.</span><span class="sxs-lookup"><span data-stu-id="74da4-109">You don't need to know anything about Azure, as we'll cover that in this introduction.</span></span> <span data-ttu-id="74da4-110">DevOps-Techniker, die sich eher auf die Vorgänge als auf die Entwicklung konzentrieren, können ebenso von diesem Leitfaden profitieren.</span><span class="sxs-lookup"><span data-stu-id="74da4-110">This guide may also be useful for DevOps engineers who are more focused on operations than development.</span></span>

<span data-ttu-id="74da4-111">Dieser Leitfaden ist für Windows-Entwickler konzipiert.</span><span class="sxs-lookup"><span data-stu-id="74da4-111">This guide targets Windows developers.</span></span> <span data-ttu-id="74da4-112">Linux und macOS werden jedoch vollständig von .NET Core unterstützt.</span><span class="sxs-lookup"><span data-stu-id="74da4-112">However, Linux and macOS are fully supported by .NET Core.</span></span> <span data-ttu-id="74da4-113">Um diesen Leitfaden für Linux bzw. macOS zu nutzen, beachten Sie die Anzeigen für Linux-/macOS-Unterschiede.</span><span class="sxs-lookup"><span data-stu-id="74da4-113">To adapt this guide for Linux/macOS, watch for callouts for Linux/macOS differences.</span></span>

## <a name="what-this-guide-doesnt-cover"></a><span data-ttu-id="74da4-114">Was in diesem Leitfaden nicht behandelt wird</span><span class="sxs-lookup"><span data-stu-id="74da4-114">What this guide doesn't cover</span></span>

<span data-ttu-id="74da4-115">Er bezieht sich auf eine kontinuierliche End-to-End-Bereitstellungserfahrung für .NET-Entwickler.</span><span class="sxs-lookup"><span data-stu-id="74da4-115">This guide is focused on an end-to-end continuous deployment experience for .NET developers.</span></span> <span data-ttu-id="74da4-116">Es handelt sich nicht um eine vollständige Anleitung für alle Azure-Themen sowie für .NET-APIs für Azure-Dienste.</span><span class="sxs-lookup"><span data-stu-id="74da4-116">It's not an exhaustive guide to all things Azure, and it doesn't focus extensively on .NET APIs for Azure services.</span></span> <span data-ttu-id="74da4-117">Der Schwerpunkt liegt vor allem bei der Continuous Integration, der Bereitstellung, der Überwachung und dem Debuggen.</span><span class="sxs-lookup"><span data-stu-id="74da4-117">The emphasis is all around continuous integration, deployment, monitoring, and debugging.</span></span> <span data-ttu-id="74da4-118">Gegen Ende dieses Leitfadens finden Sie Empfehlungen für weitere Schritte.</span><span class="sxs-lookup"><span data-stu-id="74da4-118">Near the end of the guide, recommendations for next steps are offered.</span></span> <span data-ttu-id="74da4-119">Darin enthalten sind Azure-Plattformdienste, die für ASP.NET-Entwickler nützlich sind.</span><span class="sxs-lookup"><span data-stu-id="74da4-119">Included in the suggestions are Azure platform services that are useful to ASP.NET developers.</span></span>

## <a name="whats-in-this-guide"></a><span data-ttu-id="74da4-120">In diesem Handbuch</span><span class="sxs-lookup"><span data-stu-id="74da4-120">What's in this guide</span></span>

### <a name="tools-and-downloadsxrefazuredevopstools-and-downloads"></a>[<span data-ttu-id="74da4-121">Tools und Downloads</span><span class="sxs-lookup"><span data-stu-id="74da4-121">Tools and downloads</span></span>](xref:azure/devops/tools-and-downloads)

<span data-ttu-id="74da4-122">Erfahren Sie, wo die in diesem Leitfaden verwendeten Tools abgerufen werden können.</span><span class="sxs-lookup"><span data-stu-id="74da4-122">Learn where to acquire the tools used in this guide.</span></span>

### <a name="deploy-to-app-servicexrefazuredevopsdeploy-to-app-service"></a>[<span data-ttu-id="74da4-123">Bereitstellen in App Service</span><span class="sxs-lookup"><span data-stu-id="74da4-123">Deploy to App Service</span></span>](xref:azure/devops/deploy-to-app-service)

<span data-ttu-id="74da4-124">Informationen zu den verschiedenen Methoden zum Bereitstellen einer ASP.NET Core-App zu Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="74da4-124">Learn the various methods for deploying an ASP.NET Core app to Azure App Service.</span></span>

### <a name="continuous-integration-and-deploymentxrefazuredevopscicd"></a>[<span data-ttu-id="74da4-125">Continuous Integration und Continuous Deployment</span><span class="sxs-lookup"><span data-stu-id="74da4-125">Continuous integration and deployment</span></span>](xref:azure/devops/cicd)

<span data-ttu-id="74da4-126">Stellen Sie eine End-to-End-Lösung für Continuous Integration und Continuous Deployment für Ihre ASP.NET Core-App mit GitHub, VSTS und Azure bereit.</span><span class="sxs-lookup"><span data-stu-id="74da4-126">Build an end-to-end continuous integration and deployment solution for your ASP.NET Core app with GitHub, VSTS, and Azure.</span></span>

### <a name="monitor-and-debugxrefazuredevopsmonitor"></a>[<span data-ttu-id="74da4-127">Überwachen und Debuggen</span><span class="sxs-lookup"><span data-stu-id="74da4-127">Monitor and debug</span></span>](xref:azure/devops/monitor)

<span data-ttu-id="74da4-128">Verwenden Sie Azure-Tools zum Überwachen, Optimieren und für die Problembehandlung Ihrer Anwendung.</span><span class="sxs-lookup"><span data-stu-id="74da4-128">Use Azure's tools to monitor, troubleshoot, and tune your application.</span></span>

### <a name="next-stepsxrefazuredevopsnext-steps"></a>[<span data-ttu-id="74da4-129">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="74da4-129">Next steps</span></span>](xref:azure/devops/next-steps)

<span data-ttu-id="74da4-130">Andere Lernpfade für die ASP.NET Core-Entwickler, die sich mit Azure vertraut machen.</span><span class="sxs-lookup"><span data-stu-id="74da4-130">Other learning paths for the ASP.NET Core developer learning Azure.</span></span>

## <a name="acknowledgments"></a><span data-ttu-id="74da4-131">Danksagungen</span><span class="sxs-lookup"><span data-stu-id="74da4-131">Acknowledgments</span></span>

<span data-ttu-id="74da4-132">Vielen Dank an die Personen in der .NET-Community, die zu diesem Leitfaden mit nützlichen Vorschlägen beigetragen haben.</span><span class="sxs-lookup"><span data-stu-id="74da4-132">Thank you to everyone in the .NET community who contributed to this guide with helpful suggestions!</span></span> <span data-ttu-id="74da4-133">Wir möchten besonders den folgenden Communitymitgliedern danken, die bei der letzten Überprüfung dieses Materials mitgearbeitet haben:</span><span class="sxs-lookup"><span data-stu-id="74da4-133">We'd like to specifically thank the following community members who contributed to the final review of this material:</span></span>

* [<span data-ttu-id="74da4-134">Sam Wronski</span><span class="sxs-lookup"><span data-stu-id="74da4-134">Sam Wronski</span></span>](https://www.youtube.com/c/worldofzerodevelopment)
* [<span data-ttu-id="74da4-135">Jeffrey Palermo</span><span class="sxs-lookup"><span data-stu-id="74da4-135">Jeffrey Palermo</span></span>](https://twitter.com/jeffreypalermo)

## <a name="conclusion"></a><span data-ttu-id="74da4-136">Schlussbemerkung</span><span class="sxs-lookup"><span data-stu-id="74da4-136">Conclusion</span></span>

<span data-ttu-id="74da4-137">Dieser Leitfaden bereitet Sie auf die Erstellung eines Continuous Integration-Entwicklungslebenszyklus vor, der auf ASP.NET Core und Azure App Service basiert.</span><span class="sxs-lookup"><span data-stu-id="74da4-137">This guide prepares you to build a continuous integration development lifecycle built around ASP.NET Core and Azure App Service.</span></span>

## <a name="additional-reading"></a><span data-ttu-id="74da4-138">Weiterführende Literatur</span><span class="sxs-lookup"><span data-stu-id="74da4-138">Additional reading</span></span>

* [<span data-ttu-id="74da4-139">Was ist Cloud Computing?</span><span class="sxs-lookup"><span data-stu-id="74da4-139">What is Cloud Computing?</span></span>](https://azure.microsoft.com/overview/what-is-cloud-computing/)
* [<span data-ttu-id="74da4-140">Examples of Cloud Computing (Beispiele für Cloud Computing)</span><span class="sxs-lookup"><span data-stu-id="74da4-140">Examples of Cloud Computing</span></span>](https://azure.microsoft.com/overview/examples-of-cloud-computing/)
* [<span data-ttu-id="74da4-141">Was ist IaaS?</span><span class="sxs-lookup"><span data-stu-id="74da4-141">What is IaaS?</span></span>](https://azure.microsoft.com/overview/what-is-iaas/)
* [<span data-ttu-id="74da4-142">Was ist PaaS?</span><span class="sxs-lookup"><span data-stu-id="74da4-142">What is PaaS?</span></span>](https://azure.microsoft.com/overview/what-is-paas/)
