# ATLAS SDK (ANDROID)
![android](https://img.shields.io/badge/Android-3DDC84?style=flat&logo=android&logoColor=white) ![version](https://img.shields.io/badge/version-v1.0.0-blue)

ATLAS SDK is used to capture all types of location, document, face, aadhaar, data, video, email, phone, consent, video declaration.

You can find the latest changelog at [Changelog](CHANGELOG.md).

# Table Of Content

- [Set Up Atlas SDK](#set-up-atlas-sdk)
    - [Requirements](#requirements)
    - [Download Atlas SDK](#download-atlas-sdk)
    - [Importing Atlas SDK](#importing-atlas-sdk)
- [Quick Start](#quick-start)
    - [Initialise and run the Atlas SDK](#initialise-and-run-the-atlas-sdk)
- [Atlas Error Codes](#atlas-error-codes)
- [Atlas SDK API](#atlas-sdk-api)
- [Help](#help)


## Set Up Atlas SDK

#### Requirements
Make sure that your project meets these requirements:
- Uses API Level `21` or above as `Minimum SDK Version`
- Uses Gradle 7.3 or later
- Uses Jetpack (AndroidX)

#### Download Atlas SDK
Add the following code to your `project` level `build.gradle` file

```groovy
allprojects {
    repositories {

        //Maven credentials for the Atlas SDK
        ['atlas-sdk-android'].each { value->
            maven {
                url "https://www.repo2.frslabs.space/repository/${value}/"
                credentials {
                    username '<YOUR_USERNAME>' 
                    password '<YOUR_PASSOWRD>' 
                }
            }
        }
    }
}
```

#### Importing Atlas SDK

Add the following code to your `app-level` `build.gradle` file

```groovy
android {

    // ...

    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }

    // ...

}
```

And then, add the dependencies
```groovy

// ...

dependencies {
    
    /*
     * Android Dependencies used by Atlas SDK
     */
    implementation 'androidx.appcompat:appcompat:<latest verison>'
    implementation 'com.google.android.material:material:<latest verison>' 
    implementation 'androidx.constraintlayout:constraintlayout:<latest verison>'

    /*
     * Atlas SDK Core Dependency
     */
    implementation 'com.frslabs.android.sdk:atlas:<latest version>'
}
```

## Quick Start

#### Initialise and run the Atlas SDK

Initialize an instance of `Atlas` with the appropriate parameters, and call `start()` to invoke the Atlas SDK. Refer [Atlas SDK API](#atlas-sdk-api) for more information regarding the individual APIs.

Given below is the fully configured Atlas SDK invokation.

```kotlin
  class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
      super.onCreate(savedInstanceState)
      setContentView(R.layout.activity_main)
      callAtlasSdk()
    }
  
    private fun callAtlasSdk() {
    val atlasConfig = AtlasConfig.Builder()
                .setCheckId("<CHECK_ID>")
                .setUrlId(AtlasUrlType.STAGING) // OPTIONAL: Set environments
                .build()
  
      val atlas = Atlas(atlasConfig)
  
      atlas.start(this, object : AtlasResultCallback {
        override fun onSuccess(atlasResult: String) {
          //CAPTURE SUCCESSFULLY
        }
  
        override fun onFailure(code: Int, message: String) {
          Toast.makeText(this@MainActivity,"Failure",Toast.LENGTH_LONG).show()
        }
      })
    }
  }
```

## Atlas Error Codes

Following error codes will be returned on the `onError` method of the callback

| CODE | DESCRIPTION                                     |
| ---- | ------------------------------------------------|
| 506  | No internet connection                          |
| 507  | Failed to retrieve data                         |
| 508  | Invalid settings                                |
| 509  | Camera permission denied                        |

## Atlas SDK API

See the below table for the public APIs of Atlas SDK,

##### Atlas
| Method/Constructor                                   | Comments    |
|:---------------------------------------------------- |:------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Atlas(AtlasConfig atlasConfig)                                                 | Instantiates the Atlas Object |    
| *start(Context activityContext, AtlasResultCallback atlasResultCallback)*   | Starts the Atlas SDK |

##### AtlasConfig
`AtlasConfig.Builder()` allows to instantiate the `AtlasConfig` object with customisable features. `AtlasConfig` is to be set when instantiating `Atlas` object , See [Atlas](#atlas)
| Method                                               | Default              | Required | Comments    |
|:---------------------------------------------------- |:-------------------- |:-------- |:------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| *setCheckId(String checkId)*                   | NULL                 | Yes      | Sets the check id needed for Atlas SDK                          |
| *setUrlId(AtlasUrlType atlasUrlType)*      | AtlasUrlType.PRODUCTION                | Optional      | If it is **STAGING** then it'll use STAGING base url                         |
| *build()*   | -               | -      | Builds AtlasConfig Instance  |



## Help
For any queries/feedback , contact us at `support@frslabs.com`
```
