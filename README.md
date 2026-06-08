# Zendure Energie Inzicht

[![Release](https://img.shields.io/github/v/release/arnotjes/Zendure-HA-zenSDK-uitbreiding?style=for-the-badge&label=Current%20Version&&labelColor=029c7b&color=0d2e2b)](https://github.com/arnotjes/Zendure-HA-zenSDK-uitbreiding/releases)
[![Beta](https://img.shields.io/badge/status-beta-orange?style=for-the-badge)](https://github.com/arnotjes/Zendure-HA-zenSDK-uitbreiding)

> ⚠️ **Beta versie** — Dit project is nog in actieve ontwikkeling en wordt getest. Gebruik op eigen risico. Feedback en meldingen zijn welkom via [Issues](https://github.com/arnotjes/Zendure-HA-zenSDK-uitbreiding/issues).

Een Home Assistant package die inzicht geeft in je Zendure SolarFlow — energie stromen, accu kosten, opbrengst en terugverdien berekeningen.

> ⚠️ Ontwikkeld en getest op de **SolarFlow 2400 AC**. Mogelijk werkt het ook op andere Zendure types, maar dit is niet getest.

Werkt **volledig los** van andere integraties, of als **uitbreiding op de [Gielz1986 zenSDK](https://github.com/Gielz1986/Zendure-HA-zenSDK)**.

---

## Wat doet het?

- 📊 **Energie stromen** — Zie precies waar je PV energie naartoe gaat: naar de accu, het huis of het net
- 💰 **Accu laadkosten** — Berekent wat het kost om de accu op te laden (via net of PV)
- 💵 **Accu opbrengst** — Berekent wat de accu oplevert bij ontladen
- 📈 **Terugverdien berekening** — Houdt bij hoeveel procent van je aanschafprijs je al terugverdiend hebt
- 🔋 **Accu status** — Laadpercentage, beschikbare energie, efficiëntie en RTE
- 💹 **Nordpool koppeling** — Werkt met dynamische energieprijzen
- 🌡️ **Kostprijs analyse** — Rendabel ontladen/terugleveren indicator

---

## Screenshots

> *Screenshots volgen zodra de eerste stabiele versie klaar is*

<!-- ![Energie Stromen](screenshots/energie_stromen.png) -->
<!-- ![Kosten & Opbrengst](screenshots/kosten_opbrengst.png) -->
<!-- ![Kostprijs & Rendabiliteit](screenshots/kostprijs_rendabiliteit.png) -->
<!-- ![Configuratie](screenshots/configuratie.png) -->

---

## Vereisten

- Home Assistant (2024.1 of nieuwer)
- Zendure SolarFlow verbonden met je netwerk
- [ApexCharts Card](https://github.com/RomRider/apexcharts-card) (HACS) voor de grafieken
- Optioneel: [Nordpool](https://github.com/custom-components/nordpool) (HACS) voor dynamische prijzen
- Optioneel: Homewizard P1 meter

---

## 1️⃣ Installatie

> ⚠️ **Installeer slechts één van de twee yaml bestanden uit de `packages` map — nooit allebei!**

### Optie A — Volledig los (zonder Gielz)

1. Kopieer **alleen** `zendure_energie_inzicht.yaml` naar je `packages` map
2. Zorg dat packages ingeschakeld is in `configuration.yaml`:
   ```yaml
   homeassistant:
     packages: !include_dir_named packages
   ```
3. Herstart Home Assistant
4. Maak een nieuw leeg dashboard aan via ⚙️ → **Dashboards**
5. Klik op de 3 puntjes → **Ruwe configuratie-editor**
6. Plak de inhoud van `dashboard_zendure_energie_inzicht.yaml` en sla op

### Optie B — Samen met Gielz zenSDK

1. Zorg dat `zendure_gielz1986_nl.yaml` al geïnstalleerd is
2. Kopieer **alleen** `zendure_energie_inzicht_addon.yaml` naar je `packages` map
3. Herstart Home Assistant
4. Maak een nieuw leeg dashboard aan via ⚙️ → **Dashboards**
5. Klik op de 3 puntjes → **Ruwe configuratie-editor**
6. Plak de inhoud van `dashboard_zendure_energie_inzicht.yaml` en sla op

---

## 2️⃣ Configuratie

Na installatie stel je het volgende in via het **Configuratie** tabblad in het dashboard:

| Instelling | Omschrijving |
|---|---|
| **Zendure IP-adres** | Lokaal IP-adres van je Zendure *(alleen bij losse installatie)* |
| **Homewizard P1 IP-adres** | IP-adres van je P1 meter *(alleen bij losse installatie)* |
| **Afwijkende P1 Sensor** | Gebruik een eigen P1 sensor in plaats van Homewizard |
| **Afwijkende PV Sensor** | Gebruik een eigen PV sensor (bijv. van je omvormer) |
| **Nordpool Sensor** | Jouw Nordpool sensor voor dynamische prijzen |
| **Teruglever Sensor** | Afwijkend teruglevertarief sensor |
| **15 Minuten Tarieven** | Activeer voor 15-minuten dynamische tarieven |
| **Aanschafprijs Accu** | Vul in voor de terugverdien berekening |

---

## 🔄 Reset knoppen

| Knop | Wat doet het |
|---|---|
| **Reset Statistieken** | Reset de dagelijkse laadkosten en opbrengst *(met bevestiging)* |
| **Reset Terugverdien** | Reset de totale terugverdien berekening *(met bevestiging)* |

---

## Bestanden

| Bestand | Gebruik |
|---|---|
| `zendure_energie_inzicht.yaml` | Volledig losse installatie |
| `zendure_energie_inzicht_addon.yaml` | Uitbreiding op Gielz zenSDK |
| `dashboard_zendure_energie_inzicht.yaml` | Dashboard voor beide installaties |

---

## Credits

- Gebaseerd op en compatibel met [Gielz1986 Zendure-HA-zenSDK](https://github.com/Gielz1986/Zendure-HA-zenSDK)
- Ontwikkeld door [@arnotjes](https://github.com/arnotjes)

---

## Licentie

MIT License
