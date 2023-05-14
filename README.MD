<h2 align="center">  МИНИСТЕРСТВО НАУКИ И ВЫСШЕГО ОБРАЗОВАНИЯ РОССИЙСКОЙ ФЕДЕРАЦИИ ФЕДЕРАЛЬНОЕ ГОСУДАРСТВЕННОЕ БЮДЖЕТНОЕ ОБРАЗОВАТЕЛЬНОЕ УЧРЕЖДЕНИЕ ВЫСШЕГО ОБРАЗОВАНИЯ «САХАЛИНСКИЙ ГОСУДАРСТВЕННЫЙ УНИВЕРСИТЕТ» </h2>
<div align="center">
<h3>Институт естественных наук и техносферной безопасности
<br>
Кафедра информатики
<br>
Половников Владислав Олегович</h3>

<br>
<h3>Лабораторная работа №9
<br>
“Создание интерфейсов с использованием макетов и виджетов”
<br>
01.03.02 Прикладная математика и информатика</h3>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<h3 align="right">Научный руководитель
<br>
Соболев Евгений Игоревич
</h3>

<h3 align="center">Южно-Сахалинск
<br>
2023г.
</h3>
<hr>
</div>
<p>
Kotlin - это высокоэффективный современный язык программирования, разработанный компанией JetBrains. Он имеет очень чёткий и лаконичный синтаксис, что делает ваш код лёгким для чтения. Kotlin широко используется во всём мире, и его популярность среди разработчиков постоянно растёт. Многие разработчики, использующие Kotlin, отмечают, что это делает их работу быстрее и увлекательнее.
</p>

<h3 align="center">Задание</h3>

Упражнение. Сделать функциональный макет
Необходимо реализовать макет по изображению, соблюдая отступы согласно рисунку 1. 

Реализовать простую авторизацию по логину паролю, при удачной попытке вывести пользователю сообщение об авторизации, если пароль логин неверный, то сообщение об ошибке. 

Сделать вторую Activity для восстановления пароля в стилистике рисунка 1, также сделать переход с главной Activity на вторую.





<h1 align="center">Решение</h2>
<h2 align="center">MainActivity</h2>

```kotlin
package com.example.lab7

import android.app.Activity
import android.content.Intent
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.text.TextUtils
import android.widget.Button
import android.widget.EditText
import android.widget.TextView
import android.widget.Toast


class MainActivity : AppCompatActivity() {

    private lateinit var emailText: EditText
    private lateinit var passwordText: EditText
    private lateinit var loginButton: Button
    private lateinit var forgotPassword: TextView


    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        emailText = findViewById(R.id.editText_email)
        passwordText = findViewById(R.id.editText_password)
        loginButton = findViewById(R.id.button_login)
        forgotPassword = findViewById(R.id.forgot_password)


        loginButton.setOnClickListener{
            val email = emailText.text.toString()
            val password = passwordText.text.toString()
            var textFail = false

            if (TextUtils.isEmpty(email)) {
                Toast.makeText(this,R.string.empty_login,Toast.LENGTH_SHORT).show()
                textFail = true
            }

            if (TextUtils.isEmpty(password)) {
                Toast.makeText(this,R.string.empty_password,Toast.LENGTH_SHORT).show()
                textFail = true
            }

            if (textFail == false){
                val foundAccount = accountList.find{ it.login == email}
                if(foundAccount == null) Toast.makeText(this,R.string.fail_login,Toast.LENGTH_SHORT).show()
                else {
                    if(foundAccount.password != password) Toast.makeText(this,R.string.fail_login,Toast.LENGTH_SHORT).show()
                    else Toast.makeText(this,R.string.success_login,Toast.LENGTH_SHORT).show()
                }
            }

        }

        forgotPassword.setOnClickListener {
            val intent = Intent(this, ChangePassword::class.java)
            startActivity(intent)
        }

    }

}

```

<h2 align="center">Accounts</h2>

```kotlin
package com.example.lab7


data class Accounts(val login: String, val password: String)

var accountList = listOf(
    Accounts("admin@mail.ru","1234"), 
    Accounts("test1@mail.ru","111"))

```

<h2 align="center">ChangePassword</h2>

```kotlin
package com.example.lab7

import android.app.Activity
import android.content.Intent
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.text.TextUtils
import android.widget.Button
import android.widget.EditText
import android.widget.Toast

class ChangePassword : AppCompatActivity() {

    private lateinit var emailText: EditText
    private lateinit var changebutton: Button

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_change_password)

        emailText = findViewById(R.id.editText_email)
        changebutton = findViewById(R.id.button_changepassword)

        changebutton.setOnClickListener{
            val email = emailText.text.toString()
            var textFail = false

            if (TextUtils.isEmpty(email)) {
                Toast.makeText(this,R.string.empty_login, Toast.LENGTH_SHORT).show()
                textFail = true
            }


            if (textFail == false){
                val foundAccount = accountList.find{ it.login == email}
                if(foundAccount == null) Toast.makeText(this,R.string.error_change_password,Toast.LENGTH_SHORT).show()
                else {
                    Toast.makeText(this,R.string.success_change,Toast.LENGTH_SHORT).show()
                }
            }
        }
    }


}

```

<h2 align="center">activity_main</h2>

```kotlin
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">


    <TextView
        android:id="@+id/Top_background"
        android:layout_width="match_parent"
        android:layout_height="150dp"
        android:background="@color/orange"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:id="@+id/Top_textview"
        android:layout_width="0dp"
        android:layout_height="70dp"
        android:layout_marginStart="32dp"
        android:layout_marginTop="48dp"
        android:layout_weight="1"
        android:text="@string/top_text"
        android:textColor="@color/white"
        android:textSize="30dp"
        android:textStyle="bold"
        app:layout_constraintEnd_toStartOf="@+id/Top_image"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <ImageView
        android:id="@+id/Top_image"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:layout_marginTop="32dp"
        android:layout_marginEnd="16dp"
        android:layout_weight="1"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:srcCompat="@drawable/quest" />

    <ImageView
        android:id="@+id/imageWaves"
        android:layout_width="match_parent"
        android:layout_height="100dp"
        android:layout_marginTop="-5dp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/Top_background"
        app:srcCompat="@drawable/background" />

    <LinearLayout
        android:id="@+id/layout_email"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:layout_marginStart="32dp"
        android:layout_marginEnd="32dp"
        android:orientation="horizontal"
        android:background="@drawable/rounded_orange"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/imageWaves" >

        <ImageView
            android:id="@+id/imageView"
            android:layout_width="35dp"
            android:layout_height="35dp"
            android:layout_gravity="center"
            android:layout_marginLeft="20dp"
            app:srcCompat="@drawable/email" />

        <EditText
            android:id="@+id/editText_email"
            android:layout_width="wrap_content"
            android:layout_height="match_parent"
            android:background="@android:color/transparent"
            android:hint="@string/login_email"
            android:layout_marginLeft="10dp"
            android:layout_marginRight="15dp"
            android:layout_weight="1"
            android:ems="10"
            android:inputType="textEmailAddress" />
    </LinearLayout>

    <LinearLayout
        android:id="@+id/layout_password"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:layout_marginStart="32dp"
        android:layout_marginTop="16dp"
        android:layout_marginEnd="32dp"
        android:background="@drawable/rounded_orange"
        android:orientation="horizontal"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/layout_email">

        <ImageView
            android:id="@+id/imageView2"
            android:layout_width="35dp"
            android:layout_height="35dp"
            android:layout_gravity="center"
            android:layout_marginLeft="20dp"
            app:srcCompat="@drawable/closed" />

        <EditText
            android:id="@+id/editText_password"
            android:layout_width="wrap_content"
            android:layout_height="match_parent"
            android:layout_marginLeft="10dp"
            android:layout_marginRight="15dp"
            android:layout_weight="1"
            android:background="@android:color/transparent"
            android:ems="10"
            android:hint="@string/login_password"
            android:inputType="textEmailAddress" />
    </LinearLayout>

    <androidx.appcompat.widget.AppCompatButton
        android:id="@+id/button_login"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:layout_marginStart="32dp"
        android:layout_marginTop="16dp"
        android:layout_marginEnd="32dp"
        android:background="@drawable/rounded_orange_solid"
        android:text="@string/button_login"
        android:textColor="@color/white"
        android:textSize="20dp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/layout_password"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/forgot_password"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="32dp"
        android:layout_marginTop="16dp"
        android:layout_marginEnd="32dp"
        android:gravity="center"
        android:text="@string/textview_forgot"
        android:textColor="@color/orange"
        android:textSize="15dp"
        android:textStyle="bold"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/button_login" />

    <TextView
        android:id="@+id/sing_with"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="32dp"
        android:layout_marginTop="32dp"
        android:layout_marginEnd="32dp"
        android:text="@string/sign_with"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/forgot_password" />

    <LinearLayout
        android:id="@+id/layout_sign_with"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginStart="32dp"
        android:layout_marginEnd="32dp"
        android:orientation="horizontal"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/sing_with">

        <ImageView
            android:id="@+id/imageView3"
            android:layout_width="30dp"
            android:layout_height="30dp"
            android:layout_weight="1"
            app:srcCompat="@drawable/google" />

        <ImageView
            android:id="@+id/imageView4"
            android:layout_width="30dp"
            android:layout_height="30dp"
            android:layout_weight="1"
            app:srcCompat="@drawable/fb" />
    </LinearLayout>

    <TextView
        android:id="@+id/register"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="32dp"
        android:layout_marginTop="32dp"
        android:layout_marginEnd="32dp"
        android:text="@string/register"
        android:textColor="@color/orange"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/layout_sign_with"
        android:textStyle="bold"/>

</androidx.constraintlayout.widget.ConstraintLayout>

```

<h2 align="center">activity_change_password</h2>

```kotlin
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">


    <TextView
        android:id="@+id/Top_background"
        android:layout_width="match_parent"
        android:layout_height="150dp"
        android:background="@color/orange"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:id="@+id/Top_textview"
        android:layout_width="0dp"
        android:layout_height="70dp"
        android:layout_marginStart="32dp"
        android:layout_marginTop="48dp"
        android:layout_weight="1"
        android:text="@string/textview_forgot"
        android:textColor="@color/white"
        android:textSize="30dp"
        android:textStyle="bold"
        app:layout_constraintEnd_toStartOf="@+id/Top_image"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <ImageView
        android:id="@+id/Top_image"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:layout_marginTop="32dp"
        android:layout_marginEnd="16dp"
        android:layout_weight="1"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:srcCompat="@drawable/quest" />

    <ImageView
        android:id="@+id/imageWaves"
        android:layout_width="match_parent"
        android:layout_height="100dp"
        android:layout_marginTop="-5dp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/Top_background"
        app:srcCompat="@drawable/background" />

    <LinearLayout
        android:id="@+id/layout_email"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:layout_marginStart="32dp"
        android:layout_marginEnd="32dp"
        android:orientation="horizontal"
        android:background="@drawable/rounded_orange"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/imageWaves" >

        <ImageView
            android:id="@+id/imageView"
            android:layout_width="35dp"
            android:layout_height="35dp"
            android:layout_gravity="center"
            android:layout_marginLeft="20dp"
            app:srcCompat="@drawable/email" />

        <EditText
            android:id="@+id/editText_email"
            android:layout_width="wrap_content"
            android:layout_height="match_parent"
            android:background="@android:color/transparent"
            android:hint="@string/login_email"
            android:layout_marginLeft="10dp"
            android:layout_marginRight="15dp"
            android:layout_weight="1"
            android:ems="10"
            android:inputType="textEmailAddress" />
    </LinearLayout>


    <androidx.appcompat.widget.AppCompatButton
        android:id="@+id/button_changepassword"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:layout_marginStart="32dp"
        android:layout_marginTop="16dp"
        android:layout_marginEnd="32dp"
        android:background="@drawable/rounded_orange_solid"
        android:text="@string/change_password"
        android:textColor="@color/white"
        android:textSize="20dp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/layout_email"
        tools:ignore="MissingConstraints" />


</androidx.constraintlayout.widget.ConstraintLayout>

```
<h2 align="center">strings</h2>

```kotlin
<resources>
    <string name="app_name">lab7</string>
    <string name="login_email">Email</string>
    <string name="login_password">Password</string>
    <string name="button_login">Login</string>
    <string name="textview_forgot">FORGOT PASSWORD?</string>
    <string name="sign_with">OR</string>
    <string name="success_login">Success login</string>
    <string name="fail_login">Incorrect login or password</string>
    <string name="empty_login">Write your username</string>
    <string name="empty_password">Write your password</string>
    <string name="top_text">Already Have an Account?</string>
    <string name="register">New User? Register Now</string>
    <string name="change_password">Change Password</string>
    <string name="error_change_password">Email isn\'t exist</string>
    <string name="success_change">Message with link for change password send on your email</string>
</resources>

```
<h2 align="center">Вывод</h2>
Я научился создавать красивый интерфейс с функционалом