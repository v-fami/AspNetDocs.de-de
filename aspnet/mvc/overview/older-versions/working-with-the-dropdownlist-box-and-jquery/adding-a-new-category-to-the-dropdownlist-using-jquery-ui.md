---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
title: Hinzufügen einer neuen Kategorie zu DropDownList mithilfe der jQuery-Benutzeroberfläche | Microsoft-Dokumentation
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 44aa1ac4-6ea2-48a2-972d-52710c48eae5
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: 9fb95d22be473a4318520a391fa424106246a054
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062187"
---
<a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a><span data-ttu-id="cefe3-102">Hinzufügen einer neuen Kategorie zu DropDownList mithilfe der jQuery-Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="cefe3-102">Adding a New Category to the DropDownList using jQuery UI</span></span>
====================
<span data-ttu-id="cefe3-103">durch [Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="cefe3-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

<span data-ttu-id="cefe3-104">Der HTML-Code `Select` Tag eignet sich ideal für eine geordnete Liste der festen Kategoriedaten, aber häufig müssen Sie eine neue Kategorie hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="cefe3-104">The HTML `Select` tag is ideal for presenting a list of fixed category data, but often times you need to add a new category.</span></span> <span data-ttu-id="cefe3-105">Nehmen wir an, dass das Genre "Opera", die Kategorien in der Datenbank hinzugefügt werden soll?</span><span class="sxs-lookup"><span data-stu-id="cefe3-105">Suppose we want to add the genre "Opera" to the categories in our database?</span></span> <span data-ttu-id="cefe3-106">In diesem Abschnitt verwenden wir die jQuery-Benutzeroberfläche auf ein Dialogfeld hinzufügen, mit denen wir eine neue Kategorie hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="cefe3-106">In this section, we will use jQuery UI to add a dialog box we can use to add a new category.</span></span> <span data-ttu-id="cefe3-107">Die folgende Abbildung zeigt, wie die Benutzeroberfläche im Browser darstellen wird.</span><span class="sxs-lookup"><span data-stu-id="cefe3-107">The image below shows how the UI will present in the browser.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

<span data-ttu-id="cefe3-108">Wenn ein Benutzer wählt die **Hinzufügen eines neuen "Genre"** Link, ein Popup-Dialogfeld fordert den Benutzer für einen neuen Namen für "Genre" (und optional eine Beschreibung).</span><span class="sxs-lookup"><span data-stu-id="cefe3-108">When a user selects the **Add New Genre** link, a pop-up dialog box prompts the user for a new genre name (and optionally a description).</span></span> <span data-ttu-id="cefe3-109">Das Bild unten zeigen die **hinzufügen "Genre"** Popup-Dialogfeld.</span><span class="sxs-lookup"><span data-stu-id="cefe3-109">The image below show the **Add Genre** pop-up dialog.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

<span data-ttu-id="cefe3-110">Wenn ein neuer Name für "Genre" eingegeben wird und die **speichern** Schaltfläche gedrückt wird, geschieht Folgendes:</span><span class="sxs-lookup"><span data-stu-id="cefe3-110">When a new genre name is entered and the **Save** button is pushed, the following happens:</span></span>

1. <span data-ttu-id="cefe3-111">Ein AJAX-Aufruf sendet die Daten in der Create-Methode des Controllers "Genre", die neue "Genre" in der Datenbank gespeichert und die neue "Genre"-Informationen (Name des Genres und ID) im JSON-Format zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="cefe3-111">An AJAX call posts the data to the Create method of the Genre Controller, which saves the new genre to the database and returns the new genre information (genre name and ID) as JSON.</span></span>
2. <span data-ttu-id="cefe3-112">JavaScript fügt die neuen Daten für "Genre" in der select-Liste hinzu.</span><span class="sxs-lookup"><span data-stu-id="cefe3-112">JavaScript adds the new genre data to the select list.</span></span>
3. <span data-ttu-id="cefe3-113">JavaScript macht dem neuen Genre des ausgewählten Elements an.</span><span class="sxs-lookup"><span data-stu-id="cefe3-113">JavaScript makes the new genre the selected item.</span></span>

   <span data-ttu-id="cefe3-114">In der folgenden Abbildung **Opera** wurde der Datenbank hinzugefügt und ausgewählt, die der **"Genre"** Dropdown-Liste.</span><span class="sxs-lookup"><span data-stu-id="cefe3-114">In the image below, **Opera** was added to the database and selected in the **Genre** drop down list.</span></span> 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

<span data-ttu-id="cefe3-115">Öffnen der *Views\StoreManager\Create.cshtml* -Datei und Ersetzen Sie das Markup für "Genre" durch den folgenden den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="cefe3-115">Open the *Views\StoreManager\Create.cshtml* file and replace the genre markup with the following the following code:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

<span data-ttu-id="cefe3-116">Die `_ChooseGenre` partielle Ansicht enthält die gesamte Logik, um die JavaScript- und jQuery verwendet, um das Hinzufügen neuer "Genre" Feature implementieren einbinden.</span><span class="sxs-lookup"><span data-stu-id="cefe3-116">The `_ChooseGenre` partial view will contain all the logic to hook up the JavaScript and jQuery used to implement the add new genre feature.</span></span> <span data-ttu-id="cefe3-117">Nachdem wir den Code haben, wird es sehr einfach, mit der Interpret-Benutzeroberfläche identisch sein.</span><span class="sxs-lookup"><span data-stu-id="cefe3-117">Once we have completed the code it will be simple to do the same with the artist UI.</span></span>

<span data-ttu-id="cefe3-118">Im Projektmappen-Explorer mit der rechten Maustaste die *Views\StoreManager* Ordner, und wählen **hinzufügen**, klicken Sie dann **Ansicht**.</span><span class="sxs-lookup"><span data-stu-id="cefe3-118">In Solution Explorer, right click the *Views\StoreManager* folder and select **Add**, then **View**.</span></span> <span data-ttu-id="cefe3-119">In der **Sichtname** eingeben, geben Sie `_ChooseGenre` wählen Sie dann **hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="cefe3-119">In the **View name** input, enter `_ChooseGenre` then select **Add**.</span></span> <span data-ttu-id="cefe3-120">Ersetzen Sie das Markup in der *Views\StoreManager\\_ChooseGenre.cshtml* Datei durch Folgendes:</span><span class="sxs-lookup"><span data-stu-id="cefe3-120">Replace the markup in the *Views\StoreManager\\_ChooseGenre.cshtml* file with the following:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

<span data-ttu-id="cefe3-121">Die erste Zeile gibt an, dass wir übergeben eine `Album` als unser Modell genauso model-Anweisung finden Sie in der Ansicht "erstellen".</span><span class="sxs-lookup"><span data-stu-id="cefe3-121">The first line declares that we are passing in an `Album` as our model, exactly the same model statement found in the Create view.</span></span> <span data-ttu-id="cefe3-122">Die nächsten Zeilen werden die **Bezeichnung** Helper-Markup.</span><span class="sxs-lookup"><span data-stu-id="cefe3-122">The next few lines are the **Label** helper markup.</span></span> <span data-ttu-id="cefe3-123">Die nächste Zeile ist die **DropDownList** Helper-aufrufen, wie in der ursprünglichen Create-Ansicht.</span><span class="sxs-lookup"><span data-stu-id="cefe3-123">The next line is the **DropDownList** helper call, exactly the same as in the original Create view.</span></span> <span data-ttu-id="cefe3-124">Die nächste Zeile Fügt einen Link mit dem Namen `Add New Genre`, und es wie eine Schaltfläche zu formatieren.</span><span class="sxs-lookup"><span data-stu-id="cefe3-124">The next line adds a link with the name `Add New Genre`, and styles it like a button.</span></span> <span data-ttu-id="cefe3-125">Die Zeile mit `ValidationMessageFor` direkt aus der Ansicht "erstellen" kopiert.</span><span class="sxs-lookup"><span data-stu-id="cefe3-125">The line containing `ValidationMessageFor` is copied directly from the Create view.</span></span> <span data-ttu-id="cefe3-126">Die folgenden Zeilen:</span><span class="sxs-lookup"><span data-stu-id="cefe3-126">The following lines:</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

<span data-ttu-id="cefe3-127">erstellt ein ausgeblendetes DIV-Element, mit der ID `genreDialog`.</span><span class="sxs-lookup"><span data-stu-id="cefe3-127">creates a hidden div, with the ID of `genreDialog`.</span></span> <span data-ttu-id="cefe3-128">Verwenden wir jQuery um zu verknüpfen, unsere **hinzufügen "Genre"** Dialogfeld mit der ID `genreDialog` in dieses DIV-Element</span><span class="sxs-lookup"><span data-stu-id="cefe3-128">We will use jQuery to hook up our **Add Genre** dialog box with the ID `genreDialog` in this div.</span></span> <span data-ttu-id="cefe3-129">Die letzten beiden Skripttags enthalten Links zu den JavaScript-Dateien, die wir verwenden werden, um das Hinzufügen neuer "Genre"-Feature zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="cefe3-129">The last two script tags contain links to the JavaScript files we will use to implement the add new genre feature.</span></span> <span data-ttu-id="cefe3-130">Die */Scripts/chooseGenre.js* Datei dient für Sie in das Projekt, ihn später in diesem Tutorial untersuchen wir wird.</span><span class="sxs-lookup"><span data-stu-id="cefe3-130">The */Scripts/chooseGenre.js* file is provided for you in the project, we will examine it later in the tutorial.</span></span>

<span data-ttu-id="cefe3-131">Führen Sie die Anwendung, und klicken Sie auf die **Hinzufügen eines neuen "Genre"** Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="cefe3-131">Run the application and click on the **Add New Genre** button.</span></span> <span data-ttu-id="cefe3-132">In der **hinzufügen "Genre"** Dialogfeld Geben Sie **Opera** in die **Namen** Eingabefeld.</span><span class="sxs-lookup"><span data-stu-id="cefe3-132">In the **Add Genre** dialog box, enter **Opera** in the **Name** input box.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

<span data-ttu-id="cefe3-133">Klicken Sie auf die Schaltfläche **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="cefe3-133">Click the **Save** button.</span></span> <span data-ttu-id="cefe3-134">Ein AJAX-Aufruf erstellt die Kategorie "Opera", und klicken Sie dann füllt die Dropdownliste mit Opera, und legt Opera als das ausgewählte Genre.</span><span class="sxs-lookup"><span data-stu-id="cefe3-134">An AJAX call creates the Opera category and then populates the dropdown list with Opera, and sets Opera as the selected genre.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

<span data-ttu-id="cefe3-135">Geben Sie eine Interpret, Titel und Preis, und wählen Sie dann die **erstellen** Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="cefe3-135">Enter an artist, title and price, then select the **Create** button.</span></span> <span data-ttu-id="cefe3-136">Wenn Sie einen Preis ein, der kleiner als $8,99 eingeben, wird das neue Album am oberen Rand der Ansicht "Index" angezeigt.</span><span class="sxs-lookup"><span data-stu-id="cefe3-136">If you enter a price less than $8.99, the new album will appear at the top of the Index view.</span></span> <span data-ttu-id="cefe3-137">Stellen Sie sicher, dass der neue Album-Eintrag in der Datenbank gespeichert wurde.</span><span class="sxs-lookup"><span data-stu-id="cefe3-137">Verify the new album entry was saved in the database.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

<span data-ttu-id="cefe3-138">Versuchen Sie, eine neue "Genre" mit nur einem Buchstaben zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="cefe3-138">Try creating a new genre with only one letter.</span></span> <span data-ttu-id="cefe3-139">Im folgenden code in die *Models\Genre.cs* Datei legt die minimale und maximale Länge des Namens "Genre" fest.</span><span class="sxs-lookup"><span data-stu-id="cefe3-139">The following code in the *Models\Genre.cs* file sets the minimum and maximum length of the genre name.</span></span>

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

<span data-ttu-id="cefe3-140">Clientseitige Validierung meldet, dass Sie eine Zeichenfolge zwischen 2 und 20 Zeichen eingeben müssen.</span><span class="sxs-lookup"><span data-stu-id="cefe3-140">Client side validation reports you must enter a string between 2 and 20 characters.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a><span data-ttu-id="cefe3-141">Untersuchen der wie ein neues "Genre" wird die Datenbank und der Select-Liste hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="cefe3-141">Examining How a New Genre is Added to the Database and the Select List.</span></span>

<span data-ttu-id="cefe3-142">Öffnen der *Scripts\chooseGenre.js* Datei, und überprüfen Sie den Code.</span><span class="sxs-lookup"><span data-stu-id="cefe3-142">Open the *Scripts\chooseGenre.js* file and examine the code.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

<span data-ttu-id="cefe3-143">Die zweite Zeile verwendet die ID `genreDialog` So erstellen ein Dialogfeld für das Div-Tag in die *Views\StoreManager\\_ChooseGenre.cshtml* Datei.</span><span class="sxs-lookup"><span data-stu-id="cefe3-143">The second line uses the ID `genreDialog` to create a dialog box on the div tag in the *Views\StoreManager\\_ChooseGenre.cshtml* file.</span></span> <span data-ttu-id="cefe3-144">Die meisten benannte Parameter sind Erläuterung erforderlich.</span><span class="sxs-lookup"><span data-stu-id="cefe3-144">Most of the named parameters are self explanatory.</span></span> <span data-ttu-id="cefe3-145">Die `autoOpen` Parameter auf "False" festgelegt ist Auswählen der **erstellen "Genre"** Schaltfläche wird das Dialogfeld geöffnet, explizit (hierzu finden Sie auf letztere).</span><span class="sxs-lookup"><span data-stu-id="cefe3-145">The `autoOpen` parameter is set to false, selecting the **Create Genre** button will open the dialogue explicitly (this is described latter on).</span></span> <span data-ttu-id="cefe3-146">Der Dialog besitzt zwei Schaltflächen, **speichern** und **Abbrechen**.</span><span class="sxs-lookup"><span data-stu-id="cefe3-146">The dialog has two buttons, **Save** and **Cancel**.</span></span> <span data-ttu-id="cefe3-147">Die **Abbrechen** Schaltfläche wird das Dialogfeld geschlossen.</span><span class="sxs-lookup"><span data-stu-id="cefe3-147">The **Cancel** button closes the dialog.</span></span> <span data-ttu-id="cefe3-148">Der folgende code zeigt die **speichern** Schaltfläche Funktion.</span><span class="sxs-lookup"><span data-stu-id="cefe3-148">The following code shows the **Save** button function.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

<span data-ttu-id="cefe3-149">Die `var createGenreForm` ausgewählt ist, aus der `createGenreForm` -ID.</span><span class="sxs-lookup"><span data-stu-id="cefe3-149">The `var createGenreForm` is selected from the `createGenreForm` ID.</span></span> <span data-ttu-id="cefe3-150">Die `createGenreForm` -ID wurde festgelegt, in den folgenden Code finden Sie in der *Views\Genre\\_CreateGenre.cshtml* Datei.</span><span class="sxs-lookup"><span data-stu-id="cefe3-150">The `createGenreForm` ID was set in the following code found in the *Views\Genre\\_CreateGenre.cshtml* file.</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

<span data-ttu-id="cefe3-151">Die [Html.BeginForm](https://msdn.microsoft.com/library/dd492714.aspx) Helper-Überladung, die in verwendet die *Views\Genre\\_CreateGenre.cshtml* Datei generiert HTML-Code mit einer Action-Attribut, das mit der URL zum Absenden des Formulars.</span><span class="sxs-lookup"><span data-stu-id="cefe3-151">The [Html.BeginForm](https://msdn.microsoft.com/library/dd492714.aspx) helper overload used in the *Views\Genre\\_CreateGenre.cshtml* file generates HTML with an action attribute containing the URL to submit the form.</span></span> <span data-ttu-id="cefe3-152">Sie können dies überprüfen, die Seite "Album erstellen" in einem Browser anzeigen und Auswählen der anzeigen-Quelle im Browser.</span><span class="sxs-lookup"><span data-stu-id="cefe3-152">You can see this by displaying the create album page in a browser and selecting show source in the browser.</span></span> <span data-ttu-id="cefe3-153">Das folgende Markup zeigt die generierten HTML-Code, der das Form-Tag enthält.</span><span class="sxs-lookup"><span data-stu-id="cefe3-153">The following markup shows the generated HTML containing the form tag.</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

<span data-ttu-id="cefe3-154">Die jQuery `$.post` Zeile wird einen AJAX-Aufruf an das Action-Attribut (`/StoreManager/Create`) auf und übergibt die Daten aus der **erstellen "Genre"** Dialogfeld.</span><span class="sxs-lookup"><span data-stu-id="cefe3-154">The jQuery `$.post` line makes an AJAX call to the action attribute (`/StoreManager/Create`) and passes in the data from the **Create Genre** dialog box.</span></span> <span data-ttu-id="cefe3-155">Die Daten bestehen aus den Namen für das neue Genre und eine optionale Beschreibung.</span><span class="sxs-lookup"><span data-stu-id="cefe3-155">The data consists of the name for the new genre and an optional description.</span></span> <span data-ttu-id="cefe3-156">Wenn der AJAX-Aufruf erfolgreich ist, den neuen Namen für "Genre" und den Wert der Option Markup hinzugefügt werden, und die neue "Genre" in den ausgewählten Wert festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="cefe3-156">If the AJAX call is successful, the new genre name and value are added to the Select markup, and the new genre is set to the selected value.</span></span> <span data-ttu-id="cefe3-157">Es sich dynamisch generiertes Markup handelt, nicht die neue Option für die Option durch Anzeigen der Quelle im Browser angezeigt.</span><span class="sxs-lookup"><span data-stu-id="cefe3-157">Because this is dynamically generated markup, you can't see the new select option by viewing the source in the browser.</span></span> <span data-ttu-id="cefe3-158">Sie sehen den neuen HTML-Code mit den Internet Explorer 9 F12-Entwicklertools.</span><span class="sxs-lookup"><span data-stu-id="cefe3-158">You can see the new HTML with the IE 9 F12 developer tools.</span></span> <span data-ttu-id="cefe3-159">Um die neue Option wählen, in Internet Explorer 9 anzuzeigen, drücken Sie die F12-Taste, um die F12-Entwicklertools zu starten.</span><span class="sxs-lookup"><span data-stu-id="cefe3-159">To view the new select option, in Internet Explorer 9, hit the F12 key to start the F12 developer tools.</span></span> <span data-ttu-id="cefe3-160">Navigieren Sie zu der Seite "erstellen", und fügen Sie eine neue "Genre" hinzu, damit die neue "Genre" in der Auswahlliste "Genre" ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="cefe3-160">Navigate to the Create page and add a new genre so the new genre is selected in the genre select list.</span></span> <span data-ttu-id="cefe3-161">In den Entwicklertools (F12):</span><span class="sxs-lookup"><span data-stu-id="cefe3-161">In the F12 developer tools:</span></span>

1. <span data-ttu-id="cefe3-162">Wählen Sie die Registerkarte "HTML".</span><span class="sxs-lookup"><span data-stu-id="cefe3-162">Select the HTML tab.</span></span>
2. <span data-ttu-id="cefe3-163">Drücken Sie das Aktualisierungssymbol klicken.</span><span class="sxs-lookup"><span data-stu-id="cefe3-163">Hit the refresh icon.</span></span>  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. <span data-ttu-id="cefe3-164">Geben Sie in das Suchfeld GenreID aus.</span><span class="sxs-lookup"><span data-stu-id="cefe3-164">In the search box, enter GenreID.</span></span>
4. <span data-ttu-id="cefe3-165">Verwenden den Symbol "Weiter",</span><span class="sxs-lookup"><span data-stu-id="cefe3-165">Using the next icon,</span></span>   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
   <span data-ttu-id="cefe3-166">Navigieren Sie zu der folgenden select-Kennung:</span><span class="sxs-lookup"><span data-stu-id="cefe3-166">navigate to the following select tag:</span></span>

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. <span data-ttu-id="cefe3-167">Erweitern Sie den letzten Optionswert.</span><span class="sxs-lookup"><span data-stu-id="cefe3-167">Expand the last option value.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

<span data-ttu-id="cefe3-168">Im folgenden code in der *Scripts\chooseGenre.js* Datei zeigt, wie der **Hinzufügen eines neuen "Genre"** Schaltfläche ruft verbunden, um das Click-Ereignis, und wie die **Hinzufügen eines neuen "Genre"** Dialogfeld können Sie erstellt.</span><span class="sxs-lookup"><span data-stu-id="cefe3-168">The following code in the *Scripts\chooseGenre.js* file shows the how the **Add New Genre** button gets connected to the click event, and how the **Add New Genre** dialog box is created.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

<span data-ttu-id="cefe3-169">Die erste Zeile erstellt eine auf-Funktion, die angefügt werden, um die **Hinzufügen eines neuen "Genre"** Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="cefe3-169">The first line creates a click function attached to the **Add New Genre** button.</span></span> <span data-ttu-id="cefe3-170">Das folgende Markup aus der Views\StoreManager\\_ChooseGenre.cshtml-Datei zeigt wie die **Hinzufügen eines neuen "Genre"** Schaltfläche erstellt wird:</span><span class="sxs-lookup"><span data-stu-id="cefe3-170">The following markup from the Views\StoreManager\\_ChooseGenre.cshtml file shows how the **Add New Genre** button is created:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

<span data-ttu-id="cefe3-171">Die Load-Methode erstellt und öffnet das Dialogfeld "hinzufügen" Genre "" und ruft die jQuery `parse` Methode, sodass der Client von Überprüfungen auf Daten in das Dialogfeld eingegeben haben.</span><span class="sxs-lookup"><span data-stu-id="cefe3-171">The load method creates and opens the Add Genre dialog and calls the jQuery `parse` method so client validation occurs on data entered in the dialog.</span></span>

<span data-ttu-id="cefe3-172">In diesem Abschnitt haben Sie gelernt, wie ein Dialogfeld erstellen, die verwendet werden kann, um die neue Kategoriedaten in einer select-Liste hinzufügen können.</span><span class="sxs-lookup"><span data-stu-id="cefe3-172">In this section you have learned how to create a dialog that can be used to add new category data to a select list.</span></span> <span data-ttu-id="cefe3-173">Sie können das gleiche Verfahren zum Erstellen der Benutzeroberfläche zum Hinzufügen eines neuen Interpreten der Auswahlliste der Künstler diese geändert hat folgen.</span><span class="sxs-lookup"><span data-stu-id="cefe3-173">You can follow the same procedure to create UI to add a new artist to the artist select list.</span></span> <span data-ttu-id="cefe3-174">In diesem Tutorial erhält einen Überblick über das Arbeiten mit der ASP.NET MVC-HTML-Hilfsobjekt **DropDownList**.</span><span class="sxs-lookup"><span data-stu-id="cefe3-174">This tutorial has given an overview of working with the ASP.NET MVC HTML helper **DropDownList**.</span></span> <span data-ttu-id="cefe3-175">Weitere Informationen zum Arbeiten mit der **DropDownList**, finden Sie unter folgenden Referenzabschnitt hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="cefe3-175">For additional information on working with the **DropDownList**, see the addition references section below.</span></span> <span data-ttu-id="cefe3-176">Informieren Sie uns, wenn Sie fanden dieses Lernprogramm hilfreich.</span><span class="sxs-lookup"><span data-stu-id="cefe3-176">Please let us know if this tutorial has been helpful.</span></span>

<span data-ttu-id="cefe3-177">Rick.Anderson[at]Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="cefe3-177">Rick.Anderson[at]Microsoft.com</span></span>

### <a name="additional-references"></a><span data-ttu-id="cefe3-178">Zusätzliche Referenzen</span><span class="sxs-lookup"><span data-stu-id="cefe3-178">Additional References</span></span>

- <span data-ttu-id="cefe3-179">[ASP.NET MVC – kaskadierenden Dropdownlisten Tutorial](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) von [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)</span><span class="sxs-lookup"><span data-stu-id="cefe3-179">[ASP.NET MVC–Cascading Dropdown Lists Tutorial](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) by [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)</span></span>
- <span data-ttu-id="cefe3-180">[Ausgewählte](http://harvesthq.github.com/chosen/) eine JavaScript-Plug-Ins, die mehrere Elemente auswählen und Filtern zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="cefe3-180">[Chosen](http://harvesthq.github.com/chosen/) A JavaScript plugin that support multi-select and filtering.</span></span>

### <a name="contributors"></a><span data-ttu-id="cefe3-181">Contributors</span><span class="sxs-lookup"><span data-stu-id="cefe3-181">Contributors</span></span>

- [<span data-ttu-id="cefe3-182">Radu Enuca</span><span class="sxs-lookup"><span data-stu-id="cefe3-182">Radu Enuca</span></span>](https://weblogs.asp.net/raduenuca/default.aspx)
- <span data-ttu-id="cefe3-183">Jean-Sébastien Goupil</span><span class="sxs-lookup"><span data-stu-id="cefe3-183">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="cefe3-184">Brad Wilson</span><span class="sxs-lookup"><span data-stu-id="cefe3-184">Brad Wilson</span></span>](http://bradwilson.typepad.com/)

### <a name="reviewers"></a><span data-ttu-id="cefe3-185">Bearbeiter</span><span class="sxs-lookup"><span data-stu-id="cefe3-185">Reviewers</span></span>

- <span data-ttu-id="cefe3-186">Jean-Sébastien Goupil</span><span class="sxs-lookup"><span data-stu-id="cefe3-186">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="cefe3-187">Brad Wilson</span><span class="sxs-lookup"><span data-stu-id="cefe3-187">Brad Wilson</span></span>](http://bradwilson.typepad.com/)
- <span data-ttu-id="cefe3-188">Mike Priester</span><span class="sxs-lookup"><span data-stu-id="cefe3-188">Mike Pope</span></span>
- <span data-ttu-id="cefe3-189">Tom Dykstra</span><span class="sxs-lookup"><span data-stu-id="cefe3-189">Tom Dykstra</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="cefe3-190">Vorherige</span><span class="sxs-lookup"><span data-stu-id="cefe3-190">Previous</span></span>](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)