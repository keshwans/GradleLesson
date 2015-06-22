This is a sample project to demonstrate multi-flavored Android builds using Gradle

1) It is setup to generate 4 possible variants of the module apk: 
	two productFlavors: "demo" and "full"
	two buildTypes : "debug" or "release"

To generate the signed apk for a release build for "full" flavor:(creates app-full-release.apk)
	./gradlew assembleFullRelease

To generate all 4 apks ("full" and "demo" flavors + "debug" or "release" buildType)
	./gradlew assemble

This will create:
	./app/build/outputs/apk/app-demo-debug.apk
	./app/build/outputs/apk/app-demo-release.apk
	./app/build/outputs/apk/app-full-debug.apk
	./app/build/outputs/apk/app-full-release.apk

We upload the *-release.apk files to the Play Store

Note:
You will also find the intermediate versions of apk files. 
Build process creates them first, then signs it with the digital certificate to produce the corresponding above apk files.
 
	./app/build/outputs/apk/app-demo-release-unaligned.apk
	./app/build/outputs/apk/app-demo-debug-unaligned.apk
	./app/build/outputs/apk/app-full-debug-unaligned.apk
	./app/build/outputs/apk/app-full-release-unaligned.apk

2) common gradle commands:
To show all the build tasks supported by the build.gradle:
	./gradlew tasks

To clear files created by build process (your source files will not be touched):
	./gradlew clean


3a) The gradle.properties file has an optional property:
	projectSigningPropertiesFile=./keystore.properties

3b) The module's build.gradle checks this property to locate a file that has keystore related configuration.

3c) If the above file exists, build.gradle will read the path to keystore file and the passwords from that file.

3d) If the above property does not exists, then the script will prompt for passoword interactively.

3e) The keytore. properties file used in 3b) should generally not be added to git repo. It should be manually created for a central build enviroment. All others should enter the passwords when prompted.
I have NOT yet added this to .gitignore - just so that you have a sample to start with.

3f) "app" modules build.gradle file has println statements to assist in debugging signing related configuration.
The println statements related to passwords have been commented out in build.gradle, so that passwords are not exposed. Uncomment temporarily if you need to debug.


