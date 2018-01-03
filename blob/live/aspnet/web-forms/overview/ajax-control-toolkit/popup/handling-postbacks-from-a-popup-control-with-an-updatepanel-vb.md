---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
title: Behandlung von Postbacks aus einem Popupsteuerelement mit UpdatePanel (VB) | Microsoft Docs
author: wenz
description: "Der Extender PopupControl im AJAX Control Toolkit bietet eine einfache Möglichkeit, um ein Popup auszulösen, wenn es sich bei jedem anderen Steuerelement aktiviert wird. Besondere Sorgfalt hat auszuführende..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: ec9db57c-9f68-402a-bf4c-0d63d5f6908e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: 4445437f25925429d240b7fe2d019855afc52fe0
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/10/2017
---
<a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-vb"></a><span data-ttu-id="6c33e-104">Behandlung von Postbacks aus einem Popupsteuerelement mit UpdatePanel (VB)</span><span class="sxs-lookup"><span data-stu-id="6c33e-104">Handling Postbacks from A Popup Control With an UpdatePanel (VB)</span></span>
====================
<span data-ttu-id="6c33e-105">durch [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6c33e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6c33e-106">[Herunterladen von Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip) oder [PDF herunterladen](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="6c33e-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)</span></span>

> <span data-ttu-id="6c33e-107">Der Extender PopupControl im AJAX Control Toolkit bietet eine einfache Möglichkeit, um ein Popup auszulösen, wenn es sich bei jedem anderen Steuerelement aktiviert wird.</span><span class="sxs-lookup"><span data-stu-id="6c33e-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="6c33e-108">Besondere Sorgfalt muss ausgeführt werden, wenn ein Postback solche ein Popup erfolgt.</span><span class="sxs-lookup"><span data-stu-id="6c33e-108">Special care has to be taken when a postback occurs within such a popup.</span></span>


## <a name="overview"></a><span data-ttu-id="6c33e-109">Übersicht</span><span class="sxs-lookup"><span data-stu-id="6c33e-109">Overview</span></span>

<span data-ttu-id="6c33e-110">Der Extender PopupControl im AJAX Control Toolkit bietet eine einfache Möglichkeit, um ein Popup auszulösen, wenn es sich bei jedem anderen Steuerelement aktiviert wird.</span><span class="sxs-lookup"><span data-stu-id="6c33e-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="6c33e-111">Besondere Sorgfalt muss ausgeführt werden, wenn ein Postback solche ein Popup erfolgt.</span><span class="sxs-lookup"><span data-stu-id="6c33e-111">Special care has to be taken when a postback occurs within such a popup.</span></span>

## <a name="steps"></a><span data-ttu-id="6c33e-112">Schritte</span><span class="sxs-lookup"><span data-stu-id="6c33e-112">Steps</span></span>

<span data-ttu-id="6c33e-113">Bei Verwendung einer `PopupControl` mit einem Postback ein `UpdatePanel` können verhindern, dass die Seite-Aktualisierung, die durch das Postback verursacht.</span><span class="sxs-lookup"><span data-stu-id="6c33e-113">When using a `PopupControl` with a postback, an `UpdatePanel` can prevent the page refresh caused by the postback.</span></span> <span data-ttu-id="6c33e-114">Das folgende Markup definiert eine Reihe von wichtigen Elemente:</span><span class="sxs-lookup"><span data-stu-id="6c33e-114">The following markup defines a couple of important elements:</span></span>

- <span data-ttu-id="6c33e-115">Ein `ScriptManager` steuern, sodass das ASP.NET AJAX-Steuerelement-Toolkit funktioniert</span><span class="sxs-lookup"><span data-stu-id="6c33e-115">A `ScriptManager` control so that the ASP.NET AJAX Control Toolkit works</span></span>
- <span data-ttu-id="6c33e-116">Zwei `TextBox` steuert, welche sowohl ein Popup ausgelöst werden</span><span class="sxs-lookup"><span data-stu-id="6c33e-116">Two `TextBox` controls which will both trigger a popup</span></span>
- <span data-ttu-id="6c33e-117">Ein `Panel` Steuerelement, das als das Popup fungieren soll</span><span class="sxs-lookup"><span data-stu-id="6c33e-117">A `Panel` control that will serve as the popup</span></span>
- <span data-ttu-id="6c33e-118">Innerhalb des Bereichs einer `Calendar` Steuerelement eingebettet ist ein `UpdatePanel` Steuerelement</span><span class="sxs-lookup"><span data-stu-id="6c33e-118">Within the panel, a `Calendar` control is embedded within an `UpdatePanel` control</span></span>
- <span data-ttu-id="6c33e-119">Zwei `PopupControlExtender` Steuerelemente, die im Bereich der Textfelder zuweisen</span><span class="sxs-lookup"><span data-stu-id="6c33e-119">Two `PopupControlExtender` controls that assign the panel to the text boxes</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample1.aspx)]

<span data-ttu-id="6c33e-120">Beachten Sie, dass die `OnSelectionChanged` Attribut von der `Calendar` Steuerelement festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="6c33e-120">Note that the `OnSelectionChanged` attribute of the `Calendar` control is set.</span></span> <span data-ttu-id="6c33e-121">Damit ein Postback tritt auf, wenn der Benutzer ein Datum im Kalender auswählt, und die serverseitige Methode `c1_SelectionChanged()` ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="6c33e-121">So when the user selects a date within the calendar, a postback occurs and the server-side method `c1_SelectionChanged()` is executed.</span></span> <span data-ttu-id="6c33e-122">Innerhalb dieser Methode muss das aktuelle Datum abgerufen und zurück in das Textfeld geschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="6c33e-122">Within that method, the current date must be retrieved and written back to the textbox.</span></span>

<span data-ttu-id="6c33e-123">Die Syntax lautet wie folgt: Erstens einen Proxy-Objekt für die `PopupControlExtender` auf der Seite generiert werden muss.</span><span class="sxs-lookup"><span data-stu-id="6c33e-123">The syntax for that is as follows: First of all, a proxy object for the `PopupControlExtender` on the page must be generated.</span></span> <span data-ttu-id="6c33e-124">Das ASP.NET AJAX-Steuerelement-Toolkit bietet die `GetProxyForCurrentPopup()` Methode.</span><span class="sxs-lookup"><span data-stu-id="6c33e-124">The ASP.NET AJAX Control Toolkit offers the `GetProxyForCurrentPopup()` method.</span></span> <span data-ttu-id="6c33e-125">Das Objekt, diese Methode gibt, unterstützt die `Commit()` Methode einen Wert an das Steuerelement gesendet wird, die das Popup (nicht das Steuerelement, das dem Aufruf der Methode ausgelöst!) ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="6c33e-125">The object this method returns supports the `Commit()` method which sends a value back to the control that triggered the popup (not the control that triggered the method call!).</span></span> <span data-ttu-id="6c33e-126">Der folgende Code stellt das ausgewählte Datum als Argument für die `Commit()` -Methode, sodass des Codes zum Zurückschreiben von des ausgewählten Datums in das Textfeld:</span><span class="sxs-lookup"><span data-stu-id="6c33e-126">The following code provides the selected date as the argument for the `Commit()` method, causing the code to write the selected date back to the text box:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample2.aspx)]

<span data-ttu-id="6c33e-127">Jetzt immer an einem Kalenderdatum klicken Sie auf das ausgewählte Datum angezeigt wird, klicken Sie im zugehörigen Textfeld kann ein Datumsauswahl-Steuerelement erstellen, die derzeit auf vielen Websites gefunden werden.</span><span class="sxs-lookup"><span data-stu-id="6c33e-127">Now whenever you click on a calendar date, the selected date appears in the associated text box, creating a date picker control that can currently be found on many websites.</span></span>


<span data-ttu-id="6c33e-128">[![Der Kalender wird angezeigt, wenn der Benutzer in das Textfeld klickt](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6c33e-128">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)</span></span>

<span data-ttu-id="6c33e-129">Der Kalender wird angezeigt, wenn der Benutzer in das Textfeld klickt ([klicken Sie hier, um das Bild in voller Größe angezeigt](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="6c33e-129">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png))</span></span>


<span data-ttu-id="6c33e-130">[![Durch Klicken auf ein Datum in das Textfeld eingefügt](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="6c33e-130">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)</span></span>

<span data-ttu-id="6c33e-131">Durch Klicken auf ein Datum in das Textfeld eingefügt ([klicken Sie hier, um das Bild in voller Größe angezeigt](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="6c33e-131">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png))</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="6c33e-132">[Zurück](using-multiple-popup-controls-vb.md)
[Weiter](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)</span><span class="sxs-lookup"><span data-stu-id="6c33e-132">[Previous](using-multiple-popup-controls-vb.md)
[Next](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)</span></span>