01-CharityHub, Sviluppo mobile con supporto di LLM 
Marco Napolitano 886187

## Google / Firebase configuration

Download `google-services.json` from Firebase Console > Project settings > Your
apps for the Android app `it.sal.disco.unimib.charityhub`, then place it at
`app/google-services.json` before building. The file is ignored by Git, including
variant-specific copies under `app/src/`. Existing local copies can stay in place.

For CI, store the complete JSON in a protected configuration variable or file
and write it to `app/google-services.json` before invoking Gradle. Do not print
its contents in build logs or commit generated Google resource files.

The previously committed Google API key remains in Git history. The project
owner should review its API restrictions in Google Cloud Console and replace it
if it was unrestricted or used for non-Firebase services. After replacement,
download a fresh configuration file and update both local and CI copies.

Firebase API keys are client identifiers and remain extractable from the APK;
ignoring the configuration file does not secure Firebase data. Configure the
appropriate API restrictions and Firebase Security Rules as described in the
[Firebase API key documentation](https://firebase.google.com/docs/projects/api-keys).

## GlobalGiving API key

Obtain a new GlobalGiving API key before building. The previously committed key
must be rotated by its account owner because it remains in Git history.

For local development, add the following to the root `local.properties` file,
which is already ignored by Git. Keep any existing Android SDK configuration:

```properties
GLOBALGIVING_API_KEY=YOUR_NEW_GLOBALGIVING_API_KEY
```

For CI, configure `GLOBALGIVING_API_KEY` as a secret environment variable available
to Gradle. The environment variable takes precedence over `local.properties`.
A missing or blank key fails build configuration without printing its value.

BuildConfig receives the configured key for all three GlobalGiving API calls.
This keeps the key out of tracked source, but it remains extractable from the
APK and generated build files. Do not commit or publicly share those files.
