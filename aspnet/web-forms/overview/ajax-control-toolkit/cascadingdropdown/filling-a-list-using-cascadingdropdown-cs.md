---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
title: Ausfüllen einer Liste mit CascadingDropDown (c#) | Microsoft-Dokumentation
author: wenz
description: Das Steuerelement "CascadingDropDown" im AJAX Control Toolkit erweitert ein DropDownList-Steuerelement, sodass Änderungen in einer DropDownList lädt Werte in Anoth verknüpft...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f949aafa-fe57-43b0-b722-f0dd33a900be
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 795b2a2ee80d3d2bed6f752887d5f9d974151a56
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831983"
---
<a name="filling-a-list-using-cascadingdropdown-c"></a>Ausfüllen einer Liste mit CascadingDropDown (c#)
====================
durch [Christian Wenz](https://github.com/wenz)

[Code herunterladen](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)

> Das Steuerelement "CascadingDropDown" im AJAX Control Toolkit erweitert ein DropDownList-Steuerelement, sodass Änderungen in einer DropDownList lädt Werte in einer anderen DropDownList verknüpft ist. (Z. B. eine Liste enthält eine Liste der US-Staaten und die folgenden Liste wird dann mit der größten Städte in diesem Zustand gefüllt.) Die erste Herausforderung lösen werden tatsächlich eine Dropdownliste mit diesem Steuerelement geben.


## <a name="overview"></a>Übersicht

Das Steuerelement "CascadingDropDown" im AJAX Control Toolkit erweitert ein DropDownList-Steuerelement, sodass Änderungen in einer DropDownList lädt Werte in einer anderen DropDownList verknüpft ist. (Z. B. eine Liste enthält eine Liste der US-Staaten und die folgenden Liste wird dann mit der größten Städte in diesem Zustand gefüllt.) Die erste Herausforderung lösen werden tatsächlich eine Dropdownliste mit diesem Steuerelement geben.

## <a name="steps"></a>Schritte

Um die Funktionalität von ASP.NET AJAX und das Steuerelement-Toolkit, aktivieren die `ScriptManager` Steuerelement an einer beliebigen Stelle auf der Seite platziert werden muss (jedoch innerhalb der `<form>` Element):

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample1.aspx)]

Anschließend ist ein DropDownList-Steuerelement erforderlich:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample2.aspx)]

Für diese Liste wird ein CascadingDropDown-Extender hinzugefügt. Eine asynchrone Anforderung sendet an einen Webdienst die klicken Sie dann eine Liste mit Einträgen in der Liste anzuzeigende zurückgibt. Damit dies funktioniert müssen die folgenden CascadingDropDown Attribute festgelegt werden:

- `ServicePath`: Die URL eines Webdiensts, der Einträge in der Liste bereitstellen
- `ServiceMethod`: Bereitstellen der Einträge in der Liste Web-Methode
- `TargetControlID`: Die ID von der Dropdown-Liste
- `Category`: Kategorie Informationen, die beim Aufruf der Web-Methode übermittelt wird
- `PromptText`: Der Text angezeigt wird, wenn Sie Daten aus der Liste asynchron vom Server geladen

Dies ist das Markup für die `CascadingDropDown` Element. Der einzige Unterschied zwischen c# und VB ist der Name des zugeordneten Webdiensts:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample3.aspx)]

Der JavaScript-Code, der von der `CascadingDropDown` Extender Aufrufen eine Webdienstmethode mit folgender Signatur:

[!code-csharp[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample4.cs)]

Damit der wichtigste Aspekt ist, dass die Methode ein Array vom Typ zurückgeben muss `CascadingDropDownNameValue` (definiert durch die ASP.NET AJAX Control Toolkit). In der `CascadingDropDownNameValue` Konstruktor, der erste Eintrag in der der Text, und klicken Sie dann seinen Wert angegeben werden müssen, ebenso wie `<option value="VALUE">NAME</option>` in HTML tun würden. Hier sind einige Beispieldaten:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample5.aspx)]

Die Seite im Browser laden, löst die Liste mit drei Anbietern gefüllt werden soll.


[![Die Liste wird automatisch ausgefüllt.](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)

Die Liste wird automatisch übernommen ([klicken Sie, um das Bild in voller Größe anzeigen](filling-a-list-using-cascadingdropdown-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Nächste](using-cascadingdropdown-with-a-database-cs.md)
