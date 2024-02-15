# Blusalt_Document_Verification-Android-Package

## Installation

## Step 1
```sh
#Create a github.properties file in the root folder of android. Path should be like below: E.g. "myDemoApp/android/github.properties"

# Add the following in github.properties:
USERNAME_GITHUB=MyUsernameOnGithub
TOKEN_GITHUB=TokenFromGithubClassicToken
```

## Step 2: build.gradle (project)
```gradle

buildscript {
    ...
}


allprojects {
    def githubPropertiesFile = rootProject.file("github.properties")
    def githubProperties = new Properties()
    githubProperties.load(new FileInputStream(githubPropertiesFile))

    repositories {
      

        maven {
            name "GitHubPackages"
            url 'https://maven.pkg.github.com/Blusalt-FS/Blusalt_Document_Verification-Android-Package'

            credentials {
                username githubProperties['USERNAME_GITHUB']
                password githubProperties['TOKEN_GITHUB']
            }
        }
    }
}


```
## Step 3: build.gradle (app)
```gradle


android{
    minSdkVersion 24
}


dependencies{
    implementation 'net.blusalt:identity_document_verification:1.0-1'
}
```


## USAGE
```sh
## To allow SDK to show a document picker
DocumentType.SELECTOR

## Use this to allow direct access to documents
DocumentType.NIN, DocumentType.BVN, DocumentType.PVC, DocumentType.DRIVERLICENSE, DocumentType.PASSPORT, 

Use without number
  DocumentVerifyManager.getInstance().startSDK(this, apiKey, appName, clientId, isDev, DocumentType.SELECTOR, new DocumentVerifyCompletedCallBack() {
            @Override
            public void onSuccess(ExtractedDocumentResponse response) {

                Log.e("document only success", "" + response);
            }

            @Override
            public void onFailure(int code, String error) {
                Log.e("document only failed", "" + error);
            }
        });


Use with number
  DocumentVerifyManager.getInstance().startSDKWithIdNumber(this, apiKey, appName, clientId, isDev, DocumentType.SELECTOR, "IDNumber", new DocumentVerifyCompletedCallBack() {
            @Override
            public void onSuccess(ExtractedDocumentResponse response) {

                Log.e("document only success", "" + response);
            }

            @Override
            public void onFailure(int code, String error) {
                Log.e("document only failed", "" + error);
            }
        });
```
