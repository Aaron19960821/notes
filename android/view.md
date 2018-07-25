## Layout

The android treats the UI a hierarchy component. There are two kinds of view objects here. The first one is 
**Viewgroup**, it is a container that holds all view objects. The second one is **View** and it is an actual UI object.  

Two ways to declare a layout:  

- Declare UI elements in XML.
- Instantiate layout elements at runtime.  

### Use XML For UI

A simple example of **linear view** is here below:  

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              android:orientation="vertical" >
    <TextView android:id="@+id/text"
              android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:text="Hello, I am a TextView" />
    <Button android:id="@+id/button"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Hello, I am a Button" />
</LinearLayout>
```
To use this **.xml** file, we can just do like the following:  

```java
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.main_layout);
}
```

### Size, Padding and Margins

The **size** of a view object will be expressed by two pairs of values. The first pair
is the value that will be in the parent view and the second is the actual width and height.  

To measure these dimensions, Android use **Padding** to handle these issues.  

### ConstraintLayout


