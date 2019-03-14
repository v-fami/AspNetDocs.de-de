---
uid: identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
title: Implementieren eines benutzerdefinierten MySQL ASP.NET Identity-Speicheranbieters | Microsoft-Dokumentation
author: raquelsa
description: ASP.NET Identity ist ein erweiterbares System auf das diese Weise können Sie Ihren eigenen Anbieter erstellen und es in Ihre Anwendung einbinden, ohne die anwendungse erneut verarbeitet werden...
ms.author: riande
ms.date: 05/22/2015
ms.assetid: 248f5fe7-39ba-40ea-ab1e-71a69b0bd649
msc.legacyurl: /identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
msc.type: authoredcontent
ms.openlocfilehash: 358b1a3b7277f21c63a1d395f2a5fce79bbe0d56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57025947"
---
<a name="implementing-a-custom-mysql-aspnet-identity-storage-provider"></a><span data-ttu-id="7814e-103">Implementieren eines benutzerdefinierten MySQL ASP.NET Identity-Speicheranbieters</span><span class="sxs-lookup"><span data-stu-id="7814e-103">Implementing a Custom MySQL ASP.NET Identity Storage Provider</span></span>
====================
<span data-ttu-id="7814e-104">by [Raquel Soares De Almeida](https://github.com/raquelsa), [Suhas Joshi](https://github.com/suhasj), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="7814e-104">by [Raquel Soares De Almeida](https://github.com/raquelsa), [Suhas Joshi](https://github.com/suhasj), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="7814e-105">ASP.NET Identity ist ein erweiterbares System auf das diese Weise können Sie Ihren eigenen Anbieter erstellen und es in Ihre Anwendung einbinden, ohne die Anwendung erneut verarbeitet werden muss.</span><span class="sxs-lookup"><span data-stu-id="7814e-105">ASP.NET Identity is an extensible system which enables you to create your own storage provider and plug it into your application without re-working the application.</span></span> <span data-ttu-id="7814e-106">Dieses Thema beschreibt, wie Sie einen MySQL-Speicheranbieter für ASP.NET Identity zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="7814e-106">This topic describes how to create a MySQL storage provider for ASP.NET Identity.</span></span> <span data-ttu-id="7814e-107">Eine Übersicht über benutzerdefinierte Speicheranbieter erstellen, finden Sie unter [Übersicht über die der benutzerdefinierte Speicheranbieter für ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md).</span><span class="sxs-lookup"><span data-stu-id="7814e-107">For an overview of creating custom storage providers, see [Overview of Custom Storage Providers for ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md).</span></span>
> 
> <span data-ttu-id="7814e-108">Um dieses Tutorial abzuschließen, müssen Sie Visual Studio 2013 mit Update 2 verfügen.</span><span class="sxs-lookup"><span data-stu-id="7814e-108">To complete this tutorial, you must have Visual Studio 2013 with Update 2.</span></span>
> 
> <span data-ttu-id="7814e-109">Dieses Tutorial verwendet:</span><span class="sxs-lookup"><span data-stu-id="7814e-109">This tutorial will:</span></span>
> 
> - <span data-ttu-id="7814e-110">Veranschaulicht das Erstellen einer MySQL-Datenbankinstanz in Azure.</span><span class="sxs-lookup"><span data-stu-id="7814e-110">Show how to create a MySQL database instance on Azure.</span></span>
> - <span data-ttu-id="7814e-111">Verwenden Sie eine MySQL-Client-Tool (MySQL Workbench) Tabellen erstellen und Verwalten der remote-Datenbank in Azure veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="7814e-111">Show how to use a MySQL client tool (MySQL Workbench) to create tables and manage your remote database on Azure.</span></span>
> - <span data-ttu-id="7814e-112">Veranschaulicht die Standard-Speicher-Implementierung von ASP.NET Identity durch unsere benutzerdefinierte Implementierung für ein MVC-Anwendungsprojekt zu ersetzen.</span><span class="sxs-lookup"><span data-stu-id="7814e-112">Show how to replace the default ASP.NET Identity storage implementation with our custom implementation on a MVC application project.</span></span>
> 
> <span data-ttu-id="7814e-113">In diesem Tutorial wurde ursprünglich von Raquel Soares De Almeida und Rick Anderson geschrieben ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) ).</span><span class="sxs-lookup"><span data-stu-id="7814e-113">This tutorial was originally written by Raquel Soares De Almeida and Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ).</span></span> <span data-ttu-id="7814e-114">Das Beispielprojekt wurde für Identität 2.0 von Suhas Joshi aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="7814e-114">The sample project was updated for Identity 2.0 by Suhas Joshi.</span></span> <span data-ttu-id="7814e-115">Das Thema wurde für Identität 2.0 von Tom FitzMacken aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="7814e-115">The topic was updated for Identity 2.0 by Tom FitzMacken.</span></span>


## <a name="download-completed-project"></a><span data-ttu-id="7814e-116">Heruntergeladenen Projekt</span><span class="sxs-lookup"><span data-stu-id="7814e-116">Download completed project</span></span>

<span data-ttu-id="7814e-117">Am Ende dieses Tutorials müssen Sie ein MVC-Anwendungsprojekt mit ASP.NET Identity arbeiten mit einer MySQL-Datenbank in Azure gehostet.</span><span class="sxs-lookup"><span data-stu-id="7814e-117">At the end of this tutorial, you will have an MVC application project with ASP.NET Identity working with a MySQL database hosted on Azure.</span></span>

<span data-ttu-id="7814e-118">Sie können den abgeschlossenen MySQL-Speicheranbieter auf [AspNet.Identity.MySQL (CodePlex)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/).</span><span class="sxs-lookup"><span data-stu-id="7814e-118">You can download the completed MySQL storage provider at [AspNet.Identity.MySQL (CodePlex)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/).</span></span>

## <a name="the-steps-you-will-perform"></a><span data-ttu-id="7814e-119">Die Schritte, die Sie ausführen</span><span class="sxs-lookup"><span data-stu-id="7814e-119">The steps you will perform</span></span>

<span data-ttu-id="7814e-120">In diesem Lernprogramm führen Sie folgende Aktionen ausführen:</span><span class="sxs-lookup"><span data-stu-id="7814e-120">In this tutorial you will:</span></span>

1. <span data-ttu-id="7814e-121">Erstellen Sie eine MySQL-Datenbank in Azure</span><span class="sxs-lookup"><span data-stu-id="7814e-121">Create a MySQL database on Azure</span></span>
2. <span data-ttu-id="7814e-122">Erstellen von Tabellen in MySQL für die ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="7814e-122">Create the ASP.NET Identity tables in MySQL</span></span>
3. <span data-ttu-id="7814e-123">Erstellen Sie eine MVC-Anwendung und konfigurieren Sie, dass den MySQL-Anbieter verwendet</span><span class="sxs-lookup"><span data-stu-id="7814e-123">Create an MVC application and configure it to use the MySQL provider</span></span>
4. <span data-ttu-id="7814e-124">Ausführen der App</span><span class="sxs-lookup"><span data-stu-id="7814e-124">Run the app</span></span>

<span data-ttu-id="7814e-125">In diesem Thema werden nicht behandelt, die Architektur von ASP.NET Identity und die Entscheidungen, die Sie bei der Implementierung eines Speicheranbieters Kunden treffen müssen.</span><span class="sxs-lookup"><span data-stu-id="7814e-125">This topic does not cover the architecture of ASP.NET Identity and the decisions you must make when implementing a customer storage provider.</span></span> <span data-ttu-id="7814e-126">Diese Informationen finden Sie unter [Übersicht über die der benutzerdefinierte Speicheranbieter für ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md).</span><span class="sxs-lookup"><span data-stu-id="7814e-126">For that information, see [Overview of Custom Storage Providers for ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md).</span></span>

## <a name="review-mysql-storage-provider-classes"></a><span data-ttu-id="7814e-127">Überprüfen Sie die MySQL-Storage-Anbieterklassen</span><span class="sxs-lookup"><span data-stu-id="7814e-127">Review MySQL storage provider classes</span></span>

<span data-ttu-id="7814e-128">Vor der Installation die Schritte zum Erstellen des MySQL-Speicheranbieters, sehen wir uns die Klassen, die den Speicheranbieter bilden.</span><span class="sxs-lookup"><span data-stu-id="7814e-128">Before jumping into the steps to create the MySQL storage provider, let's look at the classes that make up the storage provider.</span></span> <span data-ttu-id="7814e-129">Sie benötigen, die die Datenbankvorgänge zu verwalten und Klassen, die von der Anwendung zum Verwalten von Benutzern und Rollen aufgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="7814e-129">You will need classes that manage the database operations and classes that are called from the application to manage users and roles.</span></span>

### <a name="storage-classes"></a><span data-ttu-id="7814e-130">Speicherklassen</span><span class="sxs-lookup"><span data-stu-id="7814e-130">Storage classes</span></span>

- <span data-ttu-id="7814e-131">["Identityuser"](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityUser.cs) -Eigenschaften für den Benutzer enthält.</span><span class="sxs-lookup"><span data-stu-id="7814e-131">[IdentityUser](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityUser.cs) - contains properties for the user.</span></span>
- <span data-ttu-id="7814e-132">[UserStore](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserStore.cs) -Vorgänge zum Hinzufügen, aktualisieren oder Abrufen von Benutzern enthält.</span><span class="sxs-lookup"><span data-stu-id="7814e-132">[UserStore](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserStore.cs) - contains operations for adding, updating or retrieving users.</span></span>
- <span data-ttu-id="7814e-133">[IdentityRole](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityRole.cs) -Eigenschaften für Rollen enthält.</span><span class="sxs-lookup"><span data-stu-id="7814e-133">[IdentityRole](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityRole.cs) - contains properties for roles.</span></span>
- <span data-ttu-id="7814e-134">[RoleStore](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleStore.cs) -Vorgänge zum Hinzufügen, löschen, aktualisieren und Abrufen von Rollen enthält.</span><span class="sxs-lookup"><span data-stu-id="7814e-134">[RoleStore](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleStore.cs) - contains operations for adding, deleting, updating and retrieving roles.</span></span>

### <a name="data-access-layer-classes"></a><span data-ttu-id="7814e-135">Data Access Layer Klassen</span><span class="sxs-lookup"><span data-stu-id="7814e-135">Data access layer classes</span></span>

<span data-ttu-id="7814e-136">In diesem Beispiel enthalten die Ebene der Datenzugriffsklassen SQL-Anweisungen für die Arbeit mit den Tabellen; in Ihrem Code möchten jedoch kann objektrelationales Mapping (ORM) wie Entity Framework oder NHibernate zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="7814e-136">For this example, the data access layer classes contain SQL statements for working with the tables; however, in your code you might want to use object-relational mapping (ORM) such as Entity Framework or NHibernate.</span></span> <span data-ttu-id="7814e-137">Insbesondere kann Ihre Anwendung eine schlechte Leistung ohne ORM auftreten, die lazy Loading und das Zwischenspeichern von Objekten enthält.</span><span class="sxs-lookup"><span data-stu-id="7814e-137">In particular, your application may experience poor performance without an ORM that includes lazy loading and object caching.</span></span> <span data-ttu-id="7814e-138">Weitere Informationen finden Sie unter [ASP.NET Identity 2.0 ohne Entity Framework?](https://aspnetidentity.codeplex.com/discussions/561828)</span><span class="sxs-lookup"><span data-stu-id="7814e-138">For more information, see [ASP.NET Identity 2.0 without Entity Framework?](https://aspnetidentity.codeplex.com/discussions/561828)</span></span>

- <span data-ttu-id="7814e-139">[MySQLDatabase](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) -enthält die Verbindung für MySQL-Datenbank und die Methoden zum Ausführen von Datenbankoperationen.</span><span class="sxs-lookup"><span data-stu-id="7814e-139">[MySQLDatabase](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) - contains the MySQL database connection and methods for performing database operations.</span></span> <span data-ttu-id="7814e-140">UserStore und RoleStore, die beide mit einer Instanz dieser Klasse instanziiert werden.</span><span class="sxs-lookup"><span data-stu-id="7814e-140">UserStore and RoleStore are both instantiated with an instance of this class.</span></span>
- <span data-ttu-id="7814e-141">[RoleTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleTable.cs) -Datenbankvorgänge für die Tabelle, die Rollen speichert enthält.</span><span class="sxs-lookup"><span data-stu-id="7814e-141">[RoleTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleTable.cs) - contains database operations for the table that stores roles.</span></span>
- <span data-ttu-id="7814e-142">[UserClaimsTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) -Datenbankvorgänge für die Tabelle, die Ansprüche des Benutzers speichert enthält.</span><span class="sxs-lookup"><span data-stu-id="7814e-142">[UserClaimsTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) - contains database operations for the table that stores user claims.</span></span>
- <span data-ttu-id="7814e-143">[UserLoginsTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) -Datenbankvorgänge für die Tabelle, die Anmeldeinformationen des Benutzers speichert enthält.</span><span class="sxs-lookup"><span data-stu-id="7814e-143">[UserLoginsTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) - contains database operations for the table that stores user login information.</span></span>
- <span data-ttu-id="7814e-144">[UserRoleTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) -enthält-Datenbankvorgänge für die Tabelle, gespeichert, welche Benutzer welchen Rollen zugewiesen werden.</span><span class="sxs-lookup"><span data-stu-id="7814e-144">[UserRoleTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) - contains database operations for the table that stores which users are assigned to which roles.</span></span>
- <span data-ttu-id="7814e-145">[UserTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserTable.cs) -Datenbankvorgänge für die Tabelle, die Benutzer speichert enthält.</span><span class="sxs-lookup"><span data-stu-id="7814e-145">[UserTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserTable.cs) - contains database operations for the table that stores users.</span></span>

## <a name="create-a-mysql-database-instance-on-azure"></a><span data-ttu-id="7814e-146">Erstellen Sie eine MySQL-Datenbankinstanz in Azure</span><span class="sxs-lookup"><span data-stu-id="7814e-146">Create a MySQL database instance on Azure</span></span>

1. <span data-ttu-id="7814e-147">Melden Sie sich beim [Azure-Portal](https://manage.windowsazure.com/) an.</span><span class="sxs-lookup"><span data-stu-id="7814e-147">Log in to the [Azure Portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="7814e-148">Klicken Sie auf **+ neu** am unteren Rand der Seite, und wählen Sie dann **STORE**.</span><span class="sxs-lookup"><span data-stu-id="7814e-148">Click **+NEW** at the bottom of the page, and then select **STORE**.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.png)
3. <span data-ttu-id="7814e-149">In der **auswählen und der Add-On-** Assistenten **ClearDB MySQL-Datenbank** und klicken Sie auf den Vorwärtspfeil unten rechts im Dialogfeld.</span><span class="sxs-lookup"><span data-stu-id="7814e-149">In the **Choose and Add-on** wizard, select **ClearDB MySQL Database** and click on the next arrow at the bottom right of the dialog.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.png)
4. <span data-ttu-id="7814e-150">Behalten Sie den Standardwert **Free** planen, und ändern Sie die **Namen** zu **IdentityMySQLDatabase**.</span><span class="sxs-lookup"><span data-stu-id="7814e-150">Keep the default **Free** plan and change the **Name** to **IdentityMySQLDatabase**.</span></span> <span data-ttu-id="7814e-151">Wählen Sie die Region in Ihrer Nähe, und klicken Sie dann auf den Pfeil "Weiter".</span><span class="sxs-lookup"><span data-stu-id="7814e-151">Select the region nearest you and then click the next arrow.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.png)
5. <span data-ttu-id="7814e-152">Klicken Sie auf das Häkchen, um die Datenbankerstellung abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="7814e-152">Click the checkmark to complete the database creation.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image4.png)
6. <span data-ttu-id="7814e-153">Nachdem Ihre Datenbank erstellt wurde, können Sie verwalten, von der **-Add-Ons** Registerkarte im Verwaltungsportal.</span><span class="sxs-lookup"><span data-stu-id="7814e-153">After your database has been created, you can manage it from the **ADD-ONS** tab in the management portal.</span></span>   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image5.png)
7. <span data-ttu-id="7814e-154">Sie können die Datenbankverbindungsinformationen abrufen, indem Sie durch Klicken auf **VERBINDUNGSINFORMATIONEN** am unteren Rand der Seite.</span><span class="sxs-lookup"><span data-stu-id="7814e-154">You can get the database connection information by clicking on **CONNECTION INFO** at the bottom of the page.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image6.png)
8. <span data-ttu-id="7814e-155">Kopieren Sie die Verbindungszeichenfolge durch Klicken auf die Schaltfläche "Kopieren" aus, und speichern Sie, um Sie weiter unten in der MVC-Anwendung verwenden können.</span><span class="sxs-lookup"><span data-stu-id="7814e-155">Copy the connection string by clicking on the copy button and save it so you can use later in your MVC application.</span></span>   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image7.png)

## <a name="create-the-aspnet-identity-tables-in-a-mysql-database"></a><span data-ttu-id="7814e-156">Erstellen von Tabellen in einer MySQL-Datenbank für die ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="7814e-156">Create the ASP.NET Identity tables in a MySQL database</span></span>

### <a name="install-mysql-workbench-tool-to-connect-and-manage-mysql-database"></a><span data-ttu-id="7814e-157">Installieren von MySQL Workbench-Tool, um eine Verbindung herstellen und Verwalten von MySQL-Datenbank</span><span class="sxs-lookup"><span data-stu-id="7814e-157">Install MySQL Workbench tool to connect and manage MySQL database</span></span>

1. <span data-ttu-id="7814e-158">Installieren Sie die **MySQL Workbench** tool die [MySQL-Downloadseite](http://dev.mysql.com/downloads/windows/installer/)</span><span class="sxs-lookup"><span data-stu-id="7814e-158">Install the **MySQL Workbench** tool from the [MySQL downloads page](http://dev.mysql.com/downloads/windows/installer/)</span></span>
2. <span data-ttu-id="7814e-159">Starten Sie die app aus, und klicken Sie auf Hinzufügen der **MySQLConnections +** , um eine neue Verbindung hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="7814e-159">Launch the app and add click on the **MySQLConnections +** button to add a new connection.</span></span> <span data-ttu-id="7814e-160">Verwenden Sie die Verbindungsdaten für die Zeichenfolge, die Sie aus der Azure-MySQL-Datenbank kopiert, die Sie zuvor in diesem Tutorial erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="7814e-160">Use the connection string data you copied from the Azure MySQL database you created earlier in this tutorial.</span></span>
3. <span data-ttu-id="7814e-161">Nach dem Herstellen der Verbindung an, öffnen Sie ein neues **Abfrage** Registerkarte; fügen Sie die Befehle von [MySQLIdentity.sql](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql) in die Abfrage und führen Sie es um die Datenbanktabellen erstellen.</span><span class="sxs-lookup"><span data-stu-id="7814e-161">After establishing the connection, open a new **Query** tab; paste the commands from [MySQLIdentity.sql](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql) into the query and execute it in order to create the database tables.</span></span>
4. <span data-ttu-id="7814e-162">Sie haben jetzt alle ASP.NET Identity erforderlichen Tabellen in einer MySQL-Datenbank in Azure gehostet werden, wie unten gezeigt erstellt.</span><span class="sxs-lookup"><span data-stu-id="7814e-162">You now have all the ASP.NET Identity necessary tables created on a MySQL database hosted on Azure as shown below.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.jpg)

## <a name="create-an-mvc-application-project-from-template-and-configure-it-to-use-mysql-provider"></a><span data-ttu-id="7814e-163">Erstellen Sie eine MVC-Anwendungsprojekt aus Vorlage und konfigurieren Sie, um MySQL-Anbieters zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="7814e-163">Create an MVC application project from template and configure it to use MySQL provider</span></span>

<span data-ttu-id="7814e-164">Installieren Sie bei Bedarf entweder [Visual Studio Express 2013 für Web](https://go.microsoft.com/fwlink/?LinkId=299058) oder [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) mit Update 2.</span><span class="sxs-lookup"><span data-stu-id="7814e-164">If needed, install either [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) with Update 2.</span></span>

### <a name="download-the-aspnetidentitymysql-project-from-codeplex"></a><span data-ttu-id="7814e-165">Laden Sie das Projekt ASP.NET.Identity.MySQL von CodePlex herunter</span><span class="sxs-lookup"><span data-stu-id="7814e-165">Download the ASP.NET.Identity.MySQL project from CodePlex</span></span>

1. <span data-ttu-id="7814e-166">Navigieren Sie zu die Repository-URL auf [AspNet.Identity.MySQL (CodePlex)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/).</span><span class="sxs-lookup"><span data-stu-id="7814e-166">Browse to the repository URL at [AspNet.Identity.MySQL (CodePlex)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/).</span></span>
2. <span data-ttu-id="7814e-167">Den Quellcode herunterladen.</span><span class="sxs-lookup"><span data-stu-id="7814e-167">Download the source code.</span></span>
3. <span data-ttu-id="7814e-168">Extrahieren Sie die ZIP-Datei in einen lokalen Ordner ein.</span><span class="sxs-lookup"><span data-stu-id="7814e-168">Extract the .zip file into a local folder.</span></span>
4. <span data-ttu-id="7814e-169">Öffnen Sie die AspNet.Identity.MySQL-Projektmappe, und erstellen Sie sie.</span><span class="sxs-lookup"><span data-stu-id="7814e-169">Open the AspNet.Identity.MySQL solution and build it.</span></span>

### <a name="create-a-new-mvc-application-project-from-template"></a><span data-ttu-id="7814e-170">Erstellen Sie ein neues MVC-Anwendungsprojekt aus Vorlage</span><span class="sxs-lookup"><span data-stu-id="7814e-170">Create a new MVC application project from template</span></span>

1. <span data-ttu-id="7814e-171">Klicken Sie mit der rechten Maustaste auf die **AspNet.Identity.MySQL** Lösung und **hinzufügen**, **neues Projekt**</span><span class="sxs-lookup"><span data-stu-id="7814e-171">Right click the **AspNet.Identity.MySQL** solution and **Add**, **New Project**</span></span>
2. <span data-ttu-id="7814e-172">In der **neues Projekt hinzufügen** Dialogfeld **Visual C#-** auf der linken Seite, klicken Sie dann **Web** und wählen Sie dann **ASP.NET-Webanwendung**.</span><span class="sxs-lookup"><span data-stu-id="7814e-172">In the **Add New Project** Dialog select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="7814e-173">Benennen Sie Ihr Projekt **IdentityMySQLDemo**; und klicken Sie dann auf OK.</span><span class="sxs-lookup"><span data-stu-id="7814e-173">Name your project **IdentityMySQLDemo**; and then click OK.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.jpg)
3. <span data-ttu-id="7814e-174">In der **neues ASP.NET-Projekt** Dialogfeld Wählen Sie die MVC-Vorlage mit den Standardoptionen (dazu gehören **einzelne Benutzerkonten** als Authentifizierungsmethode), und klicken Sie auf **OK** .![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)</span><span class="sxs-lookup"><span data-stu-id="7814e-174">In the **New ASP.NET Project** dialog, select the MVC template with the default options (that includes **Individual User Accounts** as authentication method) and click **OK**.![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)</span></span>
4. <span data-ttu-id="7814e-175">Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste in des IdentityMySQLDemo-Projekts, und wählen **NuGet-Pakete verwalten**.</span><span class="sxs-lookup"><span data-stu-id="7814e-175">In Solution Explorer, right-click your IdentityMySQLDemo project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="7814e-176">Geben Sie im Dialogfeld im Feld Suchen Text **Identity.EntityFramework**.</span><span class="sxs-lookup"><span data-stu-id="7814e-176">In the search text box dialog, type **Identity.EntityFramework**.</span></span> <span data-ttu-id="7814e-177">Wählen Sie in der Liste der Ergebnisse dieses Paket aus, und klicken Sie auf **Deinstallieren**.</span><span class="sxs-lookup"><span data-stu-id="7814e-177">Select this package in the list of results and click **Uninstall**.</span></span> <span data-ttu-id="7814e-178">Sie werden zum Deinstallieren des Dependency-Pakets EntityFramework aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="7814e-178">You will be prompted to uninstall the dependency package EntityFramework.</span></span> <span data-ttu-id="7814e-179">Klicken Sie auf Ja, wie nicht mehr an diese Anwendung.</span><span class="sxs-lookup"><span data-stu-id="7814e-179">Click on Yes as we will no longer this package on this application.</span></span>
5. <span data-ttu-id="7814e-180">Klicken Sie mit der rechten Maustaste auf das IdentityMySQLDemo-Projekt, wählen Sie **hinzufügen**, **Verweis, Projektmappen, Projekten;** wählen Sie das AspNet.Identity.MySQL-Projekt, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="7814e-180">Right click the IdentityMySQLDemo project, select **Add**, **Reference, Solution, Projects;** select the AspNet.Identity.MySQL project and click **OK**.</span></span>
6. <span data-ttu-id="7814e-181">Ersetzen Sie im Projekt IdentityMySQLDemo alle Verweise auf</span><span class="sxs-lookup"><span data-stu-id="7814e-181">In the IdentityMySQLDemo project, replace all references to</span></span>  
    `using Microsoft.AspNet.Identity.EntityFramework;`  
   <span data-ttu-id="7814e-182">durch</span><span class="sxs-lookup"><span data-stu-id="7814e-182">with</span></span>  
     `using AspNet.Identity.MySQL;`
7. <span data-ttu-id="7814e-183">Legen Sie im IdentityModels.cs, **ApplicationDbContext** abgeleitet **MySqlDatabase** und fügen Sie einen Konstruktor, der einen einzelnen Parameter mit dem Namen der Verbindung.</span><span class="sxs-lookup"><span data-stu-id="7814e-183">In IdentityModels.cs, set **ApplicationDbContext** to derive from **MySqlDatabase** and include a contructor that take a single parameter with the connection name.</span></span>  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample1.cs)]
8. <span data-ttu-id="7814e-184">Öffnen Sie die IdentityConfig.cs-Datei.</span><span class="sxs-lookup"><span data-stu-id="7814e-184">Open the IdentityConfig.cs file.</span></span> <span data-ttu-id="7814e-185">In der **ApplicationUserManager.Create** -Methode, instanziieren die UserManager durch den folgenden Code ersetzen:</span><span class="sxs-lookup"><span data-stu-id="7814e-185">In the **ApplicationUserManager.Create** method, replace instantiating UserManager with the following code:</span></span>  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample2.cs)]
9. <span data-ttu-id="7814e-186">Öffnen Sie die Datei "Web.config" ein, und Ersetzen Sie die Zeichenfolge DefaultConnection mit diesem Eintrag, und Ersetzen Sie dabei die hervorgehobenen Werte durch die Verbindungszeichenfolge der MySQL-Datenbank, die Sie auf den vorherigen Schritten erstellt haben:</span><span class="sxs-lookup"><span data-stu-id="7814e-186">Open the web.config file and replace the DefaultConnection string with this entry replacing the highlighted values with the connection string of the MySQL database you created on previous steps:</span></span>  

    [!code-xml[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample3.xml?highlight=2)]

## <a name="run-the-app-and-connect-to-the-mysql-db"></a><span data-ttu-id="7814e-187">Führen Sie die app und eine Verbindung mit der MySQL-Datenbank</span><span class="sxs-lookup"><span data-stu-id="7814e-187">Run the app and connect to the MySQL DB</span></span>

1. <span data-ttu-id="7814e-188">Klicken Sie mit der rechten Maustaste auf die **IdentityMySQLDemo** Projekt, und wählen **als Startprojekt festlegen**</span><span class="sxs-lookup"><span data-stu-id="7814e-188">Right click the **IdentityMySQLDemo** project and select **Set as Startup Project**</span></span>
2. <span data-ttu-id="7814e-189">Drücken Sie **STRG + F5** erstellen und Ausführen der app.</span><span class="sxs-lookup"><span data-stu-id="7814e-189">Press **Ctrl + F5** to build and run the app.</span></span>
3. <span data-ttu-id="7814e-190">Klicken Sie auf **registrieren** Registerkarte oben auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="7814e-190">Click on **Register** tab on the top of the page.</span></span>
4. <span data-ttu-id="7814e-191">Geben Sie einen neuen Benutzernamen und ein Kennwort ein, und klicken Sie dann auf **registrieren**.</span><span class="sxs-lookup"><span data-stu-id="7814e-191">Enter a new user name and password and then click on **Register**.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image8.png)
5. <span data-ttu-id="7814e-192">Der neue Benutzer ist nun registriert und angemeldet.</span><span class="sxs-lookup"><span data-stu-id="7814e-192">The new user is now registered and logged in.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image9.png)
6. <span data-ttu-id="7814e-193">Wechseln Sie zurück zu dem Tool MySQL Workbench, und überprüfen Sie die **IdentityMySQLDatabase** des Tabelleninhalts.</span><span class="sxs-lookup"><span data-stu-id="7814e-193">Go back to the MySQL Workbench tool and inspect the **IdentityMySQLDatabase** table's contents.</span></span> <span data-ttu-id="7814e-194">Überprüfen der Tabelle für die Einträge an, wie Sie neue Benutzer registrieren.</span><span class="sxs-lookup"><span data-stu-id="7814e-194">Inspect the users table for the entries as you register new users.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image10.png)

## <a name="next-steps"></a><span data-ttu-id="7814e-195">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="7814e-195">Next Steps</span></span>

<span data-ttu-id="7814e-196">Weitere Informationen zum Aktivieren der anderen Authentifizierungsmethoden in dieser app finden Sie unter [erstellen Sie eine ASP.NET MVC 5-App mit Facebook und Google OAuth2 und OpenID-Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="7814e-196">For more information on how to enable other authentication methods on this app, refer to [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>

<span data-ttu-id="7814e-197">Um zu erfahren, wie Sie Ihre Datenbank mit OAuth zu integrieren und Rollen einrichten, um Benutzern den Zugriff auf Ihre app zu beschränken, finden Sie unter [bereitstellen eine sicheren ASP.NET MVC 5-app mit Mitgliedschaft, OAuth und SQL-Datenbank in Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="7814e-197">To learn how to integrate your DB with OAuth and to set up roles to limit users access to your app, see [Deploy a Secure ASP.NET MVC 5 app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>