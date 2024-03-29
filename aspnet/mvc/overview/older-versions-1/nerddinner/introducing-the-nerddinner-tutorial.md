---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: Einführung zum NerdDinner-Tutorial | Microsoft-Dokumentation
author: shanselman
description: Die beste Möglichkeit, erfahren, ein neues Framework ist etwas damit zu erstellen. In diesem Tutorial erläutert, wie Sie eine kleine, aber abgeschlossen ist,-Anwendung, die mithilfe von P.NET-Konfiguration erstellen...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 154cfe6694cf723c0a1f8e33bfdb42c97594518f
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/06/2019
ms.locfileid: "65122321"
---
# <a name="introducing-the-nerddinner-tutorial"></a>Einführung zum NerdDinner-Tutorial

durch [Scott Hanselman](https://github.com/shanselman)

[PDF herunterladen](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Die beste Möglichkeit, erfahren, ein neues Framework ist etwas damit zu erstellen. Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer kleines, aber abgeschlossen haben, Anwendung, die mithilfe von ASP.NET MVC-1, und eine Einführung in die wichtigsten Konzepte.
> 
> Wenn Sie ASP.NET MVC 3 verwenden, sollten Sie Sie folgen den [erste Schritte mit MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) oder [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) Tutorials.

## <a name="nerddinner-tutorial"></a>NerdDinner Tutorial

Die beste Möglichkeit, erfahren, ein neues Framework ist etwas damit zu erstellen. Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer kleines, aber abgeschlossen haben, Anwendung, die mit ASP.NET MVC, und eine Einführung in die wichtigsten Konzepte.

Die Anwendung zum Erstellen der hier verwendeten heißt "NerdDinner". NerdDinner bietet eine einfache Möglichkeit für Benutzer zum Suchen und Organisieren von Dinner online:

![](introducing-the-nerddinner-tutorial/_static/image1.png)

NerdDinner kann registrierte Benutzer erstellen, bearbeiten und Löschen von Dinner. Einen konsistenten Satz von Überprüfung und Geschäftsregeln erzwungen für die Anwendung:

![](introducing-the-nerddinner-tutorial/_static/image2.png)

Besucher können eine AJAX-basierten Zuordnung verwenden, um nach bevorstehenden Dinner verwendet wird, treten in der Nähe von ihnen zu suchen:

![](introducing-the-nerddinner-tutorial/_static/image3.png)

Durch Klicken auf einem Dinner gelangen sie auf eine Detailseite, erhalten sie weitere Informationen:

![](introducing-the-nerddinner-tutorial/_static/image4.png)

Wenn sie Ihre Teilnahme an der Dinner können auf der Website registrieren oder anmelden:

![](introducing-the-nerddinner-tutorial/_static/image5.png)

Sie können eine AJAX-basierte RSVP-Link, um das Ereignis teilnehmen klicken Sie dann auf:

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a>NerdDinner implementieren

Wir werden unsere NerdDinner-Anwendung beginnen Sie mit der Datei -&gt;Befehl für neues Projekt in Visual Studio zum Erstellen eines neuen ASP.NET MVC-Projekts. Es wird schrittweise Funktionen und Features hinzugefügt. Dabei werden folgende Themen behandelt:

1. [Vorgehensweise: Erstellen Sie ein neues ASP.NET MVC-Projekt](create-a-new-aspnet-mvc-project.md)
2. [Gewusst wie: Erstellen einer Datenbank](create-a-database.md)
3. [Gewusst wie: Erstellen eines Modells mit geschäftsregelüberprüfungen](build-a-model-with-business-rule-validations.md)
4. [Wie Sie die Controller und Ansichten verwenden, um eine Liste/Details-Benutzeroberfläche zu implementieren.](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [Gewusst wie: Bereitstellen von CRUD (erstellen, lesen, aktualisieren und löschen) Daten bilden Eintrag-Unterstützung](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [Das Verwenden von "ViewData" und Implementieren von ViewModel-Klassen](use-viewdata-and-implement-viewmodel-classes.md)
7. [Gewusst wie: Verwenden Sie die Benutzeroberfläche mit Masterseiten und teilausführungen erneut](re-use-ui-using-master-pages-and-partials.md)
8. [Gewusst wie: Implementieren von effizienten datenauslagerung](implement-efficient-data-paging.md)
9. [So sichern Sie Anwendungen mithilfe von Authentifizierung und Autorisierung](secure-applications-using-authentication-and-authorization.md)
10. [Bereitstellen von dynamischen Updates mit AJAX](use-ajax-to-deliver-dynamic-updates.md)
11. [Gewusst wie: AJAX zu verwenden, um Szenarios zu implementieren.](use-ajax-to-implement-mapping-scenarios.md)
12. [Automatisierte Komponententests aktivieren](enable-automated-unit-testing.md)

Sie können Ihr eigenes Exemplar des NerdDinner Erstellen von Grund auf neu, durch die Durchführung der einzelnen führen wir die exemplarische Vorgehensweise in diesem Kapitel. Alternativ können Sie eine abgeschlossene Version des Quellcodes hier herunterladen: [NerdDinner auf GitHub](https://github.com/AspNetMVPSamples/NerdDinner). Sie können optional auch auch [Herunterladen einer kostenlosen PDF-Version dieses Tutorials](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) sollten Sie das Tutorial offline zu lesen.

Sie können Visual Studio 2008 oder die kostenlose Visual Web Developer 2008 Express verwenden, um die Anwendung zu erstellen. Sie können entweder SQL Server oder die kostenlose SQL Server Express für die Datenbank verwenden.

Sie können ASP.NET MVC, Visual Web Developer 2008 Express und SQL Server Express (kostenlos) mithilfe von Version 2 der installieren die [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)

### <a name="now-lets-get-started"></a>Jetzt lassen Sie uns loslegen...

Nun, da wir die neuerungen NerdDinner behandelt habe, wir unsere Ärmel, und Schreiben von Code.

Wir beginnen mit Datei -&gt;neues Projekt in Visual Studio die NerdDinner-Anwendung zu erstellen.

> [!div class="step-by-step"]
> [Nächste](create-a-new-aspnet-mvc-project.md)
