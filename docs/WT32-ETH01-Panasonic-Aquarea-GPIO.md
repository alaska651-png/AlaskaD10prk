# WT32-ETH01 / Panasonic Aquarea — collegamenti GPIO

Schema di cablaggio concordato per il firmware HeishaMon personalizzato. **Il CZ-TAW1 resta scollegato durante la prima fase di test.**

## Panasonic CN-CNT ↔ level shifter ↔ WT32-ETH01

| Segnale Panasonic | Level shifter | WT32-ETH01 |
|---|---|---|
| TX Panasonic | HV2 → LV2 | GPIO35 (RX) |
| RX Panasonic | HV1 ← LV1 | GPIO17 (TX) |
| GND | GND comune | GND |
| +5 V CN-CNT | HV (alimentazione lato 5 V del convertitore) | **Non collegare al 5V della ESP32** |
| 3V3 ESP32 | LV (alimentazione lato 3,3 V del convertitore) | 3V3 |

- UART: 9600 baud, 8E1.
- Alimentazione WT32-ETH01: **5 V stabilizzati esterni**, con corrente disponibile adeguata, sul pin 5V e GND.
- Non collegare direttamente segnali a 5 V ai GPIO della ESP32.
- Il level shifter HV/LV non è un isolatore galvanico; verificare la massa comune e la compatibilità dei livelli logici.
- Non unire il +5 V Panasonic e il +5 V dell'alimentatore esterno.
- Pin CN-CNT +12 V: **non utilizzato**.

## Collegamenti CZ-TAW1 (fase successiva, NON collegare ora)

| Segnale CZ-TAW1 | Level shifter | WT32-ETH01 |
|---|---|---|
| RX CZ-TAW1 | HV3 ← LV3 | GPIO14 (TX) |
| TX CZ-TAW1 | HV4 → LV4 | GPIO36 (RX) |

**Nota:** i collegamenti del proxy CZ-TAW1 e la sua alimentazione originale devono essere verificati prima dell'attivazione; non alimentare il CZ-TAW1 dal pin 5V della ESP32.

## Stato del progetto (05/11/2026)

- Panasonic ↔ WT32-ETH01: comunicazione riuscita, letture HeishaMon al 100% corrette dopo intervento sul cavo.
- CZ-TAW1: scollegato, da affrontare per ultimo.
- Prossimo obiettivo: MQTT → Home Assistant → dashboard con setpoint, potenze e COP.
- I comandi scrivibili dipendono dal firmware effettivamente caricato; testare e confermare prima di abilitarli in HA.

Questo documento registra il cablaggio concordato; non sostituisce il manuale Panasonic né una verifica elettrica sul posto.
