# Android15.1
MainActivity
  package com.example.pankaj.sample;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.Toast;

import com.google.android.gms.maps.GoogleMap;
import com.google.android.gms.maps.MapFragment;
import com.google.android.gms.maps.OnMapReadyCallback;

public class MainActivity extends AppCompatActivity implements OnMapReadyCallback {
    private GoogleMap googleMap;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        try {
            // Loading map
            initilizeMap();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    private void initilizeMap() {
        if (googleMap == null) {
            ((MapFragment) getFragmentManager().findFragmentById(
                    R.id.map)).getMapAsync(this);

            // check if map is created successfully or not
            if (googleMap == null) {
                Toast.makeText(getApplicationContext(),
                        "Sorry! unable to create maps", Toast.LENGTH_SHORT)
                        .show();
            }
}

        }


    @Override
    public void onMapReady(GoogleMap map) {
        googleMap = map;

        setUpMap();

    }

    private void setUpMap() {

            googleMap.setMapType(GoogleMap.MAP_TYPE_HYBRID);
           // googleMap.setMyLocationEnabled(true);
            googleMap.setTrafficEnabled(true);
            googleMap.setIndoorEnabled(true);
            googleMap.setBuildingsEnabled(true);
            googleMap.getUiSettings().setZoomControlsEnabled(true);
        }
    }
-----------------------------
activity_main.xml
  <?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.pankaj.sample.MainActivity">

    <fragment
        android:id="@+id/map"
        android:name="com.google.android.gms.maps.MapFragment"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
</RelativeLayout>
---------------------
Manifest
  <?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.pankaj.sample">
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />

    <permission
        android:name="com.example.pankaj.sample.permission.MAPS_RECEIVE"
        android:protectionLevel="signature" />

    <uses-permission android:name="com.example.pankaj.sample.permission.MAPS_RECEIVE" />


    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="com.google.android.providers.gsf.permission.READ_GSERVICES" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />

    <!-- Required to show current location -->
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />

    <!-- Required OpenGL ES 2.0. for Maps V2 -->
    <uses-feature
        android:glEsVersion="0x00020000"
        android:required="true" />

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <meta-data
            android:name="com.google.android.maps.v2.API_KEY"
            android:value="AIzaSyDHphBrBXx8n88PWD6jFnKK9cs27QlRiKA" />
    </application>

</manifest>
