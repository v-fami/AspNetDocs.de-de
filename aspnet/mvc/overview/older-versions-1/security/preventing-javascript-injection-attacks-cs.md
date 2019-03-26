---
uid: mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-cs
title: Verhindern von Injection-Angriffen für JavaScript (c#) | Microsoft-Dokumentation
author: StephenWalther
description: Verhindern Sie, dass JavaScript-Injection-Angriffe und Cross-Site Scripting-Angriffe informieren möchten. In diesem Tutorial erläutert Stephen Walther an, wie Sie de auf einfache Weise...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d0136da6-81a4-4815-b002-baa84744c09e
msc.legacyurl: /mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-cs
msc.type: authoredcontent
ms.openlocfilehash: 77d0f0346e9eff756cd74c64c310918f3c367ab1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029827"
---
<a name="preventing-javascript-injection-attacks-c"></a><span data-ttu-id="f1951-104">Verhindern von Angriffen durch Einschleusung von JavaScript-Codes (C#)</span><span class="sxs-lookup"><span data-stu-id="f1951-104">Preventing JavaScript Injection Attacks (C#)</span></span>
====================
<span data-ttu-id="f1951-105">durch [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="f1951-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="f1951-106">PDF herunterladen</span><span class="sxs-lookup"><span data-stu-id="f1951-106">Download PDF</span></span>](http://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_06_CS.pdf)

> <span data-ttu-id="f1951-107">Verhindern Sie, dass JavaScript-Injection-Angriffe und Cross-Site Scripting-Angriffe informieren möchten.</span><span class="sxs-lookup"><span data-stu-id="f1951-107">Prevent JavaScript Injection Attacks and Cross-Site Scripting Attacks from happening to you.</span></span> <span data-ttu-id="f1951-108">In diesem Tutorial erläutert Stephen Walther an, wie Sie einfach diese Arten von Angriffen durch HTML-Codierung Ihrer Inhalte zunichte machen können.</span><span class="sxs-lookup"><span data-stu-id="f1951-108">In this tutorial, Stephen Walther explains how you can easily defeat these types of attacks by HTML encoding your content.</span></span>


<span data-ttu-id="f1951-109">Das Ziel in diesem Tutorial wird beschrieben, wie Sie JavaScript-Injection-Angriffen in ASP.NET MVC-Anwendungen verhindern können.</span><span class="sxs-lookup"><span data-stu-id="f1951-109">The goal of this tutorial is to explain how you can prevent JavaScript injection attacks in your ASP.NET MVC applications.</span></span> <span data-ttu-id="f1951-110">In diesem Tutorial werden zwei Ansätze zur Verteidigung Ihrer Website für einen JavaScript-Injection-Angriff erläutert.</span><span class="sxs-lookup"><span data-stu-id="f1951-110">This tutorial discusses two approaches to defending your website against a JavaScript injection attack.</span></span> <span data-ttu-id="f1951-111">Erfahren Sie, wie Sie JavaScript-Injection-Angriffe zu verhindern, indem Sie die Codierung der Daten, die angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="f1951-111">You learn how to prevent JavaScript injection attacks by encoding the data that you display.</span></span> <span data-ttu-id="f1951-112">Außerdem erfahren Sie, wie Sie JavaScript-Injection-Angriffe zu verhindern, indem Sie die Codierung der Daten, die Sie akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="f1951-112">You also learn how to prevent JavaScript injection attacks by encoding the data that you accept.</span></span>

## <a name="what-is-a-javascript-injection-attack"></a><span data-ttu-id="f1951-113">Was ist ein JavaScript-Injection-Angriff?</span><span class="sxs-lookup"><span data-stu-id="f1951-113">What is a JavaScript Injection Attack?</span></span>

<span data-ttu-id="f1951-114">Wenn Sie Benutzereingaben akzeptieren und das erneute die Benutzereingabe anzeigen, öffnen Sie Ihre Website für JavaScript-Injection-Angriffe.</span><span class="sxs-lookup"><span data-stu-id="f1951-114">Whenever you accept user input and redisplay the user input, you open your website to JavaScript injection attacks.</span></span> <span data-ttu-id="f1951-115">Betrachten Sie eine konkrete Anwendung, die für JavaScript-Injection-Angriffe geöffnet ist.</span><span class="sxs-lookup"><span data-stu-id="f1951-115">Let's examine a concrete application that is open to JavaScript injection attacks.</span></span>

<span data-ttu-id="f1951-116">Stellen Sie sich vor, dass Sie eine Kunden-Feedback-Website erstellt haben (siehe Abbildung 1).</span><span class="sxs-lookup"><span data-stu-id="f1951-116">Imagine that you have created a customer feedback website (see Figure 1).</span></span> <span data-ttu-id="f1951-117">Kunden können finden Sie auf der Website, und geben Sie Feedback an den Erfahrungen, die Ihre Produkte verwenden.</span><span class="sxs-lookup"><span data-stu-id="f1951-117">Customers can visit the website and enter feedback on their experience using your products.</span></span> <span data-ttu-id="f1951-118">Wenn ein Kunde ihr Feedback übermittelt, wird das Feedback auf der Seite "Feedback" erneut angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f1951-118">When a customer submits their feedback, the feedback is redisplayed on the feedback page.</span></span>


<span data-ttu-id="f1951-119">[![Kunden-Feedback-Website](preventing-javascript-injection-attacks-cs/_static/image2.png)](preventing-javascript-injection-attacks-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f1951-119">[![Customer Feedback Website](preventing-javascript-injection-attacks-cs/_static/image2.png)](preventing-javascript-injection-attacks-cs/_static/image1.png)</span></span>

<span data-ttu-id="f1951-120">**Abbildung 01**: Kunden-Feedback-Website ([klicken Sie, um das Bild in voller Größe anzeigen](preventing-javascript-injection-attacks-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f1951-120">**Figure 01**: Customer Feedback Website ([Click to view full-size image](preventing-javascript-injection-attacks-cs/_static/image3.png))</span></span>


<span data-ttu-id="f1951-121">Die Kunden-Feedback-Website verwendet die `controller` in Codebeispiel 1.</span><span class="sxs-lookup"><span data-stu-id="f1951-121">The customer feedback website uses the `controller` in Listing 1.</span></span> <span data-ttu-id="f1951-122">Dies `controller` enthält zwei Aktionen, die mit dem Namen `Index()` und `Create()`.</span><span class="sxs-lookup"><span data-stu-id="f1951-122">This `controller` contains two actions named `Index()` and `Create()`.</span></span>

<span data-ttu-id="f1951-123">**Codebeispiel 1: `HomeController.cs`**</span><span class="sxs-lookup"><span data-stu-id="f1951-123">**Listing 1 – `HomeController.cs`**</span></span>

[!code-csharp[Main](preventing-javascript-injection-attacks-cs/samples/sample1.cs)]

<span data-ttu-id="f1951-124">Die `Index()` Methode zeigt die `Index` anzeigen.</span><span class="sxs-lookup"><span data-stu-id="f1951-124">The `Index()` method displays the `Index` view.</span></span> <span data-ttu-id="f1951-125">Diese Methode gibt alle von der vorherigen Feedback von Kunden, die `Index` Ansicht durch Abrufen des Feedbacks aus der Datenbank (mithilfe einer LINQ to SQL-Abfrage).</span><span class="sxs-lookup"><span data-stu-id="f1951-125">This method passes all of the previous customer feedback to the `Index` view by retrieving the feedback from the database (using a LINQ to SQL query).</span></span>

<span data-ttu-id="f1951-126">Die `Create()` Methode erstellt ein neues Feedbackelement und fügt es der Datenbank hinzu.</span><span class="sxs-lookup"><span data-stu-id="f1951-126">The `Create()` method creates a new Feedback item and adds it to the database.</span></span> <span data-ttu-id="f1951-127">Die Meldung, die der Kunde in der Form gibt übergeben wird, um die `Create()` -Methode in der Meldungsparameter.</span><span class="sxs-lookup"><span data-stu-id="f1951-127">The message that the customer enters in the form is passed to the `Create()` method in the message parameter.</span></span> <span data-ttu-id="f1951-128">Ein Feedbackelement erstellt wird und die Nachricht wird des Feedbackelement zugewiesen `Message` Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="f1951-128">A Feedback item is created and the message is assigned to the Feedback item's `Message` property.</span></span> <span data-ttu-id="f1951-129">Das Feedbackelement wird übermittelt, für die Datenbank mit der `DataContext.SubmitChanges()` Methodenaufruf.</span><span class="sxs-lookup"><span data-stu-id="f1951-129">The Feedback item is submitted to the database with the `DataContext.SubmitChanges()` method call.</span></span> <span data-ttu-id="f1951-130">Schließlich wird der Besucher umgeleitet, an die `Index` anzeigen, in denen alle das Feedback wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f1951-130">Finally, the visitor is redirected back to the `Index` view where all of the feedback is displayed.</span></span>

<span data-ttu-id="f1951-131">Die `Index` Ansicht im Codebeispiel 2 enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="f1951-131">The `Index` view is contained in Listing 2.</span></span>

<span data-ttu-id="f1951-132">**Codebeispiel 2: `Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="f1951-132">**Listing 2 – `Index.aspx`**</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-cs/samples/sample2.aspx)]

<span data-ttu-id="f1951-133">Die `Index` Ansicht besteht aus zwei Abschnitten.</span><span class="sxs-lookup"><span data-stu-id="f1951-133">The `Index` view has two sections.</span></span> <span data-ttu-id="f1951-134">Der oberste Abschnitt enthält die tatsächliche Kunden-Feedback-Formular.</span><span class="sxs-lookup"><span data-stu-id="f1951-134">The top section contains the actual customer feedback form.</span></span> <span data-ttu-id="f1951-135">Der untere Abschnitt enthält eine For... Each-Schleife, die alle vorherigen Customer feedbackelemente durchläuft und zeigt die EntryDate und Nachricht Eigenschaften für jedes Feedbackelement.</span><span class="sxs-lookup"><span data-stu-id="f1951-135">The bottom section contains a For..Each loop that loops through all of the previous customer feedback items and displays the EntryDate and Message properties for each feedback item.</span></span>

<span data-ttu-id="f1951-136">Die Kunden-Feedback-Website ist eine einfache Website.</span><span class="sxs-lookup"><span data-stu-id="f1951-136">The customer feedback website is a simple website.</span></span> <span data-ttu-id="f1951-137">Leider ist die Website für JavaScript-Injection-Angriffe geöffnet.</span><span class="sxs-lookup"><span data-stu-id="f1951-137">Unfortunately, the website is open to JavaScript injection attacks.</span></span>

<span data-ttu-id="f1951-138">Stellen Sie sich, dass Sie den folgenden Text in das Kunden-Feedback-Formular eingeben:</span><span class="sxs-lookup"><span data-stu-id="f1951-138">Imagine that you enter the following text into the customer feedback form:</span></span>

[!code-html[Main](preventing-javascript-injection-attacks-cs/samples/sample3.html)]

<span data-ttu-id="f1951-139">Dieser Text stellt ein JavaScript-Skript, das eine Warnmeldung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f1951-139">This text represents a JavaScript script that displays an alert message box.</span></span> <span data-ttu-id="f1951-140">Nachdem ein Benutzer dieses Skript an das Feedback übermittelt zu bilden, die Nachricht <em>Boo!</em> wird angezeigt, wenn jeder Benutzer, die Kunden-Feedback-Website in der Zukunft besucht (siehe Abbildung 2).</span><span class="sxs-lookup"><span data-stu-id="f1951-140">After someone submits this script into the feedback form, the message <em>Boo!</em>will appear whenever anyone visits the customer feedback website in the future (see Figure 2).</span></span>


<span data-ttu-id="f1951-141">[![Einschleusung von JavaScript](preventing-javascript-injection-attacks-cs/_static/image5.png)](preventing-javascript-injection-attacks-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="f1951-141">[![JavaScript Injection](preventing-javascript-injection-attacks-cs/_static/image5.png)](preventing-javascript-injection-attacks-cs/_static/image4.png)</span></span>

<span data-ttu-id="f1951-142">**Abbildung 02**: Einschleusung von JavaScript-Befehlen ([klicken Sie, um das Bild in voller Größe anzeigen](preventing-javascript-injection-attacks-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="f1951-142">**Figure 02**: JavaScript Injection ([Click to view full-size image](preventing-javascript-injection-attacks-cs/_static/image6.png))</span></span>


<span data-ttu-id="f1951-143">Nun kann Ihre erste Reaktion auf JavaScript-Injection-Angriffen kann das zu apathie sein.</span><span class="sxs-lookup"><span data-stu-id="f1951-143">Now, your initial response to JavaScript injection attacks might be apathy.</span></span> <span data-ttu-id="f1951-144">Zunächst vermuten, dass die JavaScript-Injection-Angriffe einfach eine Art von sind *Verunstaltung* Angriff.</span><span class="sxs-lookup"><span data-stu-id="f1951-144">You might think that JavaScript injection attacks are simply a type of *defacement* attack.</span></span> <span data-ttu-id="f1951-145">Sie gehen davon aus, dass niemand alles wirklich böse ausführen können, indem ein Commit für einen JavaScript-Injection-Angriff.</span><span class="sxs-lookup"><span data-stu-id="f1951-145">You might believe that no one can do anything truly evil by committing a JavaScript injection attack.</span></span>

<span data-ttu-id="f1951-146">Leider ein Hacker möglich, einige wirklich sehr schlecht Dinge durch Einfügen von JavaScript in einer Website.</span><span class="sxs-lookup"><span data-stu-id="f1951-146">Unfortunately, a hacker can do some really, really evil things by injecting JavaScript into a website.</span></span> <span data-ttu-id="f1951-147">Sie können einen JavaScript-Injection-Angriff verwenden, Cross-Site Scripting (XSS) auszuführen.</span><span class="sxs-lookup"><span data-stu-id="f1951-147">You can use a JavaScript injection attack to perform a Cross-Site Scripting (XSS) attack.</span></span> <span data-ttu-id="f1951-148">Bei einem Angriff Cross-Site Scripting, wenn Sie vertrauliche Benutzer Daten stehlen und an eine andere Website gesendet.</span><span class="sxs-lookup"><span data-stu-id="f1951-148">In a Cross-Site Scripting attack, you steal confidential user information and send the information to another website.</span></span>

<span data-ttu-id="f1951-149">Beispielsweise kann ein Hacker einen JavaScript-Injection-Angriff verwenden, um die Werte der Cookies im Browser von anderen Benutzern zu stehlen.</span><span class="sxs-lookup"><span data-stu-id="f1951-149">For example, a hacker can use a JavaScript injection attack to steal the values of browser cookies from other users.</span></span> <span data-ttu-id="f1951-150">Wenn vertraulicher Informationen zugreifen, beispielsweise Kennwörter, Kreditkartennummern und Sozialversicherungsnummern – in die Cookies im Browser gespeichert sind, klicken Sie dann können ein Hacker einen JavaScript-Injection-Angriff Sie um diese Informationen zu stehlen.</span><span class="sxs-lookup"><span data-stu-id="f1951-150">If sensitive information -- such as passwords, credit card numbers, or social security numbers – is stored in the browser cookies, then a hacker can use a JavaScript injection attack to steal this information.</span></span> <span data-ttu-id="f1951-151">Wenn ein Benutzer vertraulichen Informationen in ein Formularfeld in eine Seite, die bei einem JavaScript-Angriff gefährdet ist eingibt, klicken Sie dann der Hacker kann auch den injizierten JavaScript-Code zum Abrufen von Daten aus dem Formular und eine andere Website an.</span><span class="sxs-lookup"><span data-stu-id="f1951-151">Or, if a user enters sensitive information in a form field contained in a page that has been compromised with a JavaScript attack, then the hacker can use the injected JavaScript to grab the form data and send it to another website.</span></span>

<span data-ttu-id="f1951-152">*Seien Sie abschreckend*.</span><span class="sxs-lookup"><span data-stu-id="f1951-152">*Please be scared*.</span></span> <span data-ttu-id="f1951-153">Nehmen Sie JavaScript-Injection-Angriffen ernst zu, und schützen Sie vertrauliche Informationen des Benutzers.</span><span class="sxs-lookup"><span data-stu-id="f1951-153">Take JavaScript injection attacks seriously and protect your user's confidential information.</span></span> <span data-ttu-id="f1951-154">In den nächsten beiden Abschnitten werden zwei Techniken, mit denen Sie Ihre ASP.NET MVC-Anwendungen von JavaScript-Injection-Angriffen zu schützen.</span><span class="sxs-lookup"><span data-stu-id="f1951-154">In the next two sections, we discuss two techniques that you can use to defend your ASP.NET MVC applications from JavaScript injection attacks.</span></span>

## <a name="approach-1-html-encode-in-the-view"></a><span data-ttu-id="f1951-155">Ansatz #1: In der Ansicht HTML-Codierung</span><span class="sxs-lookup"><span data-stu-id="f1951-155">Approach #1: HTML Encode in the View</span></span>

<span data-ttu-id="f1951-156">Eine einfache Methode zum Verhindern von JavaScript-Injection-Angriffen in HTML codieren Sie alle Daten, die von Benutzern der Website eingegeben werden, wenn Sie die Daten in einer Sicht erneut anzeigen.</span><span class="sxs-lookup"><span data-stu-id="f1951-156">One easy method of preventing JavaScript injection attacks is to HTML encode any data entered by website users when you redisplay the data in a view.</span></span> <span data-ttu-id="f1951-157">Die aktualisierte `Index` Ansicht in Programmausdruck 3 folgt diesem Ansatz.</span><span class="sxs-lookup"><span data-stu-id="f1951-157">The updated `Index` view in Listing 3 follows this approach.</span></span>

<span data-ttu-id="f1951-158">**Codebeispiel 3 – `Index.aspx` (HTML-codiert)**</span><span class="sxs-lookup"><span data-stu-id="f1951-158">**Listing 3 – `Index.aspx` (HTML Encoded)**</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-cs/samples/sample4.aspx)]

<span data-ttu-id="f1951-159">Beachten Sie, dass der Wert des `feedback.Message` ist HTML-codiert werden, bevor der Wert durch den folgenden Code angezeigt wird:</span><span class="sxs-lookup"><span data-stu-id="f1951-159">Notice that the value of `feedback.Message` is HTML encoded before the value is displayed with the following code:</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-cs/samples/sample5.aspx)]

<span data-ttu-id="f1951-160">Funktionsweise Mittelwert in HTML codieren eine Zeichenfolge?</span><span class="sxs-lookup"><span data-stu-id="f1951-160">What does it mean to HTML encode a string?</span></span> <span data-ttu-id="f1951-161">Wenn Sie HTML eine Zeichenfolge zu codieren, gefährliche Zeichen wie z. B. `<` und `>` durch Verweise auf HTML-Entitäten wie z. B. ersetzt werden `&lt;` und `&gt;`.</span><span class="sxs-lookup"><span data-stu-id="f1951-161">When you HTML encode a string, dangerous characters such as `<` and `>` are replaced by HTML entity references such as `&lt;` and `&gt;`.</span></span> <span data-ttu-id="f1951-162">Dies der Fall bei der Zeichenfolge `<script>alert("Boo!")</script>` HTML-codiert, es konvertiert `&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`.</span><span class="sxs-lookup"><span data-stu-id="f1951-162">So when the string `<script>alert("Boo!")</script>` is HTML encoded, it gets converted to `&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`.</span></span> <span data-ttu-id="f1951-163">Die codierte Zeichenfolge führt nicht mehr als einem JavaScript-Skript, wenn von einem Browser interpretiert.</span><span class="sxs-lookup"><span data-stu-id="f1951-163">The encoded string no longer executes as a JavaScript script when interpreted by a browser.</span></span> <span data-ttu-id="f1951-164">Stattdessen erhalten Sie in Abbildung 3 die harmlose Seite an.</span><span class="sxs-lookup"><span data-stu-id="f1951-164">Instead, you get the harmless page in Figure 3.</span></span>


<span data-ttu-id="f1951-165">[![JavaScript-Angriff](preventing-javascript-injection-attacks-cs/_static/image8.png)](preventing-javascript-injection-attacks-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="f1951-165">[![Defeated JavaScript Attack](preventing-javascript-injection-attacks-cs/_static/image8.png)](preventing-javascript-injection-attacks-cs/_static/image7.png)</span></span>

<span data-ttu-id="f1951-166">**Abbildung 03**: Abwehren von JavaScript-Angriff ([klicken Sie, um das Bild in voller Größe anzeigen](preventing-javascript-injection-attacks-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="f1951-166">**Figure 03**: Defeated JavaScript Attack ([Click to view full-size image](preventing-javascript-injection-attacks-cs/_static/image9.png))</span></span>


<span data-ttu-id="f1951-167">Beachten Sie, dass in der `Index` anzeigen in Programmausdruck 3 nur den Wert der `feedback.Message` codiert ist.</span><span class="sxs-lookup"><span data-stu-id="f1951-167">Notice that in the `Index` view in Listing 3 only the value of `feedback.Message` is encoded.</span></span> <span data-ttu-id="f1951-168">Der Wert des `feedback.EntryDate` ist nicht codiert.</span><span class="sxs-lookup"><span data-stu-id="f1951-168">The value of `feedback.EntryDate` is not encoded.</span></span> <span data-ttu-id="f1951-169">Sie müssen nur von einem Benutzer eingegeben Daten codieren.</span><span class="sxs-lookup"><span data-stu-id="f1951-169">You only need to encode data entered by a user.</span></span> <span data-ttu-id="f1951-170">Da der Wert des EntryDate im Controller generiert wurde, müssen Sie nicht in HTML dieses Werts codieren.</span><span class="sxs-lookup"><span data-stu-id="f1951-170">Because the value of EntryDate was generated in the controller, you don't need to HTML encode this value.</span></span>

## <a name="approach-2-html-encode-in-the-controller"></a><span data-ttu-id="f1951-171">Vorgehensweise #2: HTML-Codierung im Controller</span><span class="sxs-lookup"><span data-stu-id="f1951-171">Approach #2: HTML Encode in the Controller</span></span>

<span data-ttu-id="f1951-172">Anstelle von HTML codieren von Daten, wenn Sie die Daten in einer Ansicht anzeigen, können Sie HTML codieren Sie die Daten ein, kurz bevor die Daten in der Datenbank zu übermitteln.</span><span class="sxs-lookup"><span data-stu-id="f1951-172">Instead of HTML encoding data when you display the data in a view, you can HTML encode the data just before you submit the data to the database.</span></span> <span data-ttu-id="f1951-173">Dieser zweite Ansatz wird verwendet, in der die `controller` in Listing 4.</span><span class="sxs-lookup"><span data-stu-id="f1951-173">This second approach is taken in the case of the `controller` in Listing 4.</span></span>

<span data-ttu-id="f1951-174">**Programmausdruck 4 – `HomeController.cs` (HTML-codiert)**</span><span class="sxs-lookup"><span data-stu-id="f1951-174">**Listing 4 – `HomeController.cs` (HTML Encoded)**</span></span>

[!code-csharp[Main](preventing-javascript-injection-attacks-cs/samples/sample6.cs)]

<span data-ttu-id="f1951-175">Beachten Sie, dass der Wert der Nachricht HTML ist-codiert werden, bevor der Wert, an die Datenbank in übermittelt wird der `Create()` Aktion.</span><span class="sxs-lookup"><span data-stu-id="f1951-175">Notice that the value of Message is HTML encoded before the value is submitted to the database within the `Create()` action.</span></span> <span data-ttu-id="f1951-176">Wenn die Nachricht in der Ansicht erneut angezeigt wird, wird die Nachricht wird HTML-codiert, und JavaScript in der Nachricht eingefügt wird nicht ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="f1951-176">When the Message is redisplayed in the view, the Message is HTML encoded and any JavaScript injected in the Message is not executed.</span></span>

<span data-ttu-id="f1951-177">In der Regel sollten Sie die erste Methode, die in diesem Tutorial erläutert wird, über dieser zweite Ansatz bevorzugen.</span><span class="sxs-lookup"><span data-stu-id="f1951-177">Typically, you should favor the first approach discussed in this tutorial over this second approach.</span></span> <span data-ttu-id="f1951-178">Das Problem bei dieser zweite Ansatz ist, dass Sie HTML-codierte Daten in der Datenbank erhalten.</span><span class="sxs-lookup"><span data-stu-id="f1951-178">The problem with this second approach is that you end up with HTML encoded data in your database.</span></span> <span data-ttu-id="f1951-179">Das heißt, werden Ihre Datenbankdaten mit lustige aussehende Zeichen verschmutzte.</span><span class="sxs-lookup"><span data-stu-id="f1951-179">In other words, your database data is dirtied with funny looking characters.</span></span>

<span data-ttu-id="f1951-180">Warum dies schlecht ist?</span><span class="sxs-lookup"><span data-stu-id="f1951-180">Why is this bad?</span></span> <span data-ttu-id="f1951-181">Wenn Sie Daten in der Datenbank in einen anderen Wert als eine Webseite anzeigen müssen, klicken Sie dann haben Sie Probleme.</span><span class="sxs-lookup"><span data-stu-id="f1951-181">If you ever need to display the database data in something other than a web page, then you will have problems.</span></span> <span data-ttu-id="f1951-182">Beispielsweise können Sie nicht mehr einfach die Daten in einer Windows Forms-Anwendung anzeigen.</span><span class="sxs-lookup"><span data-stu-id="f1951-182">For example, you can no longer easily display the data in a Windows Forms application.</span></span>

## <a name="summary"></a><span data-ttu-id="f1951-183">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="f1951-183">Summary</span></span>

<span data-ttu-id="f1951-184">Der Zweck dieses Lernprogramms bestand darin, Sie über die Aussicht einen JavaScript-Injection-Angriff abschrecken.</span><span class="sxs-lookup"><span data-stu-id="f1951-184">The purpose of this tutorial was to scare you about the prospect of a JavaScript injection attack.</span></span> <span data-ttu-id="f1951-185">In diesem Tutorial erläutert zwei Ansätze zur Verteidigung von ASP.NET MVC-Anwendungen für JavaScript-Injection-Angriffen: können Sie entweder HTML codieren Benutzer übermittelt Daten in der Ansicht, oder Sie können HTML codieren Benutzer übermittelt Daten in den Controller.</span><span class="sxs-lookup"><span data-stu-id="f1951-185">This tutorial discussed two approaches for defending your ASP.NET MVC applications against JavaScript injection attacks: you can either HTML encode user submitted data in the view or you can HTML encode user submitted data in the controller.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f1951-186">[Zurück](authenticating-users-with-windows-authentication-cs.md)
> [Weiter](authenticating-users-with-forms-authentication-vb.md)</span><span class="sxs-lookup"><span data-stu-id="f1951-186">[Previous](authenticating-users-with-windows-authentication-cs.md)
[Next](authenticating-users-with-forms-authentication-vb.md)</span></span>