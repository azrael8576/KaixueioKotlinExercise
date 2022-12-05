## Kotlin 的协程用力瞥一眼
### 开启一个协程，并在协程中打印出当前线程名。
程式碼如下 : 
```kotlin
...

class MainActivity : AppCompatActivity() {

    private val TAG = MainActivity::class.java.name

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        CoroutineScope(Dispatchers.Main).launch {
            Log.d(TAG, "當前線程: ${Thread.currentThread().name}")
        }
    }
}
```

打印出的日志如下：
```
2022-12-05 23:19:28.696 14165-14165/com.alex.kotlinbasic D/com.alex.kotlinbasic.MainActivity: 當前線程: main
```

### 通过协程下载一张网络图片并显示出来。
程式碼如下 : 
```kotlin
...

class MainActivity : AppCompatActivity() {
    private val TAG = MainActivity::class.java.name

    private lateinit var mImageIv: ImageView
    private val imgUrl = "https://www.google.com.tw/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png"

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        mImageIv = findViewById<ImageView>(R.id.iv_image)

        CoroutineScope(Dispatchers.Main).launch {
            Log.d(TAG, "當前線程: ${Thread.currentThread().name}")

            val bitmap = getImage(imgUrl)
            mImageIv.setImageBitmap(bitmap)
        }
    }

    private suspend fun getImage(imgUrl: String): Bitmap = withContext(Dispatchers.IO) {
        Log.d(TAG, "withContext(Dispatchers.IO) 當前線程: ${Thread.currentThread().name}")

        val urlParam = URL(imgUrl)
        val openConnection = urlParam.openConnection() as HttpURLConnection
        openConnection.requestMethod = "GET"
        openConnection.connect()
        val inputStream = openConnection.inputStream
        BitmapFactory.decodeStream(inputStream)
    }
}
```

打印出的日志如下：
```
2022-12-06 00:40:22.941 7832-7832/com.alex.kotlinbasic D/com.alex.kotlinbasic.MainActivity: 當前線程: main
2022-12-06 00:40:22.945 7832-7902/com.alex.kotlinbasic D/com.alex.kotlinbasic.MainActivity: getImage() 當前線程: DefaultDispatcher-worker-1
```
