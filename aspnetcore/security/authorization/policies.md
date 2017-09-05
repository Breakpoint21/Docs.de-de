---
title: Benutzerdefinierte Richtlinie basierende Autorisierung
author: rick-anderson
description: 
keywords: ASP.NET Core
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: e422a1b2-dc4a-4bcc-b8d9-7ee62009b6a3
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authorization/policies
ms.openlocfilehash: dd7187f67887bb39a5ff425dcbae0927c7565cb8
ms.sourcegitcommit: 41e3e007512c175a42910bc69678f3f0403cab04
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/01/2017
---
# <a name="custom-policy-based-authorization"></a><span data-ttu-id="3e6fb-103">Benutzerdefinierte Richtlinie basierende Autorisierung</span><span class="sxs-lookup"><span data-stu-id="3e6fb-103">Custom Policy-Based Authorization</span></span>

<a name=security-authorization-policies-based></a>

<span data-ttu-id="3e6fb-104">Im Hintergrund der [Rolle Autorisierung](roles.md#security-authorization-role-based) und [Ansprüche Autorisierung](claims.md#security-authorization-claims-based) Verwenden einer Anforderung verwendet wird, einen Handler für die Anforderung und eine vorkonfigurierte Richtlinie.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-104">Underneath the covers the [role authorization](roles.md#security-authorization-role-based) and [claims authorization](claims.md#security-authorization-claims-based) make use of a requirement, a handler for the requirement and a pre-configured policy.</span></span> <span data-ttu-id="3e6fb-105">Diese Bausteine ermöglichen es Ihnen, Autorisierung auswertungen in Code, sodass eine umfangreichere, wiederverwendet werden kann, und einer leicht testfähig Autorisierung Struktur auszudrücken.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-105">These building blocks allow you to express authorization evaluations in code, allowing for a richer, reusable, and easily testable authorization structure.</span></span>

<span data-ttu-id="3e6fb-106">Eine Autorisierungsrichtlinie setzt sich aus einer oder mehreren Anforderungen und als Teil der Dienstkonfiguration Autorisierung in beim Start der Anwendung registriert ist `ConfigureServices` in der *Startup.cs* Datei.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-106">An authorization policy is made up of one or more requirements and registered at application startup as part of the Authorization service configuration, in `ConfigureServices` in the *Startup.cs* file.</span></span>

<!-- literal_block {"ids": [], "names": [], "highlight_args": {}, "backrefs": [], "dupnames": [], "linenos": false, "classes": [], "xml:space": "preserve", "language": "c#"} -->

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    services.AddAuthorization(options =>
    {
        options.AddPolicy("Over21",
                          policy => policy.Requirements.Add(new MinimumAgeRequirement(21)));
    });
}
```

<span data-ttu-id="3e6fb-107">Hier sehen Sie sich, dass eine Richtlinie "Over21" mit einer einzelnen Anforderung erstellt wird, dass von einem Mindestalter, die als Parameter mit der Anforderung übergeben wird.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-107">Here you can see an "Over21" policy is created with a single requirement, that of a minimum age, which is passed as a parameter to the requirement.</span></span>

<span data-ttu-id="3e6fb-108">Richtlinien werden angewendet, mit der `Authorize` Attribut, indem Sie den Richtliniennamen, z. B. angeben</span><span class="sxs-lookup"><span data-stu-id="3e6fb-108">Policies are applied using the `Authorize` attribute by specifying the policy name, for example;</span></span>

<!-- literal_block {"ids": [], "names": [], "highlight_args": {}, "backrefs": [], "dupnames": [], "linenos": false, "classes": [], "xml:space": "preserve", "language": "c#"} -->

```csharp
[Authorize(Policy="Over21")]
public class AlcoholPurchaseRequirementsController : Controller
{
    public ActionResult Login()
    {
    }

    public ActionResult Logout()
    {
    }
}
```

## <a name="requirements"></a><span data-ttu-id="3e6fb-109">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="3e6fb-109">Requirements</span></span>

<span data-ttu-id="3e6fb-110">Eine autorisierungsanforderung ist eine Auflistung von Datenparametern, die eine Richtlinie zum Auswerten des aktuellen Benutzerprinzipals verwenden können.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-110">An authorization requirement is a collection of data parameters that a policy can use to evaluate the current user principal.</span></span> <span data-ttu-id="3e6fb-111">In unserer Mindestalter-Richtlinie ist die Anforderung haben wir einen einzelnen Parameter das Mindestalter.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-111">In our Minimum Age policy the requirement we have is a single parameter, the minimum age.</span></span> <span data-ttu-id="3e6fb-112">Implementieren einer Anforderung muss `IAuthorizationRequirement`.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-112">A requirement must implement `IAuthorizationRequirement`.</span></span> <span data-ttu-id="3e6fb-113">Dies ist eine leere, Markierungsschnittstelle.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-113">This is an empty, marker interface.</span></span> <span data-ttu-id="3e6fb-114">Eine parametrisierte Mindestalter-Anforderung kann wie folgt implementiert werden.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-114">A parameterized minimum age requirement might be implemented as follows;</span></span>

<!-- literal_block {"ids": [], "names": [], "highlight_args": {}, "backrefs": [], "dupnames": [], "linenos": false, "classes": [], "xml:space": "preserve", "language": "c#"} -->

```csharp
public class MinimumAgeRequirement : IAuthorizationRequirement
{
    public int MinimumAge { get; private set; }
    
    public MinimumAgeRequirement(int minimumAge)
    {
        MinimumAge = minimumAge;
    }
}
```

<span data-ttu-id="3e6fb-115">Eine Anforderung benötigen nicht Daten oder Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-115">A requirement doesn't need to have data or properties.</span></span>

<a name=security-authorization-policies-based-authorization-handler></a>

## <a name="authorization-handlers"></a><span data-ttu-id="3e6fb-116">Autorisierung Handler</span><span class="sxs-lookup"><span data-stu-id="3e6fb-116">Authorization Handlers</span></span>

<span data-ttu-id="3e6fb-117">Ein Authorization-Handler ist für die Auswertung von Eigenschaften einer Anforderung verantwortlich.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-117">An authorization handler is responsible for the evaluation of any properties of a requirement.</span></span> <span data-ttu-id="3e6fb-118">Der Handler für die Autorisierung muss anhand einer bereitgestellten bewerten `AuthorizationHandlerContext` entscheiden, ob Autorisierung zugelassen wird.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-118">The  authorization handler must evaluate them against a provided `AuthorizationHandlerContext` to decide if authorization is allowed.</span></span> <span data-ttu-id="3e6fb-119">Kann die Anforderung besteht [mehrere Handler](policies.md#security-authorization-policies-based-multiple-handlers).</span><span class="sxs-lookup"><span data-stu-id="3e6fb-119">A requirement can have [multiple handlers](policies.md#security-authorization-policies-based-multiple-handlers).</span></span> <span data-ttu-id="3e6fb-120">Handler erben müssen `AuthorizationHandler<T>` , wobei T die Anforderung wird verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-120">Handlers must inherit `AuthorizationHandler<T>` where T is the requirement it handles.</span></span>

<a name=security-authorization-handler-example></a>

<span data-ttu-id="3e6fb-121">Der Handler Mindestalter kann wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="3e6fb-121">The minimum age handler might look like this:</span></span>

<!-- literal_block {"ids": [], "names": [], "highlight_args": {}, "backrefs": [], "dupnames": [], "linenos": false, "classes": [], "xml:space": "preserve", "language": "c#"} -->

```csharp
public class MinimumAgeHandler : AuthorizationHandler<MinimumAgeRequirement>
{
    protected override Task HandleRequirementAsync(AuthorizationHandlerContext context, MinimumAgeRequirement requirement)
    {
        if (!context.User.HasClaim(c => c.Type == ClaimTypes.DateOfBirth &&
                                   c.Issuer == "http://contoso.com"))
        {
            // .NET 4.x -> return Task.FromResult(0);
            return Task.CompletedTask;
        }

        var dateOfBirth = Convert.ToDateTime(context.User.FindFirst(
            c => c.Type == ClaimTypes.DateOfBirth && c.Issuer == "http://contoso.com").Value);

        int calculatedAge = DateTime.Today.Year - dateOfBirth.Year;
        if (dateOfBirth > DateTime.Today.AddYears(-calculatedAge))
        {
            calculatedAge--;
        }

        if (calculatedAge >= requirement.MinimumAge)
        {
            context.Succeed(requirement);
        }
        return Task.CompletedTask;
    }
}
```

<span data-ttu-id="3e6fb-122">Im Code über untersuchen wir zuerst um festzustellen, ob der aktuelle Benutzer principal hat ein Geburtsdatum Anspruch, der durch einen Aussteller ist bekannt und Vertrauensstellung ausgegeben wurde.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-122">In the code above we first look to see if the current user principal has a date of birth claim which has been issued by an Issuer we know and trust.</span></span> <span data-ttu-id="3e6fb-123">Wenn der Anspruch nicht vorhanden ist kann nicht wir autorisiert, sodass wir zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-123">If the claim is missing we can't authorize so we return.</span></span> <span data-ttu-id="3e6fb-124">Wenn wir einen Anspruch haben, wir herausfinden, wie ALT der Benutzer ist und, wenn sie das Mindestalter übergebener die Anforderung erfüllen dann Autorisierung wurde erfolgreich ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-124">If we have a claim, we figure out how old the user is, and if they meet the minimum age passed in by the requirement then authorization has been successful.</span></span> <span data-ttu-id="3e6fb-125">Nach dem Autorisierung erfolgreich ist, die wir rufen `context.Succeed()` in der Anforderung, die wurde erfolgreich als Parameter übergeben.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-125">Once authorization is successful we call `context.Succeed()` passing in the requirement that has been successful as a parameter.</span></span>

<a name=security-authorization-policies-based-handler-registration></a>

<span data-ttu-id="3e6fb-126">Handler werden z. B. in der Auflistung der Dienste während der Konfiguration erfasst.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-126">Handlers must be registered in the services collection during configuration, for example;</span></span>

<!-- literal_block {"ids": [], "names": [], "highlight_args": {}, "backrefs": [], "dupnames": [], "linenos": false, "classes": [], "xml:space": "preserve", "language": "c#"} -->

```csharp

public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    services.AddAuthorization(options =>
    {
        options.AddPolicy("Over21",
                          policy => policy.Requirements.Add(new MinimumAgeRequirement(21)));
    });

    services.AddSingleton<IAuthorizationHandler, MinimumAgeHandler>();
}
```

<span data-ttu-id="3e6fb-127">Jeder Handler hinzugefügt, mit der Services-Auflistung mit `services.AddSingleton<IAuthorizationHandler, YourHandlerClass>();` in Ihrer Handlerklasse übergeben.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-127">Each handler is added to the services collection by using `services.AddSingleton<IAuthorizationHandler, YourHandlerClass>();` passing in your handler class.</span></span>

## <a name="what-should-a-handler-return"></a><span data-ttu-id="3e6fb-128">Was sollte ein Handler zurückgeben?</span><span class="sxs-lookup"><span data-stu-id="3e6fb-128">What should a handler return?</span></span>

<span data-ttu-id="3e6fb-129">Sehen Sie unserer [Handler Beispiel](policies.md#security-authorization-handler-example) , die die `Handle()` Methode verfügt über keinen Wert zurückgibt, wie wir geben Erfolg oder Fehler?</span><span class="sxs-lookup"><span data-stu-id="3e6fb-129">You can see in our [handler example](policies.md#security-authorization-handler-example) that the `Handle()` method has no return value, so how do we indicate success or failure?</span></span>

* <span data-ttu-id="3e6fb-130">Ein Handler gibt die erfolgreiche Ausführung durch den Aufruf `context.Succeed(IAuthorizationRequirement requirement)`, übergeben der Anforderung, die erfolgreich überprüft wurde.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-130">A handler indicates success by calling `context.Succeed(IAuthorizationRequirement requirement)`, passing the requirement that has been successfully validated.</span></span>

* <span data-ttu-id="3e6fb-131">Ein Ereignishandler muss nicht im allgemeinen Fehler zu behandeln, wie andere Handler für die gleiche Anforderung erfolgreich ausgeführt werden können.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-131">A handler does not need to handle failures generally, as other handlers for the same requirement may succeed.</span></span>

* <span data-ttu-id="3e6fb-132">Um Fehler zu gewährleisten, selbst wenn andere Handler für eine Anforderung erfolgreich ist, rufen Sie `context.Fail`.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-132">To guarantee failure even if other handlers for a requirement succeed, call `context.Fail`.</span></span>

<span data-ttu-id="3e6fb-133">Unabhängig davon, was Sie innerhalb der Handler aufgerufen werden alle Handler für eine Anforderung aufgerufen werden, wenn eine Richtlinie der Anforderung erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-133">Regardless of what you call inside your handler all handlers for a requirement will be called when a policy requires the requirement.</span></span> <span data-ttu-id="3e6fb-134">Anforderungen an, wie z. B. Protokollierung, haben Nebeneffekte, die immer stattfinden wird dadurch auch wenn `context.Fail()` in einen anderen Handler aufgerufen wurde.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-134">This allows requirements to have side effects, such as logging, which will always take place even if `context.Fail()` has been called in another handler.</span></span>

<a name=security-authorization-policies-based-multiple-handlers></a>

## <a name="why-would-i-want-multiple-handlers-for-a-requirement"></a><span data-ttu-id="3e6fb-135">Warum würde ich mehrere Handler für eine Anforderung?</span><span class="sxs-lookup"><span data-stu-id="3e6fb-135">Why would I want multiple handlers for a requirement?</span></span>

<span data-ttu-id="3e6fb-136">In Fällen soll Auswertung auf eine **oder** Grundlage Sie mehrere Handler für eine einzelne Anforderung implementieren.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-136">In cases where you want evaluation to be on an **OR** basis you implement multiple handlers for a single requirement.</span></span> <span data-ttu-id="3e6fb-137">Microsoft hat es sich beispielsweise um Türen, die nur mit Schlüssel Karten zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-137">For example, Microsoft has doors which only open with key cards.</span></span> <span data-ttu-id="3e6fb-138">Wenn Sie Ihre Schlüsselkarte zu Hause lassen, die Apparate druckt einen temporären Aufkleber und öffnet die Tür für Sie.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-138">If you leave your key card at home the receptionist prints a temporary sticker and opens the door for you.</span></span> <span data-ttu-id="3e6fb-139">In diesem Fall müssten Sie eine einzelne Anforderung *EnterBuilding*, aber mehrere Handler, die jeweils eine einzelne Anforderung überprüfen.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-139">In this scenario you'd have a single requirement, *EnterBuilding*, but multiple handlers, each one examining a single requirement.</span></span>

<!-- literal_block {"ids": [], "names": [], "highlight_args": {}, "backrefs": [], "dupnames": [], "linenos": false, "classes": [], "xml:space": "preserve", "language": "c#"} -->

```csharp
public class EnterBuildingRequirement : IAuthorizationRequirement
{
}

public class BadgeEntryHandler : AuthorizationHandler<EnterBuildingRequirement>
{
    protected override Task HandleRequirementAsync(AuthorizationHandlerContext context, EnterBuildingRequirement requirement)
    {
        if (context.User.HasClaim(c => c.Type == ClaimTypes.BadgeId &&
                                       c.Issuer == "http://microsoftsecurity"))
        {
            context.Succeed(requirement);
        }
        return Task.CompletedTask;
    }
}

public class HasTemporaryStickerHandler : AuthorizationHandler<EnterBuildingRequirement>
{
    protected override Task HandleRequirementAsync(AuthorizationHandlerContext context, EnterBuildingRequirement requirement)
    {
        if (context.User.HasClaim(c => c.Type == ClaimTypes.TemporaryBadgeId &&
                                       c.Issuer == "https://microsoftsecurity"))
        {
            // We'd also check the expiration date on the sticker.
            context.Succeed(requirement);
        }
        return Task.CompletedTask;
    }
}
```

<span data-ttu-id="3e6fb-140">Nun sind die beiden Handler vorausgesetzt [registriert](xref:security/authorization/policies#security-authorization-policies-based-handler-registration) Wenn eine Richtlinie auswertet der `EnterBuildingRequirement` richtlinienauswertung ist erfolgreich, wenn die beiden Ereignishandler erfolgreich ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-140">Now, assuming both handlers are [registered](xref:security/authorization/policies#security-authorization-policies-based-handler-registration) when a policy evaluates the `EnterBuildingRequirement` if either handler succeeds the policy evaluation will succeed.</span></span>

## <a name="using-a-func-to-fulfill-a-policy"></a><span data-ttu-id="3e6fb-141">Func verwenden, um eine Richtlinie zu erfüllen.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-141">Using a func to fulfill a policy</span></span>

<span data-ttu-id="3e6fb-142">Es kann durchaus vorkommen, in denen Erfüllung einer Richtlinie einfach zu express im Code ist.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-142">There may be occasions where fulfilling a policy is simple to express in code.</span></span> <span data-ttu-id="3e6fb-143">Es ist möglich, geben Sie einfach eine `Func<AuthorizationHandlerContext, bool>` beim Konfigurieren der Richtlinie mit den `RequireAssertion` Richtlinie-Generator.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-143">It is possible to simply supply a `Func<AuthorizationHandlerContext, bool>` when configuring your policy with the `RequireAssertion` policy builder.</span></span>

<span data-ttu-id="3e6fb-144">Z. B. den vorherigen `BadgeEntryHandler` neu geschrieben werden, wie folgt;</span><span class="sxs-lookup"><span data-stu-id="3e6fb-144">For example the previous `BadgeEntryHandler` could be rewritten as follows;</span></span>

<!-- literal_block {"ids": [], "names": [], "highlight_args": {}, "backrefs": [], "dupnames": [], "linenos": false, "classes": [], "xml:space": "preserve", "language": "c#"} -->

```csharp
services.AddAuthorization(options =>
    {
        options.AddPolicy("BadgeEntry",
                          policy => policy.RequireAssertion(context =>
                                  context.User.HasClaim(c =>
                                     (c.Type == ClaimTypes.BadgeId ||
                                      c.Type == ClaimTypes.TemporaryBadgeId)
                                      && c.Issuer == "https://microsoftsecurity"));
                          }));
    }
 }
```

## <a name="accessing-mvc-request-context-in-handlers"></a><span data-ttu-id="3e6fb-145">Zugreifen auf die MVC-Anforderungskontext In Handlern abfangen</span><span class="sxs-lookup"><span data-stu-id="3e6fb-145">Accessing MVC Request Context In Handlers</span></span>

<span data-ttu-id="3e6fb-146">Die `Handle` Methode müssen Sie in einem Ereignishandler für die Autorisierung implementieren verfügt über zwei Parameter ein `AuthorizationContext` und `Requirement` Sie verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-146">The `Handle` method you must implement in an authorization handler has two parameters, an `AuthorizationContext` and the `Requirement` you are handling.</span></span> <span data-ttu-id="3e6fb-147">Frameworks wie z. B. Mvc- oder Jabbr sind frei, um ein Objekt zum Hinzufügen der `Resource` Eigenschaft auf die `AuthorizationContext` für die Weiterleitung über zusätzliche Informationen.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-147">Frameworks such as MVC or Jabbr are free to add any object to the `Resource` property on the `AuthorizationContext` to pass through extra information.</span></span>

<span data-ttu-id="3e6fb-148">Z. B. MVC übergibt eine Instanz des `Microsoft.AspNetCore.Mvc.Filters.AuthorizationFilterContext` in die Ressourceneigenschaft "dient zum Zugriff HttpContext", "RouteData" und "Alles" else MVC bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-148">For example MVC passes an instance of `Microsoft.AspNetCore.Mvc.Filters.AuthorizationFilterContext` in the resource property which is used to access HttpContext, RouteData and everything else MVC provides.</span></span>

<span data-ttu-id="3e6fb-149">Die Verwendung der `Resource` Eigenschaft ist für bestimmte Framework.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-149">The use of the `Resource` property is framework specific.</span></span> <span data-ttu-id="3e6fb-150">Mithilfe der Informationen in der `Resource` Eigenschaft schränkt die Autorisierungsrichtlinien auf bestimmten Frameworks.</span><span class="sxs-lookup"><span data-stu-id="3e6fb-150">Using information in the `Resource` property will limit your authorization policies to particular frameworks.</span></span> <span data-ttu-id="3e6fb-151">Sollten Sie eine Umwandlung der `Resource` Eigenschaft mit der `as` -Schlüsselwort, und überprüfen Sie die Umwandlung wurde erfolgreich ausgeführt werden, um sicherzustellen, dass Ihr Code keine stürzt ab mit `InvalidCastExceptions` bei Ausführung auf anderen Frameworks;</span><span class="sxs-lookup"><span data-stu-id="3e6fb-151">You should cast the `Resource` property using the `as` keyword, and then check the cast has succeed to ensure your code doesn't crash with `InvalidCastExceptions` when run on other frameworks;</span></span>

<!-- literal_block {"ids": [], "names": [], "highlight_args": {}, "backrefs": [], "dupnames": [], "linenos": false, "classes": [], "xml:space": "preserve", "language": "c#"} -->

```csharp
if (context.Resource is Microsoft.AspNetCore.Mvc.Filters.AuthorizationFilterContext mvcContext)
{
    // Examine MVC specific things like routing data.
}
```
