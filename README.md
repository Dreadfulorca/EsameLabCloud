WebGL App Containerizzata
Questo progetto realizza un'infrastruttura containerizzata per un'applicazione WebGL accessibile solo previa autenticazione. Tutti i componenti sono orchestrati tramite Docker Compose e isolati in container separati per una maggiore sicurezza e manutenibilità.

🔧 Stack Tecnologico
	• Nginx – Reverse Proxy (porta 8080)
	• Node.js + Express – Servizio di autenticazione
	• MySQL 8.0 – Database relazionale
	• Apache HTTP Server – Hosting dell'applicazione WebGL
	• Docker Secrets – Gestione sicura della password del database

📦 Prerequisiti
	• Docker installato
	• Docker Compose installato
	• Porta 8080 disponibile

🚀 Avvio del Progetto
1. Clona il repository
git clone https://github.com/Dreadfulorca/EsameLaboratorioCloud.git
cd EsameLaboratorioCloud
2. Avvia i container
docker compose up -d
3. Verifica lo stato dei servizi
docker compose ps

🌐 Accesso all’Applicazione
Apri il browser e visita:
http://localhost:8080
Credenziali di test
	• admin / admin123
	• user1 / password123
	• demo / demo123
Dopo il login verrai reindirizzato automaticamente all'app WebGL.

📁 Struttura del Progetto
.
├── docker-compose.yml          # Definizione e orchestrazione dei servizi
├── .env                        # Variabili d'ambiente personalizzabili
├── secrets/
│   └── db_password.txt         # Password del DB gestita con Docker Secrets
├── nginx/
│   └── nginx.conf              # Configurazione del reverse proxy
├── mysql/
│   └── init.sql                # Script di inizializzazione del database
├── auth/                       # Backend di autenticazione (Node.js)
│   ├── Dockerfile
│   ├── server.js
│   ├── package.json
│   └── public/
│       └── login.html
└── webapp/                     # Applicazione WebGL servita da Apache
    ├── Dockerfile
    └── [file dell'app WebGL]


⚙️ Configurazione
Variabili d’Ambiente (.env)
	• DB_NAME – Nome del database MySQL
	• DB_USER – Nome utente del database
	• NGINX_PORT – Porta pubblica esposta (default: 8080)
Docker Secrets
	• La password del database è salvata in secrets/db_password.txt e montata in modo sicuro tramite Docker.

🧰 Comandi Utili
Azione	Comando
Avvio servizi	docker compose up -d
Stop dei servizi	docker compose down
Visualizzazione log	docker compose logs [nome-servizio]
Rebuild di un servizio	docker compose up -d --build [servizio]
Accesso al database	docker compose exec mysql mysql -u webgl_user -p webgl_app

❗ Risoluzione Problemi
	• App non disponibile:
		○ Verifica che la porta 8080 sia libera
		○ Controlla i log: docker compose logs
		○ Assicurati che tutti i container siano attivi: docker compose ps
	• Errore di connessione al database:
		○ Attendi qualche secondo per l'inizializzazione
		○ Verifica i log del servizio di autenticazione: docker compose logs auth
	• Reset completo dell'ambiente:
docker compose down -v
docker compose up -d

🔐 Sicurezza
	• Solo Nginx è esposto all'esterno (porta 8080)
	• Autenticazione obbligatoria per accedere all'applicazione
	• Comunicazione sicura tra container su rete interna Docker
	• Password database protetta tramite Docker Secrets

🛠️ Sviluppo
Modifica dell'app WebGL
	• Aggiorna i file all’interno di webapp/
	• Ricostruisci il container:
docker compose up -d --build webapp
Modifica del sistema di autenticazione
	• Lavora sulla directory auth/
Ricostruisci il container:
docker compose up -d --build auth
