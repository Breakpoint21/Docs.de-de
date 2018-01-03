<span data-ttu-id="5b45a-101">Ersetzen Sie den Inhalt von *Controllers/HelloWorldController.cs* durch Folgendes:</span><span class="sxs-lookup"><span data-stu-id="5b45a-101">Replace the contents of *Controllers/HelloWorldController.cs* with the following:</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/HelloWorldController.cs?name=snippet_1)]

<span data-ttu-id="5b45a-102">Jede `public`-Methode in einem Controller kann als HTTP-Endpunkt aufgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="5b45a-102">Every `public` method in a controller is callable as an HTTP endpoint.</span></span> <span data-ttu-id="5b45a-103">Im obigen Beispiel geben beide Methoden eine Zeichenfolge zurück.</span><span class="sxs-lookup"><span data-stu-id="5b45a-103">In the sample above, both methods return a string.</span></span>  <span data-ttu-id="5b45a-104">Beachten Sie die Kommentare vor jeder Methode.</span><span class="sxs-lookup"><span data-stu-id="5b45a-104">Note the comments preceding each method.</span></span>

<span data-ttu-id="5b45a-105">Ein HTTP-Endpunkt ist eine Ziel-URL in der Webanwendung, wie z.B. `http://localhost:1234/HelloWorld`, und kombiniert das verwendete Protokoll `HTTP`, die Netzwerkadresse des Webservers (einschließlich TCP-Port) `localhost:1234` und den Ziel-URI `HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="5b45a-105">An HTTP endpoint is a targetable URL in the web application, such as `http://localhost:1234/HelloWorld`, and combines the protocol used: `HTTP`, the network location of the web server (including the TCP port): `localhost:1234` and the target URI `HelloWorld`.</span></span>

<span data-ttu-id="5b45a-106">Der erste Kommentar besagt, dass dies eine [HTTP GET](https://www.w3schools.com/tags/ref_httpmethods.asp)-Methode ist, die durch Anfügen von „/HelloWorld/“ an die Basis-URL aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="5b45a-106">The first comment states this is an [HTTP GET](https://www.w3schools.com/tags/ref_httpmethods.asp) method that is invoked by appending "/HelloWorld/" to the base URL.</span></span> <span data-ttu-id="5b45a-107">Der zweite Kommentar gibt eine [HTTP GET](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)-Methode an, die durch Anfügen von „/HelloWorld/Welcome/“ an die URL aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="5b45a-107">The second comment specifies an [HTTP GET](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) method that is invoked by appending "/HelloWorld/Welcome/" to the URL.</span></span> <span data-ttu-id="5b45a-108">Im weiteren Verlauf des Tutorials nutzen Sie das Gerüstbaumodul zum Generieren von `HTTP POST`-Methoden.</span><span class="sxs-lookup"><span data-stu-id="5b45a-108">Later on in the tutorial you'll use the scaffolding engine to generate `HTTP POST` methods.</span></span>

<span data-ttu-id="5b45a-109">Führen Sie die App im Nicht-Debugmodus aus, und fügen Sie „HelloWorld“ an den Pfad in der Adressleiste an.</span><span class="sxs-lookup"><span data-stu-id="5b45a-109">Run the app in non-debug mode and append "HelloWorld" to the path in the address bar.</span></span> <span data-ttu-id="5b45a-110">Die `Index`-Methode gibt eine Zeichenfolge zurück.</span><span class="sxs-lookup"><span data-stu-id="5b45a-110">The `Index` method returns a string.</span></span>

![Browserfenster mit der Anwendungsantwort „This is my default action“](../../tutorials/first-mvc-app/adding-controller/_static/hell1.png)

<span data-ttu-id="5b45a-112">MVC ruft Controllerklassen (und darin enthaltene Aktionsmethoden) abhängig von der eingehenden URL auf.</span><span class="sxs-lookup"><span data-stu-id="5b45a-112">MVC invokes controller classes (and the action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="5b45a-113">Die von MVC verwendete standardmäßige [URL-Routinglogik](../../mvc/controllers/routing.md) befolgt ein Format wie dieses, um den aufzurufenden Code zu bestimmen:</span><span class="sxs-lookup"><span data-stu-id="5b45a-113">The default [URL routing logic](../../mvc/controllers/routing.md) used by MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="5b45a-114">Sie legen das Format für das Routing in der Datei *Startup.cs* fest.</span><span class="sxs-lookup"><span data-stu-id="5b45a-114">You set the format for routing in the *Startup.cs* file.</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?name=snippet_1&highlight=5)]

<span data-ttu-id="5b45a-115">Wenn Sie die App auszuführen und keine URL-Segmente angeben, werden standardmäßig der Controller „Home“ und die Methode „Index“ verwendet, die in der oben hervorgehobenen Vorlagenzeile angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="5b45a-115">When you run the app and don't supply any URL segments, it defaults to the "Home" controller and the "Index" method specified in the template line highlighted above.</span></span>

<span data-ttu-id="5b45a-116">Das erste URL-Segment bestimmt die auszuführende Controllerklasse.</span><span class="sxs-lookup"><span data-stu-id="5b45a-116">The first URL segment determines the controller class to run.</span></span> <span data-ttu-id="5b45a-117">Daher wird `localhost:xxxx/HelloWorld` der `HelloWorldController`-Klasse zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="5b45a-117">So `localhost:xxxx/HelloWorld` maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="5b45a-118">Der zweite Teil des URL-Segments bestimmt die Aktionsmethode für die Klasse.</span><span class="sxs-lookup"><span data-stu-id="5b45a-118">The second part of the URL segment determines the action method on the class.</span></span> <span data-ttu-id="5b45a-119">Daher bewirkt `localhost:xxxx/HelloWorld/Index` das Ausführen der `Index`-Methode der `HelloWorldController`-Klasse.</span><span class="sxs-lookup"><span data-stu-id="5b45a-119">So `localhost:xxxx/HelloWorld/Index` would cause the `Index` method of the `HelloWorldController` class to run.</span></span> <span data-ttu-id="5b45a-120">Beachten Sie, dass Sie nur zu `localhost:xxxx/HelloWorld` navigieren mussten und die `Index`-Methode standardmäßig aufgerufen wurde.</span><span class="sxs-lookup"><span data-stu-id="5b45a-120">Notice that you only had to browse to `localhost:xxxx/HelloWorld` and the `Index` method was called by default.</span></span> <span data-ttu-id="5b45a-121">Der Grund hierfür ist, dass `Index` die Standardmethode ist, die für einen Controller aufgerufen wird, wenn der Methodenname nicht explizit angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="5b45a-121">This is because `Index` is the default method that will be called on a controller if a method name is not explicitly specified.</span></span> <span data-ttu-id="5b45a-122">Der dritte Teil des URL-Segments (`id`) ist für Routendaten.</span><span class="sxs-lookup"><span data-stu-id="5b45a-122">The third part of the URL segment ( `id`) is for route data.</span></span> <span data-ttu-id="5b45a-123">Routendaten werden im weiteren Verlauf dieses Tutorials behandelt.</span><span class="sxs-lookup"><span data-stu-id="5b45a-123">You'll see route data later on in this tutorial.</span></span>

<span data-ttu-id="5b45a-124">Wechseln Sie zu `http://localhost:xxxx/HelloWorld/Welcome`.</span><span class="sxs-lookup"><span data-stu-id="5b45a-124">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="5b45a-125">Die `Welcome`-Methode wird ausgeführt und gibt die Zeichenfolge „This is the Welcome action method...“ zurück.</span><span class="sxs-lookup"><span data-stu-id="5b45a-125">The `Welcome` method runs and returns the string "This is the Welcome action method...".</span></span> <span data-ttu-id="5b45a-126">Bei dieser URL ist `HelloWorld` der Controller und `Welcome` die Aktionsmethode.</span><span class="sxs-lookup"><span data-stu-id="5b45a-126">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="5b45a-127">Sie haben den Teil `[Parameters]` der URL noch nicht verwendet.</span><span class="sxs-lookup"><span data-stu-id="5b45a-127">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![Browserfenster mit der Anwendungsantwort „This is the Welcome action method“](../../tutorials/first-mvc-app/adding-controller/_static/welcome.png)

<span data-ttu-id="5b45a-129">Ändern Sie den Code so, dass Parameterinformationen von der URL an den Controller übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="5b45a-129">Modify the code to pass some parameter information from the URL to the controller.</span></span> <span data-ttu-id="5b45a-130">Beispielsweise `/HelloWorld/Welcome?name=Rick&numtimes=4`.</span><span class="sxs-lookup"><span data-stu-id="5b45a-130">For example, `/HelloWorld/Welcome?name=Rick&numtimes=4`.</span></span> <span data-ttu-id="5b45a-131">Ändern Sie `Welcome`-Methode so, dass zwei Parameter, wie im folgenden Code gezeigt, einbezogen werden.</span><span class="sxs-lookup"><span data-stu-id="5b45a-131">Change the `Welcome` method to include two parameters as shown in the following code.</span></span> 

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/HelloWorldController.cs?name=snippet_2)]

<span data-ttu-id="5b45a-132">Der vorangehende Code:</span><span class="sxs-lookup"><span data-stu-id="5b45a-132">The preceding code:</span></span>

* <span data-ttu-id="5b45a-133">Verwendet das C#-Feature „optional-parameter“, um anzugeben, dass der `numTimes`-Parameter standardmäßig 1 ist, wenn kein anderer Wert für diesen Parameter übergeben wird.</span><span class="sxs-lookup"><span data-stu-id="5b45a-133">Uses the C# optional-parameter feature to indicate that the `numTimes` parameter defaults to 1 if no value is passed for that parameter.</span></span>
* <span data-ttu-id="5b45a-134">Verwendet `HtmlEncoder.Default.Encode`, um die App vor schädlicher Eingaben (über JavaScript) zu schützen.</span><span class="sxs-lookup"><span data-stu-id="5b45a-134">Uses`HtmlEncoder.Default.Encode` to protect the app from malicious input (namely JavaScript).</span></span> 
* <span data-ttu-id="5b45a-135">Verwendet [interpolierte Zeichenfolgen](https://docs.microsoft.com/dotnet/articles/csharp/language-reference/keywords/interpolated-strings).</span><span class="sxs-lookup"><span data-stu-id="5b45a-135">Uses [Interpolated Strings](https://docs.microsoft.com/dotnet/articles/csharp/language-reference/keywords/interpolated-strings).</span></span>

<span data-ttu-id="5b45a-136">Führen Sie die App aus, und navigieren Sie zu:</span><span class="sxs-lookup"><span data-stu-id="5b45a-136">Run your app and browse to:</span></span>

   `http://localhost:xxxx/HelloWorld/Welcome?name=Rick&numtimes=4`

<span data-ttu-id="5b45a-137">(Ersetzen Sie xxxx durch Ihre Portnummer.) Sie können für `name` und `numtimes` in der URL verschiedene Werte ausprobieren.</span><span class="sxs-lookup"><span data-stu-id="5b45a-137">(Replace xxxx with your port number.) You can try different values for `name` and `numtimes` in  the URL.</span></span> <span data-ttu-id="5b45a-138">Das MVC-[Modellbindungssystem](../../mvc/models/model-binding.md) ordnet automatisch die benannten Parameter aus der Abfragezeichenfolge auf der Adressleiste den Parametern der Methode zu.</span><span class="sxs-lookup"><span data-stu-id="5b45a-138">The MVC [model binding](../../mvc/models/model-binding.md) system automatically maps the named parameters from  the query string in the address bar to parameters in your method.</span></span> <span data-ttu-id="5b45a-139">Weitere Informationen finden Sie unter [Modellbindung](../../mvc/models/model-binding.md).</span><span class="sxs-lookup"><span data-stu-id="5b45a-139">See [Model Binding](../../mvc/models/model-binding.md) for more information.</span></span>

![Browserfenster mit der Anwendungsantwort „Hello Rick, NumTimes is: 4“](../../tutorials/first-mvc-app/adding-controller/_static/rick4.png)

<span data-ttu-id="5b45a-141">In der obigen Abbildung wird das URL-Segment (`Parameters`) nicht verwendet, und die Parameter `name` und `numTimes` werden als [Abfragezeichenfolgen](https://wikipedia.org/wiki/Query_string) übergeben.</span><span class="sxs-lookup"><span data-stu-id="5b45a-141">In the image above, the URL segment (`Parameters`) is not used, the `name` and `numTimes` parameters are passed as [query strings](https://wikipedia.org/wiki/Query_string).</span></span> <span data-ttu-id="5b45a-142">Das Fragezeichen (`?`) in der obigen URL ist ein Trennzeichen, auf das die Abfragezeichenfolgen folgen.</span><span class="sxs-lookup"><span data-stu-id="5b45a-142">The `?` (question mark) in the above URL is a separator, and the query strings follow.</span></span> <span data-ttu-id="5b45a-143">Das Zeichen `&` trennt Abfragezeichenfolgen.</span><span class="sxs-lookup"><span data-stu-id="5b45a-143">The `&` character separates query strings.</span></span>

<span data-ttu-id="5b45a-144">Ersetzen Sie die `Welcome`-Methode durch folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="5b45a-144">Replace the `Welcome` method with the following code:</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/HelloWorldController.cs?name=snippet_3)]

<span data-ttu-id="5b45a-145">Führen Sie die App aus, und geben Sie die folgende URL ein: `http://localhost:xxx/HelloWorld/Welcome/3?name=Rick`</span><span class="sxs-lookup"><span data-stu-id="5b45a-145">Run the app and enter the following URL:  `http://localhost:xxx/HelloWorld/Welcome/3?name=Rick`</span></span>

![Browserfenster mit der Anwendungsantwort „Hello Rick, ID 3“](../../tutorials/first-mvc-app/adding-controller/_static/rick_routedata.png)

<span data-ttu-id="5b45a-147">Dieses Mal hat das dritte URL-Segment mit dem Routenparameter `id` übereingestimmt.</span><span class="sxs-lookup"><span data-stu-id="5b45a-147">This time the third URL segment  matched the route parameter `id`.</span></span> <span data-ttu-id="5b45a-148">Die `Welcome`-Methode enthält den Parameter `id`, der mit der URL-Vorlage in der `MapRoute`-Methode übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="5b45a-148">The `Welcome`  method contains a parameter  `id` that matched the URL template in the `MapRoute` method.</span></span> <span data-ttu-id="5b45a-149">Das nachfolgende `?` (in `id?`) gibt an, dass der Parameter `id` optional ist.</span><span class="sxs-lookup"><span data-stu-id="5b45a-149">The trailing `?`  (in `id?`) indicates the `id` parameter is optional.</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?name=snippet_1&highlight=5)]

<span data-ttu-id="5b45a-150">In diesen Beispielen hat der Controller den „VC“-Teil von MVC übernommen, d.h. die Aufgaben von „View“ (Ansicht) und „Controller“.</span><span class="sxs-lookup"><span data-stu-id="5b45a-150">In these examples the controller has been doing the "VC" portion  of MVC - that is, the view and controller work.</span></span> <span data-ttu-id="5b45a-151">Der Controller gibt HTML direkt zurück.</span><span class="sxs-lookup"><span data-stu-id="5b45a-151">The controller is returning HTML  directly.</span></span> <span data-ttu-id="5b45a-152">Im Allgemeinen sollen Controller HTML nicht direkt zurückgeben, da dies sehr aufwändig zu programmieren und pflegen ist.</span><span class="sxs-lookup"><span data-stu-id="5b45a-152">Generally you don't want controllers returning HTML directly, since  that becomes very cumbersome to code and maintain.</span></span> <span data-ttu-id="5b45a-153">Stattdessen verwenden Sie in der Regel eine separate Razor-Ansichtsvorlagendatei, um die HTML-Antwort zu generieren.</span><span class="sxs-lookup"><span data-stu-id="5b45a-153">Instead you typically use a separate Razor view template file to help generate the HTML response.</span></span> <span data-ttu-id="5b45a-154">Dies lernen Sie im nächsten Tutorial.</span><span class="sxs-lookup"><span data-stu-id="5b45a-154">You do that in the next tutorial.</span></span>