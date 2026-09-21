# Rilevamento di Attacchi DDoS mediante Tecniche di Machine Learning

Questo repository contiene il codice sorgente sviluppato per la tesi di Laurea in Ingegneria Informatica presso l'Università degli Studi di Enna "Kore".

**Titolo della tesi:** Rilevamento di Attacchi DDoS mediante Tecniche di Machine Learning in un Ambiente di Rete Simulato
**Candidato:** Nicholas Rapisarda
**Relatore:** Prof.ssa Nicole Dalia Cilia
**Correlatore:** Prof. Giovanni Pau

## Descrizione del Progetto

Il progetto simula un ambiente di rete per generare traffico legittimo e traffico malevolo (attacchi DDoS), cattura i pacchetti, costruisce un dataset etichettato e addestra modelli di Machine Learning (MLP, Decision Tree, Random Forest) per il rilevamento degli attacchi.

## Struttura del Repository

I notebook si dividono in due fasi distinte, che vengono eseguite in ambienti diversi.

### Fase 1 — Simulazione della rete (Ambiente GNS3)

I primi 5 notebook devono essere eseguiti all'interno dell'ambiente di rete simulato **GNS3**, installati all'interno dei container Docker che rappresentano i nodi della rete (client, server, vittima). Il loro scopo è generare il traffico e produrre i dataset grezzi.

Devono essere eseguiti nel seguente ordine logico:

1. `firewall.ipynb`: Configura le regole iptables per il filtraggio del traffico sulla porta 80.
2. `generatore_traffico.ipynb`: Genera traffico legittimo (HTTP) da parte dei client simulati.
3. `attacco.ipynb`: Genera il traffico di attacco DDoS simulato.
4. `sniffer.ipynb`: Cattura tutto il traffico sulla rete e genera il dataset integrale (`dataset_tesi_integrale.csv`).
5. `ricevitore.ipynb`: Simula il server web vittima in ascolto sulla porta 80, registrando le connessioni in arrivo.

### Fase 2 — Elaborazione dei dati e Machine Learning (Ambiente locale)

Gli ultimi 2 notebook devono essere eseguiti **in locale**, su un normale computer dotato di Python e delle librerie elencate nella sezione Requisiti. Essi lavorano sui dataset prodotti nella Fase 1 per costruire il dataset etichettato e addestrare i modelli di classificazione.

Devono essere eseguiti nel seguente ordine logico:

6. `etichettatura.ipynb`: Confronta il traffico catturato con i log degli attacchi per etichettare il dataset (`dataset_tesi_etichettato.csv`).
7. `Progetto_MLP_DT_RF.ipynb`: Esegue il preprocessing, l'addestramento e la valutazione dei modelli di Machine Learning.

## Dataset

Il repository include i dataset grezzi necessari per riprodurre l'intera pipeline sperimentale:
- `dataset_tesi_integrale.csv`: Dataset grezzo contenente tutto il traffico di rete catturato dallo sniffer.
- `dataset_attacco.csv`: Dataset contenente i log dei pacchetti malevoli inviati durante la fase di attacco.

Eseguendo i notebook nell'ordine indicato, verranno generati automaticamente i dataset intermedi e finali:
- `dataset_tesi_etichettato.csv` (generato da `etichettatura.ipynb`)
- `dataset_processato.csv`, `datasetTraining.csv`, `datasetTest.csv` (generati da `Progetto_MLP_DT_RF.ipynb`)

> **Nota per chi vuole testare solo i modelli di Machine Learning:** poiché i dataset grezzi (`dataset_tesi_integrale.csv` e `dataset_attacco.csv`) sono già inclusi nel repository, è possibile **saltare completamente la Fase 1** e riprodurre l'intera pipeline di elaborazione eseguendo in locale soltanto i notebook `etichettatura.ipynb` e `Progetto_MLP_DT_RF.ipynb`.

## Requisiti

Per eseguire i notebook sono necessarie le seguenti librerie Python:
- `scapy`
- `pandas`
- `scikit-learn`
- `matplotlib`

## Licenza

Questo progetto è sviluppato esclusivamente a scopo accademico per la tesi di Laurea. Tutti i diritti sono riservati all'autore.
