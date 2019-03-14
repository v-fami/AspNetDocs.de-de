---
title: Verwalten von clientseitigen Paketen mit Bower in ASP.NET Core
author: rick-anderson
description: Verwalten von clientseitigen Paketen mit Bower.
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 08/09/2018
uid: client-side/bower
ms.openlocfilehash: 06edf7ee791aac0984ff71c2f243f61093f0d503
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047987"
---
# <a name="manage-client-side-packages-with-bower-in-aspnet-core"></a><span data-ttu-id="54315-103">Verwalten von clientseitigen Paketen mit Bower in ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="54315-103">Manage client-side packages with Bower in ASP.NET Core</span></span>

<span data-ttu-id="54315-104">Durch [Rick Anderson](https://twitter.com/RickAndMSFT), [Noel Reis](https://blog.falafel.com/falafel-software-recognized-sitefinity-website-year/), und [Scott Addie](https://scottaddie.com)</span><span class="sxs-lookup"><span data-stu-id="54315-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Noel Rice](https://blog.falafel.com/falafel-software-recognized-sitefinity-website-year/), and [Scott Addie](https://scottaddie.com)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54315-105">Während der Bower verwaltet wird, wird empfohlen, die Verwalter eine andere Lösung.</span><span class="sxs-lookup"><span data-stu-id="54315-105">While Bower is maintained, its maintainers recommend using a different solution.</span></span> <span data-ttu-id="54315-106">[Hilfebibliotheks-Manager](https://blogs.msdn.microsoft.com/webdev/2018/04/18/what-happened-to-bower/) (kurz LibMan) ist Visual Studio neue clientseitige Bibliothek Lizenzerwerbs-Tool (Visual Studio 15,8 oder höher).</span><span class="sxs-lookup"><span data-stu-id="54315-106">[Library Manager](https://blogs.msdn.microsoft.com/webdev/2018/04/18/what-happened-to-bower/) (LibMan for short) is Visual Studio's new client-side library acquisition tool (Visual Studio 15.8 or later).</span></span> <span data-ttu-id="54315-107">Weitere Informationen finden Sie unter <xref:client-side/libman/index>.</span><span class="sxs-lookup"><span data-stu-id="54315-107">For more information, see <xref:client-side/libman/index>.</span></span> <span data-ttu-id="54315-108">Bower ist in Visual Studio bis Version 15.5 unterstützt.</span><span class="sxs-lookup"><span data-stu-id="54315-108">Bower is supported in Visual Studio through version 15.5.</span></span>
>
> <span data-ttu-id="54315-109">Yarn mit Webpack ist eine weit verbreitete Alternative für die [migrationsanweisungen](https://bower.io/blog/2017/how-to-migrate-away-from-bower/) stehen zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="54315-109">Yarn with Webpack is one popular alternative for which [migration instructions](https://bower.io/blog/2017/how-to-migrate-away-from-bower/) are available.</span></span>

<span data-ttu-id="54315-110">[Bower](https://bower.io/) ruft sich selbst "Paket-Manager für das Web".</span><span class="sxs-lookup"><span data-stu-id="54315-110">[Bower](https://bower.io/) calls itself "A package manager for the web".</span></span> <span data-ttu-id="54315-111">Innerhalb des Ökosystems .NET füllt die "void", um NuGets-Fehler zum Übermitteln von Dateien mit statischer Inhalt nach links.</span><span class="sxs-lookup"><span data-stu-id="54315-111">Within the .NET ecosystem, it fills the void left by NuGet's inability to deliver static content files.</span></span> <span data-ttu-id="54315-112">Diese statischen Dateien für ASP.NET Core-Projekte sind Bestandteil der clientseitige Bibliotheken wie [jQuery](http://jquery.com/) und [Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="54315-112">For ASP.NET Core projects, these static files are inherent to client-side libraries like [jQuery](http://jquery.com/) and [Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="54315-113">Für .NET Bibliotheken verwenden, verwenden Sie immer noch [NuGet](https://www.nuget.org/) -Paket-Manager.</span><span class="sxs-lookup"><span data-stu-id="54315-113">For .NET libraries, you still use [NuGet](https://www.nuget.org/) package manager.</span></span>

<span data-ttu-id="54315-114">Buildprozess für neue Projekte, die mit der richten Sie die clientseitige ASP.NET Core-Projektvorlagen erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="54315-114">New projects created with the ASP.NET Core project templates set up the client-side build process.</span></span> <span data-ttu-id="54315-115">[jQuery](http://jquery.com/) und [Bootstrap](http://getbootstrap.com/) installiert sind, und Bower wird unterstützt.</span><span class="sxs-lookup"><span data-stu-id="54315-115">[jQuery](http://jquery.com/) and [Bootstrap](http://getbootstrap.com/) are installed, and Bower is supported.</span></span>

<span data-ttu-id="54315-116">Clientseitigen Paketen finden Sie in der *"bower.JSON"* Datei.</span><span class="sxs-lookup"><span data-stu-id="54315-116">Client-side packages are listed in the *bower.json* file.</span></span> <span data-ttu-id="54315-117">Konfiguriert die ASP.NET Core-Projektvorlagen *"bower.JSON"* mit Bootstrap, jQuery und jQuery-Validierung.</span><span class="sxs-lookup"><span data-stu-id="54315-117">The ASP.NET Core project templates configures *bower.json* with jQuery, jQuery validation, and Bootstrap.</span></span>

<span data-ttu-id="54315-118">In diesem Tutorial fügen wir Unterstützung für [Font Awesome](http://fontawesome.io).</span><span class="sxs-lookup"><span data-stu-id="54315-118">In this tutorial, we'll add support for [Font Awesome](http://fontawesome.io).</span></span> <span data-ttu-id="54315-119">Bower-Pakete installiert werden können, mit der **Bower-Pakete verwalten** UI oder manuell in die *"bower.JSON"* Datei.</span><span class="sxs-lookup"><span data-stu-id="54315-119">Bower packages can be installed with the **Manage Bower Packages** UI or manually in the *bower.json* file.</span></span>

### <a name="installation-via-manage-bower-packages-ui"></a><span data-ttu-id="54315-120">Installation über Bower-Pakete verwalten UI</span><span class="sxs-lookup"><span data-stu-id="54315-120">Installation via Manage Bower Packages UI</span></span>

* <span data-ttu-id="54315-121">Erstellen einer neuen ASP.NET Core-Web-app mit der **ASP.NET Core-Webanwendung ((.NET Core)** Vorlage.</span><span class="sxs-lookup"><span data-stu-id="54315-121">Create a new ASP.NET Core Web app with the **ASP.NET Core Web Application (.NET Core)** template.</span></span> <span data-ttu-id="54315-122">Wählen Sie **Webanwendung** und **keine Authentifizierung**.</span><span class="sxs-lookup"><span data-stu-id="54315-122">Select **Web Application** and **No Authentication**.</span></span>

* <span data-ttu-id="54315-123">Mit der rechten Maustaste in des Projekts im Projektmappen-Explorer, und wählen Sie **Bower-Pakete verwalten** (Alternativ im Hauptmenü **Projekt** > **Bower-Pakete verwalten**).</span><span class="sxs-lookup"><span data-stu-id="54315-123">Right-click the project in Solution Explorer and select **Manage Bower Packages** (alternatively from the main menu, **Project** > **Manage Bower Packages**).</span></span>

* <span data-ttu-id="54315-124">In der **Bower: \<Projektname\>**  , klicken Sie auf der Registerkarte "Durchsuchen", und klicken Sie dann die Pakete durch Eingabe Filterliste `font-awesome` in das Suchfeld:</span><span class="sxs-lookup"><span data-stu-id="54315-124">In the **Bower: \<project name\>** window, click the "Browse" tab, and then filter the packages list by entering `font-awesome` in the search box:</span></span>

  ![Bower-Pakete verwalten](bower/_static/manage-bower-packages.png)

* <span data-ttu-id="54315-126">Überprüfen Sie, ob die "Änderungen in *" bower.JSON "*" das Kontrollkästchen aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="54315-126">Confirm that the "Save changes to *bower.json*" check box is checked.</span></span> <span data-ttu-id="54315-127">Wählen Sie eine Version aus der Dropdown-Liste, und klicken Sie auf die **installieren** Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="54315-127">Select a version from the drop-down list and click the **Install** button.</span></span> <span data-ttu-id="54315-128">Die **Ausgabe** Fenster zeigt die Details zur Installation.</span><span class="sxs-lookup"><span data-stu-id="54315-128">The **Output** window shows the installation details.</span></span>

### <a name="manual-installation-in-bowerjson"></a><span data-ttu-id="54315-129">Manuelle Installation in "bower.JSON"</span><span class="sxs-lookup"><span data-stu-id="54315-129">Manual installation in bower.json</span></span>

<span data-ttu-id="54315-130">Öffnen der *"bower.JSON"* Datei, und fügen Sie "Font awesome" den Abhängigkeiten hinzu.</span><span class="sxs-lookup"><span data-stu-id="54315-130">Open the *bower.json* file and add "font-awesome" to the dependencies.</span></span> <span data-ttu-id="54315-131">IntelliSense zeigt die verfügbaren Pakete.</span><span class="sxs-lookup"><span data-stu-id="54315-131">IntelliSense shows the available packages.</span></span> <span data-ttu-id="54315-132">Wenn ein Paket ausgewählt ist, werden die verfügbaren Versionen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="54315-132">When a package is selected, the available versions are displayed.</span></span> <span data-ttu-id="54315-133">Die Bilder unten älter und wird nicht übereinstimmen, was Sie sehen.</span><span class="sxs-lookup"><span data-stu-id="54315-133">The images below are older and won't match what you see.</span></span>

![IntelliSense von Bower-Paket-explorer](bower/_static/add-package.png)

![Bower-Version IntelliSense](bower/_static/version-intelliSense.png)

<span data-ttu-id="54315-136">Bower-verwendet [semantische Versionierung](http://semver.org/) zum Organisieren von Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="54315-136">Bower uses [semantic versioning](http://semver.org/) to organize dependencies.</span></span> <span data-ttu-id="54315-137">Semantischer versionsverwaltung, auch bekannt als SemVer, identifiziert die Pakete mit den Nummerierungsschema \<wichtigen >.\< kleinere >. \<Patch >.</span><span class="sxs-lookup"><span data-stu-id="54315-137">Semantic versioning, also known as SemVer, identifies packages with the numbering scheme \<major>.\<minor>.\<patch>.</span></span> <span data-ttu-id="54315-138">IntelliSense vereinfacht semantische Versionierung, indem Sie nur einige gängige Optionen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="54315-138">IntelliSense simplifies semantic versioning by showing only a few common choices.</span></span> <span data-ttu-id="54315-139">Das oberste Element in der IntelliSense-Liste (4.6.3 im obigen Beispiel), gilt die neueste stabile Version des Pakets.</span><span class="sxs-lookup"><span data-stu-id="54315-139">The top item in the IntelliSense list (4.6.3 in the example above) is considered the latest stable version of the package.</span></span> <span data-ttu-id="54315-140">Das Caretzeichen (^) Symbol entspricht, die aktuellste Version, und die Tilde (~) entspricht der aktuellsten Nebenversion.</span><span class="sxs-lookup"><span data-stu-id="54315-140">The caret (^) symbol matches the most recent major version and the tilde (~) matches the most recent minor version.</span></span>

<span data-ttu-id="54315-141">Speichern Sie die *"bower.JSON"* Datei.</span><span class="sxs-lookup"><span data-stu-id="54315-141">Save the *bower.json* file.</span></span> <span data-ttu-id="54315-142">Visual Studio wird überwacht, ob die *"bower.JSON"* -Datei für die Änderungen.</span><span class="sxs-lookup"><span data-stu-id="54315-142">Visual Studio watches the *bower.json* file for changes.</span></span> <span data-ttu-id="54315-143">Beim Speichern der *Bower Install* Befehl ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="54315-143">Upon saving, the *bower install* command is executed.</span></span> <span data-ttu-id="54315-144">Finden Sie im Ausgabefenster **Bower-/Npm** Ansicht für den genauen, ausgeführten Befehl.</span><span class="sxs-lookup"><span data-stu-id="54315-144">See the Output window's **Bower/npm** view for the exact command executed.</span></span>

<span data-ttu-id="54315-145">Öffnen der *".bowerrc"* Datei *"bower.JSON"*.</span><span class="sxs-lookup"><span data-stu-id="54315-145">Open the *.bowerrc* file under *bower.json*.</span></span> <span data-ttu-id="54315-146">Die `directory` -Eigenschaftensatz auf *Wwwroot/Lib* gibt an den Speicherort von Bower installiert die Paketressourcen.</span><span class="sxs-lookup"><span data-stu-id="54315-146">The `directory` property is set to *wwwroot/lib* which indicates the location Bower will install the package assets.</span></span>

```json
{
 "directory": "wwwroot/lib"
}
```

<span data-ttu-id="54315-147">Sie können das Suchfeld im Projektmappen-Explorer verwenden, suchen und Anzeigen der Font awesome Paket.</span><span class="sxs-lookup"><span data-stu-id="54315-147">You can use the search box in Solution Explorer to find and display the font-awesome package.</span></span>

<span data-ttu-id="54315-148">Öffnen der *Views\Shared\_Layout.cshtml* Datei und hinzufügen die Font awesome CSS-Datei in der Umgebung [Taghilfsprogramm](xref:mvc/views/tag-helpers/intro) für `Development`.</span><span class="sxs-lookup"><span data-stu-id="54315-148">Open the *Views\Shared\_Layout.cshtml* file and add the font-awesome CSS file to the environment [Tag Helper](xref:mvc/views/tag-helpers/intro) for `Development`.</span></span> <span data-ttu-id="54315-149">Klicken Sie im Projektmappen-Explorer ziehen, und legen Sie *Schriftart-awesome.css* innerhalb der `<environment names="Development">` Element.</span><span class="sxs-lookup"><span data-stu-id="54315-149">From Solution Explorer, drag and drop *font-awesome.css* inside the `<environment names="Development">` element.</span></span>

[!code-html[](bower/sample/_Layout.cshtml?highlight=4&range=9-13)]

<span data-ttu-id="54315-150">In einer Produktions-app hinzufügen *Schriftart-awesome.min.css* auf die Environment-taghilfsprogramm für `Staging,Production`.</span><span class="sxs-lookup"><span data-stu-id="54315-150">In a production app you would add *font-awesome.min.css* to the environment tag helper for `Staging,Production`.</span></span>

<span data-ttu-id="54315-151">Ersetzen Sie den Inhalt von der *Views\Home\About.cshtml* Razor-Datei mit folgendem Markup:</span><span class="sxs-lookup"><span data-stu-id="54315-151">Replace the contents of the *Views\Home\About.cshtml* Razor file with the following markup:</span></span>

[!code-html[](bower/sample/About.cshtml)]

<span data-ttu-id="54315-152">Führen Sie die app aus, und navigieren Sie zu der Ansicht "Info", um zu überprüfen, ob die Schriftart-awesome Paket funktioniert.</span><span class="sxs-lookup"><span data-stu-id="54315-152">Run the app and navigate to the About view to verify the font-awesome package works.</span></span>

## <a name="exploring-the-client-side-build-process"></a><span data-ttu-id="54315-153">Untersuchen die Client-Side-Buildprozess</span><span class="sxs-lookup"><span data-stu-id="54315-153">Exploring the client-side build process</span></span>

<span data-ttu-id="54315-154">Die meisten ASP.NET Core-Projektvorlagen sind bereits konfiguriert, um die Nutzung von bower beginnen.</span><span class="sxs-lookup"><span data-stu-id="54315-154">Most ASP.NET Core project templates are already configured to use Bower.</span></span> <span data-ttu-id="54315-155">Dieser nächste exemplarische Vorgehensweise beginnt mit einem leeren ASP.NET Core-Projekt und jedes Datenelement manuell hinzugefügt, sodass Sie ein Gefühl für die Verwendung von Bower in einem Projekt abrufen können.</span><span class="sxs-lookup"><span data-stu-id="54315-155">This next walkthrough starts with an empty ASP.NET Core project and adds each piece manually, so you can get a feel for how Bower is used in a project.</span></span> <span data-ttu-id="54315-156">Sie können sehen, was geschieht mit der Projektstruktur und die Laufzeit auszugeben, wenn jede konfigurationsänderung vorgenommen wird.</span><span class="sxs-lookup"><span data-stu-id="54315-156">You can see what happens to the project structure and the runtime output as each configuration change is made.</span></span>

<span data-ttu-id="54315-157">Die allgemeinen Schritte des Buildprozesses für die clientseitige mit Bower verwendet werden:</span><span class="sxs-lookup"><span data-stu-id="54315-157">The general steps to use the client-side build process with Bower are:</span></span>

* <span data-ttu-id="54315-158">Definieren Sie in Ihrem Projekt verwendeten Pakete.</span><span class="sxs-lookup"><span data-stu-id="54315-158">Define packages used in your project.</span></span> <!-- once defined, you don't need to download them, VS does -->
* <span data-ttu-id="54315-159">Die referenzpakete von Ihren Webseiten.</span><span class="sxs-lookup"><span data-stu-id="54315-159">Reference packages from your web pages.</span></span>

### <a name="define-packages"></a><span data-ttu-id="54315-160">Definieren von Paketen</span><span class="sxs-lookup"><span data-stu-id="54315-160">Define packages</span></span>

<span data-ttu-id="54315-161">Nachdem Sie Pakete in Auflisten der *"bower.JSON"* Visual Studio-Datei laden sie herunter.</span><span class="sxs-lookup"><span data-stu-id="54315-161">Once you list packages in the *bower.json* file, Visual Studio will download them.</span></span> <span data-ttu-id="54315-162">Im folgenden Beispiel wird Bower, jQuery und Bootstrap zum Laden der *"Wwwroot"* Ordner.</span><span class="sxs-lookup"><span data-stu-id="54315-162">The following example uses Bower to load jQuery and Bootstrap to the *wwwroot* folder.</span></span>

* <span data-ttu-id="54315-163">Erstellen einer neuen ASP.NET Core-Web-app mit der **ASP.NET Core-Webanwendung ((.NET Core)** Vorlage.</span><span class="sxs-lookup"><span data-stu-id="54315-163">Create a new ASP.NET Core Web app with the **ASP.NET Core Web Application (.NET Core)** template.</span></span> <span data-ttu-id="54315-164">Wählen Sie die **leere** Projektvorlage aus, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="54315-164">Select the **Empty** project template and click **OK**.</span></span>

* <span data-ttu-id="54315-165">Klicken Sie im Projektmappen-Explorer mit der Maustaste des Projekts > **neues Element hinzufügen** , und wählen Sie **Bower-Konfigurationsdatei**.</span><span class="sxs-lookup"><span data-stu-id="54315-165">In Solution Explorer, right-click the project > **Add New Item** and select **Bower Configuration File**.</span></span> <span data-ttu-id="54315-166">Hinweis: Ein *".bowerrc"* Datei wird ebenfalls hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="54315-166">Note: A *.bowerrc* file is also added.</span></span>

* <span data-ttu-id="54315-167">Öffnen *"bower.JSON"*, Hinzufügen von Jquery und bootstrap auf dem `dependencies` Abschnitt.</span><span class="sxs-lookup"><span data-stu-id="54315-167">Open *bower.json*, and add jquery and bootstrap to the `dependencies` section.</span></span> <span data-ttu-id="54315-168">Die resultierende *"bower.JSON"* sieht die Datei wie im folgenden Beispiel.</span><span class="sxs-lookup"><span data-stu-id="54315-168">The resulting *bower.json* file will look like the following example.</span></span> <span data-ttu-id="54315-169">Die Versionen ändert sich im Laufe der Zeit und entsprechen möglicherweise nicht die folgenden Abbildung.</span><span class="sxs-lookup"><span data-stu-id="54315-169">The versions will change over time and may not match the image below.</span></span>

[!code-json[](bower/sample/bower.json?highlight=5,6)]

* <span data-ttu-id="54315-170">Speichern Sie die *"bower.JSON"* Datei.</span><span class="sxs-lookup"><span data-stu-id="54315-170">Save the *bower.json* file.</span></span>

  <span data-ttu-id="54315-171">Überprüfen Sie das Projekt enthält die *bootstrap* und *jQuery* Verzeichnisse im *Wwwroot/Lib*.</span><span class="sxs-lookup"><span data-stu-id="54315-171">Verify the project includes the *bootstrap* and *jQuery* directories in *wwwroot/lib*.</span></span> <span data-ttu-id="54315-172">Bower-verwendet die *".bowerrc"* Datei zum Installieren der Objekte in *Wwwroot/Lib*.</span><span class="sxs-lookup"><span data-stu-id="54315-172">Bower uses the *.bowerrc* file to install the assets in *wwwroot/lib*.</span></span>

  <span data-ttu-id="54315-173">Hinweis: Die Benutzeroberfläche "Bower-Pakete verwalten" bietet eine Alternative zum manuellen-Datei bearbeitet wird.</span><span class="sxs-lookup"><span data-stu-id="54315-173">Note: The "Manage Bower Packages" UI provides an alternative to manual file editing.</span></span>

### <a name="enable-static-files"></a><span data-ttu-id="54315-174">Aktivieren Sie die statische Dateien</span><span class="sxs-lookup"><span data-stu-id="54315-174">Enable static files</span></span>

* <span data-ttu-id="54315-175">Hinzufügen der `Microsoft.AspNetCore.StaticFiles` NuGet-Paket zum Projekt.</span><span class="sxs-lookup"><span data-stu-id="54315-175">Add the `Microsoft.AspNetCore.StaticFiles` NuGet package to the project.</span></span>
* <span data-ttu-id="54315-176">Aktivieren Sie statische Dateien mit verarbeitet die [Middleware für statische Dateien](/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions).</span><span class="sxs-lookup"><span data-stu-id="54315-176">Enable static files to be served with the [Static file middleware](/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions).</span></span> <span data-ttu-id="54315-177">Fügen Sie einen Aufruf von [UseStaticFiles](/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions) auf die `Configure` -Methode der `Startup`.</span><span class="sxs-lookup"><span data-stu-id="54315-177">Add a call to [UseStaticFiles](/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions) to the `Configure` method of `Startup`.</span></span>

[!code-csharp[](bower/sample/Startup.cs?highlight=9)]

### <a name="reference-packages"></a><span data-ttu-id="54315-178">Referenzpakete</span><span class="sxs-lookup"><span data-stu-id="54315-178">Reference packages</span></span>

<span data-ttu-id="54315-179">In diesem Abschnitt erstellen Sie eine HTML-Seite, um sicherzustellen, dass sie die bereitgestellten Pakete zugreifen kann.</span><span class="sxs-lookup"><span data-stu-id="54315-179">In this section, you will create an HTML page to verify it can access the deployed packages.</span></span>

* <span data-ttu-id="54315-180">Hinzufügen einer neuen HTML-Seite, die mit dem Namen *"Index.HTML"* auf die *"Wwwroot"* Ordner.</span><span class="sxs-lookup"><span data-stu-id="54315-180">Add a new HTML page named *Index.html* to the *wwwroot* folder.</span></span> <span data-ttu-id="54315-181">Hinweis: Sie müssen die HTML-Datei zum Hinzufügen der *"Wwwroot"* Ordner.</span><span class="sxs-lookup"><span data-stu-id="54315-181">Note: You must add the HTML file to the *wwwroot* folder.</span></span> <span data-ttu-id="54315-182">Standardmäßig kann nicht außerhalb statischer Inhalt verarbeitet werden *"Wwwroot"*.</span><span class="sxs-lookup"><span data-stu-id="54315-182">By default, static content cannot be served outside *wwwroot*.</span></span> <span data-ttu-id="54315-183">Finden Sie unter [statische Dateien](xref:fundamentals/static-files) für Weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="54315-183">See [Static files](xref:fundamentals/static-files) for more information.</span></span>

  <span data-ttu-id="54315-184">Ersetzen Sie den Inhalt der *"Index.HTML"* mit folgendem Markup:</span><span class="sxs-lookup"><span data-stu-id="54315-184">Replace the contents of *Index.html* with the following markup:</span></span>

[!code-html[](bower/sample/Index.html)]

* <span data-ttu-id="54315-185">Führen Sie die app, und navigieren Sie zu `http://localhost:<port>/Index.html`.</span><span class="sxs-lookup"><span data-stu-id="54315-185">Run the app and navigate to `http://localhost:<port>/Index.html`.</span></span> <span data-ttu-id="54315-186">Sie können auch mit *"Index.HTML"* geöffnet haben, drücken Sie die `Ctrl+Shift+W`.</span><span class="sxs-lookup"><span data-stu-id="54315-186">Alternatively, with *Index.html* opened, press `Ctrl+Shift+W`.</span></span> <span data-ttu-id="54315-187">Stellen Sie sicher, dass der Jumbotron-Stil angewendet wird, der jQuery-Code reagiert werden soll, wenn die Schaltfläche geklickt wird und die Schaltfläche "Bootstrap" Zustand ändert.</span><span class="sxs-lookup"><span data-stu-id="54315-187">Verify that the jumbotron styling is applied, the jQuery code responds when the button is clicked, and that the Bootstrap button changes state.</span></span>

  ![angewendete Jumbotron-Stil](bower/_static/jumbotron.png)