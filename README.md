# Scholar Alters
Parse unread emails from Google Scholar alerts and update README.md.

## Setting for First Use
1. Enable Gmail API and Download Credentials
    1. Go to [Google Cloud Console](https://console.cloud.google.com/) 
    2. Create a new project (or select an existing one).
    3. Navigate to APIs & Services → Library, search for Gmail API, and enable it.
    4. Go to APIs & Services → Credentials → Create Credentials → OAuth Client ID.

        - Application type: Desktop app.
        
        - Download the generated credentials.json file and place it in the project root.

    Example structure:
    ```
    .
    ├── credentials.json
    ```

    Example `credentials.json`:
    ```json
    {
         "installed": {
              "client_id": "YOUR_CLIENT_ID",
              "project_id": "YOUR_PROJECT_ID",
              "auth_uri": "https://accounts.google.com/o/oauth2/auth",
              "token_uri": "https://oauth2.googleapis.com/token",
              "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
              "client_secret": "YOUR_CLIENT_SECRET",
              "redirect_uris": [
                    "http://localhost"
              ]
         }
    }
    ```

2. Configure OAuth Consent Screen (In Production)
   1. In Google Cloud Console, go to APIs & Services → OAuth consent screen.
   2. Choose External as the user type.
   3. Fill in all required fields: App name, User support email, Authorized domains, Developer contact info.\
   4. In the Scopes section, add: https://mail.google.com/, https://www.googleapis.com/auth/gmail.readonly
   5. Skip the Test users section.
   6. In the Publishing status section, click Publish App
      
3. Run `script.sh`:
    ```
    bash script.sh
    ```
    For the first run, you will need to log in to your Google account. Ensure that your Gmail account is added as a test user for your app. Refer to this [Stack Overflow post](https://stackoverflow.com/questions/75454425/access-blocked-project-has-not-completed-the-google-verification-process) for guidance.

    This will create a `./data/token.json` file.

4. Copy the information from `token.json` into a GitHub Action secret variable named `TOKEN_CONFIG_JSON`.

    Example `token.json`:
    ```json
    {
         "token": "YOUR_ACCESS_TOKEN",
         "refresh_token": "YOUR_REFRESH_TOKEN",
         "token_uri": "https://oauth2.googleapis.com/token",
         "client_id": "YOUR_CLIENT_ID",
         "client_secret": "YOUR_CLIENT_SECRET",
         "scopes": [
              "https://mail.google.com/",
              "https://www.googleapis.com/auth/gmail.readonly"
         ],
         "universe_domain": "googleapis.com",
         "account": "",
         "expiry": "YOUR_EXPIRY_DATE"
    }
    ```

## Run
Run the following command from your CLI:
```
bash script.sh
```
