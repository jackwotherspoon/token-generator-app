# token-generator-app
Simple web-app that uses an auth flow to generate a Google OAuth2 access token.

## Setup
1. Use pre-requisites from [Using OAuth2 for Web Server Applications](https://developers.google.com/identity/protocols/oauth2/web-server#python) to setup Web application credentials and consent screen (add the `https://www.googleapis.com/auth/sqlservice.admin` scope during the OAuth consent screen)

2. Download your credentials `.JSON` file, re-naming it `client_secret.json` and moving it beside the application code.

3. Copy the value from the `client_secret` field within your JSON file and paste it onto [Line 36 of app.py](https://github.com/jackwotherspoon/token-generator-app/blob/main/app.py#L36)

## Deploying the App
1. Build the container (replacing `YOUR_PROJECT_ID` with your Google Cloud Project ID)
```sh
gcloud builds submit --tag gcr.io/YOUR_PROJECT_ID/token-app
```

2. Deploy application to Cloud Run (replacing `YOUR_PROJECT_ID` with your Google Cloud Project ID)
```sh
gcloud run deploy token-app --image gcr.io/YOUR_PROJECT_ID/token-app
```

3. Copy the URL of your deployed Cloud Run service and add the base URL as well as the `/oauth2callback` route as re-direct URI's to the previously created [Application Credentials](https://console.developers.google.com/apis/credentials)

> Example: if your Cloud Run service URL is `https://my-service-url.run` then you would add both `https://my-service-url.run` and `https://my-service-url.run/oauth2callback` as re-direct URIs.
