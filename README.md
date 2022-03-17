## Flutter Mobile build iOS/Android

You can use shared workflows for build mobile and android apps:

For deploying Andorid and iOS apps, should be defined FIREBASE_APP_ID, FIREBASE_IOS_APP_ID and FIREBASE_TOKEN secrets keys

### Android build

```yml
build-android-worflow-name:
  uses: Antoniozinchenko/gh-actions/.github/workflows/build_android.yml
  with:
    base_url: https://qa-app.over-haul.com # App Base Url [REQUIRED]
    auth_url: https://qa-auth-user.aws.over-haul.com # App Auth Url [REQUIRED]
    tracking_url: https://qa-shipment-tracking.aws.over-haul.com # App Tracking Url [Optional]
    notification_url: https://qa-notification.aws.over-haul.com # App notification url [Optional]
    deploy: true # If true, will deploy app with Firebase App Distribution, by dafeult false [Optional]
    release_notes: "Some custom release notes for Firebase App Distribution" # [Optional]
    build_params: --dart-define=DEBUG_MODE=true # additional custom build parameters
  secrets:
    FIREBASE_APP_ID: ${{ secrets.FIREBASE_APP_ID }} # [REQUIRED]
    FIREBASE_TOKEN: ${{ secrets.FIREBASE_TOKEN }} # [REQUIRED]
```


### iOS build

For create ios build, you should export certificates as p12 and create base64 strings. After that, save it as **P12_BASE64** and **P12_PASSWORD**.

Also save as base64 secrets provisioning profiles: **PROVISIONING_PROFILE_PROD_BASE64** and **PROVISIONING_PROFILE_DEV_BASE64**

For more information how to make base64 secrets [check this article](https://damienaicheh.github.io/flutter/github/actions/2021/04/22/build-sign-flutter-ios-github-actions-en.html)

```yml
build-ipa-workflow:
  uses: Antoniozinchenko/gh-actions/.github/workflows/build_ios.yml
  with:
    base_url: https://qa-app.over-haul.com # App Base Url [REQUIRED]
    auth_url: https://qa-auth-user.aws.over-haul.com # App Auth Url [REQUIRED]
    tracking_url: https://qa-shipment-tracking.aws.over-haul.com # App Tracking Url [Optional]
    notification_url: https://qa-notification.aws.over-haul.com # App notification url [Optional]
    deploy: true # If true, will deploy app with Firebase App Distribution, by dafault false [Optional]
    release_notes: "Some custom release notes for Firebase App Distribution" # [Optional]
    build_params: --dart-define=DEBUG_MODE=true # additional custom build parameters [Optional]
    export_options: ExportOptions_prod.plist # Use it for make PROD build only [Optional]
  secrets:
    FIREBASE_IOS_APP_ID: ${{ secrets.FIREBASE_IOS_APP_ID }}  # [REQUIRED]
    FIREBASE_TOKEN: ${{ secrets.FIREBASE_TOKEN }} # [REQUIRED]
    P12_BASE64: ${{ secrets.P12_BASE64 }} # [REQUIRED]
    P12_PASSWORD: ${{ secrets.P12_PASSWORD }} # [REQUIRED]
    PROVISIONING_PROFILE_PROD_BASE64: ${{ secrets.PROVISIONING_PROFILE_PROD_BASE64 }} # [REQUIRED]
    PROVISIONING_PROFILE_DEV_BASE64: ${{ secrets.PROVISIONING_PROFILE_DEV_BASE64 }} # [REQUIRED]
```