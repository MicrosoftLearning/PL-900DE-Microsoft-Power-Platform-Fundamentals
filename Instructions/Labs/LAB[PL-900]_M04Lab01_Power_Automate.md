---
lab:
    title: 'Lab 6: Erstellen einer automatisierten Lösung'
    module: 'Modul 4: Erste Schritte mit Power Automate'
---

# Modul 4: Erste Schritte mit Power Automate
## Lab: Erstellen einer automatisierten Lösung

Szenario
========

Das Bellows College ist eine Bildungsorganisation mit mehreren Gebäuden auf dem Campus. Campusbesucher werden derzeit auf Papier erfasst. Die Informationen werden nicht konsistent erfasst und es gibt keine Möglichkeit, Daten über die Besuche auf dem gesamten Campus zu sammeln und zu analysieren. 

Die Campusverwaltung möchte ihr Besucherregistrierungssystem modernisieren, wobei der Zugang zu den Gebäuden von Sicherheitspersonal kontrolliert werden soll und alle Besuche von den entsprechenden Gastgebern zuvor registriert und aufgezeichnet werden müssen.

Während dieses Kurses erstellen Sie Anwendungen und führen eine Automatisierung durch, damit das Verwaltungs- und Sicherheitspersonal des Bellows College den Zugang zu den Gebäuden auf dem Campus verwalten und kontrollieren kann. 

In diesem Lab erstellen Sie Power Automate-Flows, um verschiedene Aspekte der Campusverwaltung zu automatisieren. 

Weiterführende Schritte des Lab
======================

Sie müssen die folgenden Anforderungen implementieren, um das Projekt abzuschließen.

* Der jedem Besucher zugewiesene eindeutige Code muss diesem vor seinem Besuch zur Verfügung gestellt werden.
* Das Sicherheitspersonal muss Benachrichtigungen erhalten, wenn Besucher ihre geplanten Zeitfenster überschreiten.

## Voraussetzungen

* Beendigung von **Modul 0 Lab 0 – Lab-Umgebung überprüfen**
* Beendigung von **Modul 2 Lab 1 – Einführung in Common Data Service**
* Campusmitarbeiter-App, erstellt in **Modul 3, Lab 2 – Erstellen einer Canvas-App, Teil 2** (zum Testen)
* John Doe-Kontakt, erstellt mit einer persönlichen E-Mail-Adresse in **Modul 3, Lab 4 – Erstellen einer modellgesteuerten App** (zum Testen)

Vor dem Beginn zu beachtende Dinge
-----------------------------------

-   Welcher Verteilungsmechanismus ist für die Besuchercodes am besten geeignet?
-   Wie können Überschreitungen gemessen und strenge Richtlinien durchgesetzt werden?

Übung Nr. 1: Einen Besuchsbenachrichtigungsfluss erstellen
===============================

**Ziel:** In dieser Übung erstellen Sie einen Power Automate-Flow, der die Anforderung implementiert. Dem Besucher sollte eine E-Mail gesendet werden, die den eindeutigen Code enthält, der dem Besuch zugewiesen ist.

Aufgabe Nr. 1: Flow erstellen
---------------------------

1.  Öffnen Sie Ihre Campusverwaltung-Lösung.

    -   Anmelden bei <https://make.powerapps.com>

    -   Wählen Sie Ihre **Umgebung** aus.

    -   Wählen Sie **Lösungen** aus.

    -   Klicken Sie, um Ihre **Campusverwaltung**-Lösung zu öffnen.

2.  Klicken Sie auf  **Neu** und wählen Sie  **Flow** aus. Dadurch wird der Power Automate-Flow-Editor in einem neuen Fenster geöffnet.

3. Suchen Sie nach *Aktuell* und wählen Sie **Common Data Service (aktuelle Umgebung)** aus.

4. Wählen Sie den Trigger **Wenn ein Datensatz erstellt, aktualisiert oder gelöscht wird** aus.

   * Wählen Sie**Erstellen** für **Triggerbedingung**
   
   * Wählen Sie **Besuche** als **Entitätsnamen** aus
   
   * Wählen Sie im **Bereich** **Organisation** aus
   
   * Klicken Sie im Triggerschritt auf die Schaltfläche mit den drei Punkten (**...**), und klicken Sie auf **Umbenennen**. Benennen Sie diesen Trigger in **„Wenn ein Besuch erstellt wird“** um. Dies ist eine gute Vorgehensweise, damit Sie und andere Flow-Editoren den Zweck des Schritts erkennen können, ohne tiefer in die Details gehen zu müssen.

5.  Klicken Sie auf **Neuer Schritt**. Dieser Schritt ist erforderlich, um Besucherinformationen einschließlich der E-Mail-Adresse abzurufen.

6. Suchen Sie nach *Aktuell* und wählen Sie **Common Data Service (aktuelle Umgebung)** aus.

7. Wählen Sie die Aktion **Einen Datensatz abrufen** aus. 

   * Wählen Sie **Kontakte** als **Entitätsname** aus
   
   * Fügen Sie im Feld **Element-ID** den Eintrag **Besucher (Wert)** aus der Liste für dynamische Inhalte aus.
   
   * Klicken Sie bei dieser Aktion auf die Schaltfläche mit den drei Punkten (**...**), und klicken Sie auf **Umbenennen**. Benennen Sie diese Aktion in **„Den Besucher abrufen“** um. Dies ist eine gute Vorgehensweise, damit Sie und andere Flow-Editoren den Zweck des Schritts erkennen können, ohne tiefer in die Details gehen zu müssen.

8. Klicken Sie auf **Neuer Schritt**. Dies ist der Schritt, in dem eine E-Mail erstellt und an den Besucher gesendet wird.

9. Suchen Sie nach *E-Mail*, wählen Sie den **E-Mail**-Connector und dann die Aktion **E-Mail-Benachrichtigung senden** aus. 

   * Wenn Sie aufgefordert werden, die Nutzungsbedingungen für diese Aktion zu akzeptieren, klicken Sie auf **Akzeptieren**.
   
   * Wählen Sie das Feld **An** aus, und wählen Sie **E-Mail** aus der Liste für dynamische Inhalte aus. Beachten Sie, dass sich diese unterhalb der grauen Kopfzeile **Den Besucher abrufen** befindet. Das bedeutet, dass Sie die E-Mail-Adresse auswählen, die zu dem Besucher gehört, den Sie im vorherigen Schritt nachgeschlagen haben. 

   * Geben Sie **Ihr geplanter Besuch am Bellows College** in das Feld **Betreff** ein.

   * Geben Sie den folgenden Text in **E-Mail-Text** ein:  
        
        > Dynamischer Inhalt muss dort platziert werden, wo Feldernamen in Klammern angegeben sind. Es wird empfohlen, zuerst den gesamten Text zu kopieren und einzufügen und dann dynamischen Inhalt an den richtigen Stellen hinzuzufügen.*
   
        ```
        Hallo {First Name},

        für Ihren Besuch auf dem Bellows Campus wurde der Zeitraum von {Scheduled Start} bis {Scheduled End} vermerkt.

        Ihr Sicherheitscode lautet {Code}. Bitte geben Sie ihn nicht weiter! Sie müssen diesen Code während Ihres Besuchs erzeugen.

        Mit freundlichen Grüßen

        Campusverwaltung
        Bellows College
        ```
   
10.  Wählen Sie oben den Flow-Namen **Ohne Titel** aus, und benennen Sie ihn in `Besuchsbenachrichtigung` um.

11. Wählen Sie **Speichern** aus

    Lassen Sie die Registerkarte dieses Flows für die nächste Aufgabe geöffnet. Ihr Flow sollte in etwa wie folgt aussehen:

![Power Automate-Besucherbenachrichtigungs-Flow](media/4-power-automate-notify.png)

Aufgabe Nr. 2: Flow überprüfen und aktivieren
--------------------------------

1.  Öffnen Sie in Ihrem Browser eine neue Registerkarte, und navigieren Sie zu <https://make.powerapps.com>.

2.  Klicken Sie auf **Apps**, und wählen Sie die **Campus-Mitarbeiter**-App aus, die Sie erstellt haben.

3.  Lassen Sie diese Registerkarte geöffnet, und navigieren Sie wieder zurück zu der vorherigen Registerkarte mit Ihrem Flow. 

4.  Klicken Sie in der Befehlsleiste auf **Testen**. Wählen Sie **Ich werde die Triggeraktion ausführen** und dann auf **Speichern und testen**.

5.  Lassen Sie die Flow-Registerkarte geöffnet, und navigieren Sie wieder zurück zur vorherigen Registerkarte mit der **Campus-Mitarbeiter**-App.

6.  Klicken Sie auf **+**, um einen neuen Datensatz hinzuzufügen.

7.  Geben Sie **John Doe** als **Name** ein, und wählen Sie ein beliebiges **Gebäude** aus.

8.  Wählen Sie **John Doe** als **Besucher** aus.

9.  Wählen Sie als **Geplanter Start** und **Geplantes Ende** beliebige Zeitpunkte in der Zukunft aus.

10.  Wählen Sie **Speichern** aus

11.  Navigieren Sie wieder zurück zur vorherigen Registerkarte mit dem Flow, der getestet werden soll. Beobachten Sie, wie der Flow ausgeführt wird. Beim Auftreten von Fehlern gehen Sie zurück, und vergleichen Sie Ihren Flow mit dem obigen Beispiel. Wenn die E-Mail erfolgreich gesendet wurde, erhalten Sie sie in Ihrem Posteingang. 

12.  Klicken Sie auf den Zurück-Pfeil in der Befehlsleiste.

13.  Beachten Sie, dass im Abschnitt **Details** der **Status** auf **Ein** gesetzt ist. Dies bedeutet, dass Ihr Flow immer dann ausgeführt wird, wenn ein neuer Besuch erstellt wird, bis Sie ihn deaktivieren. Jedes Mal, wenn der Flow ausgeführt wird, wird er der Liste **28-tägiger Ausführungsverlauf** hinzugefügt.

14.  Schalten Sie den Flow aus, indem Sie auf der Befehlsleiste auf **Ausschalten** klicken.

# Übung Nr. 2: Erstellen eines Security Sweep-Flows

**Ziel:** In dieser Übung erstellen Sie einen Power Automate-Flow, der die Anforderung implementiert. Alle 15 Minuten muss eine Sicherheitsprüfung durchgeführt werden. Sollte einer der Besucher seine geplante Aufenthaltszeit überschritten haben, ist die Sicherheit zu benachrichtigen.

## Aufgabe Nr. 1: Einen Flow zum Abrufen von Datensätzen erstellen

1. Öffnen Sie Ihre Campusverwaltung-Lösung.

   -   Anmelden bei <https://make.powerapps.com>

   -   Wählen Sie Ihre **Umgebung** aus.

   -   Wählen Sie **Lösungen** aus.

   -   Klicken Sie, um Ihre **Campusverwaltung**-Lösung zu öffnen.

2. Klicken Sie auf  **Neu** und wählen Sie  **Flow** aus. Dadurch wird der Power Automate-Flow-Editor in einem neuen Fenster geöffnet.

3. Suchen Sie nach *Wiederholung*, wählen Sie den **Zeitplan**-Connector und den **Wiederholung**-Trigger aus.

4. **Intervall** auf **15 Minuten** einstellen

5. Klicken Sie auf **Neuer Schritt**. Suchen Sie nach *Aktuell* und wählen Sie **Common Data Service (aktuelle Umgebung)** aus. Wählen Sie die Aktion **Datensätze auflisten**.

   * Geben Sie unter **Entitätsname** **Besuche** ein
   
   * Klicken Sie auf **Erweiterte Optionen anzeigen**.

   * Den folgenden Ausdruck als **Filterabfrage** eingeben

   ```
     statecode eq 0 and bc_actualstart ne null and bc_actualend eq null and Microsoft.Dynamics.CRM.OlderThanXMinutes(PropertyName='bc_scheduledend',PropertyValue=15)
   ```
   
   * Das bedeutet:
       * `statecode eq 0` filtert aktive Besuche (wobei „Status“ gleich „Aktiv“ ist)
       * `bc_actualstart ne null` beschränkt die Suche auf Besuche, bei denen „Tatsächlicher Start“ einen Wert hat, d. h. es wurde eingecheckt
       * `bc_actualend eq null` beschränkt die Suche auf Besuche, bei denen kein Auschecken stattgefunden hat („Tatsächliches Ende“ hat keinen Wert) 
       * `Microsoft.Dynamics.CRM.OlderThanXMinutes (PropertyName = 'bc_scheduledend', PropertyValue = 15)` beschränkt Besuche, die vor mehr als 15 Minuten abgeschlossen werden sollten.  

   * Klicken Sie bei dieser Aktion auf die Schaltfläche mit den drei Punkten (**...**), und klicken Sie auf **Umbenennen**. Benennen Sie diese Aktion in **„Aktive Besuche auflisten, die vor mehr als 15 Minuten geendet haben“** um. Dies ist eine gute Vorgehensweise, damit Sie und andere Flow-Editoren den Zweck des Schritts erkennen können, ohne tiefer in die Details gehen zu müssen.

6.  Klicken Sie auf **Neuer Schritt**. Such Sie nach **Anwenden**, und wählen Sie Aktion **Auf jedes anwenden** aus. 

7.  Wählen Sie **Wert** aus Dynamics-Inhalt im Feld **Eine Ausgabe aus vorherigen Schritten auswählen** aus. Beachten Sie, dass sich dieser unter der grauen Kopfzeile **Aktive Besuche auflisten, die vor mehr als 15 Minuten geendet haben** befindet. Dies bedeutet, dass Sie die Liste der Besuche auswählen, die Sie im vorherigen Schritt nachgeschlagen haben. 

8.  Abrufen von Gebäudedaten zu zugehörigem Datensatz

    * Klicken Sie auf **Eine Aktion hinzufügen** innerhalb der Schleife „Auf jedes anwenden“.
    
    * Suchen Sie nach *Aktuell* und wählen Sie **Common Data Service (aktuelle Umgebung)** aus. 
    
    * Wählen Sie die Aktion **Einen Datensatz abrufen** aus.
    
    * Wählen Sie **Gebäude** als **Entitätsname** aus
    
    * Wählen Sie **Gebäude (Wert)** als **Element-ID** aus dem Dynamics-Inhalt aus.
    
    * Klicken Sie auf **...** neben **Einen Datensatz abrufen**, und wählen Sie **Umbenennen** aus. Geben Sie als Schrittname **Gebäude abrufen** ein.
    
9.  Abrufen von Besucherdaten zu zugehörigem Datensatz

    * Klicken Sie auf **Eine Aktion hinzufügen** innerhalb der Schleife „Auf jedes anwenden“.
    
    * Suchen Sie nach *Aktuell* und wählen Sie **Common Data Service (aktuelle Umgebung)** aus.
    
    * Wählen Sie die Aktion **Einen Datensatz abrufen** aus.
    
    * Wählen Sie **Kontakte** als **Entitätsname** aus
    
    * Wählen Sie **Besucher (Wert)** als **Element-ID** aus dem Dynamics-Inhalt aus.
    
    * Klicken Sie auf **...** neben **Einen Datensatz abrufen**, und wählen Sie **Umbenennen** aus. Geben Sie als Schrittname **Besucher abrufen** ein.
    
11.  Fügen Sie die Aktion **Eine E-Mail-Benachrichtigung senden** aus der **Mail**-Verbindung hinzu, und bleiben Sie dabei innerhalb der Schleife **Auf jedes anwenden**.

12.  Ihre E-Mail-Adresse als **An** eingeben

13.  Geben Sie Folgendes in das Feld **Betreff** ein. **Besucher (Wert)** ist ein dynamischer Inhalt aus dem Schritt **Besucher abrufen**.

       ```
         {Full Name} hat seine/ihre Aufenthaltszeit überschritten
       ```
   
14.  Geben Sie Folgendes in das Feld **Text** ein. **Name** ist ein dynamischer Inhalt aus dem Schritt **Gebäude abrufen**.

       ```
         Im Gebäude {Name} hat jemand seine Zeit überschritten.
         
         Beste Grüße
         
         Campus-Sicherheit
       ```

17.  Wählen Sie den Flow-Namen **Ohne Titel** in der oberen linken Ecke aus, und benennen Sie ihn in **Sicherheitsüberprüfung** um.

18. Wählen Sie **Speichern** aus

    Ihr Flow sollte in etwa wie folgt aussehen:

![Sicherheitsüberprüfung, geplanter Flow, Teil 1](media/4-power-automate-security-sweep.png)

## Aufgabe Nr. 2: Flow überprüfen und aktivieren

1. Überprüfen Sie, ob Sie Datensätze zu Besuchen haben, für die Folgendes gilt:

   1. Aktivem Status
   
   2. Geplantem Ende in der Vergangenheit (über 15 Minuten)
   
   3. Wert für „Tatsächlicher Start“
   
         >**Hinweis**: Navigieren Sie zum Anzeigen dieser Daten auf einer neuen Registerkarte zu <make.powerapps.com>. Klicken Sie im linken Bereich auf „Lösungen“, um Ihre Lösung zu finden. Wählen Sie die Entität „Besuch“ aus, und wählen Sie dann die Registerkarte „Daten“ aus. Klicken Sie oben rechts auf „Aktive Besuche“, um die Ansichtsauswahl anzuzeigen, und wählen Sie dann „Alle Felder“ aus.
   
2. Navigieren Sie zu Ihrer Lösung, und suchen Sie den Flow **Sicherheitsüberprüfung**. Klicken Sie auf **...**, und klicken Sie dann auf **Bearbeiten**.

3. Wenn Ihr Flow geöffnet ist, klicken Sie auf **Testen**.

4. Wählen Sie **Ich werde die Triggeraktion ausführen** aus.

5. Klicken Sie auf **Testen** und auf **Flow ausführen**.

6. Wenn der Flow abgeschlossen ist, klicken Sie auf **Fertig**. 

7. Erweitern Sie **Auf jedes anwenden** und dann den Schritt **Eine E-Mail-Benachrichtigung senden**. Überprüfen Sie die Werte **Betreff**, **E-Mail-Text**.

8. Navigieren Sie zur Lösung, klicken Sie auf **...** neben dem Flow, und wählen Sie **Deaktivieren** aus. Dies soll verhindern, dass der Datenfluss nach einem Zeitplan auf dem Testsystem ausgeführt wird.

# Herausforderungen

* Fügen Sie dem E-Mail-Text „Tatsächlicher Start“ und „Geplantes Ende“ hinzu.
* Wie können Sie sicherstellen, dass im E-Mail-Text eine benutzerfreundliche Datumsformatierung verwendet wird?
* Ist es möglich, eine Tabelle mit Informationen zu überschrittenen Aufenthaltszeiten zu generieren und nur eine einzige E-Mail zu senden?
* Können Sie einen Barcode für den Besuchscode generieren? Wann könnte das nützlich sein?