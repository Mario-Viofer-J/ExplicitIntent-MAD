# Ex.No:2(b) To create a two screens , first screen will take one number input from user. After click on Factorial button, second screen will open and it should display factorial of the same number using Explicit Intents.


## AIM:

To create a two screens , first screen will take one number input from user. After click on Factorial button, second screen will open and it should display factorial of the same number using Explicit Intents.


## EQUIPMENTS REQUIRED:

Latest Version Android Studio

## ALGORITHM:
1. Start the application with MainActivity as the launcher activity.

2. Display a button in MainActivity to navigate forward.

3. On button click, create an explicit intent from MainActivity to MainActivity2.

4. Start MainActivity2 using the created explicit intent.

5. Display a button in MainActivity2 to navigate forward.

6. On button click, create and start an explicit intent from MainActivity2 to MainActivity3.

7. Register all three activities in the Android Manifest file.


## PROGRAM:
```
/*
Program to print the text “ExplicitIntent”.
Developed by: Mario Viofer J
Registeration Number : 212223100032
*/
```
#### 1. MainActivity.java
```
package com.example.ex2explicit;

import android.content.Intent;
import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

import com.example.ex2explicit.MainActivity2;

public class MainActivity extends AppCompatActivity {
    EditText textVal;
    Button btn;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        textVal = findViewById(R.id.editTextText);
        btn = findViewById(R.id.button);
        btn.setOnClickListener(v->{
            String input=textVal.getText().toString().trim();
            if(input.isEmpty()){
                Toast.makeText(MainActivity.this,"Please enter a number",Toast.LENGTH_SHORT).show();
                return;
            }
            try{
                int num=Integer.parseInt(input);
                if(num<0){
                    Toast.makeText(this, "Enter a non-negative number", Toast.LENGTH_SHORT).show();
                    return;
                }
                Intent intent = new Intent(MainActivity.this, MainActivity2.class);
                intent.putExtra("number",num);
                startActivity(intent);
            } catch (NumberFormatException e) {
                Toast.makeText(this, "Invalid input", Toast.LENGTH_SHORT).show();
            }

        });
    }
}
```
#### 2. ResultActivity.java
```
package com.example.ex2explicit;

import android.os.Bundle;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

import java.math.BigInteger;

public class MainActivity2 extends AppCompatActivity {
    TextView resText;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main2);
        resText = findViewById(R.id.textView4);
        int number = getIntent().getIntExtra("number",0);
        BigInteger fact = factorial(number);
        resText.setText(number+"! = "+fact.toString());
    }
    private BigInteger factorial(int n) {
        BigInteger result = BigInteger.ONE;
        for (int i = 2; i <= n; i++) {
            result = result.multiply(BigInteger.valueOf(i));
        }
        return result;
    }
}

```
#### activity_main.xml
```  
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#FFF8E1"
    android:backgroundTint="#11002A"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textView2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Factorializer"
        android:textColor="#FFFFFF"
        android:textColorHint="#FFFFFF"
        android:textColorLink="#FFFFFF"
        android:textSize="60sp"
        app:layout_constraintBottom_toTopOf="@+id/textView"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.496"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.722" />

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="308dp"
        android:text="Enter a Non-Negative Integer"
        android:textColor="#FFFFFF"
        android:textColorHighlight="#FFFFFF"
        android:textColorHint="#FFFFFF"
        android:textSize="34sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.48"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="36dp"
        android:backgroundTint="#006228"
        android:text="Fatorialize"
        android:textAlignment="center"
        android:textColor="#FFFFFF"
        android:textColorHighlight="#FFFFFF"
        android:textColorHint="#FFFFFF"
        android:textSize="20sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.498"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/editTextText" />

    <EditText
        android:id="@+id/editTextText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="24dp"
        android:ems="10"
        android:hint="eg., 5"
        android:inputType="text"
        android:textAlignment="center"
        android:textColor="#B8B6B6"
        android:textColorHighlight="#BAB5B5"
        android:textColorHint="#C5C1C1"
        android:textSize="24sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.488"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textView" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

#### activity_main2.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#FFF8E1"
    android:backgroundTint="#11002A"
    tools:context=".MainActivity2">

    <TextView
        android:id="@+id/textView3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="216dp"
        android:text="Here's Your Result"
        android:textAlignment="center"
        android:textColor="#FFFFFF"
        android:textColorHint="#FFFFFF"
        android:textColorLink="#FFFFFF"
        android:textSize="34sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.497"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:id="@+id/textView4"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="28dp"
        android:textColor="#FFFFFF"
        android:textColorHint="#FFFFFF"
        android:textColorLink="#FFFFFF"
        android:textIsSelectable="true"
        android:textSize="24sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textView3" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
## OUTPUT
<img width="590" height="1280" alt="image" src="https://github.com/user-attachments/assets/f75161b0-b4b4-4484-b03f-74ea60491de8" />

<img width="590" height="1280" alt="image" src="https://github.com/user-attachments/assets/6333c325-b723-4210-af48-ea897acb0a4e" />


## RESULT
Thus a Simple Android Application create a Explicit Intents using Android Studio is developed and executed successfully.


