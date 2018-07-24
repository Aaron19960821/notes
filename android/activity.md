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

**Intent filters**: In this stage, 