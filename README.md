# android_veci
interesting code from around the internet

### Custom Preference layout
```xml
 <PreferenceCategory
        android:title="@string/wallboard_style"
        android:layout="@layout/divider_preference">
 ```
 layout/divider_preference
 
```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    <View
        android:layout_width="match_parent"
        android:layout_height="5dp"
        android:background="@drawable/shadow_view" />
    <TextView xmlns:android="http://schemas.android.com/apk/res/android"
        android:id="@+android:id/title"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textColor="@color/colorAccent"
        android:textSize="14sp"
        android:textStyle="bold" />
</LinearLayout>
```

### SnapHelper recycler view
```java
    void attachSnapHelper(RecyclerView rw) {
        LinearSnapHelper snapHelper = new LinearSnapHelper() {
            @Override
            public int findTargetSnapPosition(RecyclerView.LayoutManager layoutManager, int velocityX, int velocityY) {
                View centerView = findSnapView(layoutManager);
                if (centerView == null)
                    return RecyclerView.NO_POSITION;

                int position = layoutManager.getPosition(centerView);
                int targetPosition = -1;
                if (layoutManager.canScrollHorizontally()) {
                    if (velocityX < 0) {
                        targetPosition = position - 1;
                    } else {
                        targetPosition = position + 1;
                    }
                }

                if (layoutManager.canScrollVertically()) {
                    if (velocityY < 0) {
                        targetPosition = position - 1;
                    } else {
                        targetPosition = position + 1;
                    }
                }

                final int firstItem = 0;
                final int lastItem = layoutManager.getItemCount() - 1;
                targetPosition = Math.min(lastItem, Math.max(targetPosition, firstItem));
                System.out.println("updte toolbar"+targetPosition);
                return targetPosition;
            }
        };
        snapHelper.attachToRecyclerView(rw);
    }
```

 ### Linear row 
 ```xml
     <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_margin="8dp">

        <EditText
            android:id="@+id/weigh"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:hint="_ _ _" />

        <android.support.v7.widget.AppCompatSpinner
            android:layout_width="wrap_content"
            android:layout_height="match_parent"
            android:entries="@array/spinner_delay" />
    </LinearLayout>
```


  

   ### String plural 
 ```xml
    <plurals name="hallo">
        <item quantity="one">Hallo %s you have %d message</item>
        <item quantity="other">Hallo %s you have %d messages</item>
    </plurals>
 ```
 
  ```kotlin
 val text = resources.getQuantityString(R.plurals.hallo,
                count, name, count)
  ```
  
   ### Formatting with HTML tags (some crazy shit) 
 ```xml
<resources>
 //we need those numbers next to placeholder in order to set values
  <string name="welcome_messages">Hello, %1$s! You have &lt;b>%2$d new messages&lt;/b> since %3$s.</string>
</resources>
 ```
 
  ```kotlin
val text = getString(R.string.welcome_messages, username, mailCount)
val styledText: CharSequence = Html.fromHtml(text)
// in case of trouble https://developer.android.com/guide/topics/resources/string-resource#StylingWithHTML
// val escapedUsername = TextUtil.htmlEncode(username)
  ```


### Fragment has option menu
  ```kotlin
    //If true, the fragment has menu items to contribute.
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setHasOptionsMenu(true)
    }
  ```
