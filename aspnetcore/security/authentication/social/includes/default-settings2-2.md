---
ms.openlocfilehash: 733a41a76e289f8aed6ec2d246ed720e44808fec
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57182760"
---
<span data-ttu-id="a124d-101">Der Aufruf von [AddIdentity](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionextensions.addidentity) konfiguriert die Einstellungen der Standard-Schema.</span><span class="sxs-lookup"><span data-stu-id="a124d-101">The call to [AddIdentity](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionextensions.addidentity) configures the default scheme settings.</span></span> <span data-ttu-id="a124d-102">Die [AddAuthentication(String)](/dotnet/api/microsoft.extensions.dependencyinjection.authenticationservicecollectionextensions.addauthentication#Microsoft_Extensions_DependencyInjection_AuthenticationServiceCollectionExtensions_AddAuthentication_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_String_) überladen, legt die [DefaultScheme](/dotnet/api/microsoft.aspnetcore.authentication.authenticationoptions.defaultscheme) Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="a124d-102">The [AddAuthentication(String)](/dotnet/api/microsoft.extensions.dependencyinjection.authenticationservicecollectionextensions.addauthentication#Microsoft_Extensions_DependencyInjection_AuthenticationServiceCollectionExtensions_AddAuthentication_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_String_) overload sets the [DefaultScheme](/dotnet/api/microsoft.aspnetcore.authentication.authenticationoptions.defaultscheme) property.</span></span> <span data-ttu-id="a124d-103">Die [AddAuthentication (Aktion&lt;authenticationoptions&gt;)](/dotnet/api/microsoft.extensions.dependencyinjection.authenticationservicecollectionextensions.addauthentication#Microsoft_Extensions_DependencyInjection_AuthenticationServiceCollectionExtensions_AddAuthentication_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_Action_Microsoft_AspNetCore_Authentication_AuthenticationOptions__) Überladung ermöglicht das Konfigurieren von Authentifizierungsoptionen, die zum Einrichten von standardmäßigen Authentifizierungsschemas für unterschiedliche Zwecke verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="a124d-103">The [AddAuthentication(Action&lt;AuthenticationOptions&gt;)](/dotnet/api/microsoft.extensions.dependencyinjection.authenticationservicecollectionextensions.addauthentication#Microsoft_Extensions_DependencyInjection_AuthenticationServiceCollectionExtensions_AddAuthentication_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_Action_Microsoft_AspNetCore_Authentication_AuthenticationOptions__) overload allows configuring authentication options, which can be used to set up default authentication schemes for different purposes.</span></span> <span data-ttu-id="a124d-104">Nachfolgende Aufrufe von `AddAuthentication` außer Kraft setzen, die zuvor konfigurierten [authenticationoptions](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions) Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="a124d-104">Subsequent calls to `AddAuthentication` override previously configured [AuthenticationOptions](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions) properties.</span></span>

<span data-ttu-id="a124d-105">[AuthenticationBuilder](/dotnet/api/microsoft.aspnetcore.authentication.authenticationbuilder) Erweiterungsmethoden, die registriert einen authentifizierungshandler für die können nur einmal pro Authentifizierungsschema aufgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="a124d-105">[AuthenticationBuilder](/dotnet/api/microsoft.aspnetcore.authentication.authenticationbuilder) extension methods that register an authentication handler may only be called once per authentication scheme.</span></span> <span data-ttu-id="a124d-106">Überladungen vorhanden sind, mit denen die Konfiguration von Eigenschaften für Schema, Name des Schemas und Anzeigename.</span><span class="sxs-lookup"><span data-stu-id="a124d-106">Overloads exist that allow configuring the scheme properties, scheme name, and display name.</span></span>