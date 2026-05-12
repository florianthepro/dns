# M365 Onboarding – Technisches Formular (Kunde ↔ IT)

**Dokument-ID:** ____________  **Version:** _____  **Datum:** ____.__._____  
**Ticket/Request-ID:** ___________________________  **Priorität:** ☐ Low ☐ Med ☐ High  
**Onboarding-Typ:** ☐ Neu ☐ Rehire ☐ Wechsel intern ☐ Extern/Guest

> **Spaltenlogik:** **Links (IT)** = erledigt + Unterschrift/Kürzel · **Rechts (Kunde/Fachbereich)** = bestätigt/angegeben

---

## 1) Stammdaten / Auftrag

| Feld | IT ✅ / Signatur | Kunde ✅ |
|------|-------------------|---------|
| Firma / Mandant | | ☐ |
| Abteilung | | ☐ |
| Standort | | ☐ |
| Kostenstelle | | ☐ |
| Eintrittsdatum | | ☐ |
| Befristet bis (optional) | | ☐ |
| Vorgesetzter (Name / Mail) | | ☐ |
| Vertrags-/Personalkategorie (intern/extern) | | ☐ |
| Standard-Sprache/Locale | | ☐ |

---

## 2) Benutzeridentität (Personendaten)

| Feld | IT ✅ / Signatur | Kunde ✅ |
|------|-------------------|---------|
| Vorname | | ☐ |
| Nachname | | ☐ |
| Anzeigename (DisplayName) | | ☐ |
| Initialen (optional) | | ☐ |
| Telefon (DID/Mobil) | | ☐ |
| Büro/Room (optional) | | ☐ |

---

## 3) Namensschema / Logins / E-Mail

| Feld | IT ✅ / Signatur | Kunde ✅ |
|------|-------------------|---------|
| Benutzername/UPN (z. B. vorname.nachname@domain) | | ☐ |
| Primäre SMTP-Adresse | | ☐ |
| Aliase (SMTP) | | ☐ |
| Mail-Domain (falls mehrere) | | ☐ |
| Anzeige im GAL: ☐ Ja ☐ Nein | | ☐ |

---

## 4) Lokales AD (On-Prem)  ✅ **(neu enthalten)**

| Punkt | IT ✅ / Signatur | Kunde ✅ |
|------|-------------------|---------|
| AD-User anlegen | | ☐ |
| OU / Pfad (DistinguishedName) gesetzt | | ☐ |
| sAMAccountName gesetzt | | ☐ |
| UPN-Suffix korrekt | | ☐ |
| Initial-Passwort gesetzt / Übergabeweg definiert | | ☐ |
| Passwortwechsel bei Erstlogin: ☐ Ja ☐ Nein | | ☐ |
| AD-Gruppen (Security) zugewiesen (Liste/Anhang) | | ☐ |
| Home-Drive/Profilpfad (falls genutzt) | | ☐ |
| On-Prem Ressourcen: Fileshare/Printer/VPN (Liste/Anhang) | | ☐ |

**AD-Gruppen (On-Prem) – Liste:**  
- __________________________________________________________  
- __________________________________________________________  
- __________________________________________________________  

---

## 5) Entra ID (Azure AD) / M365 Identität

| Punkt | IT ✅ / Signatur | Kunde ✅ |
|------|-------------------|---------|
| Benutzer in Entra ID angelegt (oder via Sync vorhanden) | | ☐ |
| Sync-Status geprüft (wenn Hybrid): ☐ OK ☐ n/a | | ☐ |
| UsageLocation gesetzt | | ☐ |
| Passwort-Reset-Optionen gesetzt (gem. Policy) | | ☐ |
| BlockSignIn = false (Account aktiv) | | ☐ |

---

## 6) M365 Kernservices (Exchange / Teams / OneDrive)

| Punkt | IT ✅ / Signatur | Kunde ✅ |
|------|-------------------|---------|
| Exchange Online Mailbox provisioniert | | ☐ |
| Archiv: ☐ Aktiv ☐ n/a | | ☐ |
| Shared Mailboxes Zugriff (Liste/Anhang) | | ☐ |
| Verteilerlisten (DL) Mitgliedschaften (Liste/Anhang) | | ☐ |
| Microsoft Teams aktiviert | | ☐ |
| Teams/Zugriffe (Teams/Channels) zugewiesen (Liste/Anhang) | | ☐ |
| OneDrive provisioniert | | ☐ |
| SharePoint Sites Zugriff (Liste/Anhang) | | ☐ |

**Zugriffslisten (M365) – optional Anhänge:**  
- Shared Mailboxes: ________________________________________  
- DLs: _____________________________________________________  
- Teams/Sites: _____________________________________________  

---

## 7) Lizenzen (vereinfacht)

| Lizenz | IT ✅ / Signatur | Kunde ✅ |
|--------|-------------------|---------|
| Lizenz 1 | | ☐ |
| Lizenz 2 | | ☐ |
| Lizenz 3 | | ☐ |

---

## 8) Gruppen & Berechtigungen (Entra/M365)

| Punkt | IT ✅ / Signatur | Kunde ✅ |
|------|-------------------|---------|
| Entra Gruppen (Security) zugewiesen (Liste/Anhang) | | ☐ |
| M365 Gruppen zugewiesen (Liste/Anhang) | | ☐ |
| Rollen (Admin/Privileged) geprüft: ☐ n/a ☐ erforderlich | | ☐ |
| App-Zugriffe (SaaS/Line-of-Business) zugewiesen | | ☐ |

**Gruppenliste (Entra/M365):**  
- __________________________________________________________  
- __________________________________________________________  
- __________________________________________________________  

---

## 9) Okta (SSO / Provisioning)

| Punkt | IT ✅ / Signatur | Kunde ✅ |
|------|-------------------|---------|
| Okta-User erstellt/aktiviert | | ☐ |
| Okta-Gruppen zugewiesen (Liste/Anhang) | | ☐ |
| SSO Apps zugewiesen (Liste/Anhang) | | ☐ |
| Provisioning/Sync geprüft: ☐ OK ☐ n/a | | ☐ |

**Okta Apps / Gruppen (Liste):**  
- __________________________________________________________  
- __________________________________________________________  

---

## 10) MFA (Auswahl & Umsetzung)

### 10.1 MFA – Methode(n) (bitte auswählen)
| Methode | IT ✅ / Signatur | Kunde ✅ |
|--------|-------------------|---------|
| Microsoft Authenticator | | ☐ |
| Okta Verify | | ☐ |
| Yubico (YubiKey) | | ☐ |
| FIDO2 Security Key | | ☐ |
| SMS (nur falls erlaubt) | | ☐ |
| Telefonanruf (nur falls erlaubt) | | ☐ |

### 10.2 MFA – Umsetzung/Status
| Punkt | IT ✅ / Signatur | Kunde ✅ |
|------|-------------------|---------|
| MFA registriert / Enrollment abgeschlossen | | ☐ |
| Conditional Access greift (Policy) | | ☐ |
| Legacy Auth blockiert (falls Policy) | | ☐ |
| Break-Glass / Ausnahmen geprüft: ☐ n/a ☐ ja | | ☐ |

---

## 11) Endpoint / Device (Intune / Autopilot)

| Punkt | IT ✅ / Signatur | Kunde ✅ |
|------|-------------------|---------|
| Gerätetyp: ☐ Laptop ☐ Desktop ☐ Mobile ☐ BYOD | | ☐ |
| Seriennummer/Asset-Tag erfasst | | ☐ |
| Autopilot: ☐ registriert ☐ n/a | | ☐ |
| Intune Enrollment abgeschlossen | | ☐ |
| Compliance Policy angewendet | | ☐ |
| BitLocker/FileVault aktiv | | ☐ |
| AV/EDR aktiv (Defender/3rd party) | | ☐ |
| VPN/WLAN Profile verteilt | | ☐ |

---

## 12) Security / Compliance (falls relevant)

| Punkt | IT ✅ / Signatur | Kunde ✅ |
|------|-------------------|---------|
| Sensitivity Labels zugewiesen (falls genutzt) | | ☐ |
| DLP/Retention (Policy) greift (falls genutzt) | | ☐ |
| Mail Flow Regeln/Transport (falls nötig) | | ☐ |
| Externes Sharing gesetzt (OneDrive/SharePoint) | | ☐ |

---

## 13) Übergabe / Abschluss

| Punkt | IT ✅ / Signatur | Kunde ✅ |
|------|-------------------|---------|
| Initial-Zugang sicher übergeben (Weg: ________) | | ☐ |
| Erstanmeldung getestet / User-Login ok | | ☐ |
| Mail/Teams/OneDrive Funktion geprüft | | ☐ |
| On-Prem Zugriff (falls) geprüft | | ☐ |
| Onboarding abgeschlossen | | ☐ |

---

## 14) Freigaben / Unterschriften

| Rolle | Name | Unterschrift / Datum |
|------|------|-----------------------|
| IT Durchführung | | |
| IT Kontrolle (4-Augen) | | |
| Fachbereich/Kunde Freigabe | | |

---
