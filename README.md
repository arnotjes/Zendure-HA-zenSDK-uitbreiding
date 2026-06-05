# Zendure-HA-zenSDK Uitbreiding

Uitbreiding op het pakket van [Gielz1986](https://github.com/Gielz1986/Zendure-HA-zenSDK).

## Wat is er toegevoegd?

### 1. Externe PV omvormer ondersteuning
Heb je een externe omvormer zoals GoodWe, SMA of Fronius?
Vul dan `input_text.afwijkende_pv_sensor` in met jouw eigen sensor.
Leeg laten = werkt zoals altijd met Zendure eigen sensoren.

### 2. Accu Kostprijs & Besparing
Elke minuut wordt bijgehouden:
- Laden van net → kostprijs stijgt (nordpool prijs)
- Laden van PV → kostprijs stijgt (export prijs)
- Ontladen → kostprijs daalt proportioneel

Nieuwe sensoren:
- `sensor.accu_gem_kostprijs_opgeslagen` — gemiddelde kostprijs per kWh
- `sensor.accu_marge_per_kwh` — winst per kWh bij zelfverbruik
- `binary_sensor.accu_rendabel_ontladen` — is ontladen nu winstgevend?
- `sensor.accu_besparing_vandaag` — besparing vandaag
- `sensor.accu_terugverdien_percentage` — % van aanschafprijs terugverdiend

## Installatie
1. Vervang `zendure_gielz1986_nl.yaml` door de bijgevoegde versie
2. Herstart Home Assistant
3. Druk op de knop **Accu Statistieken Reset**
4. Vul in de configuratiekaart in:
   - Nordpool sensor
   - PV sensor (optioneel)
   - Teruglever sensor (optioneel)
