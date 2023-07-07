# Add-Google-Map-in-Kotlin-Andrid

#build.gradle

```
//app level plugin
id 'com.google.android.libraries.mapsplatform.secrets-gradle-plugin'

// project level plugin
id 'com.google.android.libraries.mapsplatform.secrets-gradle-plugin' version '2.0.1' apply false

 //Google map dependency
 implementation 'com.google.android.gms:play-services-maps:18.1.0'

```

#activity_main.xml
```
                     <fragment
                        android:id="@+id/mapFrag"
                        android:name="com.google.android.gms.maps.SupportMapFragment"
                        android:layout_width="match_parent"
                        android:layout_height="match_parent"
                        app:layout_constraintEnd_toEndOf="parent"
                        app:layout_constraintStart_toStartOf="parent"
                        app:layout_constraintTop_toTopOf="parent"
                        tools:context=".ui.MainActivity" />
```
#MainActivity.kt 

```
class MainActivity : AppCompatActivity(), OnMapReadyCallback {
private var mMap: GoogleMap? = null
 private lateinit var binding: ActivityMainBinding

  override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

       val mapFragment = supportFragmentManager
            .findFragmentById(com.app.app.R.id.mapFrag) as SupportMapFragment
        mapFragment.getMapAsync(this)

        setMap() //call when you have lat long of place
  }

private fun setMap()
{
   val location = LatLng(9.010962, 19.055094)
        mMap?.addMarker(
            MarkerOptions()
                .position(location)
                .title("Place Title")
        )

        mMap?.moveCamera(CameraUpdateFactory.newLatLngZoom(location, 15f))
}

 override fun onMapReady(p0: GoogleMap) {
        mMap = p0
    }

}

```

#MapFragment inside Scroll view

```
 override fun onMapReady(p0: GoogleMap) {
        mMap = p0
        mMap?.setOnCameraMoveStartedListener {

            if (it == GoogleMap.OnCameraMoveStartedListener.REASON_GESTURE) {
                binding.scrollView.requestDisallowInterceptTouchEvent(true);

            } else if (it == GoogleMap.OnCameraMoveStartedListener
                    .REASON_API_ANIMATION
            ) {
                binding.scrollView.requestDisallowInterceptTouchEvent(true);

            } else if (it == GoogleMap.OnCameraMoveStartedListener
                    .REASON_DEVELOPER_ANIMATION
            ) {
                binding.scrollView.requestDisallowInterceptTouchEvent(true);

            }
        };
    }
```

