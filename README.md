# androidAndroidTestBug
Bug demonstration related to https://youtrack.jetbrains.com/issue/KT-39712

To face the issue comment the `afterEvaluate` code block here 👇 https://github.com/VincentMasselis/androidAndroidTestBug/blob/20e22e8de860de9f5f23b2ae4f4022cae18a4ef2/shared/build.gradle#L55 and run this gradle task `:shared:connectedAndroidTest` (no need to plug a device to your computer)

The issue fired by gradle will be:
```
* What went wrong:
Execution failed for task ':shared:checkDebugAndroidTestDuplicateClasses'.
> A failure occurred while executing com.android.build.gradle.internal.tasks.CheckDuplicatesRunnable
   > Duplicate class io.mockk.ValueClassSupportKt found in modules mockk-agent-android-1.12.2-runtime (io.mockk:mockk-agent-android:1.12.2) and mockk-agent-jvm-1.12.2 (io.mockk:mockk-agent-jvm:1.12.2)
```
It append because both `io.mockk:mockk-android` and `io.mockk:mockk` dependencies added to the classpath at the same time. This shoudn't append since theses dependencies are declared into separates sources sets.
