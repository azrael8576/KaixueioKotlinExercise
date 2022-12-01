
[【码上开学】](https://rengwuxian.com/tag/kotlin/)Kotlin 課後練習題 分享
## 【码上开学】Kotlin 的变量、函数和类型
### 使用 Android Studio 创建一个基于 Kotlin 的新项目（Empty Activity），添加一个新的属性（类型是非空的 View），在 onCreate 函数中初始化它。
程式碼如下 : 
```kotlin
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
```kotlin
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
## Kotlin 里那些「不是那么写的」
### 创建一个 Kotlin 类，这个类需要禁止外部通过构造器创建实例，并提供至少一种实例化方式。
程式碼如下 : 
```kotlin
class Sample private constructor(){
    companion object{
        fun newInstance(): Sample{
            return Sample()
        }
    }
}

fun main() {
    val sample = Sample.newInstance()
}
```

### 分别用 Array、IntArray、List 实现 「保存 1-100_000 的数字，并求出这些数字的平均值」，打印出这三种数据结构的执行时间。
程式碼如下 : 
```kotlin
     fun createArray() {
        var array : Array<Int>
        var arrayTimeCost = measureTime {
            array = Array(100_000) { it + 1 }
        }
        println("average: ${array.average()}, arrayTimeCost: ${arrayTimeCost.toString()}")
    }

    fun createIntArray() {
        var intArray : IntArray
        var intArrayTimeCost = measureTime {
            intArray = IntArray(100_000) { it + 1 }
        }
        println("average: ${intArray.average()}, intArrayTimeCost: ${intArrayTimeCost.toString()}")
    }

    fun createList() {
        var list : List<Int>
        var listTimeCost = measureTime {
            list = List(100_000) { it + 1 }
        }
        println("average: ${list.average()}, listTimeCost: ${listTimeCost.toString()}")
    }
```
打印出的日志如下：
```
average: 50000.5, arrayTimeCost: 12.222700ms
average: 50000.5, intArrayTimeCost: 3.033400ms
average: 50000.5, listTimeCost: 6.090700ms
```
## Kotlin 里那些「更方便的」
### 请按照以下要求实现一个 Student 类：
- 写出三个构造器，其中一个必须是主构造器
- 主构造器中的参数作为属性
- 写一个普通函数 show，要求通过字符串模板输出类中的属性

程式碼如下 : 
```kotlin
private class Student(var name: String) {
    var id = 0
    var age = 0

    constructor(name: String, id: Int) : this(name) {
        this.id = id
    }
    constructor(name: String, id: Int, age: Int) : this(name, id) {
        this.age = age
    }

    fun show() = println("Student name: ${this.name}, id: ${this.id}, age: ${this.age}")
}
```

### 编写程序，使用今天所讲的操作符，找出集合 {21, 40, 11, 33, 78} 中能够被 3 整除的所有元素，并输出。
程式碼如下 : 
```kotlin
    fun getData() {
        val myList = listOf(21, 40, 11, 33, 78)
        myList.filter { i -> i % 3 == 0 }.forEach { i -> print("$i ") }
    }
```


### End
