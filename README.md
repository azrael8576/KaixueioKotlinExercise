[【码上开学】](https://rengwuxian.com/tag/kotlin/)Kotlin 課後練習題 分享
## 【码上开学】Kotlin 的变量、函数和类型
### 使用 Android Studio 创建一个基于 Kotlin 的新项目（Empty Activity），添加一个新的属性（类型是非空的 View），在 onCreate 函数中初始化它。
程式碼如下 : 
```java
package com.alex.kotlinbasic

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.View

class MainActivity : AppCompatActivity() {

    private lateinit var view : View

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        view = findViewById(R.id.view)
    }
}
```

### 声明一个参数为 View? 类型的方法，传入刚才的 View 类型属性，并在该方法中打印出该 View? 的 id。
程式碼如下 : 
```java
package com.alex.kotlinbasic

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log
import android.view.View

class MainActivity : AppCompatActivity() {

    private var view : View? =  null
    private val TAG = MainActivity::class.java.name

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        view = findViewById(R.id.view)
        Log.i(TAG, view?.id.toString())
    }
}
```

打印出的日志如下：
```
2022-12-02 02:29:48.102 11157-11157/com.alex.kotlinbasic I/com.alex.kotlinbasic: 2131231001
``` 
