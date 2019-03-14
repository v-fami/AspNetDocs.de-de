---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
title: Ausführen eines Was-wäre, wenn Bereitstellung | Microsoft-Dokumentation
author: jrjlee
description: In diesem Thema wird beschrieben, wie "Was geschieht, wenn" ausführen (oder simulierte)-Bereitstellungen mithilfe der Internetinformationsdienste (Internet Information Services, IIS)-Webbereitstellungstool (Web Deploy) und V...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c711b453-01ac-4e65-a48c-93d99bf22e58
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
msc.type: authoredcontent
ms.openlocfilehash: 054b15e1e58164ec7e85c77c39fb47bcb47879b9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57058307"
---
<a name="performing-a-what-if-deployment"></a><span data-ttu-id="faf05-103">Durchführen einer simulierten Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="faf05-103">Performing a "What If" Deployment</span></span>
====================
<span data-ttu-id="faf05-104">durch [Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="faf05-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="faf05-105">PDF herunterladen</span><span class="sxs-lookup"><span data-stu-id="faf05-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="faf05-106">In diesem Thema wird beschrieben, wie "Was-wäre-wenn" ausführen (oder simulierte) mit dem Internet Information Services (IIS)-Webbereitstellungstool (Web Deploy) und VSDBCMD Bereitstellungen.</span><span class="sxs-lookup"><span data-stu-id="faf05-106">This topic describes how to perform "what if" (or simulated) deployments using the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) and VSDBCMD.</span></span> <span data-ttu-id="faf05-107">Dadurch können Sie die Auswirkungen Ihrer Bereitstellungslogik in einer bestimmten zielumgebung zu bestimmen, bevor Sie tatsächlich Ihre Anwendung bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="faf05-107">This lets you determine the effects of your deployment logic on a particular target environment before you actually deploy your application.</span></span>


<span data-ttu-id="faf05-108">In diesem Thema ist Teil einer Reihe von Tutorials, die auf der Basis der bereitstellungsanforderungen Enterprise ein fiktives Unternehmen, die mit dem Namen Fabrikam, Inc. Dieser tutorialreihe verwendet eine beispiellösung&#x2014;der [Contact Manager-Lösung](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;zur Darstellung einer Webanwendung mit einem realistischen Maß an Komplexität, einschließlich einer ASP.NET MVC 3-Anwendung, eine Windows-Kommunikation Foundation (WCF)-Dienst und ein Datenbankprojekt.</span><span class="sxs-lookup"><span data-stu-id="faf05-108">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="faf05-109">Die Methode für die Bereitstellung das Kernstück des in diesen Tutorials basiert auf den geteilten Projekt Dateiansatz beschrieben, die [Grundlegendes zur Projektdatei](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in dem der Build & Deployment-Prozess von gesteuert wird zwei Projektdateien&#x2014;eine die Buildanweisungen, die für jede zielumgebung, und enthält umgebungsspezifische Einstellungen für Build & Deployment gelten enthält.</span><span class="sxs-lookup"><span data-stu-id="faf05-109">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="faf05-110">Zur Erstellungszeit wird die umgebungsspezifischen-Projektdatei in die Unabhängigkeit von der Umgebung Projektdatei, um einen vollständigen Satz von einrichtungsanweisungen bilden zusammengeführt.</span><span class="sxs-lookup"><span data-stu-id="faf05-110">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="performing-a-what-if-deployment-for-web-packages"></a><span data-ttu-id="faf05-111">Ausführen einer "Was-wäre-wenn" Bereitstellung für Webpakete</span><span class="sxs-lookup"><span data-stu-id="faf05-111">Performing a "What If" Deployment for Web Packages</span></span>

<span data-ttu-id="faf05-112">Web Deploy enthält Funktionen, die Sie Bereitstellungen in "what if" durchführen kann (oder Testversion) Modus.</span><span class="sxs-lookup"><span data-stu-id="faf05-112">Web Deploy includes functionality that lets you perform deployments in "what if" (or trial) mode.</span></span> <span data-ttu-id="faf05-113">Wenn Sie Elemente in "what if"-Modus bereitstellen, generiert das Web Deploy eine Protokolldatei, mussten Sie die Bereitstellung ausgeführt, wobei jedoch eigentlich nichts ändert, auf dem Zielserver.</span><span class="sxs-lookup"><span data-stu-id="faf05-113">When you deploy artifacts in "what if" mode, Web Deploy generates a log file as if you had performed the deployment, but it doesn't actually change anything on the destination server.</span></span> <span data-ttu-id="faf05-114">Überprüfen die Protokolldatei kann Ihnen helfen, welche Auswirkungen zu verstehen, die Bereitstellung auf dem Zielserver, insbesondere muss:</span><span class="sxs-lookup"><span data-stu-id="faf05-114">Reviewing the log file can help you to understand what impact your deployment will have on the destination server, in particular:</span></span>

- <span data-ttu-id="faf05-115">Was wird hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="faf05-115">What will get added.</span></span>
- <span data-ttu-id="faf05-116">Was wird aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="faf05-116">What will get updated.</span></span>
- <span data-ttu-id="faf05-117">Welche gelöscht werden.</span><span class="sxs-lookup"><span data-stu-id="faf05-117">What will get deleted.</span></span>

<span data-ttu-id="faf05-118">Da eine "Was-wäre-wenn" Bereitstellung tatsächlich Änderungen nicht auf dem Zielserver, was immer nicht möglich ist, ist die Vorhersage, ob eine Bereitstellung erfolgreich ist, wird.</span><span class="sxs-lookup"><span data-stu-id="faf05-118">Because a "what if" deployment doesn't actually change anything on the destination server, what it can't always do is predict whether a deployment will succeed.</span></span>

<span data-ttu-id="faf05-119">Siehe [Bereitstellen von Webpaketen](../web-deployment-in-the-enterprise/deploying-web-packages.md), Bereitstellen von Webpaketen, die auf zwei Arten mit Web Deploy können&#x2014;mithilfe des Befehlszeilenprogramms MSDeploy.exe direkt oder durch Ausführen der *. "Deploy.cmd"* Datei der Buildprozess generiert.</span><span class="sxs-lookup"><span data-stu-id="faf05-119">As described in [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md), you can deploy web packages using Web Deploy in two ways&#x2014;by using the MSDeploy.exe command-line utility directly or by running the *.deploy.cmd* file that the build process generates.</span></span>

<span data-ttu-id="faf05-120">Wenn Sie MSDeploy.exe direkt verwenden, können Sie eine Bereitstellung "Was-wäre-wenn" ausführen, durch das Hinzufügen der **– Whatif** Flag, um den Befehl.</span><span class="sxs-lookup"><span data-stu-id="faf05-120">If you're using MSDeploy.exe directly, you can run a "what if" deployment by adding the **–whatif** flag to your command.</span></span> <span data-ttu-id="faf05-121">Z. B. um auszuwerten, was passieren würde, wenn Sie das Paket ContactManager.Mvc.zip in einer Stagingumgebung bereitgestellt, sieht der MSDeploy-Befehl folgendermaßen aus:</span><span class="sxs-lookup"><span data-stu-id="faf05-121">For example, to evaluate what would happen if you deployed the ContactManager.Mvc.zip package to a staging environment, the MSDeploy command should resemble this:</span></span>


[!code-console[Main](performing-a-what-if-deployment/samples/sample1.cmd)]


<span data-ttu-id="faf05-122">Wenn Sie mit den Ergebnissen der Bereitstellungskonfiguration "Was-wäre-wenn" zufrieden sind, können Sie entfernen die **– Whatif** Flag, um eine live-Bereitstellung auszuführen.</span><span class="sxs-lookup"><span data-stu-id="faf05-122">When you're satisfied with the results of your "what if" deployment, you can remove the **–whatif** flag to run a live deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="faf05-123">Weitere Informationen zu den Befehlszeilenoptionen für MSDeploy.exe finden Sie unter [Web Deploy-Vorgang Settings](https://technet.microsoft.com/library/dd569089(WS.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="faf05-123">For more information on command-line options for MSDeploy.exe, see [Web Deploy Operation Settings](https://technet.microsoft.com/library/dd569089(WS.10).aspx).</span></span>


<span data-ttu-id="faf05-124">Bei Verwendung der *. "Deploy.cmd"* -Datei können Sie eine Bereitstellung "Was-wäre-wenn" ausführen, indem die einschließlich der **/t /** flag (Testversion) moduskennzeichnung anstelle von der **/y** -Flag ("yes" oder Update-Modus) in der Befehl.</span><span class="sxs-lookup"><span data-stu-id="faf05-124">If you're using the *.deploy.cmd* file, you can run a "what if" deployment by including the **/t** flag (trial mode) flag instead of the **/y** flag ("yes," or update mode) in your command.</span></span> <span data-ttu-id="faf05-125">Beispielsweise, um auszuwerten, was passieren würde, wenn Sie durch Ausführen des Pakets ContactManager.Mvc.zip bereitgestellt der *. "Deploy.cmd"* -Datei des Befehls sollte diesem ähneln:</span><span class="sxs-lookup"><span data-stu-id="faf05-125">For example, to evaluate what would happen if you deployed the ContactManager.Mvc.zip package by running the *.deploy.cmd* file, your command should resemble this:</span></span>


[!code-console[Main](performing-a-what-if-deployment/samples/sample2.cmd)]


<span data-ttu-id="faf05-126">Wenn Sie mit den Ergebnissen der Bereitstellungskonfiguration "Testmodus" zufrieden sind, können Sie ersetzen die **/t /** flag mit einer **/y** Flag zum Ausführen einer aktiven Bereitstellung:</span><span class="sxs-lookup"><span data-stu-id="faf05-126">When you're satisfied with the results of your "trial mode" deployment, you can replace the **/t** flag with a **/y** flag to run a live deployment:</span></span>


[!code-console[Main](performing-a-what-if-deployment/samples/sample3.cmd)]


> [!NOTE]
> <span data-ttu-id="faf05-127">Weitere Informationen zu Befehlszeilenoptionen für *. "Deploy.cmd"* finden Sie unter [Vorgehensweise: Installieren eines Bereitstellungspakets mit der Datei "Deploy.cmd"](https://msdn.microsoft.com/library/ff356104.aspx).</span><span class="sxs-lookup"><span data-stu-id="faf05-127">For more information on command-line options for *.deploy.cmd* files, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span> <span data-ttu-id="faf05-128">Wenn das Ausführen der *. "Deploy.cmd"* Datei ohne Angabe von Flags, die Eingabeaufforderung zeigt eine Liste der verfügbaren Flags.</span><span class="sxs-lookup"><span data-stu-id="faf05-128">If you run the *.deploy.cmd* file without specifying any flags, the command prompt will display a list of available flags.</span></span>


## <a name="performing-a-what-if-deployment-for-databases"></a><span data-ttu-id="faf05-129">Ausführen einer "Was-wäre-wenn" Bereitstellung für Datenbanken</span><span class="sxs-lookup"><span data-stu-id="faf05-129">Performing a "What If" Deployment for Databases</span></span>

<span data-ttu-id="faf05-130">In diesem Abschnitt wird davon ausgegangen, dass Sie das Dienstprogramm VSDBCMD nutzen, inkrementelle, Schema-basierte Datenbank-Bereitstellung durchzuführen.</span><span class="sxs-lookup"><span data-stu-id="faf05-130">This section assumes that you're using the VSDBCMD utility to perform incremental, schema-based database deployment.</span></span> <span data-ttu-id="faf05-131">Dieser Ansatz wird ausführlicher beschrieben [Bereitstellen von Datenbankprojekten](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span><span class="sxs-lookup"><span data-stu-id="faf05-131">This approach is described in more detail in [Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span></span> <span data-ttu-id="faf05-132">Es wird empfohlen, dass Sie sich vertraut mit diesem Thema machen, bevor Sie die hier beschriebenen Konzepte gelten.</span><span class="sxs-lookup"><span data-stu-id="faf05-132">We recommend that you familiarize yourself with this topic before you apply the concepts described here.</span></span>

<span data-ttu-id="faf05-133">Bei Verwendung von VSDBCMD in **bereitstellen** -Modus können Sie die **dd /** (oder **/DeployToDatabase**) flag, das steuert, ob VSDBCMD tatsächlich stellt die Datenbank bereit oder nur generiert ein Skript für die Bereitstellung.</span><span class="sxs-lookup"><span data-stu-id="faf05-133">When you use VSDBCMD in **Deploy** mode, you can use the **/dd** (or **/DeployToDatabase**) flag to control whether VSDBCMD actually deploys the database or just generates a deployment script.</span></span> <span data-ttu-id="faf05-134">Wenn Sie eine DBSCHEMA-Datei bereitstellen, ist dies das Verhalten auf:</span><span class="sxs-lookup"><span data-stu-id="faf05-134">If you're deploying a .dbschema file, this is the behavior:</span></span>

- <span data-ttu-id="faf05-135">Bei Angabe von **/dd+** oder **dd /**, VSDBCMD wird ein Bereitstellungsskript generieren und Bereitstellen der Datenbank.</span><span class="sxs-lookup"><span data-stu-id="faf05-135">If you specify **/dd+** or **/dd**, VSDBCMD will generate a deployment script and deploy the database.</span></span>
- <span data-ttu-id="faf05-136">Bei Angabe von **/dd-** oder ohne den Schalter, VSDBCMD wird nur ein Bereitstellungsskript generiert.</span><span class="sxs-lookup"><span data-stu-id="faf05-136">If you specify **/dd-** or omit the switch, VSDBCMD will generate a deployment script only.</span></span>

> [!NOTE]
> <span data-ttu-id="faf05-137">Wenn Sie eine Datei DeployManifest anstelle einer DBSCHEMA-Datei, das Verhalten der bereitstellen, die **dd /** Schalter ist wesentlich komplizierter.</span><span class="sxs-lookup"><span data-stu-id="faf05-137">If you're deploying a .deploymanifest file rather than a .dbschema file, the behavior of the **/dd** switch is a lot more complicated.</span></span> <span data-ttu-id="faf05-138">Im Wesentlichen VSDBCMD ignoriert den Wert des der **dd /** wechseln, wenn die DEPLOYMANIFEST-Datei enthält eine **DeployToDatabase** Element mit einem Wert von **"true"**.</span><span class="sxs-lookup"><span data-stu-id="faf05-138">Essentially, VSDBCMD will ignore the value of the **/dd** switch if the .deploymanifest file includes a **DeployToDatabase** element with a value of **True**.</span></span> <span data-ttu-id="faf05-139">[Bereitstellen von Datenbankprojekten](../web-deployment-in-the-enterprise/deploying-database-projects.md) wird dieses Verhalten vollständig beschrieben.</span><span class="sxs-lookup"><span data-stu-id="faf05-139">[Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md) describes this behavior in full.</span></span>


<span data-ttu-id="faf05-140">Beispielsweise, um das Generieren eines Bereitstellungsskripts für die **ContactManager** Datenbank ohne Sie tatsächlich Bereitstellen der Datenbank, die den VSDBCMD-Befehl sollte diesem ähneln:</span><span class="sxs-lookup"><span data-stu-id="faf05-140">For example, to generate a deployment script for the **ContactManager** database without actually deploying the database, your VSDBCMD command should resemble this:</span></span>


[!code-console[Main](performing-a-what-if-deployment/samples/sample4.cmd)]


<span data-ttu-id="faf05-141">VSDBCMD ist ein Bereitstellungstool differenziellen Datenbank- und das Bereitstellungsskript wird als solche dynamisch generiert, um alle der SQL-Befehle erforderlich, die die aktuelle Datenbank zu aktualisieren, falls, die dem angegebenen Schema vorhanden enthalten.</span><span class="sxs-lookup"><span data-stu-id="faf05-141">VSDBCMD is a differential database deployment tool, and as such the deployment script is dynamically generated to contain all the SQL commands necessary to update the current database, if one exists, to the specified schema.</span></span> <span data-ttu-id="faf05-142">Überprüfen das Bereitstellungsskript ist eine gute Möglichkeit, um zu bestimmen, was die Bereitstellung auswirken wird in der aktuellen Datenbank und die darin enthaltenen Daten.</span><span class="sxs-lookup"><span data-stu-id="faf05-142">Reviewing the deployment script is a useful way to determine what impact your deployment will have on the current database and the data it contains.</span></span> <span data-ttu-id="faf05-143">Sie sollten z. B. um zu bestimmen:</span><span class="sxs-lookup"><span data-stu-id="faf05-143">For example, you might want to determine:</span></span>

- <span data-ttu-id="faf05-144">Gibt an, ob alle vorhandenen Tabellen entfernt werden, und gibt an, ob dies zu Datenverlust führt.</span><span class="sxs-lookup"><span data-stu-id="faf05-144">Whether any existing tables will be removed, and whether that will result in data loss.</span></span>
- <span data-ttu-id="faf05-145">Gibt an, ob die Reihenfolge der Vorgänge ein Risiko des Datenverlusts, z. B. enthält, wenn Sie teilen oder Zusammenführen von Tabellen.</span><span class="sxs-lookup"><span data-stu-id="faf05-145">Whether the order of operations carries a risk of data loss, for example, if you're splitting or merging tables.</span></span>

<span data-ttu-id="faf05-146">Wenn Sie mit dem Bereitstellungsskript zufrieden sind, können Sie die VSDBCMD mit Wiederholen einer **/dd+** Flag, um die Änderungen zu übernehmen.</span><span class="sxs-lookup"><span data-stu-id="faf05-146">If you're happy with the deployment script, you can repeat the VSDBCMD with a **/dd+** flag to make the changes.</span></span> <span data-ttu-id="faf05-147">Alternativ können Sie das Bereitstellungsskript aus, um Ihre Anforderungen erfüllen, und führen sie dann manuell auf dem Datenbankserver bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="faf05-147">Alternatively, you can edit the deployment script to meet your requirements and then execute it manually on the database server.</span></span>

## <a name="integrating-what-if-functionality-into-custom-project-files"></a><span data-ttu-id="faf05-148">Die Integration von "What If"-Funktionalität in benutzerdefinierten Projektdateien</span><span class="sxs-lookup"><span data-stu-id="faf05-148">Integrating "What If" Functionality into Custom Project Files</span></span>

<span data-ttu-id="faf05-149">In komplexeren Bereitstellungsszenarien, sollten Sie zu eine benutzerdefinierte Microsoft Build Engine (MSBuild)-Projektdatei zu verwenden, um Ihre Build- und bereitstellungs-Logik zu kapseln, wie in beschrieben [Grundlegendes zur Projektdatei](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span><span class="sxs-lookup"><span data-stu-id="faf05-149">In more complex deployment scenarios, you'll want to use a custom Microsoft Build Engine (MSBuild) project file to encapsulate your build and deployment logic, as described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span> <span data-ttu-id="faf05-150">Z. B. in der [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) beispiellösung, die *Publish.proj* Datei:</span><span class="sxs-lookup"><span data-stu-id="faf05-150">For example, in the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution, the *Publish.proj* file:</span></span>

- <span data-ttu-id="faf05-151">Erstellt die Lösung.</span><span class="sxs-lookup"><span data-stu-id="faf05-151">Builds the solution.</span></span>
- <span data-ttu-id="faf05-152">Wird die Web Deploy-Packen und Bereitstellen der Anwendung ContactManager.Mvc verwendet.</span><span class="sxs-lookup"><span data-stu-id="faf05-152">Uses Web Deploy to package and deploy the ContactManager.Mvc application.</span></span>
- <span data-ttu-id="faf05-153">Wird die Web Deploy-Packen und Bereitstellen der Anwendung ContactManager.Service verwendet.</span><span class="sxs-lookup"><span data-stu-id="faf05-153">Uses Web Deploy to package and deploy the ContactManager.Service application.</span></span>
- <span data-ttu-id="faf05-154">Stellt die **ContactManager** Datenbank.</span><span class="sxs-lookup"><span data-stu-id="faf05-154">Deploys the **ContactManager** database.</span></span>

<span data-ttu-id="faf05-155">Wenn Sie die Bereitstellung von mehreren Webpakete bzw. Datenbanken in einen Prozess Schritt für Schritt auf diese Weise integrieren, sollten Sie auch die Möglichkeit, die gesamte Bereitstellung in einem "what if"-Modus ausführen.</span><span class="sxs-lookup"><span data-stu-id="faf05-155">When you integrate the deployment of multiple web packages and/or databases into a single-step process in this way, you may also want the option of performing the entire deployment in a "what if" mode.</span></span>

<span data-ttu-id="faf05-156">Die *Publish.proj* Datei veranschaulicht, wie Sie dies tun können.</span><span class="sxs-lookup"><span data-stu-id="faf05-156">The *Publish.proj* file demonstrates how you can do this.</span></span> <span data-ttu-id="faf05-157">Zunächst müssen Sie eine Eigenschaft zum Speichern des Werts "Was-wäre-wenn" zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="faf05-157">First, you need to create a property to store the "what if" value:</span></span>


[!code-xml[Main](performing-a-what-if-deployment/samples/sample5.xml)]


<span data-ttu-id="faf05-158">In diesem Fall haben Sie eine Eigenschaft mit dem Namen erstellt **"WhatIf"** hat den Standardwert des **"false"**.</span><span class="sxs-lookup"><span data-stu-id="faf05-158">In this case, you've created a property named **WhatIf** with a default value of **false**.</span></span> <span data-ttu-id="faf05-159">Benutzer können diesen Wert durch Festlegen der Eigenschaft zu überschreiben **"true"** in einen Befehlszeilenparameter, wie Sie gleich sehen werden.</span><span class="sxs-lookup"><span data-stu-id="faf05-159">Users can override this value by setting the property to **true** in a command-line parameter, as you'll see shortly.</span></span>

<span data-ttu-id="faf05-160">Der nächste Schritt besteht, eine beliebige Web Deploy zu parametrisieren und VSDBCMD Befehle, sodass die Flags enthalten die **"WhatIf"** -Eigenschaftswert.</span><span class="sxs-lookup"><span data-stu-id="faf05-160">The next stage is to parameterize any Web Deploy and VSDBCMD commands so that the flags reflect the **WhatIf** property value.</span></span> <span data-ttu-id="faf05-161">Z. B. das nächste Ziel (stammt aus der *Publish.proj* Datei, und vereinfacht) ausgeführt wird die *. "Deploy.cmd"* Datei ein Webpaket bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="faf05-161">For example, the next target (taken from the *Publish.proj* file and simplified) runs the *.deploy.cmd* file to deploy a web package.</span></span> <span data-ttu-id="faf05-162">Standardmäßig enthält der Befehl eine **/y** Switch ("yes" oder Update-Modus).</span><span class="sxs-lookup"><span data-stu-id="faf05-162">By default, the command includes a **/Y** switch ("yes," or update mode).</span></span> <span data-ttu-id="faf05-163">Wenn **"WhatIf"** nastaven NA hodnotu **"true"**, dies wird durch ersetzt eine **/t /** Switch (Test- oder "Was-wäre-wenn"-Modus).</span><span class="sxs-lookup"><span data-stu-id="faf05-163">If **WhatIf** is set to **true**, this is replaced by a **/T** switch (trial, or "what if" mode).</span></span>


[!code-xml[Main](performing-a-what-if-deployment/samples/sample6.xml)]


<span data-ttu-id="faf05-164">Auf ähnliche Weise verwendet das nächste Ziel das VSDBCMD-Dienstprogramm zum Bereitstellen einer Datenbank.</span><span class="sxs-lookup"><span data-stu-id="faf05-164">Similarly, the next target uses the VSDBCMD utility to deploy a database.</span></span> <span data-ttu-id="faf05-165">Standardmäßig eine **dd /** Switch ist nicht enthalten.</span><span class="sxs-lookup"><span data-stu-id="faf05-165">By default, a **/dd** switch is not included.</span></span> <span data-ttu-id="faf05-166">Dies bedeutet, dass VSDBCMD ein Bereitstellungsskript generiert, aber die Datenbank nicht bereitgestellt werden&#x2014;in anderen Worten: ein "Was-wäre-wenn"-Szenario.</span><span class="sxs-lookup"><span data-stu-id="faf05-166">This means that VSDBCMD will generate a deployment script but will not deploy the database&#x2014;in other words, a "what if" scenario.</span></span> <span data-ttu-id="faf05-167">Wenn die **"WhatIf"** Eigenschaft ist nicht festgelegt, um **"true"**, **dd /** Schalter hinzugefügt wird und VSDBCMD wird die Datenbank bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="faf05-167">If the **WhatIf** property is not set to **true**, a **/dd** switch is added and VSDBCMD will deploy the database.</span></span>


[!code-xml[Main](performing-a-what-if-deployment/samples/sample7.xml)]


<span data-ttu-id="faf05-168">Sie können den gleichen Ansatz verwenden, parametrisieren Sie alle relevanten Befehle in Ihrer Projektdatei hinzu.</span><span class="sxs-lookup"><span data-stu-id="faf05-168">You can use the same approach to parameterize all the relevant commands in your project file.</span></span> <span data-ttu-id="faf05-169">Wenn Sie eine "Was-wäre-wenn"-Bereitstellung ausführen möchten, können Sie dann geben Sie einfach eine **"WhatIf"** Eigenschaftswert von der Befehlszeile aus:</span><span class="sxs-lookup"><span data-stu-id="faf05-169">When you want to run a "what if" deployment, you can then simply provide a **WhatIf** property value from the command line:</span></span>


[!code-console[Main](performing-a-what-if-deployment/samples/sample8.cmd)]


<span data-ttu-id="faf05-170">Auf diese Weise können Sie eine "Was-wäre-wenn" Bereitstellung für alle Projektkomponenten in einem einzigen Schritt ausführen.</span><span class="sxs-lookup"><span data-stu-id="faf05-170">In this way, you can run a "what if" deployment for all your project components in a single step.</span></span>

## <a name="conclusion"></a><span data-ttu-id="faf05-171">Schlussbemerkung</span><span class="sxs-lookup"><span data-stu-id="faf05-171">Conclusion</span></span>

<span data-ttu-id="faf05-172">In diesem Thema beschrieben, wie "Was-wäre-wenn"-Bereitstellungen mithilfe von Web Deploy, VSDBCMD und MSBuild ausführen.</span><span class="sxs-lookup"><span data-stu-id="faf05-172">This topic described how to run "what if" deployments using Web Deploy, VSDBCMD, and MSBuild.</span></span> <span data-ttu-id="faf05-173">Eine "Was-wäre-wenn"-Bereitstellung können Sie die Auswirkungen der vorgeschlagenen Bereitstellung ausgewertet, bevor Sie Änderungen in der zielumgebung tatsächlich vornehmen.</span><span class="sxs-lookup"><span data-stu-id="faf05-173">A "what if" deployment lets you evaluate the impact of a proposed deployment before you actually make any changes to the destination environment.</span></span>

## <a name="further-reading"></a><span data-ttu-id="faf05-174">Weiterführende Themen</span><span class="sxs-lookup"><span data-stu-id="faf05-174">Further Reading</span></span>

<span data-ttu-id="faf05-175">Weitere Informationen zu Web Deploy-Befehlszeilensyntax, finden Sie unter [Web Deploy-Vorgang Settings](https://technet.microsoft.com/library/dd569089(WS.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="faf05-175">For more information on Web Deploy command-line syntax, see [Web Deploy Operation Settings](https://technet.microsoft.com/library/dd569089(WS.10).aspx).</span></span> <span data-ttu-id="faf05-176">Informationen zu den Befehlszeilenoptionen, die bei der Verwendung der *. "Deploy.cmd"* finden Sie unter [Vorgehensweise: Installieren eines Bereitstellungspakets mit der Datei "Deploy.cmd"](https://msdn.microsoft.com/library/ff356104.aspx).</span><span class="sxs-lookup"><span data-stu-id="faf05-176">For guidance on command-line options when you use the *.deploy.cmd* file, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span> <span data-ttu-id="faf05-177">Anweisungen VSDBCMD Befehlszeilensyntax, finden Sie unter [Befehlszeilenreferenz für VSDBCMD. EXE-Datei ("Bereitstellung" und "Schema importieren")](https://msdn.microsoft.com/library/dd193283.aspx).</span><span class="sxs-lookup"><span data-stu-id="faf05-177">For guidance on VSDBCMD command-line syntax, see [Command-Line Reference for VSDBCMD.EXE (Deployment and Schema Import)](https://msdn.microsoft.com/library/dd193283.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="faf05-178">[Zurück](advanced-enterprise-web-deployment.md)
> [Weiter](customizing-database-deployments-for-multiple-environments.md)</span><span class="sxs-lookup"><span data-stu-id="faf05-178">[Previous](advanced-enterprise-web-deployment.md)
[Next](customizing-database-deployments-for-multiple-environments.md)</span></span>