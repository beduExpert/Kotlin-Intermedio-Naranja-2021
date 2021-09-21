[`Kotlin Intermedio`](../../Readme.md) > [`Sesión 06`](../Readme.md) > `Ejemplo 1`

## Ejemplo 1: Components

<div style="text-align: justify;">

### 1. Objetivos :dart:

- Implementar `Components` de Material Design en nuestra interfaz.

### 2. Requisitos :clipboard:

1. Android Studio Instalado en nuestra computadora.
2. Seguir la instrucción específica para esta sesión.

### 3. Desarrollo :computer:

La meta de este ejercicio es simple: agregar algunos de los components básicos a nuestro _layout_ y asignarles funcionalidad.

Para lograrlo realiza los siguientes pasos:

1. Abre __Android Studio__ y crea un nuevo proyecto con Activity Vacía (Empty Activity).

2. Abrimos ___app/build.gradle___ y en ___dependencies___, agregar la siguiente línea:

```kotlin
api 'com.google.android.material:material:1.3.0-alpha03'
```

Esto para tener disponible los componentes.

3. Para poder implementar satisfactoriamente nuestros `components`, creamos el archivo ___res/values/styles.mxl___ y agregamos el siguiente código. Notemos nuestro ___AppTheme___.

```xml
<resources>
    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.MaterialComponents.Light.DarkActionBar">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
    </style>

</resources>
```

y agregamos los siguiente colores a los values.

```xml
    <color name="colorPrimary">#6200EE</color>
    <color name="colorPrimaryDark">#3700B3</color>
    <color name="colorAccent">#03DAC5</color>
```

4. Abrimos el archivo ___activity_main.xml___, donde colocaremos algunos de los componentes que nos provee la biblioteca de material. Recordemos que antes de existir la biblioteca ___com.google.android.material___,  utilizábamos ___com.android.support:design___.


Ahora, vamos a utilizar el primer `component`: `TextInputLayout`.

```xml
<com.google.android.material.textfield.TextInputLayout
        android:id="@+id/inputLayout"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_margin="4dp"
        android:hint="Usuario">
        <com.google.android.material.textfield.TextInputEditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:inputType="text"
            android:maxLines="1" />
    </com.google.android.material.textfield.TextInputLayout>
```
Este componente es un `wrapper` que contiene un EditText, y provee de un `label` en la parte superior igual al hint del `EditText` cuando el usuario ingresa un texto. El `EditText` que utilizamos es un `TextInputEditText`, también perteneciente a la biblioteca de material design.

Podemos agregar un `EditText` simple para resaltar la diferencia entre estos dos.

```xml
    <EditText
        android:id="@+id/editNormal"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        app:layout_constraintTop_toBottomOf="@id/inputLayout"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:hint="Usuario"
        android:maxLines="1"
        android:layout_margin="4dp"/>
```

5. El siguiente elemento a probar, será el `MaterialButton`, que viene preconfigurado con el estilo _Material_ por defecto, sin requerir configurar la propiedad `style`.

<img src="images/1.png" width="40%">

Según Material Design, el botón con mayor importancia es un _contained button_, y la de menor importancia es un `text button`, por lo que vamos a replicar ese patrón:

```xml
    <com.google.android.material.button.MaterialButton
        android:id="@+id/cancel_button"
        style="@style/Widget.MaterialComponents.Button.TextButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginEnd="12dp"
        android:layout_marginRight="12dp"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toStartOf="@id/next_button"
        app:layout_constraintTop_toBottomOf="@id/editNormal"
        android:text="Cancelar" />

    <com.google.android.material.button.MaterialButton
        android:id="@+id/next_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Aceptar"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toEndOf="@id/cancel_button"
        app:layout_constraintTop_toBottomOf="@id/editNormal" />
```

Como podemos observar, al `text button` se le agrega un estilo de Material Components, mientras que el `contained`, utiliza el estilo por defecto.

Para corroborar que tanto las propiedades de estos `Buttons` como sus métodos funcionan como cualquier `Button`, utilizaremos su `listener`: 

declararmos las variables:

```kotlin
private lateinit var nextButton: MaterialButton
 private lateinit var cancelButton: MaterialButton
```

Relacionamos las variables al `View`:

```kotlin
 nextButton = findViewById(R.id.next_button)
 cancelButton = findViewById(R.id.cancel_button)
```

Y asignamos su respectivo click listener:

```kotlin
nextButton.setOnClickListener{
  Toast.makeText(this,getString(R.string.accept),Toast.LENGTH_SHORT).show()
}

cancelButton.setOnClickListener{
  Toast.makeText(this,getString(R.string.cancel),Toast.LENGTH_SHORT).show()
}
```

6. La biblioteca contiene muchos otros componentes listos para utilizarse, así que implementaremos otros dos: 

```xml
    <com.google.android.material.slider.Slider
        android:id="@+id/slider"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Aceptar"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="1.0"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/next_button" />
    <com.google.android.material.checkbox.MaterialCheckBox
        android:id="@+id/checkbox"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Aceptar"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/slider" />
```

Los cuales son un Slider y un Checkbox.

7. Por último, exploraremos un componente bastante característico en `material design`: El CardView. De acuerdo al sitio oficial:

> Cards contain content and actions about a single subject.

Estos elementos pueden ser una representación gráfica de un objeto o una lista de objetos, como productos, ciudades, contactos, etc. y dentro de ellas se pueden detonar acciones mediante botones.

<img src="images/3.png" width="40%">


Agregaremos un `CardView` sencillo, con un header superior con color `PrimaryDark` que simule un archivo media en la parte superior, como lo sugiere la imagen anterior. La dotaremos de un título y un subtítulo, contenidos por un `LinearLayout` horizontal.

```xml
    <com.google.android.material.card.MaterialCardView
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toBottomOf="@id/checkbox"
        android:layout_width="200dp"
        android:layout_height="180dp"
        app:cardBackgroundColor="?attr/colorPrimaryDark"
        app:cardCornerRadius="4dp">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_gravity="bottom"
            android:background="#FFFFFF"
            android:orientation="vertical"
            android:padding="8dp">

            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:padding="2dp"
                android:text="Titulo"
                android:textAppearance="?attr/textAppearanceHeadline6" />

            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:padding="2dp"
                android:text="description"
                android:textAppearance="?attr/textAppearanceBody2" />
        </LinearLayout>
    </com.google.android.material.card.MaterialCardView>
```

[`Anterior`](../Readme.md) | [`Siguiente`](../Reto-01)




</div>
