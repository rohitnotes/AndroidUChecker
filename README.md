Android UChecker
==========

Android UChecker is a library to provide a way to check if exists any newer version of your app on the GooglePlay. Works on Android 4.1 (API level 16) and upwards.

[![Release](https://img.shields.io/github/release/raxden/AndroidUChecker.svg?label=maven central)](https://jitpack.io/#raxden/AndroidUChecker/) [![API](https://img.shields.io/badge/API-16%2B-green.svg?style=flat)](https://android-arsenal.com/api?level=16)

## Getting current version published in GooglePlay.

 ```java

UCheckerRequest request = new UCheckerRequest.Builder(this).create();

ReactiveUCheckerProvider provider = new ReactiveUCheckerProvider();
Subscription subscription = provider.retrieveLastVersion(request)
        .subscribeOn(Schedulers.newThread())
        .observeOn(AndroidSchedulers.mainThread())
        .subscribe(new Action1<String>() {
            @Override
            public void call(String currentVersion) {
                doSomethingWithRetrievedCurrentVersion(currentVersion);
            }
        });

```

When you are done (for example in onStop()) remember to unsubscribe.


 ```java

 subscription.unsubscribe();

 ```

## Checking current version published in GooglePlay.

 ```java

UCheckerRequest request = new UCheckerRequest.Builder(this).create();

ReactiveUCheckerProvider provider = new ReactiveUCheckerProvider();
Subscription subscription = provider.checkVersion(request)
        .subscribeOn(Schedulers.newThread())
        .observeOn(AndroidSchedulers.mainThread())
        .subscribe(new Action1<Boolean>() {
            @Override
            public void call(Boolean isLastVersion) {
                doSomething(isLastVersion);
            }
        });

```

## Modify packageName and versionName to compare with Google Play. Simply...

 ```java

UCheckerRequest request = new UCheckerRequest
        .Builder(this)
        .setPackageName("com.google.android.gm")
        .setVersionName("1.0.0")
        .create();

```

## Usage

In order to use the library, there are 3 options:

**1. Gradle dependency**

 - 	Add the following to your `build.gradle`:
 ```gradle
repositories {
	    maven { url "https://jitpack.io" }
}

dependencies {
        compile 'org.jsoup:jsoup:1.10.19'
        compile 'io.reactivex:rxandroid:1.2.1'
        compile 'io.reactivex:rxjava:1.1.6'
	    compile 'com.github.raxden:AndroidUChecker:1.0.7@aar'
}
```

**2. Maven**
- Add the following to your `pom.xml`:
 ```xml
<repository>
       	<id>jitpack.io</id>
	    <url>https://jitpack.io</url>
</repository>

<dependency>
	    <groupId>com.github.raxden</groupId>
	    <artifactId>AndroidUChecker</artifactId>
	    <version>1.0.7</version>
</dependency>
```

**3. clone whole repository**
 - Open your **commandline-input** and navigate to your desired destination folder (where you want to put the library)
 - Use the command `git clone https://github.com/raxden/AndroidUChecker.git` to download the full AndroidUChecker repository to your computer (this includes the folder of the library project as well as the example project)

### Documentation 

For a **detailed documentation**, please have a look at the [**Wiki**](https://github.com/raxden/AndroidUChecker/wiki) or the [**Javadocs**](https://jitpack.io/com/github/raxden/AndroidUChecker/1.0.7/javadoc/).

## LICENSE

    Copyright 2015 Ángel Gómez

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.