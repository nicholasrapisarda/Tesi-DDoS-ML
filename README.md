# Tesi-DDoS-ML

# Rilevamento di Attacchi DDoS mediante Tecniche di Machine Learning

Questo repository contiene il codice sorgente sviluppato per la tesi di Laurea in Ingegneria Informatica presso l'Università degli Studi di Enna "Kore".

**Titolo della tesi:** Rilevamento di Attacchi DDoS mediante Tecniche di Machine Learning in un Ambiente di Rete Simulato
**Candidato:** Nicholas Rapisarda
**Relatore:** Prof.ssa Nicole Dalia Cilia
**Correlatore:** Prof. Giovanni Pau

## Descrizione del Progetto

Il progetto simula un ambiente di rete per generare traffico legittimo e traffico malevolo (attacchi DDoS), cattura i pacchetti, costruisce un dataset etichettato e addestra modelli di Machine Learning (MLP, Decision Tree, Random Forest) per il rilevamento degli attacchi.

## Struttura del Repository

I notebook sono progettati per essere eseguiti in un ambiente di rete simulato (GNS3) e devono essere eseguiti nel seguente ordine logico:

1. `firewall.ipynb`: Configura le regole iptables per il filtraggio del traffico sulla porta 80.
2. `generatore_traffico.ipynb`: Genera traffico legittimo (HTTP) da parte dei client simulati.
3. `attacco.ipynb`: Genera il traffico di attacco DDoS simulato.
4. `sniffer.ipynb`: Cattura tutto il traffico sulla rete e genera il dataset integrale (`dataset_tesi_integrale.csv`).
5. `ricevitore.ipynb` : Simula il server web vittima in ascolto sulla porta 80, registrando le connessioni in arrivo.
6. `etichettatura.ipynb`: Confronta il traffico catturato con i log degli attacchi per etichettare il dataset (`dataset_tesi_etichettato.csv`).
7. `Progetto_MLP_DT_RF.ipynb`: Esegue il preprocessing, l'addestramento e la valutazione dei modelli di Machine Learning.

## Requisiti

Per eseguire i notebook sono necessarie le seguenti librerie Python:
- `scapy`
- `pandas`
- `scikit-learn`
- `matplotlib`
