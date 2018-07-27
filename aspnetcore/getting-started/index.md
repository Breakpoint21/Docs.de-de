---
title: Erste Schritte mit ASP.NET Core
author: rick-anderson
description: Kurztutorial, in dem eine einfache Hello World-App mit ASP.NET Core erstellt und ausgeführt wird.
ms.author: riande
ms.custom: mvc
ms.date: 05/31/2018
uid: getting-started
ms.openlocfilehash: 7ab9f303d74786c4ac76f002d0f2c66371e78cb8
ms.sourcegitcommit: b4c7b1a4c48dec0865f27874275c73da1f75e918
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/24/2018
ms.locfileid: "39228581"
---
# <a name="get-started-with-aspnet-core"></a><span data-ttu-id="881de-103">Erste Schritte mit ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="881de-103">Get started with ASP.NET Core</span></span>

::: moniker range=">= aspnetcore-2.1"

1. <span data-ttu-id="881de-104">Installieren Sie [!INCLUDE [](~/includes/2.1-SDK.md)].</span><span class="sxs-lookup"><span data-stu-id="881de-104">Install the [!INCLUDE [](~/includes/2.1-SDK.md)].</span></span>

2. <span data-ttu-id="881de-105">Erstellen Sie ein ASP.NET Core-Projekt.</span><span class="sxs-lookup"><span data-stu-id="881de-105">Create an ASP.NET Core project.</span></span> <span data-ttu-id="881de-106">Öffnen Sie eine Befehlsshell, und geben Sie den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="881de-106">Open a command shell and enter the following command:</span></span>

    ```console
    dotnet new webapp -o aspnetcoreapp
    ```

    [!INCLUDE [](~/includes/webapp-alias-notice.md)]

3. <span data-ttu-id="881de-107">Vertrauen Sie dem HTTPS-Entwicklungszertifikat:</span><span class="sxs-lookup"><span data-stu-id="881de-107">Trust the HTTPS development certificate:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="881de-108">Windows</span><span class="sxs-lookup"><span data-stu-id="881de-108">Windows</span></span>](#tab/windows)

    ```console
    dotnet dev-certs https --trust
    ```

   <span data-ttu-id="881de-109">Über den vorherigen Befehl wird der folgende Dialog angezeigt:</span><span class="sxs-lookup"><span data-stu-id="881de-109">The preceding command displays the following dialog:</span></span>

   ![Dialogfeld „Sicherheitswarnung“](_static/cert.png)

   <span data-ttu-id="881de-111">Klicken Sie auf **Ja**, wenn Sie zustimmen möchten, dass das Entwicklungszertifikat vertrauenswürdig ist.</span><span class="sxs-lookup"><span data-stu-id="881de-111">Select **Yes** if you agree to trust the development certificate.</span></span>

# <a name="macostabmacos"></a>[<span data-ttu-id="881de-112">macOS</span><span class="sxs-lookup"><span data-stu-id="881de-112">macOS</span></span>](#tab/macos)

    ```console
    dotnet dev-certs https --trust
    ```

   <span data-ttu-id="881de-113">Über den vorherigen Befehl wird die folgende Meldung angezeigt:</span><span class="sxs-lookup"><span data-stu-id="881de-113">The preceding command displays the following message:</span></span>

   <span data-ttu-id="881de-114">*Trusting the HTTPS development certificate was requested. Sie müssen bestätigen, dass Sie dem HTTPS-Entwicklungszertifikat vertrauen. Wenn Sie dies noch nicht bestätigt haben, wird der folgende Befehl ausgeführt:*  `'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'` *Sie werden dann möglicherweise aufgefordert, Ihr Kennwort einzugeben, um das Zertifikat auf der Keychain des Systems zu installieren    Kennwort:*</span><span class="sxs-lookup"><span data-stu-id="881de-114">*Trusting the HTTPS development certificate was requested. If the certificate is not already trusted we will run the following command:* `'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'` *This command might prompt you for your password to install the certificate on the system keychain.    Password:*</span></span>

   <span data-ttu-id="881de-115">Geben Sie Ihr Kennwort ein, wenn Sie die Vertrauenswürdigkeit des Entwicklungszertifikats bestätigen möchten.</span><span class="sxs-lookup"><span data-stu-id="881de-115">Enter your password if you agree to trust the development certificate.</span></span>

# <a name="linuxtablinux"></a>[<span data-ttu-id="881de-116">Linux</span><span class="sxs-lookup"><span data-stu-id="881de-116">Linux</span></span>](#tab/linux)

   <a name="see-the-documentation-for-your-linux-distribution-on-how-to-trust-the-https-development-certificate"></a><span data-ttu-id="881de-117">Weitere Informationen zum Bestätigen der Vertrauenswürdigkeit eines HTTPS-Entwicklungszertifikats finden Sie in der Dokumentation zu Ihrer Linux-Distribution.</span><span class="sxs-lookup"><span data-stu-id="881de-117">See the documentation for your Linux distribution on how to trust the HTTPS development certificate</span></span>
---

4. <span data-ttu-id="881de-118">Führen Sie die App aus:</span><span class="sxs-lookup"><span data-stu-id="881de-118">Run the app:</span></span>

    ```console
    cd aspnetcoreapp
    dotnet run
    ```

5. <span data-ttu-id="881de-119">Wechseln Sie zu [http://localhost:5001](http://localhost:5001).</span><span class="sxs-lookup"><span data-stu-id="881de-119">Browse to [http://localhost:5001](http://localhost:5001).</span></span>  <span data-ttu-id="881de-120">Klicken Sie auf **Accept** (Akzeptieren), um die Datenschutz- und Cookierichtlinie zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="881de-120">Click **Accept** to accept the privacy and cookie policy.</span></span> <span data-ttu-id="881de-121">Diese App bewahrt keine personenbezogenen Informationen auf.</span><span class="sxs-lookup"><span data-stu-id="881de-121">This app doesn't keep personal information.</span></span>

6. <span data-ttu-id="881de-122">Öffnen Sie *Pages/About.cshtml*, und modifizieren Sie die Seite mit dem folgenden hervorgehobenen Markup:</span><span class="sxs-lookup"><span data-stu-id="881de-122">Open *Pages/About.cshtml* and modify the page with the following highlighted markup:</span></span>

    [!code-cshtml[](sample/getting-started/about.cshtml?highlight=9)]

7. <span data-ttu-id="881de-123">Navigieren Sie zu [http://localhost:5001/About](http://localhost:5001/About), und überprüfen Sie, ob die Änderungen angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="881de-123">Browse to [http://localhost:5001/About](http://localhost:5001/About) and verify the changes are displayed.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

1. <span data-ttu-id="881de-124">Installieren Sie [!INCLUDE [](~/includes/net-core-sdk-download-link.md)].</span><span class="sxs-lookup"><span data-stu-id="881de-124">Install the [!INCLUDE [](~/includes/net-core-sdk-download-link.md)].</span></span>

2. <span data-ttu-id="881de-125">Erstellen Sie ein neues ASP.NET Core-Projekt.</span><span class="sxs-lookup"><span data-stu-id="881de-125">Create a new ASP.NET Core project.</span></span>

   <span data-ttu-id="881de-126">Öffnen Sie eine Befehlsshell.</span><span class="sxs-lookup"><span data-stu-id="881de-126">Open a command shell.</span></span> <span data-ttu-id="881de-127">Geben Sie folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="881de-127">Enter the following command:</span></span>

    ```console
    dotnet new razor -o aspnetcoreapp
    ```

3. <span data-ttu-id="881de-128">Führen Sie die App mit den folgenden Befehlen aus:</span><span class="sxs-lookup"><span data-stu-id="881de-128">Run the app with the following commands:</span></span>

    ```console
    cd aspnetcoreapp
    dotnet run
    ```

4. <span data-ttu-id="881de-129">Wechseln Sie zu [http://localhost:5000](http://localhost:5000).</span><span class="sxs-lookup"><span data-stu-id="881de-129">Browse to [http://localhost:5000](http://localhost:5000).</span></span>

5. <span data-ttu-id="881de-130">Öffnen Sie *Pages/About.cshtml*, und verändern Sie die Seite so, dass sie die Meldung „Hallo Welt!“ anzeigt.</span><span class="sxs-lookup"><span data-stu-id="881de-130">Open *Pages/About.cshtml* and modify the page to display the message "Hello, world!</span></span> <span data-ttu-id="881de-131">Die Zeit auf dem Server ist @DateTime.Now" :</span><span class="sxs-lookup"><span data-stu-id="881de-131">The time on the server is @DateTime.Now":</span></span>

    [!code-cshtml[](sample/getting-started/about.cshtml?highlight=9&range=1-9)]

6. <span data-ttu-id="881de-132">Wechseln Sie zu [http://localhost:5000/About](http://localhost:5000/About), und bestätigen Sie die Änderungen.</span><span class="sxs-lookup"><span data-stu-id="881de-132">Browse to [http://localhost:5000/About](http://localhost:5000/About) and verify the changes.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

1. <span data-ttu-id="881de-133">Installieren Sie den .NET Core **SDK Installer** für SDK 1.0.4 von der .NET Core-Seite [Alle Downloads](https://www.microsoft.com/net/download/all).</span><span class="sxs-lookup"><span data-stu-id="881de-133">Install the .NET Core **SDK Installer** for SDK 1.0.4 from the [.NET Core All Downloads page](https://www.microsoft.com/net/download/all).</span></span>

2. <span data-ttu-id="881de-134">Erstellen Sie einen Ordner für das neue ASP.NET Core-Projekt.</span><span class="sxs-lookup"><span data-stu-id="881de-134">Create a folder for a new ASP.NET Core project.</span></span>

   <span data-ttu-id="881de-135">Öffnen Sie eine Befehlsshell.</span><span class="sxs-lookup"><span data-stu-id="881de-135">Open a command shell.</span></span> <span data-ttu-id="881de-136">Geben Sie die folgenden Befehle ein:</span><span class="sxs-lookup"><span data-stu-id="881de-136">Enter the following commands:</span></span>

   ```console
   mkdir aspnetcoreapp
   cd aspnetcoreapp
   ```

3. <span data-ttu-id="881de-137">Wenn Sie eine höhere Version des SDK auf Ihrem Computer installiert haben, erstellen Sie die Datei *global.json*, und wählen Sie das SDK 1.0.4 aus.</span><span class="sxs-lookup"><span data-stu-id="881de-137">If you have installed a later SDK version on your machine, create a *global.json* file to select the 1.0.4 SDK.</span></span>

   ```json
   {
     "sdk": { "version": "1.0.4" }
   }
   ```

4. <span data-ttu-id="881de-138">Erstellen Sie ein neues ASP.NET Core-Projekt.</span><span class="sxs-lookup"><span data-stu-id="881de-138">Create a new ASP.NET Core project.</span></span>

   ```console
   dotnet new web
   ```

5. <span data-ttu-id="881de-139">Stellen Sie die Pakete wieder her.</span><span class="sxs-lookup"><span data-stu-id="881de-139">Restore the packages.</span></span>

    ```console
    dotnet restore
    ```

6. <span data-ttu-id="881de-140">Führen Sie die App aus.</span><span class="sxs-lookup"><span data-stu-id="881de-140">Run the app.</span></span>

   ```console
   dotnet run
   ```

   <span data-ttu-id="881de-141">Mit dem Befehl [dotnet run](/dotnet/core/tools/dotnet-run) wird die App bei Bedarf zunächst erstellt.</span><span class="sxs-lookup"><span data-stu-id="881de-141">The [dotnet run](/dotnet/core/tools/dotnet-run) command builds the app first, if needed.</span></span>

7. <span data-ttu-id="881de-142">Wechseln Sie zu `http://localhost:5000`.</span><span class="sxs-lookup"><span data-stu-id="881de-142">Browse to `http://localhost:5000`.</span></span>

[!INCLUDE [next steps](~/includes/getting-started/next-steps.md)]
::: moniker-end
