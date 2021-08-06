# Project Setup
## Gradle

Before installing a project, developers need to learn which libraries and plugins the team will use for the project.

We use a standard set of libraries, look at them bellow.

#### Plugins for app
```groovy
plugins {
    id 'com.android.application'
    id 'kotlin-android'
    id 'kotlin-parcelize'
    id 'kotlin-kapt'
    id 'com.google.gms.google-services' // optional
    id 'com.google.firebase.crashlytics'
}
```

#### Signing Configs
```groovy
signingConfigs {
  prod {
    storeFile file("keys.jks")
    storePassword "storePassword"
    keyAlias "key0"
    keyPassword "keyPassword"
  }
}
```

#### Build types and flavors
```groovy
buildTypes {
  dummy {
    initWith(buildTypes.debug)
  }
  release {
    minifyEnabled false
    proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
  }
}

flavorDimensions "version"
  productFlavors {
    dev {
      dimension "version"
      applicationIdSuffix ".dev"
      versionNameSuffix "-dev"
      
      buildConfigField "String", "BASE_URL", '"https://domain.dev"'
    }
    prod {
      dimension "version"
      buildConfigField "String", "BASE_URL", '"https://domain"'
      signingConfig signingConfigs.prod
    }
}
```


## Dependencies


#### Annotation, [Link](https://developer.android.com/jetpack/androidx/releases/annotation#declaring_dependencies)
```groovy
// Annotation
implementation "androidx.annotation:annotation:1.2.0"
```

#### Lifecycle, [Link](https://developer.android.com/jetpack/androidx/releases/lifecycle#kotlin)
```groovy
def lifecycle_version = "2.4.0-alpha03"

// ViewModel
implementation "androidx.lifecycle:lifecycle-viewmodel-ktx:$lifecycle_version"
// LiveData
implementation "androidx.lifecycle:lifecycle-livedata-ktx:$lifecycle_version"
```

#### ViewBinding Delegate (by Kirill Rozov), [Link](https://github.com/kirich1409/ViewBindingPropertyDelegate#add-library-to-a-project)
```groovy
// ViewBinding Delegate
implementation 'com.github.kirich1409:viewbindingpropertydelegate:1.4.6'
```
 
#### Recycler view with ConcatAdapter, [Link](https://developer.android.com/jetpack/androidx/releases/recyclerview#declaring_dependencies)
```groovy
// include ConcatAdapter
implementation "androidx.recyclerview:recyclerview:1.2.1"
````

#### Navigation Components (for Kotlin), [Link](https://developer.android.com/guide/navigation/navigation-getting-started#groovy)
```groovy
def nav_version = "2.3.5"

// Navigation
implementation "androidx.navigation:navigation-fragment-ktx:$nav_version"
implementation "androidx.navigation:navigation-ui-ktx:$nav_version"
```

#### Activity, Fragment (usually used for result), [Link](https://developer.android.com/jetpack/androidx/releases/activity#declaring_dependencies)
```groovy
def activity_version = "1.3.1"
def fragment_version = "1.3.3"

// Activity, Fragment
implementation "androidx.activity:activity-ktx:$activity_version"
implementation "androidx.fragment:fragment-ktx:$fragment_version"
```

## Facebook 👍
#### Facebook Login, [Link](https://developers.facebook.com/docs/facebook-login/android)

```groovy
// Facebook Login 
implementation 'com.facebook.android:facebook-login:8.1.0'
```
#### Facebook Shimmer, [Link](http://facebook.github.io/shimmer-android/)
```groovy
// Shimmer
implementation 'com.facebook.shimmer:shimmer:0.5.0'
```

## Network
#### Gson, [Link](https://github.com/google/gson#download)
#### Retrofit, [Link](https://square.github.io/retrofit/)
#### Retrofit Converters, [Link](https://github.com/square/retrofit/blob/master/retrofit-converters/gson/README.md)
#### Okhttp, [Link](https://github.com/square/okhttp#releases)

```groovy
def retrofit_version = "2.9.0"
def okhttp3_version = "4.9.1"

// Gson
implementation 'com.google.code.gson:gson:2.8.6'

// Retrofir
implementation "com.squareup.retrofit2:retrofit:$retrofit_version"
implementation "com.squareup.retrofit2:converter-gson:$retrofit_version"

// OhHttp
implementation platform("com.squareup.okhttp3:okhttp-bom:$okhttp3_version")
implementation "com.squareup.okhttp3:okhttp"
implementation "com.squareup.okhttp3:logging-interceptor"
```

## Image Loading
#### Glide, [Link](https://github.com/bumptech/glide#download)
```groovy
repositories {
  google()
  mavenCentral()
}

def glide_version = "4.12.0"

// Glide
implementation "com.github.bumptech.glide:glide:$glide_version"
kapt "com.github.bumptech.glide:compiler:$glide_version"
```
#### Photo Gallery, [Fresco](https://github.com/facebook/fresco#using-fresco-in-your-application), [PhotoDraweeView](https://github.com/ongakuer/PhotoDraweeView#gradle)
```groovy Gallery
// Photo Gallery
implementation 'com.facebook.fresco:fresco:2.5.0'
implementation 'me.relex:photodraweeview:2.0.0'
```

## Coroutines
#### Coroutines, [Link](https://github.com/Kotlin/kotlinx.coroutines#gradle)
```groovy
// Coroutines
implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-core:1.5.1'
```

## Jetpack 🔥
#### Room
```groovy
def room_version = "2.3.0"

// Room
implementation("androidx.room:room-runtime:$room_version")
annotationProcessor "androidx.room:room-compiler:$room_version"
// To use Kotlin annotation processing tool (kapt)
kapt("androidx.room:room-compiler:$room_version")
// Kotlin Extensions and Coroutines support for Room
implementation("androidx.room:room-ktx:$room_version")
```
Configuring Compiler Options
```groovy
android {
    ...
    defaultConfig {
        ...
        javaCompileOptions {
            annotationProcessorOptions {
                arguments += [
                    "room.schemaLocation":"$projectDir/schemas".toString(),
                    "room.incremental":"true",
                    "room.expandProjection":"true"]
            }
        }
    }
}
```
https://developer.android.com/jetpack/androidx/releases/room#declaring_dependencies

## Firebase
#### BoM & Analytics, [Link](https://firebase.google.com/docs/android/setup)
```groovy
// Firebase BoM
implementation platform('com.google.firebase:firebase-bom:26.5.0')
// Firebase Analytics
implementation 'com.google.firebase:firebase-analytics-ktx'
```

#### Firebase Crashlytics, [Link](https://firebase.google.com/docs/crashlytics/get-started?platform=android)
```groovy
// Add the Crashlytics Gradle plugin
classpath 'com.google.firebase:firebase-crashlytics-gradle:2.7.1'

// Firebase Crashlytics
implementation 'com.google.firebase:firebase-crashlytics-ktx'
```

#### Firebase Auth, [Link](https://firebase.google.com/docs/auth/android/start)
```groovy
// Firebase Auth
implementation 'com.google.firebase:firebase-auth-ktx'
```

#### Firestore, [Link](https://firebase.google.com/docs/firestore/quickstart#kotlin+ktx_1)
```groovy
// Firestore
implementation 'com.google.firebase:firebase-firestore-ktx'
```

#### Firebase Dynamic, [Link](https://firebase.google.com/docs/dynamic-links/android/create#set-up-firebase-and-the-dynamic-links-sdk)
```groovy
// Firebase Dynamic
implementation 'com.google.firebase:firebase-dynamic-links-ktx'
```

## Play Services
#### Google auth, [Link](https://developers.google.com/identity/sign-in/android)
```groovy
// Google auth
implementation 'com.google.android.gms:play-services-auth:19.0.0'
```

## UI

#### Image Picker
```groovy
// ImagePicker
implementation 'com.github.dhaval2404:imagepicker:2.0'
```

#### ViewPager2
```groovy
// ViewPager2
implementation "androidx.viewpager2:viewpager2:1.0.0"
```
#### Dots Indicator
```groovy
// Dots Indicator
implementation 'com.tbuonomo:dotsindicator:4.2'
```
https://github.com/tommybuonomo/dotsindicator


#### UI Utils
[Progress Button](https://github.com/razir/ProgressButton#gradle-dependency)
```groovy
// Progress Button
implementation 'com.github.razir.progressbutton:progressbutton:2.1.0'
```

[Rating Bar (with animation)](https://github.com/williamyyu/SimpleRatingBar)
```groovy
// Ratin Bar
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
    }
}

dependencies {
    compile 'com.github.ome450901:SimpleRatingBar:1.5.1'
}
```
[Font awesome](https://github.com/ravi8x/Android-Font-Awesome#how-to-use)
```groovy
// Font Awesome
implementation 'info.androidhive:fontawesome:0.0.5'
```
[CheckBoxGroup](https://github.com/xeoh/CheckBoxGroup)
```groovy
// check box group
implementation 'com.xeoh.android:checkboxgroup:1.0.1'
```

## Additional
```groovy
// Debug
implementation 'com.facebook.stetho:stetho:1.5.1'

implementation 'com.github.rubensousa:gravitysnaphelper:2.2.1'
// check box group
implementation 'com.xeoh.android:checkboxgroup:1.0.1'
```

#### Video 
```groovy
//ScalableVideoView
implementation 'com.yqritc:android-scalablevideoview:1.0.4'
```
#### PDF Viewer 
```groovy
// PDF Viewer
implementation 'com.github.barteksc:pdf-view-pager:1.0.3'
```

## Utils
KeyboardVisibilityEvent, [Link](https://github.com/yshrsmz/KeyboardVisibilityEvent)
```groovy
// Keyboard visibility event
implementation "net.yslibrary.keyboardvisibilityevent:keyboardvisibilityevent:3.0.0-RC3"
```
