---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
title: Erste Schritte mit Entity Framework 4.0 Database First und ASP.NET 4 Web Forms – Teil 7 | Microsoft-Dokumentation
author: tdykstra
description: Die Contoso University-Beispielwebanwendung veranschaulicht, wie ASP.NET Web Forms-Anwendungen, die mithilfe von Entity Framework. Die beispielanwendung ist...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: f8afb245-b705-419c-8790-0b295e90d5e2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
msc.type: authoredcontent
ms.openlocfilehash: 48092838ac0b00137ae0a4e37391c31883afcd09
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57027917"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-7"></a><span data-ttu-id="357ef-104">Erste Schritte mit Entity Framework 4.0 Database First und ASP.NET 4 Web Forms – Teil 7</span><span class="sxs-lookup"><span data-stu-id="357ef-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 7</span></span>
====================
<span data-ttu-id="357ef-105">durch [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="357ef-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="357ef-106">Die Contoso University-Beispielwebanwendung veranschaulicht, wie ASP.NET Web Forms-Anwendungen, die mit dem Entity Framework 4.0 und Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="357ef-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="357ef-107">Weitere Informationen zu dieser tutorialreihe finden Sie unter [im ersten Tutorial der Reihe](the-entity-framework-and-aspnet-getting-started-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="357ef-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>


## <a name="using-stored-procedures"></a><span data-ttu-id="357ef-108">Verwenden von gespeicherten Prozeduren</span><span class="sxs-lookup"><span data-stu-id="357ef-108">Using Stored Procedures</span></span>

<span data-ttu-id="357ef-109">Im vorherigen Tutorial implementiert Sie eine Tabelle pro Hierarchie Vererbungsmuster.</span><span class="sxs-lookup"><span data-stu-id="357ef-109">In the previous tutorial you implemented a table-per-hierarchy inheritance pattern.</span></span> <span data-ttu-id="357ef-110">Dieses Tutorial zeigt Ihnen, wie Sie gespeicherte Prozeduren zu verwenden, um mehr Kontrolle über Zugriff auf die Datenbank zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="357ef-110">This tutorial will show you how to use stored procedures to gain more control over database access.</span></span>

<span data-ttu-id="357ef-111">Das Entity Framework können Sie angeben, dass gespeicherte Prozeduren für den Datenbankzugriff verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="357ef-111">The Entity Framework lets you specify that it should use stored procedures for database access.</span></span> <span data-ttu-id="357ef-112">Für jeden Entitätstyp können Sie eine gespeicherte Prozedur für die Verwendung für erstellen, aktualisieren oder Löschen von Entitäten des Typs angeben.</span><span class="sxs-lookup"><span data-stu-id="357ef-112">For any entity type, you can specify a stored procedure to use for creating, updating, or deleting entities of that type.</span></span> <span data-ttu-id="357ef-113">Im Datenmodell können Sie dann Verweise auf gespeicherte Prozeduren, mit denen Sie Aufgaben wie das Abrufen von Gruppen von Entitäten hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="357ef-113">Then in the data model you can add references to stored procedures that you can use to perform tasks such as retrieving sets of entities.</span></span>

<span data-ttu-id="357ef-114">Verwenden von gespeicherten Prozeduren ist eine häufige Anforderung für den Datenbankzugriff.</span><span class="sxs-lookup"><span data-stu-id="357ef-114">Using stored procedures is a common requirement for database access.</span></span> <span data-ttu-id="357ef-115">In einigen Fällen kann ein Datenbankadministrator erfordert, dass gespeicherte Prozeduren aus Sicherheitsgründen jeglicher Datenbankzugriff durchlaufen.</span><span class="sxs-lookup"><span data-stu-id="357ef-115">In some cases a database administrator may require that all database access go through stored procedures for security reasons.</span></span> <span data-ttu-id="357ef-116">In anderen Fällen empfiehlt es sich um Geschäftslogik in einige der Prozesse zu erstellen, die das Entity Framework verwendet, wenn die Datenbank aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="357ef-116">In other cases you may want to build business logic into some of the processes that the Entity Framework uses when it updates the database.</span></span> <span data-ttu-id="357ef-117">Z. B. wenn eine Entität gelöscht wird empfiehlt in einer Datenbank "Archive" kopieren.</span><span class="sxs-lookup"><span data-stu-id="357ef-117">For example, whenever an entity is deleted you might want to copy it to an archive database.</span></span> <span data-ttu-id="357ef-118">Oder wenn eine Zeile aktualisiert wird möglicherweise einer Zeile in einer Protokollierungstabelle, in dem aufgezeichnet schreiben möchten, die Änderung vorgenommen hat.</span><span class="sxs-lookup"><span data-stu-id="357ef-118">Or whenever a row is updated you might want to write a row to a logging table that records who made the change.</span></span> <span data-ttu-id="357ef-119">Sie können diese Arten von Aufgaben in einer gespeicherten Prozedur ausführen, die aufgerufen wird, wenn Entity Framework eine Entität löscht oder eine Entität aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="357ef-119">You can perform these kinds of tasks in a stored procedure that's called whenever the Entity Framework deletes an entity or updates an entity.</span></span>

<span data-ttu-id="357ef-120">Wie im vorherigen Tutorial erstellen Sie keine neuen Seiten.</span><span class="sxs-lookup"><span data-stu-id="357ef-120">As in the previous tutorial, you'll not create any new pages.</span></span> <span data-ttu-id="357ef-121">Stattdessen werden Sie ändern, wie das Entity Framework die Datenbank für einige Seiten greift auf Sie bereits erstellt.</span><span class="sxs-lookup"><span data-stu-id="357ef-121">Instead, you'll change the way the Entity Framework accesses the database for some of the pages you already created.</span></span>

<span data-ttu-id="357ef-122">In diesem Tutorial erstellen Sie gespeicherte Prozeduren in der Datenbank für das Einfügen von `Student` und `Instructor` Entitäten.</span><span class="sxs-lookup"><span data-stu-id="357ef-122">In this tutorial you'll create stored procedures in the database for inserting `Student` and `Instructor` entities.</span></span> <span data-ttu-id="357ef-123">Fügen Sie sie in das Datenmodell, und geben Sie, dass sie Entity Framework zum Hinzufügen von verwenden soll `Student` und `Instructor` Entitäten in der Datenbank.</span><span class="sxs-lookup"><span data-stu-id="357ef-123">You'll add them to the data model, and you'll specify that the Entity Framework should use them for adding `Student` and `Instructor` entities to the database.</span></span> <span data-ttu-id="357ef-124">Sie erstellen auch eine gespeicherte Prozedur, die Sie, zum Abrufen verwenden können `Course` Entitäten.</span><span class="sxs-lookup"><span data-stu-id="357ef-124">You'll also create a stored procedure that you can use to retrieve `Course` entities.</span></span>

## <a name="creating-stored-procedures-in-the-database"></a><span data-ttu-id="357ef-125">Erstellen von gespeicherten Prozeduren in der Datenbank</span><span class="sxs-lookup"><span data-stu-id="357ef-125">Creating Stored Procedures in the Database</span></span>

<span data-ttu-id="357ef-126">(Bei Verwendung der *School.mdf* Datei aus dem Projekt heruntergeladen, die in diesem Tutorial können Sie diesen Abschnitt überspringen, da die gespeicherten Prozeduren bereits vorhanden sind.)</span><span class="sxs-lookup"><span data-stu-id="357ef-126">(If you're using the *School.mdf* file from the project available for download with this tutorial, you can skip this section because the stored procedures already exist.)</span></span>

<span data-ttu-id="357ef-127">In **Server-Explorer**, erweitern Sie *School.mdf*, mit der rechten Maustaste **gespeicherte Prozeduren**, und wählen Sie **neue gespeicherte Prozedur hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="357ef-127">In **Server Explorer**, expand *School.mdf*, right-click **Stored Procedures**, and select **Add New Stored Procedure**.</span></span>

<span data-ttu-id="357ef-128">[![image15](the-entity-framework-and-aspnet-getting-started-part-7/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="357ef-128">[![image15](the-entity-framework-and-aspnet-getting-started-part-7/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image1.png)</span></span>

<span data-ttu-id="357ef-129">Kopieren Sie die folgenden SQL-Anweisungen, und fügen Sie sie in der gespeicherten Prozedur-Fenster, und Ersetzen Sie dabei die Skelette gespeicherte Prozedur.</span><span class="sxs-lookup"><span data-stu-id="357ef-129">Copy the following SQL statements and paste them into the stored procedure window, replacing the skeleton stored procedure.</span></span>

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample1.sql)]

<span data-ttu-id="357ef-130">[![image14](the-entity-framework-and-aspnet-getting-started-part-7/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="357ef-130">[![image14](the-entity-framework-and-aspnet-getting-started-part-7/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image3.png)</span></span>

<span data-ttu-id="357ef-131">`Student` Entitäten verfügen über vier Eigenschaften: `PersonID`, `LastName`, `FirstName`, und `EnrollmentDate`.</span><span class="sxs-lookup"><span data-stu-id="357ef-131">`Student` entities have four properties: `PersonID`, `LastName`, `FirstName`, and `EnrollmentDate`.</span></span> <span data-ttu-id="357ef-132">Generiert die Datenbank automatisch den ID-Wert, und die gespeicherte Prozedur akzeptiert Parameter für die anderen drei.</span><span class="sxs-lookup"><span data-stu-id="357ef-132">The database generates the ID value automatically, and the stored procedure accepts parameters for the other three.</span></span> <span data-ttu-id="357ef-133">Die gespeicherte Prozedur gibt den Wert des Schlüssels für die neue-Zeile-Datensatz, damit Entity Framework, die in der Version der Entität mitverfolgen können, die sie im Arbeitsspeicher beibehält.</span><span class="sxs-lookup"><span data-stu-id="357ef-133">The stored procedure returns the value of the new row's record key so that the Entity Framework can keep track of that in the version of the entity it keeps in memory.</span></span>

<span data-ttu-id="357ef-134">Speichern Sie und schließen Sie das Fenster für die gespeicherte Prozedur.</span><span class="sxs-lookup"><span data-stu-id="357ef-134">Save and close the stored procedure window.</span></span>

<span data-ttu-id="357ef-135">Erstellen Sie eine `InsertInstructor` gespeicherte Prozedur auf die gleiche Weise, die mit den folgenden SQL-Anweisungen:</span><span class="sxs-lookup"><span data-stu-id="357ef-135">Create an `InsertInstructor` stored procedure in the same manner, using the following SQL statements:</span></span>

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample2.sql)]

<span data-ttu-id="357ef-136">Erstellen Sie `Update` gespeicherte Prozeduren für `Student` und `Instructor` Entitäten auch.</span><span class="sxs-lookup"><span data-stu-id="357ef-136">Create `Update` stored procedures for `Student` and `Instructor` entities also.</span></span> <span data-ttu-id="357ef-137">(Die Datenbank verfügt bereits über eine `DeletePerson` gespeicherte Prozedur das funktioniert für beide `Instructor` und `Student` Entitäten.)</span><span class="sxs-lookup"><span data-stu-id="357ef-137">(The database already has a `DeletePerson` stored procedure which will work for both `Instructor` and `Student` entities.)</span></span>

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample3.sql)]

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample4.sql)]

<span data-ttu-id="357ef-138">In diesem Tutorial ordnen Sie alle drei Funktionen: Insert, Update und Delete – für jeden Entitätstyp.</span><span class="sxs-lookup"><span data-stu-id="357ef-138">In this tutorial you'll map all three functions -- insert, update, and delete -- for each entity type.</span></span> <span data-ttu-id="357ef-139">Entity Framework, Version 4 können Sie nur eine zuordnen oder zwei dieser Funktionen zu gespeicherten Prozeduren ohne Zuordnung, die anderen, mit einer Ausnahme: Wenn Sie die Update-Funktion, aber nicht die Löschfunktion zugeordnet, die Entity Framework löst eine Ausnahme bei der Sie Es wurde versucht, eine Entität zu löschen.</span><span class="sxs-lookup"><span data-stu-id="357ef-139">The Entity Framework version 4 allows you to map just one or two of these functions to stored procedures without mapping the others, with one exception: if you map the update function but not the delete function, the Entity Framework will throw an exception when you attempt to delete an entity.</span></span> <span data-ttu-id="357ef-140">In Entity Framework, Version 3.5, Sie keine viel Flexibilität beim Zuordnen von gespeicherten Prozeduren: Wenn Sie eine Funktion zugeordnet war es erforderlich, alle drei zuordnen.</span><span class="sxs-lookup"><span data-stu-id="357ef-140">In the Entity Framework version 3.5, you did not have this much flexibility in mapping stored procedures: if you mapped one function you were required to map all three.</span></span>

<span data-ttu-id="357ef-141">Um eine gespeicherte Prozedur zu erstellen, die gelesen, anstatt Daten aktualisiert, erstellen, der alle ausgewählt `Course` Entitäten, die mit den folgenden SQL-Anweisungen:</span><span class="sxs-lookup"><span data-stu-id="357ef-141">To create a stored procedure that reads rather than updates data, create one that selects all `Course` entities, using the following SQL statements:</span></span>

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample5.sql)]

## <a name="adding-the-stored-procedures-to-the-data-model"></a><span data-ttu-id="357ef-142">Die gespeicherten Prozeduren hinzufügen in das Datenmodell</span><span class="sxs-lookup"><span data-stu-id="357ef-142">Adding the Stored Procedures to the Data Model</span></span>

<span data-ttu-id="357ef-143">Die gespeicherten Prozeduren werden nun in der Datenbank definiert, aber sie müssen hinzugefügt werden, um das Datenmodell auf Entity Framework zur Verfügung stellen.</span><span class="sxs-lookup"><span data-stu-id="357ef-143">The stored procedures are now defined in the database, but they must be added to the data model to make them available to the Entity Framework.</span></span> <span data-ttu-id="357ef-144">Open *SchoolModel.edmx*mit der rechten Maustaste auf die Entwurfsoberfläche, und wählen Sie **Modell aus der Datenbank aktualisieren**.</span><span class="sxs-lookup"><span data-stu-id="357ef-144">Open *SchoolModel.edmx*, right-click the design surface, and select **Update Model from Database**.</span></span> <span data-ttu-id="357ef-145">In der **hinzufügen** Registerkarte die **Datenbankobjekte auswählen** Dialogfeld erweitern Sie **gespeicherte Prozeduren**, wählen Sie die neu erstellten gespeicherten Prozeduren und die `DeletePerson` gespeicherte Prozedur, und klicken Sie dann auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="357ef-145">In the **Add** tab of the **Choose Your Database Objects** dialog box, expand **Stored Procedures**, select the newly created stored procedures and the `DeletePerson` stored procedure, and then click **Finish**.</span></span>

<span data-ttu-id="357ef-146">[![image20](the-entity-framework-and-aspnet-getting-started-part-7/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="357ef-146">[![image20](the-entity-framework-and-aspnet-getting-started-part-7/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image5.png)</span></span>

## <a name="mapping-the-stored-procedures"></a><span data-ttu-id="357ef-147">Die gespeicherten Prozeduren zuordnen</span><span class="sxs-lookup"><span data-stu-id="357ef-147">Mapping the Stored Procedures</span></span>

<span data-ttu-id="357ef-148">In der Data Model-Designer, mit der Maustaste der `Student` Entität, und wählen **Zuordnung der gespeicherten Prozedur**.</span><span class="sxs-lookup"><span data-stu-id="357ef-148">In the data model designer, right-click the `Student` entity and select **Stored Procedure Mapping**.</span></span>

<span data-ttu-id="357ef-149">[![image21](the-entity-framework-and-aspnet-getting-started-part-7/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="357ef-149">[![image21](the-entity-framework-and-aspnet-getting-started-part-7/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image7.png)</span></span>

<span data-ttu-id="357ef-150">Die **Mappingdetails** Fenster angezeigt wird, in dem Sie die gespeicherte Prozeduren angeben können, die das Entity Framework verwenden soll, für das Einfügen, aktualisieren und Löschen von Entitäten, die dieses Typs.</span><span class="sxs-lookup"><span data-stu-id="357ef-150">The **Mapping Details** window appears, in which you can specify stored procedures that the Entity Framework should use for inserting, updating, and deleting entities of this type.</span></span>

<span data-ttu-id="357ef-151">[![image22](the-entity-framework-and-aspnet-getting-started-part-7/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="357ef-151">[![image22](the-entity-framework-and-aspnet-getting-started-part-7/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image9.png)</span></span>

<span data-ttu-id="357ef-152">Legen Sie die **einfügen** -Funktion **InsertStudent**.</span><span class="sxs-lookup"><span data-stu-id="357ef-152">Set the **Insert** function to **InsertStudent**.</span></span> <span data-ttu-id="357ef-153">Das Fenster zeigt eine Liste der Parameter der gespeicherten Prozedur, von die jede eine Entitätseigenschaft zugeordnet werden muss.</span><span class="sxs-lookup"><span data-stu-id="357ef-153">The window shows a list of stored procedure parameters, each of which must be mapped to an entity property.</span></span> <span data-ttu-id="357ef-154">Zwei davon werden automatisch zugeordnet, da die Namen identisch sind.</span><span class="sxs-lookup"><span data-stu-id="357ef-154">Two of these are mapped automatically because the names are the same.</span></span> <span data-ttu-id="357ef-155">Es gibt keine Entitätseigenschaft, die mit dem Namen `FirstName`, daher müssen Sie manuell auswählen `FirstMidName` aus einer Dropdown-Liste, die verfügbaren Entitätseigenschaften anzeigt.</span><span class="sxs-lookup"><span data-stu-id="357ef-155">There's no entity property named `FirstName`, so you must manually select `FirstMidName` from a drop-down list that shows available entity properties.</span></span> <span data-ttu-id="357ef-156">(Dies ist, da Sie geändert, dass der Name des der `FirstName` Eigenschaft `FirstMidName` im ersten Tutorial.)</span><span class="sxs-lookup"><span data-stu-id="357ef-156">(This is because you changed the name of the `FirstName` property to `FirstMidName` in the first tutorial.)</span></span>

<span data-ttu-id="357ef-157">[![image23](the-entity-framework-and-aspnet-getting-started-part-7/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="357ef-157">[![image23](the-entity-framework-and-aspnet-getting-started-part-7/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image11.png)</span></span>

<span data-ttu-id="357ef-158">In der gleichen **Mappingdetails** Fenster, Zuordnung der `Update` -Funktion der `UpdateStudent` gespeicherte Prozedur (Geben Sie unbedingt `FirstMidName` als Parameterwert für `FirstName`, ebenso wie für die `Insert` gespeicherte Prozedur) und die `Delete` Funktion, um die `DeletePerson` gespeicherte Prozedur.</span><span class="sxs-lookup"><span data-stu-id="357ef-158">In the same **Mapping Details** window, map the `Update` function to the `UpdateStudent` stored procedure (make sure you specify `FirstMidName` as the parameter value for `FirstName`, as you did for the `Insert` stored procedure) and the `Delete` function to the `DeletePerson` stored procedure.</span></span>

<span data-ttu-id="357ef-159">[![Image01 abgerufen wird](the-entity-framework-and-aspnet-getting-started-part-7/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="357ef-159">[![image01](the-entity-framework-and-aspnet-getting-started-part-7/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image13.png)</span></span>

<span data-ttu-id="357ef-160">Führen Sie dasselbe Verfahren zum Zuordnen von den INSERT-, Update- und Delete gespeicherten Prozeduren für Dozenten zu der `Instructor` Entität.</span><span class="sxs-lookup"><span data-stu-id="357ef-160">Follow the same procedure to map the insert, update, and delete stored procedures for instructors to the `Instructor` entity.</span></span>

<span data-ttu-id="357ef-161">[![image02](the-entity-framework-and-aspnet-getting-started-part-7/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="357ef-161">[![image02](the-entity-framework-and-aspnet-getting-started-part-7/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image15.png)</span></span>

<span data-ttu-id="357ef-162">Für gespeicherte Prozeduren, die statt der Update-Daten lesen, verwenden Sie die **Modellbrowser** Fenster aus, um die gespeicherte Prozedur für die Entität zugeordnet. Geben Sie ihn gibt.</span><span class="sxs-lookup"><span data-stu-id="357ef-162">For stored procedures that read rather than update data, you use the **Model Browser** window to map the stored procedure to the entity type it returns.</span></span> <span data-ttu-id="357ef-163">In der Data Model-Designer, mit der Maustaste Entwurfsoberfläche, und wählen **Modellbrowser**.</span><span class="sxs-lookup"><span data-stu-id="357ef-163">In the data model designer, right-click the design surface and select **Model Browser**.</span></span> <span data-ttu-id="357ef-164">Öffnen Sie die **SchoolModel.Store** Knoten, und öffnen Sie dann die **gespeicherte Prozeduren** Knoten.</span><span class="sxs-lookup"><span data-stu-id="357ef-164">Open the **SchoolModel.Store** node and then open the **Stored Procedures** node.</span></span> <span data-ttu-id="357ef-165">Klicken Sie dann mit der rechten Maustaste die `GetCourses` gespeicherte Prozedur, und wählen Sie **Funktionsimport hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="357ef-165">Then right-click the `GetCourses` stored procedure and select **Add Function Import**.</span></span>

<span data-ttu-id="357ef-166">[![image24](the-entity-framework-and-aspnet-getting-started-part-7/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="357ef-166">[![image24](the-entity-framework-and-aspnet-getting-started-part-7/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image17.png)</span></span>

<span data-ttu-id="357ef-167">In der **Funktionsimport hinzufügen** Dialogfeld **gibt eine Auflistung von** wählen **Entitäten**, und wählen Sie dann `Course` als den Entitätstyp zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="357ef-167">In the **Add Function Import** dialog box, under **Returns a Collection Of** select **Entities**, and then select `Course` as the entity type returned.</span></span> <span data-ttu-id="357ef-168">Wenn Sie fertig sind, klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="357ef-168">When you're done, click **OK**.</span></span> <span data-ttu-id="357ef-169">Speichern und schließen Sie die *EDMX* Datei.</span><span class="sxs-lookup"><span data-stu-id="357ef-169">Save and close the *.edmx* file.</span></span>

<span data-ttu-id="357ef-170">[![image25](the-entity-framework-and-aspnet-getting-started-part-7/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="357ef-170">[![image25](the-entity-framework-and-aspnet-getting-started-part-7/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image19.png)</span></span>

## <a name="using-insert-update-and-delete-stored-procedures"></a><span data-ttu-id="357ef-171">Verwenden von Insert, aktualisieren und Löschen von gespeicherten Prozeduren</span><span class="sxs-lookup"><span data-stu-id="357ef-171">Using Insert, Update, and Delete Stored Procedures</span></span>

<span data-ttu-id="357ef-172">Gespeicherte Prozeduren zum Einfügen, aktualisieren und Löschen von Daten wird vom Entity Framework automatisch nach dem Datenmodell hinzugefügt wurden und sie die entsprechenden Entitäten zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="357ef-172">Stored procedures to insert, update, and delete data are used by the Entity Framework automatically after you've added them to the data model and mapped them to the appropriate entities.</span></span> <span data-ttu-id="357ef-173">Sie können jetzt ausführen der *StudentsAdd.aspx* Seite und jedes Mal, wenn Sie einen neuen Studenten erstellt haben, wird das Entity Framework verwenden die `InsertStudent` gespeicherte Prozedur, um die neue Zeile hinzuzufügen der `Student` Tabelle.</span><span class="sxs-lookup"><span data-stu-id="357ef-173">You can now run the *StudentsAdd.aspx* page, and every time you create a new student, the Entity Framework will use the `InsertStudent` stored procedure to add the new row to the `Student` table.</span></span>

<span data-ttu-id="357ef-174">[![image03](the-entity-framework-and-aspnet-getting-started-part-7/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="357ef-174">[![image03](the-entity-framework-and-aspnet-getting-started-part-7/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image21.png)</span></span>

<span data-ttu-id="357ef-175">Führen Sie die *Students.aspx* Seite und den neuen Studenten in der Liste angezeigt.</span><span class="sxs-lookup"><span data-stu-id="357ef-175">Run the *Students.aspx* page and the new student appears in the list.</span></span>

<span data-ttu-id="357ef-176">[![image04](the-entity-framework-and-aspnet-getting-started-part-7/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="357ef-176">[![image04](the-entity-framework-and-aspnet-getting-started-part-7/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image23.png)</span></span>

<span data-ttu-id="357ef-177">Ändern Sie den Namen, um sicherzustellen, dass die Update-Funktion funktioniert, und löschen Sie dann die "Student", um sicherzustellen, dass die Delete-Funktion arbeitet.</span><span class="sxs-lookup"><span data-stu-id="357ef-177">Change the name to verify that the update function works, and then delete the student to verify that the delete function works.</span></span>

<span data-ttu-id="357ef-178">[![image05](the-entity-framework-and-aspnet-getting-started-part-7/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="357ef-178">[![image05](the-entity-framework-and-aspnet-getting-started-part-7/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image25.png)</span></span>

## <a name="using-select-stored-procedures"></a><span data-ttu-id="357ef-179">Verwenden von auf gespeicherten Prozeduren</span><span class="sxs-lookup"><span data-stu-id="357ef-179">Using Select Stored Procedures</span></span>

<span data-ttu-id="357ef-180">Entity Framework ist nicht automatisch gespeicherten Prozeduren ausführen, wie z. B. `GetCourses`, und Sie nicht verwenden, mit der `EntityDataSource` Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="357ef-180">The Entity Framework does not automatically run stored procedures such as `GetCourses`, and you cannot use them with the `EntityDataSource` control.</span></span> <span data-ttu-id="357ef-181">Um diese zu verwenden, rufen Sie sie aus Code.</span><span class="sxs-lookup"><span data-stu-id="357ef-181">To use them, you call them from code.</span></span>

<span data-ttu-id="357ef-182">Öffnen der *InstructorsCourses.aspx.cs* Datei.</span><span class="sxs-lookup"><span data-stu-id="357ef-182">Open the *InstructorsCourses.aspx.cs* file.</span></span> <span data-ttu-id="357ef-183">Die `PopulateDropDownLists` Methode verwendet eine LINQ to Entities-Abfrage, um alle Course-Entitäten abgerufen werden, damit sie die Liste durchlaufen und bestimmen, welche ein Dozent zugewiesen ist und welche nicht zugewiesen werden kann:</span><span class="sxs-lookup"><span data-stu-id="357ef-183">The `PopulateDropDownLists` method uses a LINQ-to-Entities query to retrieve all course entities so that it can loop through the list and determine which ones an instructor is assigned to and which ones are unassigned:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample6.cs)]

<span data-ttu-id="357ef-184">Ersetzen Sie dies durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="357ef-184">Replace this with the following code:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample7.cs)]

<span data-ttu-id="357ef-185">Die Seite nun verwendet der `GetCourses` gespeicherte Prozedur zum Abrufen der Liste aller Kurse.</span><span class="sxs-lookup"><span data-stu-id="357ef-185">The page now uses the `GetCourses` stored procedure to retrieve the list of all courses.</span></span> <span data-ttu-id="357ef-186">Führen Sie die Seite, um sicherzustellen, dass es funktioniert wie vorher.</span><span class="sxs-lookup"><span data-stu-id="357ef-186">Run the page to verify that it works as it did before.</span></span>

<span data-ttu-id="357ef-187">(Eigenschaften von Entitäten abgerufen, indem eine gespeicherte Prozedur können mit den Daten, die im Zusammenhang mit diesen Entitäten, die je nach nicht automatisch aufgefüllt `ObjectContext` Standardeinstellungen.</span><span class="sxs-lookup"><span data-stu-id="357ef-187">(Navigation properties of entities retrieved by a stored procedure might not be automatically populated with the data related to those entities, depending on `ObjectContext` default settings.</span></span> <span data-ttu-id="357ef-188">Weitere Informationen finden Sie unter [laden verbundener Objekte](https://msdn.microsoft.com/library/bb896272.aspx) in der MSDN Library.)</span><span class="sxs-lookup"><span data-stu-id="357ef-188">For more information, see [Loading Related Objects](https://msdn.microsoft.com/library/bb896272.aspx) in the MSDN Library.)</span></span>

<span data-ttu-id="357ef-189">Im nächsten Tutorial erfahren Sie, wie Sie Dynamic Data-Funktionalität verwenden, um die Anwendung und Testen von Formatierung und Validierung Regeln zu vereinfachen.</span><span class="sxs-lookup"><span data-stu-id="357ef-189">In the next tutorial, you'll learn how to use Dynamic Data functionality to make it easier to program and test data formatting and validation rules.</span></span> <span data-ttu-id="357ef-190">Anstatt auf jeder Webseite-Regeln, wie z. B. Daten Formatzeichenfolgen und davon, ob ein Feld erforderlich ist, können Sie diese Regeln in Datenmodellmetadaten angeben, und sie werden automatisch auf jeder Seite angewendet.</span><span class="sxs-lookup"><span data-stu-id="357ef-190">Instead of specifying on each web page rules such as data format strings and whether or not a field is required, you can specify such rules in data model metadata and they're automatically applied on every page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="357ef-191">[Zurück](the-entity-framework-and-aspnet-getting-started-part-6.md)
> [Weiter](the-entity-framework-and-aspnet-getting-started-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="357ef-191">[Previous](the-entity-framework-and-aspnet-getting-started-part-6.md)
[Next](the-entity-framework-and-aspnet-getting-started-part-8.md)</span></span>