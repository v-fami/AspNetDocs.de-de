---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
title: URL-Routing | Microsoft-Dokumentation
author: Erikre
description: Diese lernprogrammreihe vermittelt Ihnen die Grundlagen zum Erstellen einer ASP.NET Web Forms-Anwendung mithilfe von ASP.NET 4.5 und Microsoft Visual Studio Express 2013 für wir...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 4f4bf092-c400-471f-a876-78fda0417890
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
msc.type: authoredcontent
ms.openlocfilehash: d9f0779d560d6ec7796a16dc2996b959dd171c80
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062357"
---
<a name="url-routing"></a><span data-ttu-id="27141-103">URL-Routing</span><span class="sxs-lookup"><span data-stu-id="27141-103">URL Routing</span></span>
====================
<span data-ttu-id="27141-104">by [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="27141-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="27141-105">[Herunterladen der Wingtip Toys-Beispielprojekts (c#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) oder [E-Book (PDF) herunterladen](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="27141-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="27141-106">Diese lernprogrammreihe vermittelt Ihnen die Grundlagen zum Erstellen einer ASP.NET Web Forms-Anwendung mithilfe von ASP.NET 4.5 und Microsoft Visual Studio Express 2013 für Web.</span><span class="sxs-lookup"><span data-stu-id="27141-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="27141-107">Eine Visual Studio 2013 [-Projekts mit C#-Quellcode](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) ist verfügbar, die dieser tutorialreihe begleitet.</span><span class="sxs-lookup"><span data-stu-id="27141-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>


<span data-ttu-id="27141-108">In diesem Tutorial ändern Sie die Wingtip Toys-beispielanwendung, um URL-routing zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="27141-108">In this tutorial, you will modify the Wingtip Toys sample application to support URL routing.</span></span> <span data-ttu-id="27141-109">Routing können Ihre Webanwendung in URLs verwenden, die benutzerfreundliche, leichter zu merken und von Suchmaschinen besser unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="27141-109">Routing enables your web application to use URLs that are friendly, easier to remember, and better supported by search engines.</span></span> <span data-ttu-id="27141-110">Dieses Tutorial baut auf dem vorherigen Lernprogramm "Mitgliedschaft und Verwaltung" und ist Teil der tutorialreihe Wingtip Toys.</span><span class="sxs-lookup"><span data-stu-id="27141-110">This tutorial builds on the previous tutorial "Membership and Administration" and is part of the Wingtip Toys tutorial series.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="27141-111">Sie lernen Folgendes:</span><span class="sxs-lookup"><span data-stu-id="27141-111">What you'll learn:</span></span>

- <span data-ttu-id="27141-112">Vorgehensweise: Registrieren von Routen für eine ASP.NET Web Forms-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="27141-112">How to register routes for an ASP.NET Web Forms application.</span></span>
- <span data-ttu-id="27141-113">Das Hinzufügen von Routen zu einer Webseite.</span><span class="sxs-lookup"><span data-stu-id="27141-113">How to add routes to a web page.</span></span>
- <span data-ttu-id="27141-114">Auswählen von Daten aus einer Datenbank aus, um Routen zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="27141-114">How to select data from a database to support routes.</span></span>

## <a name="aspnet-routing-overview"></a><span data-ttu-id="27141-115">Übersicht über ASP.NET das Routing</span><span class="sxs-lookup"><span data-stu-id="27141-115">ASP.NET Routing Overview</span></span>

<span data-ttu-id="27141-116">URL-routing, können Sie zum Konfigurieren einer Anwendung zum Akzeptieren von Anforderungs-URLs, die nicht auf physischen Dateien zugeordnet sind.</span><span class="sxs-lookup"><span data-stu-id="27141-116">URL routing allows you to configure an application to accept request URLs that do not map to physical files.</span></span> <span data-ttu-id="27141-117">Eine Anforderungs-URL ist einfach die URL, die ein Benutzer in ihrem Browser eine Seite auf Ihrer Website sucht eingibt.</span><span class="sxs-lookup"><span data-stu-id="27141-117">A request URL is simply the URL a user enters into their browser to find a page on your web site.</span></span> <span data-ttu-id="27141-118">Sie verwenden routing, um die URLs zu definieren, die semantisch für Benutzer von Bedeutung sind, und suchen-suchmaschinenoptimierung (SEO) unterstützen kann.</span><span class="sxs-lookup"><span data-stu-id="27141-118">You use routing to define URLs that are semantically meaningful to users and that can help with search-engine optimization (SEO).</span></span>

<span data-ttu-id="27141-119">Standardmäßig enthält die Web Forms-Vorlage [Friendly URLs von ASP.NET](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/).</span><span class="sxs-lookup"><span data-stu-id="27141-119">By default, the Web Forms template includes [ASP.NET Friendly URLs](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/).</span></span> <span data-ttu-id="27141-120">Großteil der Arbeit mit grundlegenden routing wird implementiert werden, indem *Friendly URLs*.</span><span class="sxs-lookup"><span data-stu-id="27141-120">Much of the basic routing work will be implemented by using *Friendly URLs*.</span></span> <span data-ttu-id="27141-121">In diesem Tutorial werden Sie jedoch benutzerdefinierte Routingfunktionen hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="27141-121">However, in this tutorial you will add customized routing capabilities.</span></span>

<span data-ttu-id="27141-122">Vor dem Anpassen der URL-routing, kann die Wingtip Toys-beispielanwendung mit einem Produkt mit der folgenden URL verknüpfen:</span><span class="sxs-lookup"><span data-stu-id="27141-122">Before customizing URL routing, the Wingtip Toys sample application can link to a product using the following URL:</span></span>

`https://localhost:44300/ProductDetails.aspx?productID=2`

<span data-ttu-id="27141-123">Durch das Anpassen der URL-routing, werden die Wingtip Toys-beispielanwendung ein einfacher, lesen Sie die URL mit dem Produkt verknüpft:</span><span class="sxs-lookup"><span data-stu-id="27141-123">By customizing URL routing, the Wingtip Toys sample application will link to the same product using an easier to read URL:</span></span>

`https://localhost:44300/Product/Convertible%20Car`

### <a name="routes"></a><span data-ttu-id="27141-124">Routen</span><span class="sxs-lookup"><span data-stu-id="27141-124">Routes</span></span>

<span data-ttu-id="27141-125">Eine Route ist ein URL-Muster, das einen Handler zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="27141-125">A route is a URL pattern that is mapped to a handler.</span></span> <span data-ttu-id="27141-126">Der Handler kann es sich um eine physische Datei, z. B. eine ASPX-Datei in einer Web Forms-Anwendung sein.</span><span class="sxs-lookup"><span data-stu-id="27141-126">The handler can be a physical file, such as an .aspx file in a Web Forms application.</span></span> <span data-ttu-id="27141-127">Ein Ereignishandler kann auch eine Klasse sein, die die Anforderung verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="27141-127">A handler can also be a class that processes the request.</span></span> <span data-ttu-id="27141-128">Um eine Route definieren, erstellen Sie eine Instanz der Klasse Route durch Angabe der URL-Muster, die Ereignishandler und optional einen Namen für die Route an.</span><span class="sxs-lookup"><span data-stu-id="27141-128">To define a route, you create an instance of the Route class by specifying the URL pattern, the handler, and optionally a name for the route.</span></span>

<span data-ttu-id="27141-129">Die Route wird zur Anwendung hinzufügen, durch das Hinzufügen der `Route` Objekt an die statische `Routes` Eigenschaft der `RouteTable` Klasse.</span><span class="sxs-lookup"><span data-stu-id="27141-129">You add the route to the application by adding the `Route` object to the static `Routes` property of the `RouteTable` class.</span></span> <span data-ttu-id="27141-130">Die Routen-Eigenschaft ist eine `RouteCollection` -Objekt, das alle Routen für die Anwendung gespeichert.</span><span class="sxs-lookup"><span data-stu-id="27141-130">The Routes property is a `RouteCollection` object that stores all the routes for the application.</span></span>

### <a name="url-patterns"></a><span data-ttu-id="27141-131">URL-Muster</span><span class="sxs-lookup"><span data-stu-id="27141-131">URL Patterns</span></span>

<span data-ttu-id="27141-132">Ein URL-Muster kann es sich um Literalwerte und Variable Platzhalter (bezeichnet als URL-Parameter) enthalten.</span><span class="sxs-lookup"><span data-stu-id="27141-132">A URL pattern can contain literal values and variable placeholders (referred to as URL parameters).</span></span> <span data-ttu-id="27141-133">Literalwerte und Platzhalter befinden sich in Segmente der URL durch den Schrägstrich getrennt sind (`/`) Zeichen.</span><span class="sxs-lookup"><span data-stu-id="27141-133">The literals and placeholders are located in segments of the URL which are delimited by the slash (`/`) character.</span></span>

<span data-ttu-id="27141-134">Wenn eine Anforderung an Ihre Web-Anwendung erfolgt, die URL in Segmente und Platzhalter zerlegt wird, und die Variablenwerte werden bereitgestellt, um den Ereignishandler der Anforderung.</span><span class="sxs-lookup"><span data-stu-id="27141-134">When a request to your web application is made, the URL is parsed into segments and placeholders, and the variable values are provided to the request handler.</span></span> <span data-ttu-id="27141-135">Dieser Prozess ist ähnlich wie die Daten in einer Abfragezeichenfolge analysiert und an den Ereignishandler der Anforderung übergeben.</span><span class="sxs-lookup"><span data-stu-id="27141-135">This process is similar to the way the data in a query string is parsed and passed to the request handler.</span></span> <span data-ttu-id="27141-136">In beiden Fällen Informationen enthalten, die in der URL und der Handler in Form von Schlüssel-Wert-Paaren übergeben.</span><span class="sxs-lookup"><span data-stu-id="27141-136">In both cases, variable information is included in the URL and passed to the handler in the form of key-value pairs.</span></span> <span data-ttu-id="27141-137">Sind für Abfragezeichenfolgen beide Schlüssel und die Werte in der URL ein.</span><span class="sxs-lookup"><span data-stu-id="27141-137">For query strings, both the keys and the values are in the URL.</span></span> <span data-ttu-id="27141-138">Für Routen die Schlüssel sind die Platzhalternamen, die in der URL-Muster definiert, und nur die Werte sind in der URL.</span><span class="sxs-lookup"><span data-stu-id="27141-138">For routes, the keys are the placeholder names defined in the URL pattern, and only the values are in the URL.</span></span>

<span data-ttu-id="27141-139">In einem URL-Muster, definieren Sie Platzhalter in geschweiften Klammern ( `{` und `}` ).</span><span class="sxs-lookup"><span data-stu-id="27141-139">In a URL pattern, you define placeholders by enclosing them in braces ( `{` and `}` ).</span></span> <span data-ttu-id="27141-140">Sie können mehrere Platzhalter in einem Segment definieren, aber die Platzhalter durch einen Literalwert getrennt werden.</span><span class="sxs-lookup"><span data-stu-id="27141-140">You can define more than one placeholder in a segment, but the placeholders must be separated by a literal value.</span></span> <span data-ttu-id="27141-141">Z. B. `{language}-{country}/{action}` ist eine gültige Route-Muster.</span><span class="sxs-lookup"><span data-stu-id="27141-141">For example, `{language}-{country}/{action}` is a valid route pattern.</span></span> <span data-ttu-id="27141-142">Allerdings `{language}{country}/{action}` ist kein gültiges Muster, da kein Literalwert oder Trennzeichen zwischen den Platzhalter vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="27141-142">However, `{language}{country}/{action}` is not a valid pattern, because there is no literal value or delimiter between the placeholders.</span></span> <span data-ttu-id="27141-143">Routing kann daher nicht, wo Sie den Wert für den sprachplatzhalter aus dem Wert für den Platzhalter Land zu trennen bestimmen.</span><span class="sxs-lookup"><span data-stu-id="27141-143">Therefore, routing cannot determine where to separate the value for the language placeholder from the value for the country placeholder.</span></span>

### <a name="mapping-and-registering-routes"></a><span data-ttu-id="27141-144">Zuordnen und Registrieren von Routen</span><span class="sxs-lookup"><span data-stu-id="27141-144">Mapping and Registering Routes</span></span>

<span data-ttu-id="27141-145">Bevor Sie die Routen zu Seiten, die von das Wingtip Toys-beispielanwendung einfügen können, müssen Sie die Routen registrieren, beim Starten der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="27141-145">Before you can include routes to pages of the Wingtip Toys sample application, you must register the routes when the application starts.</span></span> <span data-ttu-id="27141-146">Um die Routen zu registrieren, ändern Sie die `Application_Start` -Ereignishandler.</span><span class="sxs-lookup"><span data-stu-id="27141-146">To register the routes, you will modify the `Application_Start` event handler.</span></span>

1. <span data-ttu-id="27141-147">In **Projektmappen-Explorer**von Visual Studio, suchen und öffnen Sie die *"Global.asax.cs"* Datei.</span><span class="sxs-lookup"><span data-stu-id="27141-147">In **Solution Explorer**of Visual Studio, find and open the *Global.asax.cs* file.</span></span>
2. <span data-ttu-id="27141-148">Fügen Sie den Code in Gelb zu markiert die *"Global.asax.cs"* -Datei wie folgt:</span><span class="sxs-lookup"><span data-stu-id="27141-148">Add the code highlighted in yellow to the *Global.asax.cs* file as follows:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample1.cs?highlight=30-31,34-46)]

<span data-ttu-id="27141-149">Wenn die Bezeichnung "Wingtip Toys"-Anwendung gestartet wird Beispiel, ruft er die `Application_Start` -Ereignishandler.</span><span class="sxs-lookup"><span data-stu-id="27141-149">When the Wingtip Toys sample application starts, it calls the `Application_Start` event handler.</span></span> <span data-ttu-id="27141-150">Am Ende der Ereignishandler der `RegisterCustomRoutes` Methode wird aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="27141-150">At the end of this event handler, the `RegisterCustomRoutes` method is called.</span></span> <span data-ttu-id="27141-151">Die `RegisterCustomRoutes` Methode fügt jede Route hinzu, durch den Aufruf der `MapPageRoute` Methode der `RouteCollection` Objekt.</span><span class="sxs-lookup"><span data-stu-id="27141-151">The `RegisterCustomRoutes` method adds each route by calling the `MapPageRoute` method of the `RouteCollection` object.</span></span> <span data-ttu-id="27141-152">Routen werden mit einem Routennamen, die Routen-URL und eine physische URL definiert.</span><span class="sxs-lookup"><span data-stu-id="27141-152">Routes are defined using a route name, a route URL and a physical URL.</span></span>

<span data-ttu-id="27141-153">Der erste Parameter ("`ProductsByCategoryRoute`") ist der Routenname.</span><span class="sxs-lookup"><span data-stu-id="27141-153">The first parameter ("`ProductsByCategoryRoute`") is the route name.</span></span> <span data-ttu-id="27141-154">Es wird verwendet, um die Route aufgerufen, wenn er benötigt wird.</span><span class="sxs-lookup"><span data-stu-id="27141-154">It is used to call the route when it is needed.</span></span> <span data-ttu-id="27141-155">Der zweite Parameter ("`Category/{categoryName}`") definiert die friendly URL, die dynamisch sein kann, auf Code basierend ersetzt.</span><span class="sxs-lookup"><span data-stu-id="27141-155">The second parameter ("`Category/{categoryName}`") defines the friendly replacement URL that can be dynamic based on code.</span></span> <span data-ttu-id="27141-156">Verwenden Sie diese Route, wenn Sie ein Steuerelement mit Links, die generiert werden, basierend auf Daten auffüllen.</span><span class="sxs-lookup"><span data-stu-id="27141-156">You use this route when you are populating a data control with links that are generated based on data.</span></span> <span data-ttu-id="27141-157">Eine Route wird folgendermaßen angezeigt:</span><span class="sxs-lookup"><span data-stu-id="27141-157">A route is shown as follows:</span></span>

[!code-csharp[Main](url-routing/samples/sample2.cs)]

<span data-ttu-id="27141-158">Der zweite Parameter der Route enthält einen dynamischen Wert, der von geschweiften Klammern angegeben (`{ }`).</span><span class="sxs-lookup"><span data-stu-id="27141-158">The second parameter of the route includes a dynamic value specified by braces (`{ }`).</span></span> <span data-ttu-id="27141-159">In diesem Fall die `categoryName` ist eine Variable, die verwendet wird, um den richtigen Routingpfad zu bestimmen.</span><span class="sxs-lookup"><span data-stu-id="27141-159">In this case, the `categoryName` is a variable that will be used to determine the proper routing path.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="27141-160">**Optional**</span><span class="sxs-lookup"><span data-stu-id="27141-160">**Optional**</span></span>
> 
> <span data-ttu-id="27141-161">Sie finden es vielleicht einfacher zum Verwalten Ihres Codes durch das Verschieben der `RegisterCustomRoutes` Methode, um eine separate Klasse.</span><span class="sxs-lookup"><span data-stu-id="27141-161">You might find it easier to manage your code by moving the `RegisterCustomRoutes` method to a separate class.</span></span> <span data-ttu-id="27141-162">In der *Logik* Ordner, erstellen Sie eine Separate `RouteActions` Klasse.</span><span class="sxs-lookup"><span data-stu-id="27141-162">In the *Logic* folder, create a separate `RouteActions` class.</span></span> <span data-ttu-id="27141-163">Verschieben Sie den oben genannten `RegisterCustomRoutes` Methode aus der *"Global.asax.cs"* Datei in das neue `RoutesActions` Klasse.</span><span class="sxs-lookup"><span data-stu-id="27141-163">Move the above `RegisterCustomRoutes` method from the *Global.asax.cs* file into the new `RoutesActions` class.</span></span> <span data-ttu-id="27141-164">Verwenden der `RoleActions` Klasse und die `createAdmin` Methode als ein Beispiel zum Aufrufen der `RegisterCustomRoutes` Methode aus der *"Global.asax.cs"* Datei.</span><span class="sxs-lookup"><span data-stu-id="27141-164">Use the `RoleActions` class and the `createAdmin` method as an example of how to call the `RegisterCustomRoutes` method from the *Global.asax.cs* file.</span></span>


<span data-ttu-id="27141-165">Sie haben wahrscheinlich ebenfalls bemerkt der `RegisterRoutes` Methode mit der `RouteConfig` Objekt am Anfang der `Application_Start` -Ereignishandler.</span><span class="sxs-lookup"><span data-stu-id="27141-165">You may also have noticed the `RegisterRoutes` method call using the `RouteConfig` object at the beginning of the `Application_Start` event handler.</span></span> <span data-ttu-id="27141-166">Dieser Aufruf wird durchgeführt, um Standardrouting zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="27141-166">This call is made to implement default routing.</span></span> <span data-ttu-id="27141-167">Es war als Standard-Code enthalten, wenn Sie die Anwendung mit Visual Studio Web Forms-Vorlage erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="27141-167">It was included as default code when you created the application using Visual Studio's Web Forms template.</span></span>

## <a name="retrieving-and-using-route-data"></a><span data-ttu-id="27141-168">Abrufen und Verwenden von Routendaten</span><span class="sxs-lookup"><span data-stu-id="27141-168">Retrieving and Using Route Data</span></span>

<span data-ttu-id="27141-169">Wie bereits erwähnt, können die Routen definiert werden.</span><span class="sxs-lookup"><span data-stu-id="27141-169">As mentioned above, routes can be defined.</span></span> <span data-ttu-id="27141-170">Der Code, der Sie hinzugefügt haben die `Application_Start` -Ereignishandler in der *"Global.asax.cs"* -Datei lädt die definierbaren Routen.</span><span class="sxs-lookup"><span data-stu-id="27141-170">The code that you added to the `Application_Start` event handler in the *Global.asax.cs* file loads the definable routes.</span></span>

### <a name="setting-routes"></a><span data-ttu-id="27141-171">Festlegen von Routen</span><span class="sxs-lookup"><span data-stu-id="27141-171">Setting Routes</span></span>

<span data-ttu-id="27141-172">Routen müssen Sie zusätzlichen Code hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="27141-172">Routes require you to add additional code.</span></span> <span data-ttu-id="27141-173">In diesem Tutorial verwenden Sie modellbindung zum Abrufen einer `RouteValueDictionary` -Objekt, das beim Generieren der Routen, die mithilfe von Daten aus einem Steuerelement verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="27141-173">In this tutorial, you will use model binding to retrieve a `RouteValueDictionary` object that is used when generating the routes using data from a data control.</span></span> <span data-ttu-id="27141-174">Die `RouteValueDictionary` Objekt enthält eine Liste der Produktnamen, die auf eine bestimmte Kategorie von Produkten gehören.</span><span class="sxs-lookup"><span data-stu-id="27141-174">The `RouteValueDictionary` object will contain a list of product names that belong to a specific category of products.</span></span> <span data-ttu-id="27141-175">Für jedes Produkt, das auf Basis der Daten und die Route wird ein Link erstellt.</span><span class="sxs-lookup"><span data-stu-id="27141-175">A link is created for each product based on the data and route.</span></span>

#### <a name="enable-routes-for-categories-and-products"></a><span data-ttu-id="27141-176">Aktivieren von Routen für Kategorien und Produkte</span><span class="sxs-lookup"><span data-stu-id="27141-176">Enable Routes for Categories and Products</span></span>

<span data-ttu-id="27141-177">Als Nächstes aktualisieren Sie die Anwendung zur Verwendung der `ProductsByCategoryRoute` um zu bestimmen, die richtige Route für jedes Product Category-Link enthält.</span><span class="sxs-lookup"><span data-stu-id="27141-177">Next, you'll update the application to use the `ProductsByCategoryRoute` to determine the correct route to include for each product category link.</span></span> <span data-ttu-id="27141-178">Aktualisieren Sie zudem die *"ProductList.aspx"* Seite, um eine geroutete Link für jedes Produkt enthalten.</span><span class="sxs-lookup"><span data-stu-id="27141-178">You'll also update the *ProductList.aspx* page to include a routed link for each product.</span></span> <span data-ttu-id="27141-179">Die Links werden angezeigt wie vor der Änderung jedoch die Links jetzt an die URL-routing verwendet.</span><span class="sxs-lookup"><span data-stu-id="27141-179">The links will be displayed as they were before the change, however the links will now use URL routing.</span></span>

1. <span data-ttu-id="27141-180">In **Projektmappen-Explorer**öffnen die *Site.Master* Seite, wenn es nicht bereits geöffnet ist.</span><span class="sxs-lookup"><span data-stu-id="27141-180">In **Solution Explorer**, open the *Site.Master* page if it is not already open.</span></span>
2. <span data-ttu-id="27141-181">Update der **ListView** Steuerelement mit dem Namen "`categoryList`" mit den Änderungen in gelb hervorgehoben, sodass das Markup wie folgt angezeigt:</span><span class="sxs-lookup"><span data-stu-id="27141-181">Update the **ListView** control named "`categoryList`" with the changes highlighted in yellow, so the markup appears as follows:</span></span>   

    [!code-aspx[Main](url-routing/samples/sample3.aspx?highlight=7-9)]
3. <span data-ttu-id="27141-182">In **Projektmappen-Explorer**öffnen die *"ProductList.aspx"* Seite.</span><span class="sxs-lookup"><span data-stu-id="27141-182">In **Solution Explorer**, open the *ProductList.aspx* page.</span></span>
4. <span data-ttu-id="27141-183">Update der `ItemTemplate` Element der *"ProductList.aspx"* Seite mit den Updates in gelb hervorgehoben werden, damit das Markup wie folgt aussieht:</span><span class="sxs-lookup"><span data-stu-id="27141-183">Update the `ItemTemplate` element of the *ProductList.aspx* page with the updates highlighted in yellow, so the markup appears as follows:</span></span>   

    [!code-aspx[Main](url-routing/samples/sample4.aspx?highlight=6-9,14-16)]
5. <span data-ttu-id="27141-184">Öffnen Sie den Code-Behind der *ProductList.aspx.cs* und fügen Sie den folgenden Namespace als Gelb:</span><span class="sxs-lookup"><span data-stu-id="27141-184">Open the code-behind of *ProductList.aspx.cs* and add the following namespace as highlighted in yellow:</span></span>  

    [!code-csharp[Main](url-routing/samples/sample5.cs?highlight=9)]
6. <span data-ttu-id="27141-185">Ersetzen Sie die `GetProducts` -Methode der Code-Behind (*ProductList.aspx.cs*) durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="27141-185">Replace the `GetProducts` method of the code-behind (*ProductList.aspx.cs*) with the following code:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample6.cs)]

#### <a name="add-code-for-product-details"></a><span data-ttu-id="27141-186">Fügen Sie Code für die Produktdetails hinzu.</span><span class="sxs-lookup"><span data-stu-id="27141-186">Add Code for Product Details</span></span>

<span data-ttu-id="27141-187">Aktualisieren Sie nun die Code-Behind (*ProductDetails.aspx.cs*) für die *ProductDetails.aspx* Seite, um die Weiterleitung von Daten verwenden.</span><span class="sxs-lookup"><span data-stu-id="27141-187">Now, update the code-behind (*ProductDetails.aspx.cs*) for the *ProductDetails.aspx* page to use route data.</span></span> <span data-ttu-id="27141-188">Beachten Sie, dass die neue `GetProduct` -Methode akzeptiert auch den Wert einer Abfragezeichenfolge für den Fall, in denen der Benutzer einen Link ein Lesezeichen erstellt hat, die die ältere nicht optimierte und nicht-Routing-URL verwendet.</span><span class="sxs-lookup"><span data-stu-id="27141-188">Notice that the new `GetProduct` method also accepts a query string value for the case where the user has a link bookmarked that uses the older non-friendly, non-routed URL.</span></span>

1. <span data-ttu-id="27141-189">Ersetzen Sie die `GetProduct` -Methode der Code-Behind (*ProductDetails.aspx.cs*) durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="27141-189">Replace the `GetProduct` method of the code-behind (*ProductDetails.aspx.cs*) with the following code:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample7.cs)]

## <a name="running-the-application"></a><span data-ttu-id="27141-190">Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="27141-190">Running the Application</span></span>

<span data-ttu-id="27141-191">Sie können die Anwendung nun auf die aktualisierte Routen finden Sie unter ausführen.</span><span class="sxs-lookup"><span data-stu-id="27141-191">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="27141-192">Drücken Sie **F5** zum Ausführen der Wingtip Toys-beispielanwendung.</span><span class="sxs-lookup"><span data-stu-id="27141-192">Press **F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="27141-193">Der Browser wird geöffnet und zeigt die *"default.aspx"* Seite.</span><span class="sxs-lookup"><span data-stu-id="27141-193">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="27141-194">Klicken Sie auf die **Produkte** Link am oberen Rand der Seite.</span><span class="sxs-lookup"><span data-stu-id="27141-194">Click the **Products** link at the top of the page.</span></span>  
 <span data-ttu-id="27141-195">Alle Produkte werden angezeigt, auf die *"ProductList.aspx"* Seite.</span><span class="sxs-lookup"><span data-stu-id="27141-195">All products are displayed on the *ProductList.aspx* page.</span></span> <span data-ttu-id="27141-196">Die folgende URL (unter Verwendung Ihrer Portnummer) wird für den Browser angezeigt:</span><span class="sxs-lookup"><span data-stu-id="27141-196">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/ProductList`
3. <span data-ttu-id="27141-197">Klicken Sie anschließend die **Autos** Kategorielink am oberen Rand der Seite.</span><span class="sxs-lookup"><span data-stu-id="27141-197">Next, click the **Cars** category link near the top of the page.</span></span>  
 <span data-ttu-id="27141-198">Nur Autos werden angezeigt, auf die *"ProductList.aspx"* Seite.</span><span class="sxs-lookup"><span data-stu-id="27141-198">Only cars are displayed on the *ProductList.aspx* page.</span></span> <span data-ttu-id="27141-199">Die folgende URL (unter Verwendung Ihrer Portnummer) wird für den Browser angezeigt:</span><span class="sxs-lookup"><span data-stu-id="27141-199">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/Category/Cars`
4. <span data-ttu-id="27141-200">Klicken Sie auf der Link, mit dem Namen des jeweils ersten Fahrzeugs auf der Seite angezeigt ("**konvertierbar sein Auto**") um die Produktdetails anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="27141-200">Click the link containing the name of the first car listed on the page ("**Convertible Car**") to display the product details.</span></span>  
 <span data-ttu-id="27141-201">Die folgende URL (unter Verwendung Ihrer Portnummer) wird für den Browser angezeigt:</span><span class="sxs-lookup"><span data-stu-id="27141-201">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/Product/Convertible%20Car`
5. <span data-ttu-id="27141-202">Geben Sie anschließend die folgende nicht weitergeleitete URL (unter Verwendung Ihrer Portnummer) in den Browser ein:</span><span class="sxs-lookup"><span data-stu-id="27141-202">Next, enter the following non-routed URL (using your port number) into the browser:</span></span>  
    `https://localhost:44300/ProductDetails.aspx?productID=2`  
 <span data-ttu-id="27141-203">Der Code erkennt immer noch eine URL mit einer Abfragezeichenfolge für den Fall, in denen ein Benutzer einen Link ein Lesezeichen erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="27141-203">The code still recognizes a URL that includes a query string, for the case where a user has a link bookmarked.</span></span>

## <a name="summary"></a><span data-ttu-id="27141-204">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="27141-204">Summary</span></span>

<span data-ttu-id="27141-205">In diesem Tutorial haben Sie Routen für Kategorien und Produkte hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="27141-205">In this tutorial, you have added routes for categories and products.</span></span> <span data-ttu-id="27141-206">Sie haben gelernt, wie Routen mit Datensteuerelementen integriert werden können, die modellbindung zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="27141-206">You have learned how routes can be integrated with data controls that use model binding.</span></span> <span data-ttu-id="27141-207">Im nächsten Tutorial implementieren Sie globale Fehlerbehandlung.</span><span class="sxs-lookup"><span data-stu-id="27141-207">In the next tutorial, you will implement global error handling.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="27141-208">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="27141-208">Additional Resources</span></span>

[<span data-ttu-id="27141-209">ASP.NET Friendly URLs</span><span class="sxs-lookup"><span data-stu-id="27141-209">ASP.NET Friendly URLs</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)  
[<span data-ttu-id="27141-210">Bereitstellen einer sicheren ASP.NET Web Forms-App mit Mitgliedschaft, OAuth und SQL-Datenbank in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="27141-210">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[<span data-ttu-id="27141-211">Microsoft Azure – kostenlose Testversion</span><span class="sxs-lookup"><span data-stu-id="27141-211">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> <span data-ttu-id="27141-212">[Zurück](membership-and-administration.md)
> [Weiter](aspnet-error-handling.md)</span><span class="sxs-lookup"><span data-stu-id="27141-212">[Previous](membership-and-administration.md)
[Next](aspnet-error-handling.md)</span></span>