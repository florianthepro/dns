# E-Mail-Isolation für Benutzer (Subdomain + Zoho)

Diese Anleitung beschreibt, wie du für einen Benutzer (z. B. `user`) ein eigenständiges Postfach einrichtest, das nach außen als `user@example.com` erscheint, aber intern isoliert auf einer Subdomain (`user.user.example.com`) bei Zoho läuft.

## 1. Subdomain-Postfach bei Zoho anlegen

- In der **Zoho Admin Console** → **Users** → **Create**.
- **E-Mail-Adresse:** `user@user.example.com`  
  (Beispiel: `user@user.example.com`)
- **Passwort** vergeben (notieren für Schritt 3).
- Benutzer erstellen.

## 2. Domain‑Aliasing für die Hauptdomain aktivieren

- **Admin Console** → **Domains** → `example.com` → **Settings**.
- **Domain Aliasing** → **Select new alias domain** → `user.example.com` auswählen → **+** klicken.

> Jetzt kann der Benutzer als `user@example.com` senden/empfangen.

## 3. DNS‑MX‑Einträge für die Subdomain setzen (Cloudflare)

- In deinem Cloudflare‑Dashboard für `example.com`:
  - **Neuen MX‑Eintrag** für `user.example.com` anlegen.
  - Ziel: Zoho‑Mailserver (`mx.zoho.com`, Priorität 10).
- (Die MX‑Einträge der Hauptdomain bleiben unberührt.)

## 4. Zugangsdaten für den Benutzer

Die folgenden Daten gibst du dem Benutzer (z. B. per sicherer Nachricht). Er kann sie in Thunderbird, Outlook oder jedem anderen E‑Mail‑Client verwenden.

---

### 📧 Kopierfertiger Text für den Benutzer

```text
Hallo,

hier sind deine Zugangsdaten für dein E‑Mail‑Postfach.

Deine E‑Mail-Adresse: user@example.com
Dein Passwort: [das von mir vergebene Passwort]

Server-Einstellungen für jedes E‑Mail‑Programm (z. B. Thunderbird):

- Posteingangsserver (IMAP): imap.zoho.com
  - Port: 993
  - Verschlüsselung: SSL/TLS

- Postausgangsserver (SMTP): smtp.zoho.com
  - Port: 465
  - Verschlüsselung: SSL/TLS

Benutzername für beide Server: user@user.example.com (vollständige Subdomain-Adresse)

Nach der Einrichtung kannst du als user@example.com senden und empfangen. Du hast keinerlei Zugriff auf andere Postfächer oder die Domain-Einstellungen.
