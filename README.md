# JCenter Uploader

A gradle script to easily upload Android libraries to *JCenter* for distribution.

**Reference:** For a full article explaining the whole process check this [Medium post](https://medium.com/@yegor_zatsepin/simple-way-to-publish-your-android-library-to-jcenter-d1e145bacf13) written by [Yegor Zatsepin](https://medium.com/@yegor_zatsepin)

*Example:* For a real library uploaded using this process check *[LifecycleCells](https://github.com/Sarquella/LifecycleCells)*

# Usage

In order to upload the library, the following steps must be reproduced:

1. **Setup [Bintray](https://bintray.com)**

	i. Sign in or create an account to *Bintray* (A free open-source account can be created [here](https://bintray.com/signup/oss))
	
	ii. Create a new repository selecting `Maven` as type
	
	iii. Create a new package in the repository, adding the corresponding *GitHub* links (Website, Issue Tracker and VCS)
	
2. **Setup the Android library**

	i. Add the following lines to your `local.properties` file 
	
	**Important**: Make sure it is listed in your `.gitignore` file to avoid uploading it
	
	```
	bintray.user=USERNAME
	bintray.apikey=API_KEY
	```
	
	Where `USERNAME` is your *Bintray* username and `API_KEY` can be retrieved from https://bintray.com/profile/edit
	
	ii. Add the following lines in your library's level `build.gradle` file
	
	```
	buildscript {
		repositories {
			jcenter()
		}
		dependencies {
		    classpath 'com.github.dcendents:android-maven-gradle-plugin:2.1'
				classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.8.4'
		}
	}
	apply plugin: 'com.android.library'
	apply plugin: 'com.github.dcendents.android-maven'
	apply plugin: 'com.jfrog.bintray'
	```

	iii. In the same library's level `build.gradle` file add the following lines. Replace the variable names with the appropriate values for your library
	
	**Note**: Your library will be finally published as `publishedGroupId:artifact:libraryVersion`
	
	```
	ext {
		bintrayRepo = 'BINTRAY_REPOSITORY_NAME'
		bintrayName = 'BINTRAY_PACKAGE_NAME'

		publishedGroupId = 'PUBLISHED_GROUP_ID'
		libraryName = 'LIBRARY_NAME'
		artifact = 'ARTIFACT'

		libraryDescription = 'LIBRARY_DESCRIPTION'

		siteUrl = 'SITE_URL' //https://github.com/<username/<repository>
		gitUrl = 'GIT_URL' //https://github.com/<username/<repository>.git

		libraryVersion = 'LIBRARY_VERSION' //1.0.0

		developerId = 'DEVELOPER_ID'
		developerName = 'DEVELOPER_NAME'
		developerEmail = 'DEVELOPER_EMAIL'

		licenseName = 'LICENSE_NAME' //Ex: The Apache Software License, Version 2.0
		licenseUrl = 'LICENSE_URL' //Ex: http://www.apache.org/licenses/LICENSE-2.0.txt
		allLicenses = [LICENSES] //Ex: ["Apache-2.0"]
	}
	```
	
	iv. In the same library's level `build.gradle` file add the following line
	
	```
	apply from: 'https://raw.githubusercontent.com/Sarquella/JCenter-Uploader/master/jcenter_uploader.gradle'
	```
	
3. **Package and upload**

Finally run the following two commands to upload the library to *JCenter*

```
./gradlew install
./gradlew bintrayUpload
```

# License

[LICENSE](https://github.com/Sarquella/JCenter-Uploader/blob/master/LICENSE)

```
Copyright 2019 Adrià Sarquella Farrés

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

	http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
