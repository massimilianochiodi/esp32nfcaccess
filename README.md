# NFC Access Control System

## Descrizione del Progetto

Questo progetto è un sistema di controllo accessi basato su NFC (Near Field Communication). Utilizza un modulo NFC PN532 per leggere i tag NFC, un modulo Wi-Fi per la connessione a una rete locale e un display TFT per l'interazione utente. Il sistema si integra anche con un server web locale per gestire i tag e visualizzare i log.

### Caratteristiche principali:
- **Lettura tag NFC**: Utilizza il modulo PN532 per leggere i tag NFC MIFARE.
- **Wi-Fi**: Connessione alla rete Wi-Fi per la gestione remota.
- **Server Web**: Permette di aggiungere, rimuovere e visualizzare i tag NFC tramite una pagina web.
- **Display TFT**: Mostra il risultato dell'accesso e altre informazioni.
- **Registrazione Accessi**: Memorizza gli accessi e li visualizza sul server web.
- **Gestione Errori**: Mostra la lista dei tag falliti se l'accesso non è autorizzato.

## Hardware Necessario

- **ESP32** (o altro microcontrollore compatibile con Wi-Fi)
- **Modulo NFC PN532** (per leggere i tag NFC)
- **Display TFT** (per visualizzare i messaggi)
- **Relè** (per controllare l'accesso fisico)
- **Wi-Fi Router** (per la connessione di rete)

## Requisiti Software

- **Arduino IDE** con le seguenti librerie installate:
  - `WiFi.h`
  - `WebServer.h`
  - `HTTPClient.h`
  - `NTPClient.h`
  - `WiFiUdp.h`
  - `ArduinoJson.h`
  - `SPIFFS.h`
  - `Wire.h`
  - `PN532_I2C.h`
  - `PN532.h`
  - `SPI.h`
  - `TFT_eSPI.h`
  - `TimeLib.h`

## Funzionamento

1. **Connessione Wi-Fi**: All'avvio, il sistema si connette alla rete Wi-Fi configurata. Se la connessione ha successo, l'indirizzo IP del dispositivo viene mostrato sul display TFT.
   
2. **Lettura del Tag NFC**: Quando un tag NFC viene avvicinato al lettore PN532, il sistema tenta di leggere il suo UID. Se il tag è autorizzato (ovvero presente nel file JSON), l'accesso viene consentito e il relè viene attivato per un breve periodo. Altrimenti, l'accesso viene negato e viene visualizzato un messaggio di errore sul display.

3. **Gestione tramite Web Server**:
   - Il sistema ospita una semplice pagina web accessibile tramite l'indirizzo IP del dispositivo.
   - Dalla pagina web, puoi aggiungere nuovi tag NFC, rimuovere quelli esistenti e visualizzare la lista dei tag registrati.

4. **File di Configurazione JSON**: I dati dei tag NFC autorizzati (UID, nome, email) vengono memorizzati in un file JSON salvato nel filesystem SPIFFS. Questo file viene letto ogni volta che un tag viene scansionato per verificare se l'accesso è consentito.

## Setup

1. **Connessione hardware**: Collegare il modulo NFC PN532 all'ESP32 e il display TFT come indicato nel codice.
   
2. **Configurazione Wi-Fi**: Sostituire le credenziali Wi-Fi nel codice con quelle della propria rete:
   ```cpp
   const char* ssid = "NomeRete";
   const char* password = "PasswordRete";
