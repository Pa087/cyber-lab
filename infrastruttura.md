# Infrastruttura gestita — farmacia

Dal 2014 mi occupo dell'IT di una farmacia con un ruolo ibrido (amministrazione + supporto IT).
Questa pagina descrive cosa gestisco, non come è configurata la rete del mio datore di lavoro:
nessun indirizzo, nessun nome di fornitore, nessuna credenziale.

**Periodo:** 2014 – oggi\
**Utenti serviti:** 7\
**Postazioni e dispositivi:** 10

---

## Postazioni e periferiche

- Installazione, configurazione e manutenzione di postazioni Windows e terminali di cassa
- Stampanti di rete e locali: installazione, driver, risoluzione dei guasti
- Sostituzione hardware e migrazione dati fra postazioni

## Rete

- Troubleshooting di connettività: apparati, cablaggio, DHCP, DNS
- Isolamento del guasto fra rete interna, linea del provider e software house
- Operazioni puntuali sul firewall; la configurazione è in carico a un fornitore esterno

## Account e permessi

- Creazione e chiusura degli account utente
- Permessi sul gestionale in funzione del ruolo
- Rotazione delle credenziali e consegna agli utenti

## Backup

- Backup della documentazione amministrativa: esecuzione, verifica, ripristino
- Il backup principale del gestionale è in carico alla software house

## Supporto agli utenti

- Assistenza in loco e da remoto; la maggior parte delle richieste si chiude internamente
- Punto di contatto unico fra il personale e la software house: raccolta del problema, apertura del ticket, verifica della risoluzione
- Formazione del personale sulle procedure operative

## Contesto normativo

- La farmacia tratta dati personali e dati sanitari, con gli obblighi GDPR che ne derivano
- Procedure amministrative soggette a controllo e tracciabilità

---

## Tre casi

### Mail sospetta su presunti insoluti

- **Sintomo:** il titolare riceve una mail su presunti insoluti che chiede di aprire un link per vedere un documento, e non è sicuro che sia legittima.
- **Diagnosi:** analisi di mittente e header, senza aprire link né allegati. Mittente fuori dal dominio abituale del fornitore, su un servizio di posta consumer, contatto non ricorrente.
- **Soluzione:** verifica out-of-band. Ho contattato il fornitore su un recapito già noto e indipendente dalla mail, e ha confermato di non averla inviata. Mail segnalata e messa in quarantena.
- **Esito:** circa 45 minuti, telefonata compresa. Nessun clic, nessun pagamento, nessuna credenziale esposta.

### POS bloccato da un conflitto di indirizzi IP

- **Sintomo:** pagamenti elettronici bloccati al banco.
- **Diagnosi:** l'indirizzo del POS era già in uso da un altro dispositivo della LAN.
- **Soluzione:** prima la continuità, poi la causa. Vendite spostate sul POS con SIM dati, poi indirizzo libero nella subnet, riserva DHCP legata al MAC del POS e rinnovo della connessione.
- **Esito:** vendite ripartite in circa 5 minuti, correzione definitiva in circa 40. Nessun episodio successivo.
- **Dopo:** inventario degli indirizzi (IP, MAC, dispositivo) e riserve DHCP per tutti i dispositivi fissi critici, con il pool dinamico ridotto.

### Gestionale lento su tutte le postazioni

- **Sintomo:** gestionale rallentato su tutte le postazioni, code al banco.
- **Diagnosi:** il problema era simultaneo su più terminali, quindi un guasto locale era improbabile e sono partito dall'infrastruttura. LAN e raggiungibilità del server regolari. Causa: un processo del gestionale con un consumo di risorse anomalo e prolungato sul server.
- **Soluzione:** prima ho verificato che il servizio associato non fosse condiviso con altri servizi critici. Poi ho terminato il processo e riavviato solo il servizio applicativo, senza riavviare il server e senza fermare la farmacia. Verifica con operazioni reali dalle postazioni: accesso, consultazione, vendita.
- **Esito:** circa 40 minuti, senza interruzione dell'operatività.
- **Dopo:** ricorrenza annotata e segnalazione al fornitore con i dati raccolti. Il gestionale è chiuso e di terzi: la causa del blocco può determinarla solo lui.

---

## Cosa mi porto dietro

- Chiudo un intervento con una verifica funzionale reale (una ricetta elaborata, una stampa, una vendita), non con un "adesso dovrebbe andare"
- Un ambiente dove un fermo blocca il servizio al pubblico: si diagnostica in fretta e si spiega a chi non è tecnico
- Il rapporto quotidiano con un fornitore IT esterno, da entrambi i lati del ticket
- L'abitudine a lavorare dentro procedure controllate e tracciate, con dati che non possono uscire
