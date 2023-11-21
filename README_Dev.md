# UTILISATION DEV GN CITIZEN

## Lancement de l'application en mode dev

1. D'abord lancer taxhub (port_number = à celle établi dans la configuration `config.toml` --> `API_TAXHUB`)

   ```sh
    flask run --port <port_number>
   ```

2. Lancement du backend de GN Citizen

   ```sh
   export FLASK_ENV=development;
   export FLASK_DEBUG=1;
   export FLASK_RUN_PORT=5002;
   export FLASK_APP=wsgi;
   python -m flask run --host=127.0.0.1
   ```

3. Lancement du frontend de GN Citizen

   ```sh
   cd frontend
   nvm use
   ng serve
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
