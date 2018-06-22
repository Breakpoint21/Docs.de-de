---
title: Gerüst Identität in ASP.NET Core-Projekten
author: rick-anderson
description: Erfahren Sie, wie das Gerüst für Identität in einem Projekt auf ASP.NET Core erstellen.
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 5/16/2018
uid: security/authentication/scaffold-identity
ms.openlocfilehash: cf6544d8b671f026c8466fa8dff506027b64cf1f
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2018
ms.locfileid: "36276317"
---
# <a name="scaffold-identity-in-aspnet-core-projects"></a><span data-ttu-id="14aa9-103">Gerüst Identität in ASP.NET Core-Projekten</span><span class="sxs-lookup"><span data-stu-id="14aa9-103">Scaffold Identity in ASP.NET Core projects</span></span>

<span data-ttu-id="14aa9-104">Von [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="14aa9-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="14aa9-105">ASP.NET Core 2.1 und höher bietet [ASP.NET Core Identity](xref:security/authentication/identity) als eine [Razor-Klassenbibliothek](xref:razor-pages/ui-class).</span><span class="sxs-lookup"><span data-stu-id="14aa9-105">ASP.NET Core 2.1 and later provides [ASP.NET Core Identity](xref:security/authentication/identity) as a [Razor Class Library](xref:razor-pages/ui-class).</span></span> <span data-ttu-id="14aa9-106">Anwendungen, die Identität können der Scaffolder um selektiv hinzufügen, den Quellcode in der Identität Razor Klasse Bibliothek (RCL) enthalten angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="14aa9-106">Applications that include Identity can apply the scaffolder to selectively add the source code contained in the Identity Razor Class Library (RCL).</span></span> <span data-ttu-id="14aa9-107">Möglicherweise möchten Generieren von Quellcode, dadurch können Sie den Code zu ändern und das Verhalten zu ändern.</span><span class="sxs-lookup"><span data-stu-id="14aa9-107">You might want to generate source code so you can modify the code and change the behavior.</span></span> <span data-ttu-id="14aa9-108">Sie können z. B. die Scaffolder zum Generieren des Codes in der Registrierung verwendete anweisen.</span><span class="sxs-lookup"><span data-stu-id="14aa9-108">For example, you could instruct the scaffolder to generate the code used in registration.</span></span> <span data-ttu-id="14aa9-109">Generierter Code hat Vorrang vor den gleichen Code in der Identität RCL.</span><span class="sxs-lookup"><span data-stu-id="14aa9-109">Generated code takes precedence over the same code in the Identity RCL.</span></span> <span data-ttu-id="14aa9-110">Um die vollständige Kontrolle über die Benutzeroberfläche zu erhalten, und verwenden Sie nicht den Standardnamen RCL, finden Sie im Abschnitt [erstellen vollständige Identität UI Quelle](#full).</span><span class="sxs-lookup"><span data-stu-id="14aa9-110">To gain full control of the UI and not use the default RCL, see the section [Create full identity UI source](#full).</span></span>

<span data-ttu-id="14aa9-111">Anwendungen, die **nicht** enthalten Authentifizierung kann die Scaffolder zum Hinzufügen des Pakets RCL Identität anwenden.</span><span class="sxs-lookup"><span data-stu-id="14aa9-111">Applications that do **not** include authentication can apply the scaffolder to add the RCL Identity package.</span></span> <span data-ttu-id="14aa9-112">Sie haben die Möglichkeit, auswählen von ID-Code generiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="14aa9-112">You have the option of selecting Identity code to be generated.</span></span>

<span data-ttu-id="14aa9-113">Obwohl die Scaffolder Großteil der erforderliche Code generiert, müssen Sie Ihrem Projekt zum Abschließen des Vorgangs aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="14aa9-113">Although the scaffolder generates most of the necessary code, you'll have to update your project to complete the process.</span></span> <span data-ttu-id="14aa9-114">Dieses Dokument erläutert die Schritte zum Abschließen eines Identität Gerüstbau Updates erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="14aa9-114">This document explains the steps needed to complete an Identity scaffolding update.</span></span>

<span data-ttu-id="14aa9-115">Wenn die Identität Scaffolder ausgeführt wird, eine *ScaffoldingReadme.txt* Datei ist im Projektverzeichnis erstellt.</span><span class="sxs-lookup"><span data-stu-id="14aa9-115">When the Identity scaffolder is run, a *ScaffoldingReadme.txt* file is created in the project directory.</span></span> <span data-ttu-id="14aa9-116">Die *ScaffoldingReadme.txt* -Datei enthält allgemeine Anweisungen auf, was erforderlich ist, um die Identität des Gerüstbaus Aktualisierung abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="14aa9-116">The *ScaffoldingReadme.txt* file contains general instructions on what's needed to complete the Identity scaffolding update.</span></span> <span data-ttu-id="14aa9-117">Dieses Dokument enthält ausführlichere Anweisungen als die *ScaffoldingReadme.txt* Datei.</span><span class="sxs-lookup"><span data-stu-id="14aa9-117">This document contains more complete instructions than the *ScaffoldingReadme.txt* file.</span></span>

<span data-ttu-id="14aa9-118">Es wird empfohlen, mit einem Quellcodeverwaltungssystem, die die Unterschiede zwischen und bietet die Möglichkeit, außerhalb des gültigen Änderungen sichern.</span><span class="sxs-lookup"><span data-stu-id="14aa9-118">We recommend using a source control system that shows file differences and allows you to back out of changes.</span></span> <span data-ttu-id="14aa9-119">Überprüfen Sie die Änderungen nach dem Ausführen der Identität Scaffolder.</span><span class="sxs-lookup"><span data-stu-id="14aa9-119">Inspect the changes after running the Identity scaffolder.</span></span>

## <a name="scaffold-identity-into-an-empty-project"></a><span data-ttu-id="14aa9-120">Gerüst Identität in ein leeres Projekt</span><span class="sxs-lookup"><span data-stu-id="14aa9-120">Scaffold identity into an empty project</span></span>

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg.md)]

<span data-ttu-id="14aa9-121">Fügen Sie die folgenden hervorgehobenen Aufrufe an die `Startup` Klasse:</span><span class="sxs-lookup"><span data-stu-id="14aa9-121">Add the following highlighted calls to the `Startup` class:</span></span>

[!code-csharp[](scaffold-identity/sample/StartupEmpty.cs?name=snippet1&highlight=5,20-23)]

[!INCLUDE[](~/includes/scaffold-identity/hsts.md)]

[!INCLUDE[](~/includes/scaffold-identity/migrations.md)]

## <a name="scaffold-identity-into-a-razor-project-without-existing-authorization"></a><span data-ttu-id="14aa9-122">Gerüst Identität in einer Razor-Projekt, ohne vorhandene Autorisierung</span><span class="sxs-lookup"><span data-stu-id="14aa9-122">Scaffold identity into a Razor project without existing authorization</span></span>

<!--
set projNam=RPnoAuth
set projType=razor
set version=2.1.0

dotnet new %projType% -o %projNam%
cd %projNam%
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design -v %version%
dotnet restore
dotnet aspnet-codegenerator identity --useDefaultUI
dotnet ef migrations add CreateIdentitySchema
dotnet ef database update
-->

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg.md)]

<span data-ttu-id="14aa9-123">Identität konfiguriert ist, *Areas/Identity/IdentityHostingStartup.cs*.</span><span class="sxs-lookup"><span data-stu-id="14aa9-123">Identity is configured in *Areas/Identity/IdentityHostingStartup.cs*.</span></span> <span data-ttu-id="14aa9-124">Weitere Informationen finden Sie unter [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration).</span><span class="sxs-lookup"><span data-stu-id="14aa9-124">for more information, see [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration).</span></span>

<a name="efm"></a>

### <a name="migrations-useauthentication-and-layout"></a><span data-ttu-id="14aa9-125">Migrationen, UseAuthentication und layout</span><span class="sxs-lookup"><span data-stu-id="14aa9-125">Migrations, UseAuthentication, and layout</span></span>

[!INCLUDE[](~/includes/scaffold-identity/migrations.md)]

<span data-ttu-id="14aa9-126">In der `Configure` Methode der `Startup` -Klasse, rufen Sie [UseAuthentication](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_) nach `UseStaticFiles`:</span><span class="sxs-lookup"><span data-stu-id="14aa9-126">In the `Configure` method of the `Startup` class, call [UseAuthentication](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_) after `UseStaticFiles`:</span></span>

[!code-csharp[](scaffold-identity/sample/StartupRPnoAuth.cs?name=snippet1&highlight=29)]

[!INCLUDE[](~/includes/scaffold-identity/hsts.md)]

### <a name="layout-changes"></a><span data-ttu-id="14aa9-127">Änderungen am Layout</span><span class="sxs-lookup"><span data-stu-id="14aa9-127">Layout changes</span></span>

<span data-ttu-id="14aa9-128">Optional: Fügen Sie der partiellen Anmeldung hinzu (`_LoginPartial`) in der Layoutdatei:</span><span class="sxs-lookup"><span data-stu-id="14aa9-128">Optional: Add the login partial (`_LoginPartial`) to the layout file:</span></span>

[!code-html[Main](scaffold-identity/sample/_Layout.cshtml?highlight=37)]

## <a name="scaffold-identity-into-a-razor-project-with-authorization"></a><span data-ttu-id="14aa9-129">Gerüst Identität in einer Razor-Projekt mit Autorisierung</span><span class="sxs-lookup"><span data-stu-id="14aa9-129">Scaffold identity into a Razor project with authorization</span></span>

<!--
Use >=2.1: dotnet new webapp -au Individual -o RPauth
Use = 2.0: dotnet new razor -au Individual -o RPauth
cd RPauth
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
dotnet aspnet-codegenerator identity -dc RPauth.Data.ApplicationDbContext --files Account.Register

[!INCLUDE[](~/includes/webapp-alias-notice.md)]
-->

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg-auth.md)]
<span data-ttu-id="14aa9-130">Einige identitätsoptionen im konfiguriert sind *Areas/Identity/IdentityHostingStartup.cs*.</span><span class="sxs-lookup"><span data-stu-id="14aa9-130">Some Identity options are configured in *Areas/Identity/IdentityHostingStartup.cs*.</span></span> <span data-ttu-id="14aa9-131">Weitere Informationen finden Sie unter [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration).</span><span class="sxs-lookup"><span data-stu-id="14aa9-131">For more information, see [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration).</span></span>

## <a name="scaffold-identity-into-an-mvc-project-without-existing-authorization"></a><span data-ttu-id="14aa9-132">Gerüst Identität in einer MVC-Projekt, ohne vorhandene Autorisierung</span><span class="sxs-lookup"><span data-stu-id="14aa9-132">Scaffold identity into an MVC project without existing authorization</span></span>

<!--
set projNam=MvcNoAuth
set projType=mvc
set version=2.1.0

dotnet new %projType% -o %projNam%
cd %projNam%
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design -v %version%
dotnet restore
dotnet aspnet-codegenerator identity --useDefaultUI
dotnet ef migrations add CreateIdentitySchema
dotnet ef database update
-->

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg.md)]

<span data-ttu-id="14aa9-133">Optional: Fügen Sie der partiellen Anmeldung hinzu (`_LoginPartial`), die *Views/Shared/_Layout.cshtml* Datei:</span><span class="sxs-lookup"><span data-stu-id="14aa9-133">Optional: Add the login partial (`_LoginPartial`) to the *Views/Shared/_Layout.cshtml* file:</span></span>

[!code-html[](scaffold-identity/sample/_LayoutMvc.cshtml?highlight=37)]

* <span data-ttu-id="14aa9-134">Verschieben der *Pages/Shared/_LoginPartial.cshtml* Datei *Views/Shared/_LoginPartial.cshtml*</span><span class="sxs-lookup"><span data-stu-id="14aa9-134">Move the *Pages/Shared/_LoginPartial.cshtml* file to *Views/Shared/_LoginPartial.cshtml*</span></span>

<span data-ttu-id="14aa9-135">Identität konfiguriert ist, *Areas/Identity/IdentityHostingStartup.cs*.</span><span class="sxs-lookup"><span data-stu-id="14aa9-135">Identity is configured in *Areas/Identity/IdentityHostingStartup.cs*.</span></span> <span data-ttu-id="14aa9-136">Weitere Informationen finden Sie unter IHostingStartup.</span><span class="sxs-lookup"><span data-stu-id="14aa9-136">For more information, see IHostingStartup.</span></span>

[!INCLUDE[](~/includes/scaffold-identity/migrations.md)]

<span data-ttu-id="14aa9-137">Rufen Sie [UseAuthentication](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_) nach `UseStaticFiles`:</span><span class="sxs-lookup"><span data-stu-id="14aa9-137">Call [UseAuthentication](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_) after `UseStaticFiles`:</span></span>

[!code-csharp[](scaffold-identity/sample/StartupMvcNoAuth.cs?name=snippet1&highlight=23)]

[!INCLUDE[](~/includes/scaffold-identity/hsts.md)]

## <a name="scaffold-identity-into-an-mvc-project-with-authorization"></a><span data-ttu-id="14aa9-138">Gerüst Identität in einer MVC-Projekt mit Autorisierung</span><span class="sxs-lookup"><span data-stu-id="14aa9-138">Scaffold identity into an MVC project with authorization</span></span>

<!--
dotnet new mvc -au Individual -o MvcAuth
cd MvcAuth
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
dotnet aspnet-codegenerator identity -dc MvcAuth.Data.ApplicationDbContext --files Account.Register
-->

[!INCLUDE[](~/includes/scaffold-identity/id-scaffold-dlg-auth.md)]

<span data-ttu-id="14aa9-139">Löschen der *Seiten/freigegebene* Ordner und Dateien in diesem Ordner.</span><span class="sxs-lookup"><span data-stu-id="14aa9-139">Delete the *Pages/Shared* folder and the files in that folder.</span></span>

<a name="full"></a>

## <a name="create-full-identity-ui-source"></a><span data-ttu-id="14aa9-140">Vollständige Identität UI Quelle erstellen</span><span class="sxs-lookup"><span data-stu-id="14aa9-140">Create full identity UI source</span></span>

<span data-ttu-id="14aa9-141">Um vollen Zugriff auf die Identity-Benutzeroberfläche zu gewährleisten, führen Sie die Identität Scaffolder, und wählen Sie **alle Dateien überschreiben**.</span><span class="sxs-lookup"><span data-stu-id="14aa9-141">To maintain full control of the Identity UI, run the Identity scaffolder and select **Override all files**.</span></span>

<span data-ttu-id="14aa9-142">Die folgende hervorgehobene Code zeigt die Änderungen an der Identity-Standardbenutzeroberfläche mit der Identität in einer ASP.NET Core 2.1-Web-app zu ersetzen.</span><span class="sxs-lookup"><span data-stu-id="14aa9-142">The following highlighted code shows the changes to replace the default Identity UI with Identity in an ASP.NET Core 2.1 web app.</span></span> <span data-ttu-id="14aa9-143">Möglicherweise möchten diese Option, um die vollständige Kontrolle über die Benutzeroberfläche der Identität haben müssen.</span><span class="sxs-lookup"><span data-stu-id="14aa9-143">You might want to do this to have full control of the Identity UI.</span></span>

[!code-csharp[](scaffold-identity/sample/StartupFull.cs?name=snippet1&highlight=13-14,17-999)]

<span data-ttu-id="14aa9-144">Im folgenden Code wird der Standard-Identität ersetzt:</span><span class="sxs-lookup"><span data-stu-id="14aa9-144">The default Identity is replaced in the following code:</span></span>

[!code-csharp[](scaffold-identity/sample/StartupFull.cs?name=snippet2)]

<span data-ttu-id="14aa9-145">Die folgenden legt der Code die [LoginPath](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.loginpath), [logoutpath für](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.logoutpath), und [AccessDeniedPath](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.accessdeniedpath):</span><span class="sxs-lookup"><span data-stu-id="14aa9-145">The following the code sets the [LoginPath](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.loginpath), [LogoutPath](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.logoutpath), and [AccessDeniedPath](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.accessdeniedpath):</span></span>

[!code-csharp[](scaffold-identity/sample/StartupFull.cs?name=snippet3)]

<span data-ttu-id="14aa9-146">Registrieren einer `IEmailSender` Implementierung, beispielsweise:</span><span class="sxs-lookup"><span data-stu-id="14aa9-146">Register an `IEmailSender` implementation, for example:</span></span>

[!code-csharp[](scaffold-identity/sample/StartupFull.cs?name=snippet4)]
