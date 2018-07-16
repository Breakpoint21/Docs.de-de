---
title: Erste Schritte mit Razor-Seiten in ASP.NET Core mit Visual Studio Code
author: rick-anderson
description: Erfahren Sie Grundlegendes über das Erstellen einer Razor-Seiten-Web-App in ASP-NET Core mit Visual Studio Code.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 08/27/2017
uid: tutorials/razor-pages-vsc/razor-pages-start
ms.openlocfilehash: b1f1dcc1401d707cff79f3269ab70b900e9fc21c
ms.sourcegitcommit: b8a2f14bf8dd346d7592977642b610bbcb0b0757
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2018
ms.locfileid: "38123382"
---
# <a name="get-started-with-aspnet-core-razor-pages-in-visual-studio-code"></a><span data-ttu-id="4bdec-103">Erste Schritte mit Razor-Seiten in ASP.NET Core mit Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="4bdec-103">Get started with ASP.NET Core Razor Pages in Visual Studio Code</span></span>

<span data-ttu-id="4bdec-104">Von [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="4bdec-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="4bdec-105">In diesem Tutorial lernen Sie Grundlegendes zur Erstellung einer ASP.NET Core-Webapp mit Razor Pages.</span><span class="sxs-lookup"><span data-stu-id="4bdec-105">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span> <span data-ttu-id="4bdec-106">Wir empfehlen Ihnen, zuerst das Tutorial [Introduction to Razor Pages (Einführung in Razor Pages)](xref:razor-pages/index) durchzuarbeiten, bevor Sie mit diesem Tutorial beginnen.</span><span class="sxs-lookup"><span data-stu-id="4bdec-106">We recommend you complete [Introduction to Razor Pages](xref:razor-pages/index) before starting this tutorial.</span></span> <span data-ttu-id="4bdec-107">Razor Pages sind der empfohlene Weg für die Erstellung von Benutzeroberflächen für Webanwendungen in ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="4bdec-107">Razor Pages is the recommended way to build UI for web applications in ASP.NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4bdec-108">Erforderliche Komponenten</span><span class="sxs-lookup"><span data-stu-id="4bdec-108">Prerequisites</span></span>

[!INCLUDE [](~/includes/net-core-prereqs-vscode.md)]

## <a name="create-a-razor-web-app"></a><span data-ttu-id="4bdec-109">Erstellen einer Razor-Web-App</span><span class="sxs-lookup"><span data-stu-id="4bdec-109">Create a Razor web app</span></span>

<span data-ttu-id="4bdec-110">Führen Sie über ein Terminal die folgenden Befehle aus:</span><span class="sxs-lookup"><span data-stu-id="4bdec-110">From a terminal, run the following commands:</span></span>

::: moniker range=">= aspnetcore-2.1"

```console
dotnet new webapp -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

[!INCLUDE[](~/includes/webapp-alias-notice.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```console
dotnet new razor -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

::: moniker-end

<span data-ttu-id="4bdec-111">Diese Befehle verwenden die [.NET Core-CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet), um ein Projekt mit Razor Pages zu erstellen und auszuführen.</span><span class="sxs-lookup"><span data-stu-id="4bdec-111">The preceding commands use the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet) to create and run a Razor Pages project.</span></span> <span data-ttu-id="4bdec-112">Öffnen Sie http://localhost:5000 in einem Browser, um sich die Anwendung anzeigen zu lassen.</span><span class="sxs-lookup"><span data-stu-id="4bdec-112">Open a browser to http://localhost:5000 to view the application.</span></span>

![Start- oder Indexseite](../razor-pages/razor-pages-start/_static/home.png)

[!INCLUDE [razor-pages-start](../../includes/RP/razor-pages-start.md)]

## <a name="open-the-project"></a><span data-ttu-id="4bdec-114">Öffnen des Projekts</span><span class="sxs-lookup"><span data-stu-id="4bdec-114">Open the project</span></span>

<span data-ttu-id="4bdec-115">Drücken Sie STRG+C, um die Anwendung zu beenden.</span><span class="sxs-lookup"><span data-stu-id="4bdec-115">Press Ctrl+C to shut down the application.</span></span>

<span data-ttu-id="4bdec-116">Klicken Sie in Visual Studio Code (VS Code) auf **Datei > Ordner öffnen**, und wählen Sie dann den Ordner *RazorPagesMovie* aus.</span><span class="sxs-lookup"><span data-stu-id="4bdec-116">From Visual Studio Code (VS Code), select **File > Open Folder**, and then select the *RazorPagesMovie* folder.</span></span>

- <span data-ttu-id="4bdec-117">Klicken Sie auf **Ja**, wenn die **Warnung** „Required assets to build and debug are missing from 'RazorPagesMovie'. Add them?“ („Die erforderlichen Objekte für die Erstellung und das Debugging sind in 'RazorPagesMovie' nicht vorhanden.</span><span class="sxs-lookup"><span data-stu-id="4bdec-117">Select **Yes** to the **Warn** message "Required assets to build and debug are missing from 'RazorPagesMovie'.</span></span> <span data-ttu-id="4bdec-118">Sollen Sie hinzugefügt werden?“) angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="4bdec-118">Add them?"</span></span>
- <span data-ttu-id="4bdec-119">Klicken Sie bei der **Infomeldung** „There are unresolved depedencies“ („Es bestehen ungelöste Abhängigkeiten“) auf **Wiederherstellen**.</span><span class="sxs-lookup"><span data-stu-id="4bdec-119">Select **Restore** to the **Info** message "There are unresolved dependencies".</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="4bdec-120">Starten der App</span><span class="sxs-lookup"><span data-stu-id="4bdec-120">Launch the app</span></span>

<span data-ttu-id="4bdec-121">Drücken Sie STRG+F5, um die App ohne Debugging zu starten.</span><span class="sxs-lookup"><span data-stu-id="4bdec-121">Press Ctrl+F5 to start the app without debugging.</span></span> <span data-ttu-id="4bdec-122">Alternativ können Sie auch über das Menü **Debuggen** die Option **Starten ohne Debugging** auswählen.</span><span class="sxs-lookup"><span data-stu-id="4bdec-122">Alternatively, from the **Debug** menu, select **Start Without Debugging**.</span></span>

<span data-ttu-id="4bdec-123">Im nächsten Tutorial fügen wir dem Projekt ein Modell hinzu.</span><span class="sxs-lookup"><span data-stu-id="4bdec-123">In the next tutorial, we add a model to the project.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="4bdec-124">Weiter: Hinzufügen eines Modells</span><span class="sxs-lookup"><span data-stu-id="4bdec-124">Next: Adding a model</span></span>](xref:tutorials/razor-pages-vsc/model)  
