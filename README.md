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
