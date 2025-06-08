## Code
1. Generate Certificate keys with
```bash
keytool -genkey -v -keystore upload-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias upload
```

- Put your password and name and some metadata
- Export certificate from these keys with this
```bash
keytool -export -rfc -alias upload -file upload_cert.pem -keystore upload-key.jks
```
- Put these files in `private` dir inside the `android` folder.
2. Go to `android/app/build.gradle.kts` and make sure it's on this format
```kotlin
import java.util.Properties
import java.io.FileInputStream

plugins {
	id("com.android.application")
	id("kotlin-android")
	// The Flutter Gradle Plugin must be applied after the Android and Kotlin Gradle plugins.
	id("dev.flutter.flutter-gradle-plugin")
}

val keystoreProperties = Properties().apply {
	val keystorePropertiesFile = rootProject.file("keystore.properties")
	if (keystorePropertiesFile.exists()) {
		load(keystorePropertiesFile.inputStream())
	}
}

  

android {
	namespace = "com.smartsocial.app"
	compileSdk = 35
	ndkVersion = "27.2.12479018"
	compileOptions {	
		sourceCompatibility = JavaVersion.VERSION_11
		targetCompatibility = JavaVersion.VERSION_11
	}
	
	kotlinOptions {
		jvmTarget = JavaVersion.VERSION_11.toString()
	}
	
	  
	
	defaultConfig {
		applicationId = "com.smartsocial.app"
		minSdk = 29
		targetSdk = 29
		versionCode = flutter.versionCode
		versionName = flutter.versionName
	}
	
	signingConfigs {
		create("release") {
		keyAlias = keystoreProperties["keyAlias"] as? String ?: error("Missing keyAlias in keystore.properties")
		keyPassword = keystoreProperties["keyPassword"] as? String ?: error("Missing keyPassword in keystore.properties")
		storeFile = keystoreProperties["storeFile"]?.let { file(it as String) } ?: error("Missing storeFile in keystore.properties")
		storePassword = keystoreProperties["storePassword"] as? String ?: error("Missing storePassword in keystore.properties")	
		}
	}
	
	buildTypes {
		release {
			signingConfig = signingConfigs.getByName("release")
		}
	}

}

  

flutter {

source = "../.."

}
```

3. for `keystore.properties` is should be under `android` dir with these values
```bash
storePassword=password
keyPassword=password
keyAlias=upload
storeFile=private/upload-key.jks
```
4. run the following for building
```bash
flutter build appbundle --release
```
5. upload certificate to your app in google store console
