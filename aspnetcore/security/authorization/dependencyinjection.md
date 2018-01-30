---
title: "Abhängigkeitsinjektion in Anforderung Handler"
author: rick-anderson
description: "Dieses Dokument beschreibt, wie Sie Autorisierung Anforderung Handler in einer ASP.NET Core-app mithilfe der Abhängigkeitsinjektion einfügen."
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/dependencyinjection
ms.openlocfilehash: 1b7506b49109264a8c628ea2e39ded9f5ace95d3
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/30/2018
---
# <a name="dependency-injection-in-requirement-handlers"></a><span data-ttu-id="060b2-103">Abhängigkeitsinjektion in Anforderung Handler</span><span class="sxs-lookup"><span data-stu-id="060b2-103">Dependency Injection in requirement handlers</span></span>

<a name="security-authorization-di"></a>

<span data-ttu-id="060b2-104">[Müssen Autorisierung Handler registriert werden](policies.md#handler-registration) in die Auflistung während der Konfiguration (mit [Abhängigkeitsinjektion](../../fundamentals/dependency-injection.md#fundamentals-dependency-injection)).</span><span class="sxs-lookup"><span data-stu-id="060b2-104">[Authorization handlers must be registered](policies.md#handler-registration) in the service collection during configuration (using [dependency injection](../../fundamentals/dependency-injection.md#fundamentals-dependency-injection)).</span></span>

<span data-ttu-id="060b2-105">Angenommen, mussten Sie ein Repository mit Regeln innerhalb eines ereignishandlers Autorisierung auswerten möchten, und diesem Repository registriert wurde, in die Auflistung.</span><span class="sxs-lookup"><span data-stu-id="060b2-105">Suppose you had a repository of rules you wanted to evaluate inside an authorization handler and that repository was registered in the service collection.</span></span> <span data-ttu-id="060b2-106">Die Autorisierung wird beheben und einfügen, die in Ihrem Konstruktor.</span><span class="sxs-lookup"><span data-stu-id="060b2-106">Authorization will resolve and inject that into your constructor.</span></span>

<span data-ttu-id="060b2-107">Angenommen, Sie ASP verwenden möchten. NET der Infrastruktur, die Sie einfügen möchten Protokollierung `ILoggerFactory` in den Handler.</span><span class="sxs-lookup"><span data-stu-id="060b2-107">For example, if you wanted to use ASP.NET's logging infrastructure you would want to inject `ILoggerFactory` into your handler.</span></span> <span data-ttu-id="060b2-108">Ein Handler möglicherweise formuliert werden:</span><span class="sxs-lookup"><span data-stu-id="060b2-108">Such a handler might look like:</span></span>

```csharp
public class LoggingAuthorizationHandler : AuthorizationHandler<MyRequirement>
   {
       ILogger _logger;

       public LoggingAuthorizationHandler(ILoggerFactory loggerFactory)
       {
           _logger = loggerFactory.CreateLogger(this.GetType().FullName);
       }

       protected override Task HandleRequirementAsync(AuthorizationHandlerContext context, MyRequirement requirement)
       {
           _logger.LogInformation("Inside my handler");
           // Check if the requirement is fulfilled.
           return Task.CompletedTask;
       }
   }
   ```

<span data-ttu-id="060b2-109">Registrieren Sie den Handler mit `services.AddSingleton()`:</span><span class="sxs-lookup"><span data-stu-id="060b2-109">You would register the handler with `services.AddSingleton()`:</span></span>

```csharp
services.AddSingleton<IAuthorizationHandler, LoggingAuthorizationHandler>();
```

<span data-ttu-id="060b2-110">Eine Instanz der Ereignishandler wird beim Start der Anwendung erstellt werden und DI wird die registrierte einfügen `ILoggerFactory` in Ihrem Konstruktor.</span><span class="sxs-lookup"><span data-stu-id="060b2-110">An instance of the handler will be created when your application starts, and DI will inject the registered `ILoggerFactory` into your constructor.</span></span>

> [!NOTE]
> <span data-ttu-id="060b2-111">Handler, die Verwendung von Entity Framework darf nicht als Singletons registriert werden.</span><span class="sxs-lookup"><span data-stu-id="060b2-111">Handlers that use Entity Framework shouldn't be registered as singletons.</span></span>
