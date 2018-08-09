## Activity

One paradigm of android: The app can be entered from multiple entries. And the entries are called **Activities.**

### Concepts

**Activity** is the entry point for an app to interact with the user. An activity class should be the subclass
of **Activity**. Most time an activity will provide a UI.  

### Configure

To declare an activity, you should just add **<activity>** as a child of **<application>** element. For example:  

```xml
<application>
    <activity android:name=".HelloWorld">
</application>
```

**Intent filters**: In this stage, we use a **intent filter** to show who have the permission to enter this activity.  

### The Activity lifecycle

The lifecycle of an activity: **onCreate, onStart, onResume, onPause, onStop, onDestroy**.  

- onCreate: Must be implemented. Most time it should load saved instanced state and set the content view. 
- onStart: It is when the app is coming into the interactive mode.  
- onResume: When the user is back to the application
- onPause: Means the app is not run on the foreground.
- onStop: When the app is not run 
