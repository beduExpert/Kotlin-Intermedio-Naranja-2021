[`Kotlin Intermedio`](../../Readme.md) > [`Sesión 05`](../Readme.md) > `Reto 2`

## Reto 2: Agregando Items al RecyclerView

<div style="text-align: justify;">

### 1. Objetivos :dart:

- Que el programador aprenda a actualizar el RecyclerView cuando se le agregue un nuevo elemento

### 2. Requisitos :clipboard:

1. Android Studio Instalado en nuestra computadora.
2. Seguir la instrucción específica para esta sesión.

### 3. Desarrollo :computer:

Crea una biblioteca de vídeo juegos utilizando `RecyclerView`, cada juego debe de tener su imagen, el nombre, el género, una calificación en estrellas y su clasificación de edad.

Se recomienda la siguiente vista, pero pueden ponerse creativos.

<img src="result.png" width="45%">

En [esta carpeta](./resources) pueden encontrar los recursos que necesitan.

Se puede utilizar el siguiente layout para los items del `RecyclerView`. Que se ve como el de la imagen anterior.

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    tools:context=".GameAdapter"
    android:layout_width="match_parent"
    android:layout_height="match_parent">


    <androidx.constraintlayout.widget.Guideline
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/guideline"
        app:layout_constraintGuide_begin="44dp"
        android:orientation="horizontal" />

    <androidx.constraintlayout.widget.Guideline
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/guideline2"
        app:layout_constraintGuide_begin="84dp"
        android:orientation="horizontal" />

    <androidx.constraintlayout.widget.Guideline
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/guideline3"
        app:layout_constraintGuide_begin="118dp"
        android:orientation="horizontal" />

    <androidx.constraintlayout.widget.Guideline
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/guideline4"
        app:layout_constraintGuide_begin="172dp"
        android:orientation="horizontal" />

    <androidx.constraintlayout.widget.Guideline
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/guideline5"
        app:layout_constraintGuide_begin="193dp"
        android:orientation="horizontal" />

    <androidx.constraintlayout.widget.Guideline
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/guideline6"
        app:layout_constraintGuide_begin="16dp"
        android:orientation="horizontal" />

    <androidx.constraintlayout.widget.Guideline
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/guideline7"
        app:layout_constraintGuide_begin="122dp"
        android:orientation="vertical" />

    <TextView
        android:id="@+id/tvTitulo"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="8dp"
        android:layout_marginLeft="8dp"
        android:layout_marginTop="8dp"
        android:text="TextView"
        android:textSize="18sp"
        app:layout_constraintBottom_toTopOf="@+id/guideline2"
        app:layout_constraintLeft_toLeftOf="@+id/guideline7"
        app:layout_constraintTop_toTopOf="@+id/guideline" />

    <TextView
        android:id="@+id/tvCategoria"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="8dp"
        android:layout_marginLeft="8dp"
        android:layout_marginTop="8dp"
        android:text="TextView"
        android:textSize="16sp"
        app:layout_constraintBottom_toTopOf="@+id/guideline3"
        app:layout_constraintLeft_toLeftOf="@+id/guideline7"
        app:layout_constraintTop_toTopOf="@+id/guideline2" />

    <TextView
        android:id="@+id/tvClasificacion"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="8dp"
        android:layout_marginRight="8dp"
        android:text="TextView"
        app:layout_constraintBottom_toTopOf="@+id/guideline4"
        app:layout_constraintRight_toRightOf="parent" />

    <RatingBar
        android:id="@+id/rbCalificacion"
        style="@style/Widget.AppCompat.RatingBar.Indicator"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="8dp"
        android:layout_marginLeft="8dp"
        android:layout_marginTop="8dp"
        app:layout_constraintBottom_toTopOf="@+id/guideline4"
        app:layout_constraintLeft_toLeftOf="@+id/guideline7"
        app:layout_constraintTop_toTopOf="@+id/guideline3" />

    <ImageView
        android:id="@+id/imgPortada"
        android:layout_width="105dp"
        android:layout_height="138dp"
        android:layout_marginBottom="8dp"
        android:layout_marginLeft="8dp"
        android:layout_marginRight="8dp"
        android:layout_marginTop="8dp"
        app:layout_constraintBottom_toTopOf="@+id/guideline5"
        app:layout_constraintHorizontal_bias="1.0"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toLeftOf="@+id/guideline7"
        app:layout_constraintTop_toTopOf="@+id/guideline6"
        app:srcCompat="@drawable/smash" />


</androidx.constraintlayout.widget.ConstraintLayout>
```





[`Anterior`](../Ejemplo-03/Readme.md) | [`Siguiente`](../Proyecto/Readme.md)




</div>

