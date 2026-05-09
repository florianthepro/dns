# E-Mail-Isolation für `user@example.com`

## Ausgangslage
- Hauptdomain `example.com` bei **iCloud+** (Catch‑All aktiv)
- Kein MX‑Wechsel für `example.com`
- Zusätzliche Adresse `user@example.com` soll isoliert bei **Zoho** laufen
- Empfang & Versand als `user@example.com` – kein Zugriff auf andere Postfächer

---

## 1. Subdomain bei Zoho anlegen

1. **Zoho Admin Console** → **Domains** → **Add Domain**
2. Domain eingeben: `user.example.com`
3. Verifikation per TXT‑ oder CNAME‑Eintrag (Zoho zeigt an)
4. Nach Verifikation Domain in Zoho speichern

## 2. Benutzerpostfach erstellen

- **Users** → **Create User**
- **Email Address**: `user@user.example.com`
- Passwort vergeben (notieren für Übergabe)

## 3. Domain‑Aliasing einrichten (Zoho)

> Damit der Benutzer als `user@example.com` senden/empfangen kann.

- **Domains** → `user.example.com` → Tab **Settings**
- **Domain Aliasing** → **Select new alias domain** → `example.com` auswählen → **Add**
- Warnung bestätigen (Zoho deaktiviert Mail‑Hosting für `user.example.com`)

## 4. DNS‑Einträge bei Cloudflare (exakte Werte)

Für die Subdomain `user.example.com` folgende Einträge **hinzufügen** (bestehende Einträge von `example.com` bleiben unberührt):

| Typ  | Name                 | Wert                                         | Priority / TTL |
|------|----------------------|----------------------------------------------|----------------|
| MX   | `user.example.com`   | `mx.zoho.com`                                | 10             |
| MX   | `user.example.com`   | `mx2.zoho.com`                               | 20             |
| MX   | `user.example.com`   | `mx3.zoho.com`                               | 50             |
| TXT  | `user.example.com`   | `v=spf1 include:zoho.com -all`               | Auto           |
| TXT  | `user.example.com`   | `v=DKIM1; k=rsa; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC...` (von Zoho) | Auto |

**DKIM generieren:**
- In Zoho: **Email Authentication** → **DKIM** → Domain `user.example.com` auswählen → **Generate** → angezeigten TXT‑Wert kopieren.

## 5. iCloud‑Einträge für Hauptdomain bleiben bestehen

- `mx01.mail.icloud.com` (Priority 10)
- `mx02.mail.icloud.com` (Priority 10)

## 6. Zugangsdaten für den Benutzer

Kopiere folgenden Block und ersetze `[PASSWORT]` durch das vergebene Passwort:

```text
E-Mail-Adresse: user@example.com
Passwort: [PASSWORT]

Posteingangsserver (IMAP):
- Server: imap.zoho.com
- Port: 993
- Verschlüsselung: SSL/TLS

Postausgangsserver (SMTP):
- Server: smtp.zoho.com
- Port: 465
- Verschlüsselung: SSL/TLS

Benutzername für beide Server: user@user.example.com
