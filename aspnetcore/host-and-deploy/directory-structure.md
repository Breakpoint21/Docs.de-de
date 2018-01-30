---
title: ASP.NET Core-Verzeichnisstruktur
author: guardrex
description: "Finden Sie die Verzeichnisstruktur veröffentlichter ASP.NET Core-Anwendungen."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/directory-structure
ms.openlocfilehash: 55e1e0dac32609446243098dbb4a4373f06b4212
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/30/2018
---
# <a name="directory-structure-of-published-aspnet-core-apps"></a><span data-ttu-id="fcb1b-103">Verzeichnisstruktur der veröffentlichten ASP.NET Core-apps</span><span class="sxs-lookup"><span data-stu-id="fcb1b-103">Directory structure of published ASP.NET Core apps</span></span>

<span data-ttu-id="fcb1b-104">Von [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="fcb1b-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="fcb1b-105">In ASP.NET Core, das Anwendungsverzeichnis *veröffentlichen*, Anwendungsdateien, Konfigurationsdateien, statische Bestand, Pakete und die Common Language Runtime (für eigenständige apps) besteht.</span><span class="sxs-lookup"><span data-stu-id="fcb1b-105">In ASP.NET Core, the application directory, *publish*, is comprised of application files, config files, static assets, packages, and the runtime (for self-contained apps).</span></span>

| <span data-ttu-id="fcb1b-106">App-Typ</span><span class="sxs-lookup"><span data-stu-id="fcb1b-106">App Type</span></span>                       | <span data-ttu-id="fcb1b-107">Verzeichnisstruktur</span><span class="sxs-lookup"><span data-stu-id="fcb1b-107">Directory Structure</span></span> |
| ------------------------------ | ------------------- |
| <span data-ttu-id="fcb1b-108">Framework-abhängige-Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="fcb1b-108">Framework-dependent Deployment</span></span> | <ul><li><span data-ttu-id="fcb1b-109">Veröffentlichen\*</span><span class="sxs-lookup"><span data-stu-id="fcb1b-109">publish\*</span></span><ul><li><span data-ttu-id="fcb1b-110">Protokolle\* (falls in PublishOptions eingeschlossen)</span><span class="sxs-lookup"><span data-stu-id="fcb1b-110">logs\* (if included in publishOptions)</span></span></li><li><span data-ttu-id="fcb1b-111">refs\*</span><span class="sxs-lookup"><span data-stu-id="fcb1b-111">refs\*</span></span></li><li><span data-ttu-id="fcb1b-112">Laufzeiten\*</span><span class="sxs-lookup"><span data-stu-id="fcb1b-112">runtimes\*</span></span></li><li><span data-ttu-id="fcb1b-113">Sichten\* (falls in PublishOptions eingeschlossen)</span><span class="sxs-lookup"><span data-stu-id="fcb1b-113">Views\* (if included in publishOptions)</span></span></li><li><span data-ttu-id="fcb1b-114">"Wwwroot"\* (falls in PublishOptions eingeschlossen)</span><span class="sxs-lookup"><span data-stu-id="fcb1b-114">wwwroot\* (if included in publishOptions)</span></span></li><li><span data-ttu-id="fcb1b-115">DLL-Datei</span><span class="sxs-lookup"><span data-stu-id="fcb1b-115">.dll files</span></span></li><li><span data-ttu-id="fcb1b-116">myapp.deps.json</span><span class="sxs-lookup"><span data-stu-id="fcb1b-116">myapp.deps.json</span></span></li><li><span data-ttu-id="fcb1b-117">myapp.dll</span><span class="sxs-lookup"><span data-stu-id="fcb1b-117">myapp.dll</span></span></li><li><span data-ttu-id="fcb1b-118">myapp.pdb</span><span class="sxs-lookup"><span data-stu-id="fcb1b-118">myapp.pdb</span></span></li><li><span data-ttu-id="fcb1b-119">"MyApp". PrecompiledViews.dll (wenn es sich um eine Razor-Ansichten Vorkompilieren von)</span><span class="sxs-lookup"><span data-stu-id="fcb1b-119">myapp.PrecompiledViews.dll (if precompiling Razor Views)</span></span></li><li><span data-ttu-id="fcb1b-120">myapp.PrecompiledViews.pdb (if precompiling Razor Views)</span><span class="sxs-lookup"><span data-stu-id="fcb1b-120">myapp.PrecompiledViews.pdb (if precompiling Razor Views)</span></span></li><li><span data-ttu-id="fcb1b-121">myapp.runtimeconfig.json</span><span class="sxs-lookup"><span data-stu-id="fcb1b-121">myapp.runtimeconfig.json</span></span></li><li><span data-ttu-id="fcb1b-122">"Web.config" (falls in PublishOptions eingeschlossen)</span><span class="sxs-lookup"><span data-stu-id="fcb1b-122">web.config (if included in publishOptions)</span></span></li></ul></li></ul> |
| <span data-ttu-id="fcb1b-123">Eigenständige Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="fcb1b-123">Self-contained Deployment</span></span>      | <ul><li><span data-ttu-id="fcb1b-124">Veröffentlichen\*</span><span class="sxs-lookup"><span data-stu-id="fcb1b-124">publish\*</span></span><ul><li><span data-ttu-id="fcb1b-125">Protokolle\* (falls in PublishOptions eingeschlossen)</span><span class="sxs-lookup"><span data-stu-id="fcb1b-125">logs\* (if included in publishOptions)</span></span></li><li><span data-ttu-id="fcb1b-126">refs\*</span><span class="sxs-lookup"><span data-stu-id="fcb1b-126">refs\*</span></span></li><li><span data-ttu-id="fcb1b-127">Sichten\* (falls in PublishOptions eingeschlossen)</span><span class="sxs-lookup"><span data-stu-id="fcb1b-127">Views\* (if included in publishOptions)</span></span></li><li><span data-ttu-id="fcb1b-128">"Wwwroot"\* (falls in PublishOptions eingeschlossen)</span><span class="sxs-lookup"><span data-stu-id="fcb1b-128">wwwroot\* (if included in publishOptions)</span></span></li><li><span data-ttu-id="fcb1b-129">DLL-Datei</span><span class="sxs-lookup"><span data-stu-id="fcb1b-129">.dll files</span></span></li><li><span data-ttu-id="fcb1b-130">myapp.deps.json</span><span class="sxs-lookup"><span data-stu-id="fcb1b-130">myapp.deps.json</span></span></li><li><span data-ttu-id="fcb1b-131">myapp.exe</span><span class="sxs-lookup"><span data-stu-id="fcb1b-131">myapp.exe</span></span></li><li><span data-ttu-id="fcb1b-132">myapp.pdb</span><span class="sxs-lookup"><span data-stu-id="fcb1b-132">myapp.pdb</span></span></li><li><span data-ttu-id="fcb1b-133">"MyApp". PrecompiledViews.dll (wenn es sich um eine Razor-Ansichten Vorkompilieren von)</span><span class="sxs-lookup"><span data-stu-id="fcb1b-133">myapp.PrecompiledViews.dll (if precompiling Razor Views)</span></span></li><li><span data-ttu-id="fcb1b-134">myapp.PrecompiledViews.pdb (if precompiling Razor Views)</span><span class="sxs-lookup"><span data-stu-id="fcb1b-134">myapp.PrecompiledViews.pdb (if precompiling Razor Views)</span></span></li><li><span data-ttu-id="fcb1b-135">myapp.runtimeconfig.json</span><span class="sxs-lookup"><span data-stu-id="fcb1b-135">myapp.runtimeconfig.json</span></span></li><li><span data-ttu-id="fcb1b-136">"Web.config" (falls in PublishOptions eingeschlossen)</span><span class="sxs-lookup"><span data-stu-id="fcb1b-136">web.config (if included in publishOptions)</span></span></li></ul></li></ul> |
<span data-ttu-id="fcb1b-137">\*Gibt ein Verzeichnis an</span><span class="sxs-lookup"><span data-stu-id="fcb1b-137">\* Indicates a directory</span></span>

<span data-ttu-id="fcb1b-138">Den Inhalt der *veröffentlichen* Verzeichnis darstellt der *Content Stammpfad*auch Namens der *Anwendungsbasispfads*, der Bereitstellung.</span><span class="sxs-lookup"><span data-stu-id="fcb1b-138">The contents of the *publish* directory represents the *content root path*, also called the *application base path*, of the deployment.</span></span> <span data-ttu-id="fcb1b-139">Auf einen beliebigen Namen gewährt wird die *veröffentlichen* Verzeichnis in der Bereitstellung am Speicherort mit dem physischen Pfad des Servers für die gehostete Anwendung dient.</span><span class="sxs-lookup"><span data-stu-id="fcb1b-139">Whatever name is given to the *publish* directory in the deployment, its location serves as the server's physical path to the hosted application.</span></span> <span data-ttu-id="fcb1b-140">Die *"Wwwroot"* Verzeichnis, falls vorhanden, enthält nur statische Objekte.</span><span class="sxs-lookup"><span data-stu-id="fcb1b-140">The *wwwroot* directory, if present, only contains static assets.</span></span> <span data-ttu-id="fcb1b-141">Die *Protokolle* Verzeichnis in der Bereitstellung enthalten sein kann, indem es in das Projekt erstellen und Hinzufügen der `<Target>` folgenden Element Ihre *csproj* Datei oder beim Erstellen des Verzeichnisses physisch auf den Server.</span><span class="sxs-lookup"><span data-stu-id="fcb1b-141">The *logs* directory may be included in the deployment by creating it in the project and adding the `<Target>` element shown below to your *.csproj* file or by physically creating the directory on the server.</span></span>

```xml
<Target Name="CreateLogsFolder" AfterTargets="Publish">
  <MakeDir Directories="$(PublishDir)Logs" 
           Condition="!Exists('$(PublishDir)Logs')" />
  <WriteLinesToFile File="$(PublishDir)Logs\.log" 
                    Lines="Generated file" 
                    Overwrite="True" 
                    Condition="!Exists('$(PublishDir)Logs\.log')" />
</Target>
```

<span data-ttu-id="fcb1b-142">Die `<MakeDir>` Element erstellt ein leeres *Protokolle* Ordner in der veröffentlichten Ausgabe.</span><span class="sxs-lookup"><span data-stu-id="fcb1b-142">The `<MakeDir>` element creates an empty *Logs* folder in the published output.</span></span> <span data-ttu-id="fcb1b-143">Das Element verwendet die `PublishDir` -Eigenschaft können Sie den Zielspeicherort für die Ordner erstellen, zu bestimmen.</span><span class="sxs-lookup"><span data-stu-id="fcb1b-143">The element uses the `PublishDir` property to determine the target location for creating the folder.</span></span> <span data-ttu-id="fcb1b-144">Mehrere Bereitstellungsmethoden zur Verfügung, z. B. Webbereitstellung, überspringen Sie leere Ordner während der Bereitstellung.</span><span class="sxs-lookup"><span data-stu-id="fcb1b-144">Several deployment methods, such as Web Deploy, skip empty folders during deployment.</span></span> <span data-ttu-id="fcb1b-145">Die `<WriteLinesToFile>` Element erzeugt eine Datei in die *Protokolle* Ordner, in dem Bereitstellung des Ordners mit dem Server gewährleistet.</span><span class="sxs-lookup"><span data-stu-id="fcb1b-145">The `<WriteLinesToFile>` element generates a file in the *Logs* folder, which guarantees deployment of the folder to the server.</span></span> <span data-ttu-id="fcb1b-146">Beachten Sie, dass Ordner erstellen noch fehlschlagen, wenn der Arbeitsprozess Schreibzugriff in den Zielordner keine.</span><span class="sxs-lookup"><span data-stu-id="fcb1b-146">Note that folder creation may still fail if the worker process doesn't have write access to the target folder.</span></span>

<span data-ttu-id="fcb1b-147">Das Bereitstellungsverzeichnis erfordert Lese-/Execute-Berechtigungen, während die *Protokolle* Directory erfordert Lese-/Schreibberechtigungen.</span><span class="sxs-lookup"><span data-stu-id="fcb1b-147">The deployment directory requires Read/Execute permissions, while the *Logs* directory requires Read/Write permissions.</span></span> <span data-ttu-id="fcb1b-148">Weitere Verzeichnisse, in denen Objekte geschrieben wird, erfordert Lese-/Schreibberechtigungen.</span><span class="sxs-lookup"><span data-stu-id="fcb1b-148">Additional directories where assets will be written require Read/Write permissions.</span></span>