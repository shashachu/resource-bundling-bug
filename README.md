Demo project demonstrating a bug where layout files will not be seen as inputs to the `:app:processDebugResources` task if you set with `srcDirs` to the default values.

## Repro
1. Install the app using `./gradlew installDebug` and launch it. Note the background of the activity is purple.
2. Change the background color of the activity to something else.
3. Re-build and install using `./gradlew installDebug` and note the background is still purple.

Commenting out the `srcDirs` block in `app/build.gradle` will fix the issue.

## Other info
* If you run `./gradlew clean installDebug` between layout changes, it will work

## Log output
The `:app:mergeDebugResources` task does recognize that the layout file has changed:
```
Task ':app:mergeDebugResources' is not up-to-date because:
  Input property 'rawLocalResources' file /Users/shasha/code/shashachu/baseresources/app/src/main/res/layout/activity_main.xml has changed.
```

The `:app:processDebugResources` does not:
```
> Task :app:processDebugResources UP-TO-DATE
```
