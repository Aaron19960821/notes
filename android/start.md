## Start

### Overview

- Android Apps may have multiple entry points, the **mainActivity** is the entry of the whole App.
- App can adapt to different devices, UI and SDK...

### Get Start

- **MainActivity** is the activity when u click on the icon of the app.
- a **xml** file will provided to define the UI of an activity.
- a **manifest** file is used to describe the characteristic of the app.
- **gradle** meta file of the project.

### UI Guideline

- layouts(ViewGroup): Container
- widgets(view objects): Object
- Android provides XML for **ViewGroup** and **View** objects.

#### Simple Overview

We take the **constraint view** as an example in this stage.  

- We can set the constraint of an object to the left and right side.  
- Baseline: align the two different objects.
- Use resources to set the UI Strings.
- To make the size flexible, we can make **chains** and complete the restrictions.  

#### Between different views

- We use **Intent** object to bind two components together(Including two activities)

```java
    public void sendMessage(View view)
    {
        Intent intent = new Intent(this, DisplayMessage.class);
        EditText editText = (EditText) findViewById(R.id.editText);
        String message = editText.getText().toString();
        intent.putExtra(EXTRA_MESSAGE, message); //Android enables users to put key-value pairs in their intents
        startActivity(intent);
        return;
    }
```

### Application Fundamentals

The android is a multi-user Linux system and each app is a different user. Each app will have a unique user ID and can only
get access to the data that is only available for their running.  

#### App components

There are four different types of app components: Avtivities, Services, Broadcast receivers and content providers.  

- Activity: Entry point of the user interface.  
- Service: Entry point for keeping an app running in the background for all kinds of reasons. e.g: Music Playing  
- Broadcast receivers: Enable users to deliver events to the app outside of a regular user flow. Notification
- Content providers: Data manager of an app.

#### Activating components

Use the class **Intent** to bind two components together.  

#### The manifest fike

Record the following things:  

- Compoents that the app has.  
- User permissions, API Levels and API libraries that the app needs.

#### Resources

Android use an **xml** file to manage different resources. It will generate an ID for a unique resource. For example:  

```
A resource is stored at res/drawable/, then it will generate an ID called **R.drawable.xxx**
```




