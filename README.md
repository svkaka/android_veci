# android_veci
interesting code from around the internet

### Custom Preference layout
 <PreferenceCategory
        android:title="@string/wallboard_style"
        android:layout="@layout/divider_preference">
        
<!----layout/divider_preference---->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical">


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

### SnapHelper recycler view

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
