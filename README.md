# Home Assistant Blueprints

Blueprinty pre Home Assistant.

## Aqara W100 – ovládanie termostatu

[![Importovať blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/create-link/?redirect=blueprint_import&blueprint_url=https%3A%2F%2Fgithub.com%2FIgypop78%2Fblueprints%2Fblob%2Fmain%2Fautomation%2Faqara_w100_thermostat.yaml)

Tlačidlami +/- na Aqara W100 (Zigbee2MQTT) mení cieľovú teplotu termostatu
(jedno stlačenie = malý krok, dvojité = veľký krok). Cieľová teplota sa zapisuje
do externej teploty W100, takže ju LCD zobrazuje.

**Požiadavky**
- Home Assistant 2024.10 alebo novší
- W100 v Zigbee2MQTT s režimom senzora `external` (entita `number.<nazov>_external_temperature`)

**Vstupy**
| Vstup | Popis |
|---|---|
| Aqara W100 | zariadenie z Z2M |
| Termostat | `climate` entita izby |
| Externá teplota W100 | `number.<nazov>_external_temperature` |
| Krok – jedno stlačenie | predvolene 0,5 °C |
| Krok – dvojité stlačenie | predvolene 1 °C |

**Ručný import:** Nastavenia → Automatizácie a scény → Blueprinty → Importovať blueprint →
`https://github.com/Igypop78/blueprints/blob/main/automation/aqara_w100_thermostat.yaml`

## Kúrenie – otvorené okno

[![Importovať blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/create-link/?redirect=blueprint_import&blueprint_url=https%3A%2F%2Fgithub.com%2FIgypop78%2Fblueprints%2Fblob%2Fmain%2Fautomation%2Fkurenie_otvorene_okno.yaml)

Pri otvorenom okne alebo dverách vypne termostat izby a po zatvorení ho vráti na `heat`.
Jedna automatizácia = jedna izba, každá s vlastnými časmi.

- Okno otvorené dlhšie ako *X* → termostat `off`.
- Okno zatvorené dlhšie ako *Y* → termostat späť na `heat`, ak je vypnutý a **nevypol ho ručne používateľ**
  v HA (dashboard, aplikácia – zmena s používateľom). Funguje aj po reštarte HA a pri opakovanom otváraní.
- Po štarte HA: ak je okno otvorené a termostat kúri, vypne ho.
- Ukladá 20 posledných spustení (trace) na ľahšie dohľadanie.

**Požiadavky**
- Home Assistant 2024.10 alebo novší
- `binary_sensor` okna/dverí a `climate` termostat s režimami `heat` / `off` (napr. generic_thermostat)

**Vstupy**
| Vstup | Popis |
|---|---|
| Okno / dvere | `binary_sensor` (on = otvorené) |
| Termostat | `climate` entita izby |
| Vypnúť kúrenie po otvorení na | predvolene 2 min |
| Zapnúť kúrenie po zatvorení na | predvolene 10 min |

**Obmedzenia**
- Termostat, ktorý vypla iná automatizácia (alebo ručne cez fyzický panel ovládaný automatizáciou),
  sa po zatvorení okna znova zapne.
- Ručné vypnutie pred reštartom HA sa po reštarte nepozná – po zatvorení okna sa termostat zapne.
- Ak sa HA reštartuje počas čakania po zatvorení okna, termostat ostane vypnutý do ďalšieho otvorenia/zatvorenia.

**Ručný import:** Nastavenia → Automatizácie a scény → Blueprinty → Importovať blueprint →
`https://github.com/Igypop78/blueprints/blob/main/automation/kurenie_otvorene_okno.yaml`

## Kúrenie – prikúrenie izieb pri štarte kotla

[![Importovať blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/create-link/?redirect=blueprint_import&blueprint_url=https%3A%2F%2Fgithub.com%2FIgypop78%2Fblueprints%2Fblob%2Fmain%2Fautomation%2Fkurenie_prikurenie_pri_starte_kotla.yaml)

Keď sa zapne kotol, krátko zvýši cieľovú teplotu všetkých zapnutých termostatov a hneď ju vráti.
Izby, ktorým do cieľa chýba len kúsok, sa zapnú spolu s ostatnými a dokúria sa naraz – kotol
potom zbytočne necykluje kvôli jednej izbe. Hodí sa pre `generic_thermostat` s hlavicami on/off.

- Vypnuté termostaty (napr. kvôli otvorenému oknu) preskočí.
- Pôvodné teploty si zapamätá na začiatku a vráti presne tie.

**Požiadavky**
- Home Assistant 2024.10 alebo novší
- spínač kotla (`switch` / `input_boolean`) a `climate` termostaty

**Vstupy**
| Vstup | Popis |
|---|---|
| Kotol | spínač kotla |
| Termostaty | termostaty izieb (viac naraz) |
| Zvýšenie cieľovej teploty | predvolene 0,5 °C |
| Počkať po zapnutí kotla | predvolene 10 s |
| Ako dlho držať zvýšenú teplotu | predvolene 5 s |

**Ručný import:** Nastavenia → Automatizácie a scény → Blueprinty → Importovať blueprint →
`https://github.com/Igypop78/blueprints/blob/main/automation/kurenie_prikurenie_pri_starte_kotla.yaml`
