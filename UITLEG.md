# Uitbreiding Zendure-HA-zenSDK

Getest op: Home Assistant 2026.5.4 met Zendure 2400 AC

## 1. Externe PV omvormer ondersteuning

Standaard gebruikt het pakket de Zendure eigen PV sensoren.
Heb je een externe omvormer (bijv. GoodWe, SMA, Fronius)?
Vul dan `input_text.afwijkende_pv_sensor` in met jouw eigen sensor.

**Werking:**
- Veld leeg → alles werkt zoals altijd (Zendure eigen sensoren)
- Veld ingevuld → vier universele sensoren gebruiken de externe omvormer:
  - `sensor.pv_aansturing_vermogen`
  - `sensor.pv_vermogen_naar_batterij`
  - `sensor.pv_vermogen_naar_huis`
  - `sensor.pv_doorvoer`

✅ Volledig backwards compatible — bestaande gebruikers merken niks.

---

## 2. Accu Kostprijs Analyse

De bestaande methode telt laadkosten direct af bij het laden.
Bij gedeeltelijke cycli geeft dit een vertekend beeld.

**De nieuwe aanpak — elke minuut:**
- Laden van net → kostprijs stijgt (nordpool prijs)
- Laden van PV → kostprijs stijgt NIET (gratis)
- Ontladen → kostprijs daalt proportioneel
- Accu leeg → kostprijs reset naar 0

**Voorbeeld:**
4 kWh net (€0,20) + 4 kWh PV (gratis) = 8 kWh voor €0,80
→ Gemiddelde kostprijs: **€0,10/kWh**

---

## Nieuwe sensoren

| Sensor | Omschrijving |
|---|---|
| `sensor.accu_kwh_in_accu` | Hoeveel kWh zit er nu in de accu |
| `sensor.accu_gem_kostprijs_opgeslagen` | Gemiddelde kostprijs per kWh opgeslagen |
| `sensor.accu_kostprijs_per_kwh_uit` | Kostprijs per kWh na ontlaadverliezen |
| `sensor.accu_marge_per_kwh` | Winst per kWh bij zelfverbruik |
| `sensor.accu_marge_teruglevering` | Winst per kWh bij teruglevering aan net |
| `binary_sensor.accu_rendabel_ontladen` | Ja/Nee: zelfverbruik winstgevend? |
| `binary_sensor.accu_rendabel_terugleveren` | Ja/Nee: terugleveren winstgevend? |
| `sensor.accu_laadkosten_vandaag` | Laadkosten vandaag (reset middernacht) |
| `sensor.accu_besparing_vandaag` | Opbrengst vandaag (reset middernacht) |
| `sensor.accu_netto_besparing_gecorrigeerd` | Totale besparing (handmatig te resetten) |
| `sensor.accu_terugverdien_percentage` | % van aanschafprijs terugverdiend |

---

## Terugleverprijs

De nordpool all-in prijs (inkoop) verschilt van de verkoopprijs
(~€0,13-0,15 verschil in NL).
Stel een aparte sensor in via `input_text.accu_teruglever_sensor`.
Leeg laten = valt terug op de all-in nordpool prijs.

---

## Installatie

1. Vervang `zendure_gielz1986_nl.yaml` door de bijgevoegde versie
2. Herstart Home Assistant
3. Druk op de knop **Accu Statistieken Reset**
4. Vul in de configuratiekaart in:
   - Nordpool sensor
   - PV sensor (optioneel)
   - Teruglever sensor (optioneel)
