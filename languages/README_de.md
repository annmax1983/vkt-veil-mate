# VKT VeilMate

[English](../README.md) | [中文](README_zh.md) | Deutsch | [Español](README_es.md) | [日本語](README_ja.md) | [Français](README_fr.md)

Ein Vorhang für den Browser: ein Klick deckt alle Tabs ab, und beim Entsperren ist alles genau wie vorher — nichts lädt neu, keine Formulare gehen verloren, kein Video bricht ab.

> Chrome · Edge · Firefox · Manifest V3 · Minimale Berechtigungen · Keine Analyse · 100 % lokal

---

## Warum VKT VeilMate?

Sie gehen einen Kaffee holen. Jemand schaut auf Ihren Bildschirm: halb geschriebene E-Mail, ein Banking-Tab, eine private Nachricht. Sie wollen eine Decke über den Browser werfen — kein Sicherheitsprodukt.

Bestehende „Browser-Sperren" machen meist eines von beidem schlecht:

| Deren Ansatz | Was schiefgeht |
|---|---|
| Jeden Tab auf eine Sperrseite navigieren | Beim Entsperren lädt alles neu — Formulare weg, Video startet neu, SPA-Zustand verloren |
| „Unbefugten Zugriff verhindern" versprechen | Neues Profil, privates Fenster oder Task-Manager gehen einfach daran vorbei, und die Rezensionen sagen es |

VKT VeilMate nimmt die entgegengesetzte Haltung ein:

| Unser Ansatz | Ergebnis |
|---|---|
| **Abdecken, nie navigieren** — eine Shadow-DOM-Ebene wird in jede Seite injiziert | Entsperren ist sofort und verlustfrei |
| **Sagen, was es nicht kann** — auf der Einstellungsseite und in der Beschreibung | Keine enttäuschten Erwartungen, keine Ein-Stern-Bewertungen für ein Versprechen, das niemand halten kann |
| **Kein Weg zurück** — kein Wiederherstellungscode, kein Reset-Endpunkt, und die Sperre übersteht einen Browser-Neustart | Ein Vorhang, den man umgehen kann, ist kein Vorhang; ein vergessenes Passwort bedeutet, die Erweiterung zu entfernen, und das steht auf jedem Bildschirm |

---

## Funktionen

### 🆓 Dauerhaft kostenlos

| Funktion | Detail |
|---|---|
| Sperren mit einem Klick | Schaltfläche in der Symbolleiste — kein Tastenkürzel wird registriert |
| Ausnahmeliste | Bis zu 10 Domains bleiben lesbar, alles andere wird abgedeckt |
| Verlustfreie Ebene | Jeder http/https-Tab wird an Ort und Stelle abgedeckt; nichts lädt neu |
| Eingabeblockade | Klicks, Scrollen, Tastatur, Ziehen, Kopieren und Kontextmenü werden auf abgedeckten Seiten gestoppt; beim Sperren wird der Fokus zurück auf die Ebene geholt, damit keine Tastendrücke in einem Editor im iframe landen |
| Neue Tabs & Adressleiste | Neue Tabs, neue Fenster und eingetippte URLs werden im gesperrten Zustand abgefangen |
| Passwort-Entsperrung | PBKDF2-SHA256, 310.000 Runden, zufälliges Salt, Vergleich in konstanter Zeit |
| Sperre, die bleibt | Der Zustand liegt in `storage.local`; ein Browser-Neustart hebt ihn nicht auf |
| Kein Wiederherstellungsweg | Die Erweiterung in `chrome://extensions` zu entfernen ist der einzige Ausweg bei vergessenem Passwort |
| Automatische Sperre bei Inaktivität | Nutzt die Leerlauferkennung des Browsers |
| Wachsende Wartezeit | Fünf Fehlversuche → 30 Sekunden, danach 2 Minuten, 10 Minuten, 30 Minuten, 1 Stunde. Jede Passwortprüfung — Entsperren wie Passwort ändern — zählt auf denselben Zähler |
| Versteckte Tab-Titel | Im gesperrten Zustand zeigen Tab-Leiste und Fenstertitel einen neutralen Namen statt der Seite, die du liest |
| Kontextmenü | Alles sperren oder die aktuelle Seite lesbar lassen, ohne das Popup zu öffnen |
| Große Uhr | Große Uhr auf dem Sperrbildschirm, 12/24 Stunden, Datum optional |
| Sechs Sprachen | English, 中文, 日本語, Deutsch, Español, Français |

### ⭐ Pro (Lizenz erforderlich)

| Funktion | Detail |
|---|---|
| Gezieltes Sperren | Die Domainliste auf „nur abdecken…" umstellen — Intranet sperren, alles andere lesbar lassen. Auch direkt im Kontextmenü. Kostenlos sind 10 Domains und immer „alles außer…" |
| Sperre zu einer festen Uhrzeit | Alles zu einer festen Zeit abdecken, täglich oder nur werktags. Ein einmaliger Alarm, der sich nach jedem Lauf neu stellt; ein Termin, der verpasst wurde, weil der Browser zu war, löst beim Start nicht nachträglich aus |
| Zeitfenster ohne Passwort | Wenige Minuten nach einem echten Entsperren lässt sich eine erneute Sperre ohne Passwort aufheben. Die Abkürzung verlängert sich nicht selbst, ein Browser-Neustart fragt immer, und ein Passwortwechsel macht sie sofort ungültig |
| Biometrisches Entsperren | Windows Hello / Touch ID über WebAuthn, das Passwort bleibt immer als Rückweg. **Eine Abkürzung zum Tippen, kein zweiter Schlüssel**: die Prüfung läuft auf dem Sperrbildschirm, und wer dort DevTools öffnet, kann dieselbe Nachricht senden — dieselbe Stufe wie jemand an der Tastatur. Die Grenze bleibt die Passwortprüfung |
| Sperre bei Fokusverlust | Sperrt wenige Sekunden nach dem Wechsel in eine andere Anwendung |
| Kopplung an die Systemsperre | Folgt der Bildschirmsperre des Betriebssystems |
| Sperre beim Browserstart | Fragt beim ersten Öffnen des Browsers nach dem Passwort |
| Privatsphäre-Vorhang | Die aktuelle Seite ohne Sperre weichzeichnen; Klick zum Aufdecken |
| Tarnseite | Abgedeckte Seiten sehen aus wie ein gewöhnliches „Diese Website ist nicht erreichbar" statt wie ein offensichtlicher Sperrbildschirm; „Neu laden" führt zum Sperrbildschirm |
| Sperrprotokoll | Lokale Aufzeichnung der Entsperrversuche auf diesem Gerät, auch der Prüfungen aus dem Formular zum Passwortändern |
| Hintergrundbild & Meldung | Sechs eingebaute Verläufe oder ein eigenes Bild, dazu eine eigene Zeile auf dem Sperrbildschirm |
| Geräteübergreifende Synchronisierung | Aussehen, Uhr, Einstellungen zur automatischen Sperre **und die Domainliste** reisen über `chrome.storage.sync` (Chrome über Google, Edge über Microsoft, Firefox über Firefox Sync). Änderungen werden kurz nach dem Speichern automatisch hochgeladen und beim Schreiben des anderen Geräts sofort übernommen. Das Passwort wird nie synchronisiert; ein hochgeladenes Hintergrundbild überschreitet das Kontingent von 8 KB pro Element, daher reisen nur die eingebauten Verläufe |

---

## Vorschau

> 📸 Store-Material und Screenshots liegen in [`screenshots/`](../screenshots/) — sechs Aufnahmen in 1280×800 sowie Werbebilder in 1400×560 und 440×280.

| Screenshot | Zeigt |
|---|---|
| [`01-lock-all-tabs.png`](../screenshots/01-lock-all-tabs.png) | Ein Klick deckt alle Tabs in allen Fenstern ab |
| [`02-lock-screen.png`](../screenshots/02-lock-screen.png) | Entsperren auf dem Sperrbildschirm mit der großen Uhr |
| [`03-popup.png`](../screenshots/03-popup.png) | Das Popup: sperren, Passwort setzen, Pro-Status |
| [`04-auto-lock-scope.png`](../screenshots/04-auto-lock-scope.png) | Automatische Sperre und Sperrumfang (Domainliste) |
| [`05-honest.png`](../screenshots/05-honest.png) | Die Tabelle „es kann / es kann nicht" |
| [`06-security.png`](../screenshots/06-security.png) | Passwort- und Biometrie-Einstellungen |

---

## Unterstützte Browser

| Browser | Status | Mindestversion | Hinweise |
|---------|--------|----------------|----------|
| Google Chrome | ✅ Vollständig unterstützt | Chrome 116+ | Manifest V3, Service Worker |
| Microsoft Edge | ✅ Vollständig unterstützt | Edge 116+ | Gleicher Build, Chromium-basiert |
| Andere Chromium-Browser (Brave, Vivaldi, Opera) | ⚠️ Nach bestem Bemühen | Chromium 116+ | Ungetestet; dieselben APIs |
| Mozilla Firefox | ✅ Voll unterstützt | Firefox 121+ | MV3-Build wird im dedizierten Firefox-Repository gepflegt |
| Mobile Browser | ❌ Nicht unterstützt | — | Keine Symbolleiste zum Klicken und kein Fenstermodell zum Abdecken |

> **Windows Hello / Touch ID** setzen WebAuthn der Plattform voraus: Windows 10 1903+ mit eingerichteter PIN oder Fingerabdruck, oder macOS mit Touch ID. Das Passwort ist immer verfügbar, ein Rechner ohne Biometrie verliert also nur den Komfort.

---

## Installation

| Store | Link |
|---|---|
| Chrome Web Store | 🔜 In Prüfung — Link folgt nach der Freigabe |
| Microsoft Edge Add-ons | 🔜 In Prüfung — Link folgt nach der Freigabe |
| Firefox Add-ons (AMO) | [Für Firefox installieren](https://addons.mozilla.org/firefox/addon/vkt-veilmate/) |

> Bitte nur aus den oben genannten offiziellen Stores installieren.

---

## Verwendung

### Erste Einrichtung

1. Symbol in der Symbolleiste anklicken → **Passwort setzen**. Es gibt keinen Wiederherstellungscode — notieren Sie das Passwort selbst an einem sicheren Ort.
2. Beim Verlassen des Platzes **Jetzt sperren** anklicken.
3. Auf dem Sperrbildschirm mit Passwort oder (Pro) Biometrie entsperren.

### Sperrumfang einrichten

Domains werden über das Ende mit Punktgrenze abgeglichen: `example.com` deckt `example.com`, `www.example.com` und `a.b.example.com` ab, nicht aber `notexample.com`. Schema, führendes `www.`, Pfad, Port und Platzhalter-Präfix werden automatisch entfernt; ein blankes `com` wird abgelehnt.

Seiten ohne Hostnamen (`chrome://`, `file://`, `about:blank`, lokale PDFs, Erweiterungsseiten) werden immer abgedeckt, unabhängig von der Liste — die Liste gilt nur für http und https.

### Passwort vergessen

Es gibt genau einen Weg: **die Erweiterung in `chrome://extensions` entfernen und neu installieren.**

Dabei werden auch Hintergrundbild und alle Einstellungen gelöscht. Es gibt keinen Wiederherstellungscode, keinen Reset-Endpunkt und keinen Support, der entsperren könnte — ein Schloss mit Hintertür ist kein Schloss. Den Browser zu schließen hilft ebenfalls nicht: Der Zustand liegt in `storage.local` und ist nach einem Neustart noch da.

Das Feld „Passwort vergessen" auf dem Sperrbildschirm verlinkt direkt auf `chrome://extensions/?id=<diese Erweiterung>`, sodass Sie nie ohne Ausweg dastehen — nur ohne Abkürzung.

---

## So funktioniert es

```
Auslöser (Schaltfläche / Kontextmenü / Inaktivität / Fokusverlust / Systemsperre / Start / Uhrzeit)
  → Sperrzustand in storage.local schreiben (übersteht Browser-Neustart)
  → für jeden http(s)-Tab: tabs.sendMessage({type:'veil:lock'}) → Ebene injizieren
  → für Tabs ohne Injektion: URL merken, tabs.update(lock.html)
  → tabs.onCreated / tabs.onUpdated fangen weiter alles Neue ab
  → windows.onCreated deckt Ctrl+N, „in neuem Fenster öffnen" und private Fenster ab
  → chrome://extensions/?id=<selbst> ist die einzige erlaubte interne Seite,
    damit die Erweiterung immer entfernbar bleibt
Entsperren
  → Passwort / WebAuthn auf der Erweiterungsseite prüfen
  → Zustand löschen, Ebenen entfernen, ersetzte Tabs an Ort und Stelle wiederherstellen
```

Wissenswerte Designentscheidungen:

- **Passwörter werden nur auf Erweiterungsseiten eingegeben.** Das JavaScript einer Seite sieht das Feld nie, keine Website kann es abgreifen.
- **Gehasht wird im Service Worker.** Gespeichert wird nur `{salt, iter, hash}`; das Passwort selbst wird nirgends geschrieben.
- **Vergleich in konstanter Zeit.** Der Hash-Vergleich verrät keine Zeitinformationen.
- **Die Ebene liegt in einem geschlossenen Shadow Root.** Seiten-Skripte kommen nicht hinein und können das Innere nicht umgestalten. Das Trägerelement steht aber im Seitendokument, ein Site-Stylesheet kann es also ansprechen — deshalb werden die entscheidenden Eigenschaften als Inline-`!important` gesetzt, und eine Wache stellt die Ebene wieder her, wenn sie entfernt oder versteckt wird.

---

## Häufige Fragen

**Bleibt die Sperre erhalten, wenn ich den Browser schließe?** Ja. Der Zustand liegt in `storage.local`, der Browser öffnet also gesperrt, bis Sie entsperren.

**Ist das ein Sicherheitsprodukt?** Nein. Es verbirgt Tabs vor Vorbeigehenden. Wer die Maschine kontrolliert, kann es in `chrome://extensions` deaktivieren, ein anderes Profil nutzen oder den Browser im Task-Manager beenden. All das steht auch in der Store-Beschreibung.

**Warum gibt es keine Passwort-Wiederherstellung?** Ein Wiederherstellungscode ist ein zweiter Schlüssel, und ein zweiter Schlüssel ist eine Hintertür. Der einzige Ausweg ist das Entfernen der Erweiterung — dokumentiert auf dem Sperrbildschirm selbst.

**Ist die Biometrie ein zweiter Weg hinein?** Sie ist eine Abkürzung, kein zweiter Schlüssel. Die Passwortprüfung liegt im Hintergrundskript, und beide Stellen, an denen ein Passwort eingegeben wird — Entsperren und Passwort ändern — zählen auf denselben Zähler und dieselbe Wartezeit. Das Zeitfenster ohne Passwort prüft gar kein Passwort: Es gilt nur wenige Minuten nach einem echten Entsperren und hinterlässt einen `quick`-Eintrag im Protokoll. Wer aber DevTools auf einer Erweiterungsseite öffnen kann, kann die Nachrichten-API der Erweiterung selbst bedienen, und das verhindert keine Erweiterung. Biometrie heißt „weniger tippen", nicht „sicherer".

**Was passiert nach dem fünften Fehlversuch?** 30 Sekunden Pause, dann 2 Minuten, 10 Minuten, 30 Minuten und schließlich eine Stunde zwischen den Versuchen. Der Zähler gilt pro Gerät und ist im Sperrprotokoll sichtbar.

**Wird etwas hochgeladen?** Kein Seiteninhalt, keine URLs, keine Tastendrücke, keine Screenshots. Die einzige ausgehende Anfrage ist Lizenzaktivierung oder -prüfung.

**Warum ist die Domainliste kostenlos auf 10 begrenzt?** Der kostenlose Modus ist „alles außer…" — eine kurze Liste deckt den realistischen Fall ab (Webmail, Kalender, eine Seite, die man gerade liest). Der umgekehrte Modus „nur…" ist das, was ein Arbeitsnotebook braucht, und gehört zu Pro.

**Kann ich eine Lizenz für zwei Browser nutzen?** Ja, eine Lizenz aktiviert zwei Browser; wird sie aus einem entfernt, ist der Platz wieder frei.

---

## Datenschutz

- Keine Analyse, keine Telemetrie, keine Werbung, keine Konten.
- Kein Seiteninhalt, keine URL, kein Titel und kein Tastendruck verlässt den Browser.
- Hintergrundbild und Meldung bleiben auf Ihrem Gerät: hochgeladene Bilder werden verkleinert und in diesem Browserprofil gespeichert, nie irgendwohin gesendet.
- Die geräteübergreifende Synchronisierung (Pro) nutzt `chrome.storage.sync`, den Synchronisierungskanal des Browsers selbst. Auf diesem Weg gibt es keinen Server von uns, und wir können ihn nicht lesen. Das Passwort ist bewusst von der Synchronisierung ausgenommen, und hochgeladene Hintergrundbilder überschreiten das Kontingent, sodass nur Einstellungsfelder reisen.
- Die einzige Netzwerkanfrage ist die Lizenzaktivierung bzw. -prüfung, und nur wenn Sie einen Schlüssel einfügen.

- [Vollständige Datenschutzerklärung](https://annmax1983.github.io/vkt-veil-mate/privacy-policy.html)

### Berechtigungen

| Berechtigung | Zweck |
|---|---|
| `storage` | Einstellungen (nur Hashes), dauerhafter Sperrzustand und Pro-Daten über `storage.sync` speichern |
| `tabs` | Tabs abdecken, neue Tabs und eingetippte Adressen im gesperrten Zustand abfangen |
| `windows` | Auf Fokuswechsel reagieren, um die Sperre bei Fokusverlust umzusetzen |
| `idle` | Automatische Sperre bei Inaktivität |
| `alarms` | Sperre zur festen Uhrzeit und verzögerte Fokus-Sperre, ohne dass der Hintergrunddienst wach bleiben muss |
| `contextMenus` | Das Kontextmenü (alles sperren / diese Seite lesbar lassen) |
| `https://api.annmax1983.com/*` | Ausschließlich Lizenzaktivierung und -prüfung |

Content Scripts laufen auf `http://*/*` und `https://*/*` und tun genau eines: die Ebene zeichnen, wenn der Service Worker es verlangt.

---

## Urheberrecht

1. VKT VeilMate deckt die Seiten des Browsers auf Ihrem eigenen Gerät ab und verändert, speichert oder überträgt keine Inhalte von Websites.
2. Die Urheberrechte an abgedeckten Seiteninhalten liegen bei den jeweiligen Anbietern; VKT VeilMate erhebt keine Ansprüche darauf.
3. Bei der Nutzung sind lokale Gesetze sowie die Geräte- und Nutzungsrichtlinien des Arbeitgebers zu beachten.

---

## Hinweis zum Quellcode

> ⚠️ **Dieses Repository dient der Entwicklung und dem Verpacken von Releases.** Der Quellcode ist proprietär und darf nicht weiterverbreitet oder neu verpackt werden. Die Erweiterung wird über offizielle Browser-Stores (Chrome Web Store, Microsoft Edge Add-ons, Firefox Add-ons (AMO)) verteilt; Offline-Installationspakete werden Endnutzern nicht bereitgestellt.

---

## Lizenz

Copyright © 2026 VKT VeilMate. Alle Rechte vorbehalten.

Diese Software ist proprietäre Closed-Source-Software. Ohne offizielle schriftliche Genehmigung ist strengstens untersagt:
- Dekompilieren, Cracken oder Verändern des Programmcodes
- Neuverpacken, Weiterverbreiten, Teilen oder gewerblicher Weiterverkauf
- Einbetten in andere Software zur Bündelverteilung

---

## ❤️ Unterstützung

Wenn VKT VeilMate Ihnen hilft, spendieren Sie dem Entwickler doch einen Kaffee!

**[👉 Lizenz erwerben](https://annmax1983.com/extensions/veilmate)** · **[☕ Kaffee spendieren](https://ko-fi.com/annmax?ref=vkt-veil-mate)** · [Quellcode auf GitHub](https://github.com/annmax1983/vkt-veil-mate) · [Offizielle Website](https://annmax1983.com/)
