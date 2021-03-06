---
title: Problembehandlung bei ASP.NET Core in IIS
author: guardrex
description: Erfahren Sie, wie Sie Probleme mit IIS-Bereitstellungen (IIS = Internet Information Services) von ASP.NET Core-Apps diagnostizieren können.
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: host-and-deploy/iis/troubleshoot
ms.openlocfilehash: 2b23bf8230f7a1c207ef7870da098ffb0c597fd5
ms.sourcegitcommit: fc7eb4243188950ae1f1b52669edc007e9d0798d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2018
ms.locfileid: "51225446"
---
# <a name="troubleshoot-aspnet-core-on-iis"></a>Problembehandlung bei ASP.NET Core in IIS

Von [Luke Latham](https://github.com/guardrex)

Dieser Artikel enthält Anweisungen zum Diagnostizieren eines Startproblems der ASP.NET Core-App beim Hosten mithilfe von [Internet Information Services (IIS)](/iis). Die in diesem Artikel enthaltenen Informationen gelten für das Hosting in IIS unter Windows Server und Windows Desktop.

::: moniker range=">= aspnetcore-2.2"

In Visual Studio entspricht ein ASP.NET Core-Projekt standardmäßig dem [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)-Hosting während des Debuggens. Ein *502.5: Prozessfehler* oder ein *500.30: Startfehler*, der beim lokalen Debuggen auftritt, kann mithilfe der Hinweise in diesem Thema behoben werden.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

In Visual Studio entspricht ein ASP.NET Core-Projekt standardmäßig dem [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)-Hosting während des Debuggens. Ein *502.5: Prozessfehler*, der beim lokalen Debuggen auftritt, kann mithilfe der Hinweise in diesem Thema behoben werden.

::: moniker-end

Weitere Themen zur Problembehandlung:

<xref:host-and-deploy/azure-apps/troubleshoot>  
Obwohl App Service das [ASP.NET Core-Modul](xref:fundamentals/servers/aspnet-core-module) und IIS für das Hosten von Apps verwendet, finden Sie im dedizierten Thema weitere, für App Service spezifische Anweisungen.

<xref:fundamentals/error-handling>  
Informationen zur Behandlung von Fehlern in ASP.NET Core-Apps während der Bereitstellung auf einem lokalen System.

[Lernen Sie das Debuggen mit Visual Studio](/visualstudio/debugger/getting-started-with-the-debugger)  
In diesem Thema werden die Features des Visual Studio-Debuggers vorgestellt.

[Debuggen mit Visual Studio Code](https://code.visualstudio.com/docs/editor/debugging)  
Hier finden Sie weitere Informationen zur integrierten Debuggingunterstützung in Visual Studio Code.

## <a name="app-startup-errors"></a>App-Startfehler

**502.5: Prozessfehler**  
Der Workerprozess schlägt fehl. Die App wird nicht gestartet.

Das ASP.NET Core-Modul kann den .NET-Back-End-Prozess nicht starten. Die Ursache für einen Fehler beim Starten eines Prozesses kann in der Regel über Einträge im [Anwendungsereignisprotokoll](#application-event-log) und im [stdout-Protokoll des ASP.NET Core-Moduls](#aspnet-core-module-stdout-log) ermittelt werden. 

Eine allgemeine Fehlerbedingung ist, dass die App aufgrund einer Version des freigegebenen ASP.NET Core-Frameworks falsch konfiguriert ist, die nicht vorhanden ist. Überprüfen Sie, welche Versionen des freigegebenen ASP.NET Core-Frameworks auf dem Zielcomputer installiert sind.

Die Fehlerseite *502.5: Prozessfehler* wird zurückgegeben, wenn ein falsch konfiguriertes Hosting oder eine falsch konfigurierte App bewirkt, dass der Workerprozess fehlschlägt:

![Browserfenster mit der Seite „502.5: Prozessfehler“](troubleshoot/_static/process-failure-page.png)

::: moniker range=">= aspnetcore-2.2"

**500.30 In-Process-Startfehler**

Der Workerprozess schlägt fehl. Die App wird nicht gestartet.

Das ASP.NET Core-Modul kann den .NET Core-CLR-In-Process nicht starten. Die Ursache für einen Fehler beim Starten eines Prozesses kann in der Regel über Einträge im [Anwendungsereignisprotokoll](#application-event-log) und im [stdout-Protokoll des ASP.NET Core-Moduls](#aspnet-core-module-stdout-log) ermittelt werden. 

Eine allgemeine Fehlerbedingung ist, dass die App aufgrund einer Version des freigegebenen ASP.NET Core-Frameworks falsch konfiguriert ist, die nicht vorhanden ist. Überprüfen Sie, welche Versionen des freigegebenen ASP.NET Core-Frameworks auf dem Zielcomputer installiert sind.

**500.0 Fehler beim Laden des In-Process-Handlers**

Der Workerprozess schlägt fehl. Die App wird nicht gestartet.

Das ASP.NET Core-Modul kann die .NET Core-CLR und den In-Process-Anforderungshandler (*aspnetcorev2_inprocess.dll*) nicht finden. Überprüfen Sie Folgendes:

* Diese App legt entweder das NuGet-Paket [Microsoft.AspNetCore.Server.IIS](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IIS) oder das Metapaket [Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) als Ziel fest.
* Die Version des freigegebenen ASP.NET Core-Frameworks, die von der App als Ziel festgelegt ist, ist auf dem Zielcomputer installiert.

**500.0 Fehler beim Laden des Out-of-Process-Handlers**

Der Workerprozess schlägt fehl. Die App wird nicht gestartet.

Das ASP.NET Core-Modul kann den Out-of-Process-Hostinganforderungshandler nicht finden. Stellen Sie sicher, dass sich *aspnetcorev2_outofprocess.dll* in einem Unterordner mit *aspnetcorev2.dll* befindet. 

::: moniker-end

**500: Interner Serverfehler**  
Die App wird gestartet, aber ein Fehler verhindert, dass der Server auf die Anforderung eingeht.

Dieser Fehler tritt im Code der App während des Starts oder bei der Erstellung einer Antwort auf. Die Antwort enthält möglicherweise keinen Inhalt oder die Antwort wird als *500: Interner Serverfehler* im Browser angezeigt. Das Anwendungsereignisprotokoll gibt normalerweise an, dass die Anwendung normal gestartet wurde. Aus Sicht des Servers ist dies richtig. Die App wurde gestartet, sie kann jedoch keine gültige Antwort generieren. [Führen Sie die App in einer Eingabeaufforderung](#run-the-app-at-a-command-prompt) auf dem Server aus oder [aktivieren Sie das stdout-Protokoll des ASP.NET Core-Moduls](#aspnet-core-module-stdout-log), um das Problem zu beheben.

**Verbindungszurücksetzung**

Falls ein Fehler auftritt, nachdem die Header gesendet wurden, ist es zu spät für den Server, einen **500: Interner Serverfehler** zu senden, wenn ein Fehler auftritt. Dies ist häufig der Fall, wenn während der Serialisierung komplexer Objekte für eine Antwort ein Fehler auftritt. Diese Art von Fehler wird angezeigt, wenn ein *Verbindungszurücksetzungsfehler* auf dem Client auftritt. Mithilfe der [Anwendungsprotokollierung](xref:fundamentals/logging/index) können diese Fehlertypen behoben werden.

## <a name="default-startup-limits"></a>Standardstarteinschränkungen

Das ASP.NET Core-Modul wurde mit dem Standardwert 120 Sekunden für das *StartupTimeLimit* konfiguriert. Wenn der Standardwert beibehalten wird, dauert der Start einer App möglicherweise bis zu zwei Minuten. Erst danach kann das Modul einen Prozessfehler protokollieren. Weitere Informationen zum Konfigurieren des Moduls finden Sie unter [Attribute des aspNetCore-Elements](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element).

## <a name="troubleshoot-app-startup-errors"></a>Problembehandlung bei App-Startfehlern

### <a name="application-event-log"></a>Anwendungsereignisprotokoll

Greifen Sie auf das Anwendungsereignisprotokoll zu:

1. Öffnen Sie das Menü „Start“, suchen Sie nach der **Ereignisanzeige**, und wählen Sie anschließend die App **Ereignisanzeige** aus.
1. Öffnen Sie unter **Ereignisanzeige** den Knoten **Windows-Protokolle**.
1. Wählen Sie **Anwendung** aus, um das Anwendungsereignisprotokoll zu öffnen.
1. Suchen Sie nach Fehlern, die mit der fehlerhaften App im Zusammenhang stehen. Fehler weisen in der Spalte *Quelle* den Wert *IIS AspNetCore-Modul* oder *IIS Express AspNetCore-Modul* auf.

### <a name="run-the-app-at-a-command-prompt"></a>Ausführen der App in einer Eingabeaufforderung

Viele Startfehler erzeugen keine nützlichen Informationen im Anwendungsereignisprotokoll. Sie können die Ursache für einige Fehler ermitteln, indem Sie die App in einer Eingabeaufforderung auf dem Hostsystem ausführen.

**Framework-abhängige Bereitstellung**

Wenn es sich bei der App um eine [Framework-abhängige Bereitstellung handelt](/dotnet/core/deploying/#framework-dependent-deployments-fdd):

1. Navigieren Sie in einer Eingabeaufforderung zum Bereitstellungsordner und führen Sie die App aus, indem Sie die Assembly der App mit *dotnet.exe* ausführen. Ersetzen Sie in folgendem Befehl den Namen der Assembly der App durch \<assembly_name>: `dotnet .\<assembly_name>.dll`.
1. Die Konsolenausgabe der App, die Fehler anzeigt, wird in das Konsolenfenster geschrieben.
1. Wenn der Fehler während einer Anforderung an die App auftritt, führen Sie eine Anforderung an den Host und Port aus, auf dem Kestrel empfangsbereit ist. Führen Sie unter Verwendung der Standardhosts und -ports eine Anforderung für `http://localhost:5000/` aus. Wenn die App normalerweise auf die Kestrel-Endpunktadresse reagiert, hängt das Problem wahrscheinlich eher mit der Reverseproxykonfiguration und weniger mit der App selbst zusammen.

**Eigenständige Bereitstellung**

Wenn es sich bei der App um eine [eigenständige Bereitstellung](/dotnet/core/deploying/#self-contained-deployments-scd) handelt:

1. Navigieren Sie in einer Eingabeaufforderung zum Bereitstellungsordner und führen Sie die ausführbaren Dateien der App aus. Ersetzen Sie in folgendem Befehl den Namen der Assembly der App durch \<assembly_name>: `<assembly_name>.exe`.
1. Die Konsolenausgabe der App, die Fehler anzeigt, wird in das Konsolenfenster geschrieben.
1. Wenn der Fehler während einer Anforderung an die App auftritt, führen Sie eine Anforderung an den Host und Port aus, auf dem Kestrel empfangsbereit ist. Führen Sie unter Verwendung der Standardhosts und -ports eine Anforderung für `http://localhost:5000/` aus. Wenn die App normalerweise auf die Kestrel-Endpunktadresse reagiert, hängt das Problem wahrscheinlich eher mit der Reverseproxykonfiguration und weniger mit der App selbst zusammen.

### <a name="aspnet-core-module-stdout-log"></a>stdout-Protokoll des ASP.NET Core-Moduls

So aktivieren Sie stdout-Protokolle und zeigen diese an:

1. Navigieren Sie zum Bereitstellungsordner der Website auf dem Hostsystem.
1. Erstellen Sie den Ordner *logs*, wenn dieser nicht vorhanden ist. Anweisungen zum Aktivieren von MSBuild für die automatische Erstellung des Ordners *logs* in der Bereitstellung finden Sie im Thema [Verzeichnisstruktur](xref:host-and-deploy/directory-structure).
1. Bearbeiten Sie die Datei *web.config*. Legen Sie **stdoutLogEnabled** auf `true` fest, und ändern Sie den Pfad von **stdoutLogFile** so, dass auf den Ordner *logs* verwiesen wird (Beispiel: `.\logs\stdout`). `stdout` im Pfad ist das Präfix des Protokolldateinamens. Ein Zeitstempel, eine Prozess-ID und eine Dateierweiterung werden bei der Protokollerstellung automatisch hinzugefügt. Mit `stdout` als Präfix des Dateinamens wird eine typische Protokolldatei als *stdout_20180205184032_5412.log* benannt. 
1. Stellen Sie sicher, dass die Identität des Anwendungspools über Schreibberechtigungen für den Ordner *Protokolle* verfügt.
1. Speichern Sie die aktualisierte Datei *web.config*.
1. Führen Sie eine Anforderung an die App aus.
1. Navigieren Sie zu dem Ordner *logs*. Suchen und öffnen Sie das aktuelle stdout-Protokoll.
1. Untersuchen Sie das Protokoll auf Fehler.

**Wichtig** Deaktivieren Sie die stdout-Protokollierung, wenn die Problembehandlung abgeschlossen ist.

1. Bearbeiten Sie die Datei *web.config*.
1. Legen Sie **stdoutLogEnabled** auf `false` fest.
1. Speichern Sie die Datei.

> [!WARNING]
> Wenn das stdout-Protokoll nicht deaktiviert wird, können App- oder Serverfehler auftreten. Für die Protokollgröße oder die Anzahl von erstellten Protokolldateien ist kein Grenzwert festgelegt.
>
> Verwenden Sie für die routinemäßige Protokollierung in einer ASP.NET Core-App eine Protokollierungsbibliothek, die die Protokolldateigröße beschränkt und die Protokolle rotiert. Weitere Informationen finden Sie im Artikel zur [Protokollierung von Drittanbietern](xref:fundamentals/logging/index#third-party-logging-providers).

## <a name="enabling-the-developer-exception-page"></a>Aktivieren der Seite mit Ausnahmen für Entwickler

Die `ASPNETCORE_ENVIRONMENT` [Umgebungsvariable kann zur Datei web.config hinzugefügt werden](xref:host-and-deploy/aspnet-core-module#setting-environment-variables), um die App in der Entwicklungsumgebung auszuführen. Solange die Umgebung nicht beim Starten der App von `UseEnvironment` im Host-Builder außer Kraft gesetzt wird, kann die [Seite mit Ausnahmen für Entwickler](xref:fundamentals/error-handling) durch Festlegen der Umgebungsvariable angezeigt werden, wenn die App ausgeführt wird.

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile=".\logs\stdout">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
  </environmentVariables>
</aspNetCore>
```

Das Festlegen der Umgebungsvariablen für `ASPNETCORE_ENVIRONMENT` wird nur bei der Verwendung von Staging- und Testservern empfohlen, die nicht für das Internet verfügbar gemacht werden. Entfernen Sie nach der Fehlerbehebung die Umgebungsvariable aus der Datei *web.config*. Informationen zum Festlegen von Umgebungsvariablen in der Datei *web.config* finden Sie unter [Untergeordnetes environmentVariables-Element von aspNetCore](xref:host-and-deploy/aspnet-core-module#setting-environment-variables).

## <a name="common-startup-errors"></a>Häufige Startfehler 

Siehe <xref:host-and-deploy/azure-iis-errors-reference>. Die meisten der häufig auftretenden Probleme, die den Start von Apps verhindern, werden im Referenzartikel behandelt.

## <a name="slow-or-hanging-app"></a>Langsame oder hängende App

Wenn eine App bei einer Anforderung langsam reagiert oder hängt, rufen Sie eine [Dumpdatei](/visualstudio/debugger/using-dump-files) ab und analysieren diese. Dumpdateien können mit einem der folgenden Tools abgerufen werden:

* [ProcDump](/sysinternals/downloads/procdump)
* [DebugDiag](https://www.microsoft.com/download/details.aspx?id=49924)
* WinDbg: [Herunterladen von Debugtools für Windows](https://developer.microsoft.com/windows/hardware/download-windbg), [Debuggen mit WinDbg](/windows-hardware/drivers/debugger/debugging-using-windbg)

## <a name="remote-debugging"></a>Remotedebuggen

Siehe [Remotedebuggen von ASP.NET Core auf einem IIS-Remotecomputer in Visual Studio 2017](/visualstudio/debugger/remote-debugging-aspnet-on-a-remote-iis-computer) in der Dokumentation zu Visual Studio.

## <a name="application-insights"></a>Application Insights

[Application Insights](/azure/application-insights/) stellt Telemetriedaten von Apps bereit, die von IIS gehostet werden, einschließlich Features für die Fehlerprotokollierung und die Berichterstellung. Application Insights kann nur Fehler melden, die nach dem Start der App auftreten, wenn die Protokollierungsfeatures der App verfügbar werden. Weitere Informationen finden Sie unter [Application Insights for ASP.NET Core (Application Insights für ASP.NET Core)](/azure/application-insights/app-insights-asp-net-core).

## <a name="additional-troubleshooting-advice"></a>Weitere Hinweise zur Problembehandlung

Manchmal schlägt eine funktionsfähige App direkt nach der Durchführung eines Upgrades des .NET Core SDK auf dem Entwicklungscomputer oder der Paketversionen in der App fehl. In einigen Fällen können inkohärente Pakete eine App beschädigen, wenn größere Upgrades durchgeführt werden. Die meisten dieser Probleme können durch Befolgung der folgenden Anweisungen behoben werden:

1. Löschen Sie die Ordner *bin* und *obj*.
1. Löschen Sie die Paketcaches unter *%UserProfile%\\.nuget\\packages* und *%LocalAppData%\\Nuget\\v3-cache*.
1. Stellen Sie das Projekt wieder her und erstellen Sie es neu.
1. Überprüfen Sie, ob die vorherige Bereitstellung auf dem Server vollständig gelöscht wurde, bevor Sie die App erneut bereitstellen.

> [!TIP]
> Sie können Paketcaches ganz einfach löschen, indem Sie `dotnet nuget locals all --clear` über eine Eingabeaufforderung ausführen.
> 
> Darüber hinaus können Paketcaches mit dem Tool [nuget.exe](https://www.nuget.org/downloads) und durch Ausführung des Befehls `nuget locals all -clear` gelöscht werden. *nuget.exe* ist wird unter dem Windows Desktop-Betriebssystem nicht gebündelt installiert und muss separat von der [NuGet-Website](https://www.nuget.org/downloads) abgerufen werden.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* <xref:fundamentals/error-handling>
* <xref:host-and-deploy/azure-iis-errors-reference>
* <xref:host-and-deploy/aspnet-core-module>
* <xref:host-and-deploy/azure-apps/troubleshoot>
