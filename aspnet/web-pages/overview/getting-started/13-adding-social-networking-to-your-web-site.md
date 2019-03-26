---
uid: web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
title: Hinzufügen von sozialen Netzwerken zu ASP.NET Web Pages (Razor) Sites | Microsoft-Dokumentation
author: Rick-Anderson
description: In diesem Kapitel wird erläutert, wie Sie Ihre Website in soziale Netzwerkdienste integrieren. In diesem Kapitel erfahren Sie, wie Sie den Personenkreis Lesezeichenlink/Ihrer Website...
ms.author: riande
ms.date: 02/21/2014
ms.assetid: 03c342f9-b35c-4d7c-b9ed-cd9aaaffedb6
msc.legacyurl: /web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: d2b970e7b80e4129d0a912f648f9c4a54df531b2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57041847"
---
<a name="adding-social-networking-to-aspnet-web-pages-razor-sites"></a><span data-ttu-id="29f30-104">Hinzufügen von soziale Websites für Networking ASP.NET-Webseiten (Razor)</span><span class="sxs-lookup"><span data-stu-id="29f30-104">Adding Social Networking to ASP.NET Web Pages (Razor) Sites</span></span>
====================
<span data-ttu-id="29f30-105">durch [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="29f30-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="29f30-106">Dieser Artikel beschreibt das Hinzufügen von Links zu sozialen Netzwerken für Facebook, Twitter, Reddit und Digg zu Seiten, die auf einer Website für ASP.NET Web Pages (Razor), und wie Sie Twitter-Feeds, Xbox Spieler Karten und Gravatar-Bilder enthalten.</span><span class="sxs-lookup"><span data-stu-id="29f30-106">This article explains how to add social networking links for Facebook, Twitter, Reddit, and Digg to pages in an ASP.NET Web Pages (Razor) website, and how to include Twitter feeds, Xbox gamer cards, and Gravatar images.</span></span>
> 
> <span data-ttu-id="29f30-107">Sie lernen Folgendes:</span><span class="sxs-lookup"><span data-stu-id="29f30-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="29f30-108">Wie Sie Personen Lesezeichenlink/Ihrer Website zu überlassen.</span><span class="sxs-lookup"><span data-stu-id="29f30-108">How to let people bookmark/link your site.</span></span>
> - <span data-ttu-id="29f30-109">So fügen Sie einen Twitter-Feed.</span><span class="sxs-lookup"><span data-stu-id="29f30-109">How to add a Twitter feed.</span></span>
> - <span data-ttu-id="29f30-110">Gewusst wie: Hinzufügen von Facebook **wie** Schaltfläche, um Seiten.</span><span class="sxs-lookup"><span data-stu-id="29f30-110">How to add a Facebook **Like** button to pages.</span></span>
> - <span data-ttu-id="29f30-111">Informationen zum Rendern von Bildern von Gravatar.com.</span><span class="sxs-lookup"><span data-stu-id="29f30-111">How to render Gravatar.com images.</span></span>
> - <span data-ttu-id="29f30-112">Wie eine Spiele Xbox-Karte auf Ihrer Website anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="29f30-112">How to display an Xbox gamer card on your site.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="29f30-113">Softwareversionen, die in diesem Tutorial verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="29f30-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="29f30-114">ASP.NET Web Pages (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="29f30-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="29f30-115">ASP.NET Web-Hilfsbibliothek (NuGet-Paket)</span><span class="sxs-lookup"><span data-stu-id="29f30-115">ASP.NET Web Helper Library (NuGet package)</span></span>
>   
> 
> <span data-ttu-id="29f30-116">In diesem Tutorial funktioniert auch mit ASP.NET Web Pages-3, mit Ausnahme der Teile, die die ASP.NET Web-Hilfsbibliothek verwenden.</span><span class="sxs-lookup"><span data-stu-id="29f30-116">This tutorial also works with ASP.NET Web Pages 3, except for parts that use the ASP.NET Web Helper Library.</span></span>


<a id="Linking_Your_Website"></a>
## <a name="linking-your-website-on-social-networking-sites"></a><span data-ttu-id="29f30-117">Verknüpfen Ihre Website auf Websites für soziale Netzwerke</span><span class="sxs-lookup"><span data-stu-id="29f30-117">Linking Your Website on Social Networking Sites</span></span>

<span data-ttu-id="29f30-118">Wenn der Benutzer etwas an Ihrem Standort zufrieden sind, möchten sie häufig für Freunde freigeben.</span><span class="sxs-lookup"><span data-stu-id="29f30-118">If people like something on your site, they often want to share it with friends.</span></span> <span data-ttu-id="29f30-119">Sie können diesen Vorgang vereinfachen durch Anzeigen der Symbole (Symbole), die Benutzer klicken können, um eine Seite auf Digg, Reddit, Facebook, Twitter oder ähnliche Websites gemeinsam nutzen.</span><span class="sxs-lookup"><span data-stu-id="29f30-119">You can make this easy by displaying glyphs (icons) that people can click to share a page on Digg, Reddit, Facebook, Twitter, or similar sites.</span></span>

<span data-ttu-id="29f30-120">Um diese Symbole anzuzeigen, fügen die `LinkSharecode` Hilfsmethode zu einer Seite.</span><span class="sxs-lookup"><span data-stu-id="29f30-120">To display these glyphs, add the `LinkSharecode` helper to a page.</span></span> <span data-ttu-id="29f30-121">Personen, die Ihre Seite besuchen, können ein einzelnes Symbol klicken.</span><span class="sxs-lookup"><span data-stu-id="29f30-121">People who visit your page can click an individual glyph.</span></span> <span data-ttu-id="29f30-122">Wenn sie ein Konto mit dieser Website für soziale Netzwerke verfügen, können sie einen Link zu Ihrer Seite klicken Sie dann auf dieser Website bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="29f30-122">If they have an account with that social networking site, they can then post a link to your page on that site.</span></span>

![Abbildung 1](13-adding-social-networking-to-your-web-site/_static/image1.jpg)

1. <span data-ttu-id="29f30-124">Die ASP.NET Web Helpers Library zu Ihrer Website hinzufügen, wie in beschrieben [Hilfsprogramme installieren, in einer ASP.NET Web Pages-Website](https://go.microsoft.com/fwlink/?LinkId=252372), falls Sie bereits it. - hinzugefügt haben erstellen Sie eine Seite mit dem Namen *ListLinkShare.cshtml* und hinzufügen Das folgende Markup:</span><span class="sxs-lookup"><span data-stu-id="29f30-124">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.- Create a page named *ListLinkShare.cshtml* and add the following markup:</span></span>

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample1.cshtml)]

    <span data-ttu-id="29f30-125">In diesem Beispiel ist bei der `LinkShare` ausgeführt, den Seitentitel als Parameter verwendet, das den Titel der Seite auf der Website für soziale Netzwerke weiterleitet übergeben wird.</span><span class="sxs-lookup"><span data-stu-id="29f30-125">In this example, when the `LinkShare` helper runs, the page title is passed as a parameter, which in turn passes the page title to the social networking site.</span></span> <span data-ttu-id="29f30-126">Jedoch könnten Sie eine beliebige Zeichenfolge übergeben Sie die gewünschten.</span><span class="sxs-lookup"><span data-stu-id="29f30-126">However, you could pass in any string you want.</span></span> <span data-ttu-id="29f30-127">In diesem Beispiel gibt auch die Websites für soziale Netzwerke, die in der Liste enthalten.</span><span class="sxs-lookup"><span data-stu-id="29f30-127">This example also specifies which social networking sites to include in the list.</span></span> <span data-ttu-id="29f30-128">Sie können die Websites für soziale Netzwerke angeben, die auf Ihrer Website relevant sind.</span><span class="sxs-lookup"><span data-stu-id="29f30-128">You can specify the social networking sites that are relevant to your site.</span></span>
2. <span data-ttu-id="29f30-129">Führen Sie die *ListLinkShare.cshtml* Seite in einem Browser.</span><span class="sxs-lookup"><span data-stu-id="29f30-129">Run the *ListLinkShare.cshtml* page in a browser.</span></span> <span data-ttu-id="29f30-130">(Stellen Sie sicher, dass die Seite ist ausgewählt, der **Dateien** Arbeitsbereich vor der Ausführung.)</span><span class="sxs-lookup"><span data-stu-id="29f30-130">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
3. <span data-ttu-id="29f30-131">Klicken Sie auf ein Symbol für einen dieser Standorte, denen Sie registriert sind.</span><span class="sxs-lookup"><span data-stu-id="29f30-131">Click a glyph for one of the sites that you're signed up for.</span></span> <span data-ttu-id="29f30-132">Der Link leitet Sie auf der Seite auf der ausgewählten soziales Netzwerk-Website, in dem Sie gemeinsam nutzen, können, einen Link.</span><span class="sxs-lookup"><span data-stu-id="29f30-132">The link takes you to the page on the selected social network site where you can share a link.</span></span> <span data-ttu-id="29f30-133">Z. B. Wenn Sie den Reddit-Link klicken, Sie gelangen auf die `submit to reddit` auf der Website Reddit.</span><span class="sxs-lookup"><span data-stu-id="29f30-133">For example, if you click the Reddit link, you're taken to the `submit to reddit` page on the Reddit website.</span></span>

     ![Abbildung 2](13-adding-social-networking-to-your-web-site/_static/image2.jpg)

<a id="Adding_a_Twitter_Feed"></a>
## <a name="adding-a-twitter-feed"></a><span data-ttu-id="29f30-135">Hinzufügen einer Twitter-Feed</span><span class="sxs-lookup"><span data-stu-id="29f30-135">Adding a Twitter Feed</span></span>

<span data-ttu-id="29f30-136">Weitere Informationen zur Verwendung einer Twitter-Hilfsprogramms, das mit der aktuellen Version der Twitter-API kompatibel ist, finden Sie unter [Twitter-Hilfsprogramm](../ui-layouts-and-themes/twitter-helper.md).</span><span class="sxs-lookup"><span data-stu-id="29f30-136">For information about using a Twitter helper that is compatible with the current version of the Twitter API, see [Twitter helper](../ui-layouts-and-themes/twitter-helper.md).</span></span> <span data-ttu-id="29f30-137">Dieses Beispiel zeigt, wie Sie Ihre eigenen Hilfsprogramm schreiben, sodass Sie den Code aus vielen Seiten einfach wiederverwenden können.</span><span class="sxs-lookup"><span data-stu-id="29f30-137">This example shows how to write your own helper so you can easily reuse the code from many pages.</span></span>

<a id="Displaying_a_Facebook_Button"></a>
## <a name="displaying-a-facebook-quotlikequot-button"></a><span data-ttu-id="29f30-138">Anzeigen von Facebook &quot;wie&quot; Schaltfläche</span><span class="sxs-lookup"><span data-stu-id="29f30-138">Displaying a Facebook &quot;Like&quot; Button</span></span>

<span data-ttu-id="29f30-139">In einigen Fällen ist die beste Möglichkeit, den Code direkt aus dem Anbieter des sozialen Netzwerks Netzwerk statt eines Hilfsprogramms abrufen.</span><span class="sxs-lookup"><span data-stu-id="29f30-139">In some cases, your best option is to get the code directly from the social networking provider rather than relying on a helper.</span></span> <span data-ttu-id="29f30-140">Dies ist insbesondere dann, wenn der Anbieter des sozialen Netzwerks ihrer Optionen updates schneller als das Hilfsobjekt aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="29f30-140">This is especially true if the social network provider updates its options more quickly than the helper is updated.</span></span>

<span data-ttu-id="29f30-141">Um Facebook-Features (z. B. die Schaltfläche "Like") auf Ihrer Website hinzuzufügen, können Sie Codeausschnitte aus Abrufen der ["Developers.Facebook.com"](https://developers.facebook.com/) Standort.</span><span class="sxs-lookup"><span data-stu-id="29f30-141">To add Facebook features (such as the Like button) to your site, you can retrieve code snippets from the [developers.facebook.com](https://developers.facebook.com/) site.</span></span> <span data-ttu-id="29f30-142">Auf der Facebook-Website verwenden Sie ihre Tools, um einen Codeausschnitt zu generieren, der auf Ihrer Website relevant sind.</span><span class="sxs-lookup"><span data-stu-id="29f30-142">On the Facebook site, you use their tools to generate a code snippet that is relevant to your site.</span></span>

<span data-ttu-id="29f30-143">Der folgende hervorgehobene Code ist der Code, der das Tool wie Schaltfläche auf der Website "Developers.Facebook.com" abgerufen wurde.</span><span class="sxs-lookup"><span data-stu-id="29f30-143">The following highlighted code is the code that was retrieved from the Like Button tool on the developers.facebook.com site.</span></span> <span data-ttu-id="29f30-144">Sie müssen Ihre eigenen app-ID angeben.</span><span class="sxs-lookup"><span data-stu-id="29f30-144">You must provide your own app ID.</span></span>

[!code-html[Main](13-adding-social-networking-to-your-web-site/samples/sample2.html?highlight=7-14,16-17)]

<a id="Rendering_a_Gravatar_Image"></a>
## <a name="rendering-a-gravatar-image"></a><span data-ttu-id="29f30-145">Rendern einer Gravatar-Bilds</span><span class="sxs-lookup"><span data-stu-id="29f30-145">Rendering a Gravatar Image</span></span>

<span data-ttu-id="29f30-146">Ein *Gravatar* (eine &quot;weltweit anerkannten Avatar&quot;) ist ein Bild, das für mehrere Websites als Ihren Avatar verwendet werden kann &#8212; , also ein Image, das Sie darstellt.</span><span class="sxs-lookup"><span data-stu-id="29f30-146">A *Gravatar* (a &quot;globally recognized avatar&quot;) is an image that can be used on multiple websites as your avatar &#8212; that is, an image that represents you.</span></span> <span data-ttu-id="29f30-147">Beispielsweise kann ein Gravatar identifizieren eine Person in einem Forumsbeitrag in einem Blogkommentar, und so weiter.</span><span class="sxs-lookup"><span data-stu-id="29f30-147">For example, a Gravatar can identify a person in a forum post, in a blog comment, and so on.</span></span> <span data-ttu-id="29f30-148">(Sie können Ihre eigenen Gravatar an der Gravatar-Website unter registrieren [ http://www.gravatar.com/ ](http://www.gravatar.com/).) Wenn Sie Images, die neben den Namen oder e-Mail-Adressen der Personen auf Ihrer Website anzeigen möchten, können Sie das Gravatar-Hilfsprogramm.</span><span class="sxs-lookup"><span data-stu-id="29f30-148">(You can register your own Gravatar at the Gravatar website at [http://www.gravatar.com/](http://www.gravatar.com/).) If you want to display images next to people's names or email addresses on your website, you can use the Gravatar helper.</span></span>

<span data-ttu-id="29f30-149">In diesem Beispiel verwenden Sie eine einzelne Gravatar, die sich selbst darstellt.</span><span class="sxs-lookup"><span data-stu-id="29f30-149">In this example, you're using a single Gravatar that represents yourself.</span></span> <span data-ttu-id="29f30-150">Eine weitere Möglichkeit zum Verwenden einer Gravatar besteht darin, Personen, die ihre Gravatar-Adresse angeben, wenn sie auf der Website registrieren.</span><span class="sxs-lookup"><span data-stu-id="29f30-150">Another way to use a Gravatar is to let people specify their Gravatar address when they register on your site.</span></span> <span data-ttu-id="29f30-151">(Sie können erfahren Sie, wie Benutzer in registrieren können [Hinzufügen von Sicherheit und die Mitgliedschaft in einer ASP.NET Web Pages-Website](https://go.microsoft.com/fwlink/?LinkId=202904).) Klicken Sie dann, wenn Sie die Informationen für diesen Benutzer anzeigen, können Sie einfach hinzufügen der Gravatar, in dem Sie den Namen des Benutzers anzeigen.</span><span class="sxs-lookup"><span data-stu-id="29f30-151">(You can learn how to let people register in [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).) Then whenever you display information for that user, you can just add the Gravatar to where you display the user's name.</span></span>

1. <span data-ttu-id="29f30-152">Die ASP.NET Web Helpers Library zu Ihrer Website hinzufügen, wie in beschrieben [Hilfsprogramme installieren, in einer ASP.NET Web Pages-Website](https://go.microsoft.com/fwlink/?LinkId=252372), sofern Sie noch nicht geschehen.</span><span class="sxs-lookup"><span data-stu-id="29f30-152">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="29f30-153">Erstellen einer neuen Webseite mit dem Namen *Gravatar.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="29f30-153">Create a new web page named *Gravatar.cshtml*.</span></span>
3. <span data-ttu-id="29f30-154">Fügen Sie der Datei das folgende Markup hinzu:</span><span class="sxs-lookup"><span data-stu-id="29f30-154">Add the following markup to the file:</span></span> 

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample3.cshtml)]

    <span data-ttu-id="29f30-155">Die `Gravatar.GetHtml` Methode zeigt die Gravatar-Image auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="29f30-155">The `Gravatar.GetHtml` method displays the Gravatar image on the page.</span></span> <span data-ttu-id="29f30-156">Um die Größe des Bilds zu ändern, können Sie eine Zahl als zweiten Parameter einschließen.</span><span class="sxs-lookup"><span data-stu-id="29f30-156">To change the size of the image, you can include a number as a second parameter.</span></span> <span data-ttu-id="29f30-157">Die Standardgröße ist 80.</span><span class="sxs-lookup"><span data-stu-id="29f30-157">The default size is 80.</span></span> <span data-ttu-id="29f30-158">Zahlen von weniger als 80 stellen das Image kleiner.</span><span class="sxs-lookup"><span data-stu-id="29f30-158">Numbers less than 80 make the image smaller.</span></span> <span data-ttu-id="29f30-159">Die Anzahl ist größer als 80 das Bild vergrößert wird.</span><span class="sxs-lookup"><span data-stu-id="29f30-159">Numbers greater than 80 make the image larger.</span></span>
4. <span data-ttu-id="29f30-160">In der `Gravatar.GetHtml` Methoden ersetzen `<Your Gravatar account here>` mit der e-Mail-Adresse, die Sie für Ihr Konto Gravatar verwenden.</span><span class="sxs-lookup"><span data-stu-id="29f30-160">In the `Gravatar.GetHtml` methods, replace `<Your Gravatar account here>` with the email address that you use for your Gravatar account.</span></span> <span data-ttu-id="29f30-161">(Wenn Sie nicht über ein Gravatar-Konto verfügen, können Sie die e-Mail-Adresse einer Person, der die verwenden.)</span><span class="sxs-lookup"><span data-stu-id="29f30-161">(If you don't have a Gravatar account, you can use the email address of someone who does.)</span></span>
5. <span data-ttu-id="29f30-162">Führen Sie die Seite in Ihrem Browser.</span><span class="sxs-lookup"><span data-stu-id="29f30-162">Run the page in your browser.</span></span> <span data-ttu-id="29f30-163">Die Seite zeigt zwei Gravatar-Bilder für die e-Mail-Adresse, die Sie angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="29f30-163">The page displays two Gravatar images for the email address you specified.</span></span> <span data-ttu-id="29f30-164">Das zweite Bild ist kleiner als die erste.</span><span class="sxs-lookup"><span data-stu-id="29f30-164">The second image is smaller than the first.</span></span> 

    ![Abbildung 4](13-adding-social-networking-to-your-web-site/_static/image3.jpg)

<a id="Displaying_an_Xbox_Gamer_Card"></a>
## <a name="displaying-an-xbox-gamer-card"></a><span data-ttu-id="29f30-166">Anzeigen einer Spieler Xbox-Karte</span><span class="sxs-lookup"><span data-stu-id="29f30-166">Displaying an Xbox Gamer Card</span></span>

<span data-ttu-id="29f30-167">Wenn Personen Microsoft Xbox-online-Spiele spielen, hat jeder Benutzer eine eindeutige ID.</span><span class="sxs-lookup"><span data-stu-id="29f30-167">When people play Microsoft Xbox games online, each user has a unique ID.</span></span> <span data-ttu-id="29f30-168">Statistiken werden für jeden Spieler in Form einer Karte Spieler beibehalten, zeigt ihre Ruf, Spieler Bewertung und zuletzt Spiele gespielt.</span><span class="sxs-lookup"><span data-stu-id="29f30-168">Statistics are kept for each player in the form of a gamer card, which shows their reputation, gamer score, and recently played games.</span></span> <span data-ttu-id="29f30-169">Wenn Sie eine Xbox Spieler sind, können Sie Ihre Spiele Karte auf Seiten auf Ihrer Website anzeigen, indem Sie mit der `GamerCard` Helper.</span><span class="sxs-lookup"><span data-stu-id="29f30-169">If you're an Xbox gamer, you can show your gamer card on pages in your site by using the `GamerCard` helper.</span></span>

1. <span data-ttu-id="29f30-170">Die ASP.NET Web Helpers Library zu Ihrer Website hinzufügen, wie in beschrieben [Hilfsprogramme installieren, in einer ASP.NET Web Pages-Website](https://go.microsoft.com/fwlink/?LinkId=252372), sofern Sie noch nicht geschehen.</span><span class="sxs-lookup"><span data-stu-id="29f30-170">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="29f30-171">Erstellen Sie eine neue Seite mit dem Namen *XboxGamer.cshtml* und fügen Sie das folgende Markup hinzu.</span><span class="sxs-lookup"><span data-stu-id="29f30-171">Create a new page named *XboxGamer.cshtml* and add the following markup.</span></span>

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample4.cshtml)]

    <span data-ttu-id="29f30-172">Sie verwenden die `GamerCard.GetHtml` -Eigenschaft an den Alias für die Spieler Karte angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="29f30-172">You use the `GamerCard.GetHtml` property to specify the alias for the gamer card to be displayed.</span></span>
3. <span data-ttu-id="29f30-173">Führen Sie die Seite in Ihrem Browser.</span><span class="sxs-lookup"><span data-stu-id="29f30-173">Run the page in your browser.</span></span> <span data-ttu-id="29f30-174">Die Seite zeigt die Spiele Xbox-Karte, die Sie angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="29f30-174">The page displays the Xbox gamer card that you specified.</span></span>

    ![Abbildung 5](13-adding-social-networking-to-your-web-site/_static/image4.jpg)