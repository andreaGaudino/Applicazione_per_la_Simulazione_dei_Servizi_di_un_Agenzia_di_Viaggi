# Applicazione per la Simulazione dei Servizi di un’Agenzia di Viaggi

Questo documento fornisce le istruzioni per la configurazione, l'installazione e l'avvio dell'applicazione per la simulazione dei servizi di un'agenzia di viaggi, inclusi i dettagli su come connettersi al server MySQL.

Nella cartella **documents** è presente la relazione tecnica in formato docx e pdf.

## Istruzioni per l'Utilizzo e l'Avvio

### 1. Preparazione del Progetto

- Effettuare il fork del progetto al seguente URI e clonarlo nel proprio ambiente di sviluppo: https://github.com/TdP-prove-finali/GaudinoAndrea

- Importare il progetto nel proprio ambiente di sviluppo.

### 2. Prerequisiti Software

- Prima di eseguire il codice Python, assicurarsi di aver installato la libreria necessaria per la gestione della connessione MySQL.

- Installare MySQL Connector/Python
   
- Installare la libreria richiesta tramite pip:
###
     pip install mysql-connector-python

### 3. Configurazione del Database (MySQL)

  Questa sezione spiega come configurare le credenziali e importare i dati necessari per l'applicazione.

  ### A. Configurazione del File connector.cnf
Il codice Python utilizza la classe DBConnect per gestire un pool di connessioni al database. Questa classe legge le credenziali da un file di configurazione chiamato connector.cnf.

Azioni richieste:

1. Creare/Modificare il file connector.cnf.

2. Posizionare il file nella stessa directory del file Python contenente la classe DBConnect.

3. Sostituire YOUR_MYSQL_USERNAME e YOUR_MYSQL_PASSWORD con le proprie credenziali del server MySQL.

###
  
    user: Nome utente MySQL (es. root, db_user)
    
    password: Password per l'utente specificato
    
    host: Indirizzo del server MySQL (es. 127.0.0.1 per locale)
    
    database: Nome del database di destinazione (deve essere travel)

###

Contenuto di connector.cnf:

###
    [client]
    user=YOUR_MYSQL_USERNAME
    password=YOUR_MYSQL_PASSWORD
    host=127.0.0.1
    database=travel
    raise_on_warnings=True

  ### B. Importazione del Data-set
L'applicazione richiede l'esistenza di specifici dati e tabelle nel database.

Azioni richieste:

  1. Importare il data-set denominato script_finale.
  
  2. Il file SQL di importazione si trova all'interno della cartella database del progetto.
  
  3. Eseguire lo script SQL sul proprio server MySQL per creare il database travel e popolare le tabelle.



### 4. Come Avviene la Connessione (Dettagli Tecnici)
Il metodo di classe DBConnect.get_connection() localizza il file connector.cnf in modo dinamico.

La libreria MySQL Connector/Python legge le credenziali dal file grazie alla riga:

###
    option_files=f"{pathlib.Path(__file__).resolve().parent}/connector.cnf"

  1. pathlib.Path(__file__).resolve().parent risolve il percorso completo alla directory che contiene lo script Python.
  
  2. Aggiunge /connector.cnf per creare il percorso completo al file di configurazione.
  
  3. Il pool di connessioni MySQL utilizza le credenziali trovate nella sezione [client] di quel file per stabilire le connessioni.



### 5. Avvio del Programma
Una volta completata la configurazione del database e del file connector.cnf eseguire il file **main.py** del progetto per avviare il programma.

Per una presentazione video, visitare il seguente link:
https://www.youtube.com/watch?v=aG2oLluywMc
