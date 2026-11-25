# Ex.No:3 Develop a simple application to play and control the audio file in android studio.


## AIM:

To develop a simple application, to play and control the audio file and to perfrom the start,pause and stop opeartion in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as audiofile and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml and create start,pause and stop button.

Step 6: Display message give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to play and control the audio file”.
Developed by: Vikaskumar M
Registeration Number : 212224220122
*/
```
## MainActivity.java
```java
package com.example.exp_4;

import android.media.MediaPlayer;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import androidx.appcompat.app.AppCompatActivity;
public class MainActivity extends AppCompatActivity {
    private MediaPlayer mediaPlayer;
    private Button btnPlay, btnPause, btnStop;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        btnPlay = findViewById(R.id.btnPlay);
        btnPause = findViewById(R.id.btnPause);
        btnStop = findViewById(R.id.btnStop);
        // Create MediaPlayer and load the audio file from res/raw
        mediaPlayer = MediaPlayer.create(this, R.raw.audio); // replace "song" with your file name
        // Play button
        btnPlay.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (mediaPlayer != null && !mediaPlayer.isPlaying()) {
                    mediaPlayer.start();
                }
            }
        });
        // Pause button
        btnPause.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (mediaPlayer != null && mediaPlayer.isPlaying()) {
                    mediaPlayer.pause();
                }
            }
        });
        // Stop button
        btnStop.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (mediaPlayer != null) {
                    mediaPlayer.stop();
                    // After stop, you must prepare again to play from start
                    try {
                        mediaPlayer.prepare();
                    } catch (Exception e) {
                        e.printStackTrace();
                    }
                }
            }
        });
    }
    // Release MediaPlayer when app is destroyed to save resources
    @Override
    protected void onDestroy() {
        super.onDestroy();
        if (mediaPlayer != null) {
            mediaPlayer.release();
            mediaPlayer = null;
        }
    }
}
```
## activity_main.xml
```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    android:padding="24dp"
    android:background="#17152F">

    <!-- Main Player Card -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:gravity="center"
        android:padding="28dp"
        android:background="@drawable/player_card"
        android:elevation="10dp">

        <!-- Music Icon -->
        <TextView
            android:layout_width="130dp"
            android:layout_height="130dp"
            android:gravity="center"
            android:text="♫"
            android:textSize="75sp"
            android:textColor="#FFFFFF"
            android:background="@drawable/music_circle"/>

        <!-- Title -->
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="NOW PLAYING"
            android:textColor="#B8A8FF"
            android:textSize="13sp"
            android:textStyle="bold"
            android:letterSpacing="0.2"
            android:layout_marginTop="30dp"/>

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Audio Player"
            android:textSize="28sp"
            android:textStyle="bold"
            android:textColor="#FFFFFF"
            android:layout_marginTop="8dp"/>

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Enjoy your favourite music"
            android:textSize="14sp"
            android:textColor="#B9B7CB"
            android:layout_marginTop="6dp"/>

        <!-- Progress Bar -->
        <SeekBar
            android:id="@+id/seekBar"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="30dp"
            android:progressTint="#A78BFA"
            android:thumbTint="#FFFFFF"
            android:progress="35"/>

        <!-- Time -->
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="horizontal"
            android:gravity="center_vertical">

            <TextView
                android:text="00:00"
                android:textColor="#B9B7CB"
                android:textSize="12sp"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"/>

            <View
                android:layout_width="0dp"
                android:layout_height="1dp"
                android:layout_weight="1"/>

            <TextView
                android:text="03:45"
                android:textColor="#B9B7CB"
                android:textSize="12sp"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"/>
        </LinearLayout>

        <!-- Control Buttons -->
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="horizontal"
            android:gravity="center"
            android:layout_marginTop="30dp">

            <Button
                android:id="@+id/btnStop"
                android:layout_width="0dp"
                android:layout_height="55dp"
                android:layout_weight="1"
                android:text="■ Stop"
                android:textColor="#FFFFFF"
                android:textStyle="bold"
                android:textSize="13sp"
                android:backgroundTint="#E05B73"
                android:layout_margin="5dp"/>

            <Button
                android:id="@+id/btnPlay"
                android:layout_width="0dp"
                android:layout_height="60dp"
                android:layout_weight="1.2"
                android:text="▶ Play"
                android:textColor="#FFFFFF"
                android:textStyle="bold"
                android:textSize="14sp"
                android:backgroundTint="#7957E8"
                android:layout_margin="5dp"/>

            <Button
                android:id="@+id/btnPause"
                android:layout_width="0dp"
                android:layout_height="55dp"
                android:layout_weight="1"
                android:text="Ⅱ Pause"
                android:textColor="#FFFFFF"
                android:textStyle="bold"
                android:textSize="13sp"
                android:backgroundTint="#514B78"
                android:layout_margin="5dp"/>

        </LinearLayout>

    </LinearLayout>

    <!-- Footer -->
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="♪  MUSIC PLAYER"
        android:textColor="#88839F"
        android:textSize="12sp"
        android:letterSpacing="0.15"
        android:layout_marginTop="25dp"/>

</LinearLayout>


```
## play_card.xml
```java
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <corners android:radius="28dp"/>
    <gradient
        android:startColor="#29264D"
        android:endColor="#211F3B"
        android:angle="135"/>
</shape>

```
## music_xml
```java
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <corners android:radius="100dp"/>
    <gradient
        android:startColor="#A78BFA"
        android:endColor="#6845CE"
        android:angle="135"/>
</shape>

```
## OUTPUT
<img width="1326" height="734" alt="Screenshot 2026-11-25 213101" src="https://github.com/user-attachments/assets/1675b349-275b-4691-95bc-af49db09317b" />

<img width="292" height="591" alt="Screenshot 2026-11-25 213118" src="https://github.com/user-attachments/assets/2ca96492-8bda-4b8c-af13-1006ca86b687" />

## RESULT
   Thus a simple application, to play and control the audio file and to perfrom the start,pause and stop opeartion in Android Studio is developed and executed successfully.
