# JCenter Uploader

A gradle script to easily upload Android libraries to *JCenter* for distribution.

**Reference:** For a full article explaining the whole process check this [Medium post](https://medium.com/@yegor_zatsepin/simple-way-to-publish-your-android-library-to-jcenter-d1e145bacf13) written by [Yegor Zatsepin](https://medium.com/@yegor_zatsepin)

# Usage

In order to upload the library, the next steps must be followed:

1. **Setup [Bintray](https://bintray.com)**

	i. Sign in or create an account to *Bintray* (A free open-source account can be created [here](https://bintray.com/signup/oss))
	
	ii. Create a new repository selecting `Maven` as type
	
	iii. Create a new package in the repository
	
2. **Setup the Android library**

	i. Add the following lines to your `local.properties` file 
	
	> **Important**: Make sure it is listed in your `.gitignore` file to avoid uploading it
	
	```
	bintray.user=USERNAME
	bintray.apikey=API_KEY
	```
	
	Where `USERNAME` is your *Bintray* username and `API_KEY` can be retrieved from https://bintray.com/profile/edit
	
	ii. Add the following lines in your **project**'s level `build.gradle` file
	
	`maven_version` [ ![Download](https://api.bintray.com/packages/dcendents/gradle-plugins/com.github.dcendents%3Aandroid-maven-gradle-plugin/images/download.svg) ](https://bintray.com/dcendents/gradle-plugins/com.github.dcendents%3Aandroid-maven-gradle-plugin/_latestVersion)
	
	`bintray_version` [ ![Download](https://api.bintray.com/packages/jfrog/jfrog-jars/gradle-bintray-plugin/images/download.svg) ](https://bintray.com/jfrog/jfrog-jars/gradle-bintray-plugin/_latestVersion)
	
	```
	buildscript {
		//...
		dependencies {
			//...
			classpath "com.github.dcendents:android-maven-gradle-plugin:$maven_version"
			classpath "com.jfrog.bintray.gradle:gradle-bintray-plugin:$bintray_version"
		}
	}
	```

	iii. Add the following lines in your **library**'s level `build.gradle`. Replace the variable names with the appropriate values for your library
	
	 **Note**: Your library will be finally published as `publishedGroupId:artifact:libraryVersion`
	 
	 > Only the mandatory parameters are listed in this example. For a full list of all the available parameters, as well as a brief explanation of each, see the [Parameters](#parameters) section
	
	```
	ext {
		bintrayRepo = 'BINTRAY_REPOSITORY_NAME'
		bintrayName = 'BINTRAY_PACKAGE_NAME'

		publishedGroupId = 'PUBLISHED_GROUP_ID'
		artifact = 'ARTIFACT'
		
		libraryVersion = 'LIBRARY_VERSION'

		gitUrl = 'GIT_URL'

		developerName = 'DEVELOPER_NAME'
		developerEmail = 'DEVELOPER_EMAIL'

		licenseId = 'LICENSE_ID'
		licenseName = 'LICENSE_NAME' 
		licenseUrl = 'LICENSE_URL'
	}
	```
	
	iv. Add the following line in your **library**'s level `build.gradle`
	
	```
	apply from: 'https://raw.githubusercontent.com/Sarquella/JCenter-Uploader/master/jcenter_uploader.gradle'
	```
	
3. **Package and upload**

Finally run the following two commands to upload the library to *Bintray*

```
./gradlew install
./gradlew bintrayUpload
```

# Parameters 

* `bintrayRepo`: Name of the *Bintray* repo created at *1.ii*

* `bintrayName`: Name of the *Bintray* package created at *1.iii*

* `organizaton` [*Optional*]: Organization's *Bintray* username. In case the repo's owner is an organization instead of the username provided at *2.i*

* `publishedGroupId`: Library's group name (e.g., *com.company.library*)

* `artifact`: Library's concrete artifact name

* `libraryVersion`: Library's current version (e.g., *1.0.0*) 

* `libraryDescription` [*Optional*]: Short description about the library 

* `gitUrl`: Version control url (e.g., *https://github.com/<username/<repository>.git*)

* `siteUrl` [*Optional*]: Library's website url

* `developerName`: Library's developer name

* `developerEmail`: Library's developer email

*  `licenseId`: Library's license id (e.g., *Apache-2.0*)

* `licenseName`: Library's license name (e.g., *The Apache Software License, Version 2.0*) 

*  `licenseUrl`: Library's license url (e.g., *http://www.apache.org/licenses/LICENSE-2.0.txt*)

* `overrideExisting` [*Optional*]: Boolean describing if the script should fail (`false`) or not (`true`) when trying to publish an already existing library's version, overriding it. Default is `false`

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
