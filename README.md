# react-native-custom-in-app-update
Google released the In-App Update feature, but there isn't a supported react-native library for it. Therefore, I implemented a custom solution.

### How to use ?
1. Open the android folder in your React Native project using Android Studio. Add implementation 'com.google.android.play:core:1.7.3' at the end of the dependencies section in the build.gradle(app) file, like so:
```
dependencies {
    implementation fileTree(dir: "libs", include: ["*.jar"])
    //noinspection GradleDynamicVersion
    implementation "com.facebook.react:react-native:+"  // From node_modules


    .......
    implementation 'com.google.android.play:core:1.10.3' // add it at the end of file
}

```
Cick sync after adding the dependency.         

2. Download `CustomInAppUpdateModule.java` and `CustomInAppUpdatePackage.java` files and place in them in the same directory of `MainActivity.java`(`android/app/src/main/java/<package>/`)
3. Change the package names in both CustomInAppUpdateModule.java and CustomInAppUpdatePackage.java to match your project's package name (com.sandeepsingh91.custominappupdate).
4. Open `MainApplication.java` and add `CustomInAppUpdatePackage` to the getPackages method:
```
        @Override
protected List<ReactPackage> getPackages() {
  @SuppressWarnings("UnnecessaryLocalVariable")
  List<ReactPackage> packages = new PackageList(this).getPackages();
  // Packages that cannot be autolinked yet can be added manually here, for example:
  // packages.add(new MyReactNativePackage());
  packages.add(new CustomInAppUpdatePackage());
  return packages;
}
```
5. Download `CustomInAppUpdate.js` and place it into your `react-native` project.
6. Import the `CustomInAppUpdate.js` in any `js` file, wherever you want to use. And use it like below.

```
   useEffect(() => {
    CustomInAppUpdate.checkForUpdate(); // this is how you check for update
  }, []); // empty dependency array ensures this runs only once on mount
```
7. That's it.


### Important Details

1. By default, it's a FLEXIBLE update. If the user doesn't update within 5 days, it becomes an IMMEDIATE update. You can adjust this timeframe by editing STALE_DAYS in CustomInAppUpdateModule.java.
2. Priority updates are not included. You can implement them by modifying the checkForUpdate method in CustomInAppUpdateModule.java. Refer to the Android Developer Guide on In-App Updates for more information.


