# UTILISATION DEV GN CITIZEN

## Lancement de l'application en mode dev

1. D'abord lancer taxhub (port_number = à celle établi dans la configuration `config.toml` --> `API_TAXHUB`)

   ```sh
   source venv/bin/activate
    flask run --port <port_number>
   ```

2. Lancement du backend de GN Citizen

   ```sh
   source backend/venv/bin/activate
   export FLASK_ENV=development;
   export FLASK_DEBUG=1;
   export FLASK_RUN_PORT=5002;
   export FLASK_APP=wsgi;
   cd backend
   python -m flask run --host=127.0.0.1 --port=5002
   ```

3. Lancement du frontend de GN Citizen

   ```sh
   cd frontend
   nvm use
   npm run start
   ```

Si ça ne fonctionne pas , plusieurs raisons :

- node n'utilise pas la bonne version et donc préciser celle présente ici [https://geonature-citizen.readthedocs.io/fr/latest/devs/init_launch_frontend.html](https://geonature-citizen.readthedocs.io/fr/latest/devs/init_launch_frontend.html)

  - ```sh
    -- possiblement obsolète en fonction de la version , verifier le lien de la doc officielle

    nvm install v10.16
    nvm use v10.16
    ```

- Si ça ne fonctionne toujours pas, suivre les instructions [https://geonature-citizen.readthedocs.io/fr/latest/devs/init_launch_frontend.html](https://geonature-citizen.readthedocs.io/fr/latest/devs/init_launch_frontend.html) et voir pour éxécuter cette partie

  - ```sh
      -- possiblement obsolète en fonction de la version , verifier le lien de la doc officielle

      npm install -g @angular/cli@v8-lts
      npm install
    ```

⚠️ Pour le moment l'utilisation du server side rendering pose problème en local (WIP):

`npm run build:ssr && npm run serve:ssr`

4. Configurer l'app GN_Citizen pour un client

- 4.1 Demander les éléments liés aux mails
  ```py
    # config/config.toml
    # exemple
    [MAIL]
    MAIL_USE_SSL = false
    MAIL_STARTTLS = true
    MAIL_HOST = 'smtp.office365.com'
    MAIL_PORT = 587  # mandatory SSL port
    MAIL_AUTH_LOGIN = 'andria_capai@natural-solutions.eu'
    MAIL_AUTH_PASSWD = 'xxxxxxx'
  ```
- 4.2 Créer un utilisateur et vérifier si on recoit le mail
- 4.3 Ajouter un programme

  ```sh
      db_name='gncitizen'
      sudo -u postgres -s psql -d $db_name -c 'CREATE EXTENSION IF NOT EXISTS "uuid-ossp";'
  ```

  ```sh
     # Ajout d'un programme
     project_name="'project_2'"
     sudo -u postgres -s psql -d $db_name -f /home/andriac/applications/gn-citizen-dev/sql_citizen/add_project.sql -v project_name=$project_name

  ```
- 4.4 Insertion d'une géometrie
    ```sh
     # Ajout d'une geom
     geom_name="'geom_name'"
     desc="'description'"
     sudo -u postgres -s psql -d $db_name -f /home/andriac/applications/gn-citizen-dev/sql_citizen/add_geom.sql -v geom_name=$geom_name
  ```
  
- 4.5 Insertion d'un programme

  ```sh
     # Ajout d'un programme
     id_project=4;
     title="'programme_exemple'";
     id_module=2; # id_module = 2 (inventaire) et 1 = observations taxo
     id_geom=1;
     sudo -u postgres -s psql -d $db_name -f /home/andriac/applications/gn-citizen-dev/sql_citizen/add_program.sql -v id_project=$id_project title=$title id_module=$id_module id_geom=$id_geom
  ```
