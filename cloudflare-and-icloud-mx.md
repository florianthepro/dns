# E-Mail-Isolation für `user@example.com` (Cloudflare + iCloud)

## Ausgangslage
- **Hauptdomain `example.com`** ist bei **iCloud+** eingerichtet und funktioniert normal (inkl. Catch-all).
- **Ziel**: Eine zusätzliche E-Mail-Adresse (`user@example.com`) soll isoliert laufen.
- **Anforderung**: Der Nutzer dieser Adresse bekommt **keinen Zugriff** auf andere Postfächer (`info@example.com`, `admin@example.com` usw.).

> **Wichtig**: Cloudflare Email Routing leitet eingehende E-Mails nur weiter, stellt aber **kein eigenes Postfach** zur Verfügung. Das bietet dir aber den entscheidenden Vorteil: Du kannst einem Nutzer einfach eine Weiterleitung zu seinem eigenen, bereits bestehenden E-Mail-Konto (z. B. Gmail, Outlook) geben. Er loggt sich in seinem gewohnten Postfach ein, empfängt und sendet aber als `user@example.com`.[reference:0][reference:1]

---

## 1. Voraussetzungen
- Domain (`example.com`) ist bei Cloudflare als DNS-Provider eingetragen
- iCloud+ Abonnement ist aktiv
- Du hast Zugriff auf die E-Mail-Adresse, an die weitergeleitet werden soll (z. B. `user@gmail.com`)

## 2. Cloudflare Email Routing für Empfang einrichten

### 2.1 Email Routing aktivieren
1.  Gehe in deinem Cloudflare-Dashboard zu **E-Mail** > **Email Routing**.
2.  Klicke auf **Erste Schritte / Get started**.
3.  Cloudflare zeigt dir an, welche MX- und TXT-Einträge automatisch hinzugefügt werden. Bestätige mit **Einträge hinzufügen und aktivieren**.[reference:2][reference:3]

### 2.2 Zieladresse (Destination) hinzufügen
1.  Gehe zu **Routing-Regeln** > **Zieladressen**.
2.  Klicke auf **Adresse hinzufügen**.
3.  Gib die E-Mail-Adresse des Nutzers ein (z. B. `gabrielas.private@gmail.com`).[reference:4]
4.  Cloudflare sendet einen Bestätigungslink an diese Adresse. Der Nutzer muss darauf klicken, um die Adresse zu verifizieren.[reference:5]

### 2.3 Regel für die isolierte E-Mail-Adresse erstellen
1.  Gehe zu **Routing-Regeln** > **Benutzerdefinierte Adressen**.
2.  Klicke auf **Adresse erstellen**.
3.  **Benutzerdefinierte Adresse:** `user@example.com`
4.  **Aktion:** `An eine E-Mail-Adresse senden`
5.  **Zieladresse:** Wähle die soeben verifizierte Adresse des Nutzers aus.
6.  Klicke auf **Speichern**.[reference:6]

### Ergebnisse nach diesem Schritt:
| Wer schreibt an … | Was passiert? |
|-------------------|----------------|
| `user@example.com` | E-Mail landet im privaten Postfach des Nutzers (Gmail, etc.). |
| `info@example.com` | E-Mail landet weiterhin wie gewohnt in deinem iCloud-Postfach. |
| `xyz123@example.com` | (Falls Catch-all in iCloud aktiviert) landet bei dir. |

> **Sicherheitshinweis**: Du musst **kein Catch-all in Cloudflare** aktivieren. Damit stellst du sicher, dass nur genau die Adressen weitergeleitet werden, die du explizit freigibst. Alle anderen landen bei dir in iCloud. Das ist der entscheidende Punkt für die Isolation![reference:7]

## 3. Versand einrichten (am Beispiel Gmail/iCloud)

Da Cloudflare selbst **keinen SMTP-Server** anbietet, musst du den Versand über das Postfach des Nutzers realisieren.[reference:8][reference:9] Das geht in wenigen Schritten:

### 3.1 Konto des Nutzers vorbereiten
Der Nutzer muss in seinem E-Mail-Konto (Gmail, iCloud, Outlook etc.) die Funktion **"Send Mail As"** (Als ... senden) einrichten.

- **In Gmail**: Einstellungen → "Konten und Import" → "Eine weitere E-Mail-Adresse hinzufügen".  
  Als SMTP-Server trägst du die Daten *seines* Providers ein (z. B. `smtp.gmail.com` für Gmail). Unbedingt ein **App-Passwort** verwenden, wenn 2FA aktiviert ist.[reference:10]
- **In iCloud-Mail**: Gehe zu Einstellungen > "Custom Email Domain" (siehe Abschnitt 3.2).

### 3.2 Alternative: iCloud direkt als "Send Mail As" nutzen (nur für Apple-User)
Falls der Nutzer selbst iCloud+ nutzt (er muss also ein aktives iCloud+ Abo haben) und du ihm **volle Kontrolle über die Domain** geben willst, kannst du ihn direkt zu deiner iCloud Custom Domain einladen.

1.  Auf deinem Gerät: **Einstellungen → [Dein Name] → iCloud → iCloud Mail → Custom Email Domain**.[reference:11][reference:12]
2.  Tippe auf deine Domain und wähle **"Person hinzufügen" / "Add Member"**.
3.  Gib die E-Mail-Adresse des Nutzers ein. Er erhält eine Einladung per Mail.
4.  Nach Annahme kann er in der Mail-App auswählen, ob er als seine private `@icloud.com`-Adresse oder als seine neue `@example.com`-Adresse senden möchte.[reference:13]

> **⚠️ Wichtig**: Diese Methode gibt dem Nutzer **Admin-ähnliche Rechte auf die Domain**. Er kann dann eigene Adressen anlegen oder bestehende verwalten. **Nur anwenden**, wenn du dem Nutzer vertraust und er selbst iCloud+ nutzt! Verwende für Gast-Zugänge ohne iCloud+ daher besser die reine Weiterleitung + "Send Mail As" in Gmail & Co.

## 4. Testen der Einrichtung
1.  **Empfangstest**:
    - Sende eine E-Mail von einer dritten Adresse an `user@example.com`.
    - Prüfe, ob die E-Mail im privaten Postfach des Nutzers ankommt und die Absenderadresse korrekt ist.
2.  **Versandtest**:
    - Der Nutzer schreibt eine neue E-Mail von seinem privaten Postfach aus und wählt als Absender `user@example.com` aus.
    - Schickt sie an eine zweite Testadresse.
    - Prüfe, ob die E-Mail mit dem korrekten Absender `user@example.com` ankommt, nicht etwa als `user@gmail.com im Auftrag von`.  
      Falls "im Auftrag von" erscheint, liegt es an fehlenden SPF/DKIM-Einträgen (siehe Schritt 5).
3.  **Isolationstest**:
    - Der Nutzer versucht, eine E-Mail an `info@example.com` zu senden und diese in seinem Postfach zu empfangen – das ist nicht möglich.  
      (Falls du trotzdem Mails von `info` an ihn weiterleiten willst, müsstest du eine extra Regel in Cloudflare anlegen – also bewusst nicht gemacht.)
4.  **Negativtest**:
    - Sende eine E-Mail an `doesnotexist@example.com`.  
      Diese sollte **nicht** beim Nutzer landen, sondern wie gewohnt bei dir im iCloud-Catch-all (oder nirgendwo, falls Catch-all deaktiviert).

## 5. Fehlerbehebung
| Problem | Lösung |
|---------|--------|
| Empfang funktioniert nicht | Prüfe, ob die Zieladresse verifiziert wurde und die Routing-Regel aktiv ist. |
| Versand zeigt "im Auftrag von" an | Fehlende SPF/DKIM-Einträge. Diese müssen für `example.com` im Cloudflare-DNS gesetzt werden. Die nötigen Werte bekommst du von iCloud (bei Einrichtung der Custom Domain). |
| E-Mail landet im Spam | Senderichtlinien (SPF, DKIM) überprüfen. Eventuell DMARC-Record anlegen. |
| Cloudflare findet Domain nicht | Stelle sicher, dass die Nameserver der Domain auf Cloudflare zeigen.[reference:14] |

---

## Fazit

| Methode | Isolation | Versand über | iCloud+ nötig? |
|---------|-----------|--------------|----------------|
| **Cloudflare Routing + "Send Mail As"** | ✅ vollständig | eigenes Postfach des Nutzers | ❌ Nein |
| **iCloud Domain Sharing** | ❌ eingeschränkt | iCloud-Mail des Nutzers | ✅ Ja |

Für dein konkretes Szenario (`user@example.com` ohne Zugriff auf andere Adressen) ist **Cloudflare Email Routing + "Send Mail As"** die sauberste Lösung und benötigt kein iCloud+ beim Nutzer.
