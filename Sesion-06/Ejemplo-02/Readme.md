[`Kotlin Intermedio`](../../Readme.md) > [`Sesión 06`](../Readme.md) > `Ejemplo 2`

## Ejemplo 2: Appbar y Navigation Drawer

<div style="text-align: justify;">

### 1. Objetivos :dart:

- Implementar Appbar y NavigationDrawer_ de Material Design en nuestra interfaz.

### 2. Requisitos :clipboard:

1. Android Studio Instalado en nuestra computadora.
2. Seguir la instrucción específica para esta sesión.

### 3. Desarrollo :computer:

Implementaremos ahora dos `componets` importantes para material design: Appbar y Navigation Drawer.

* En [Este enlace](https://material.io/components/app-bars-top) podemos leer acerca de las App bars.
* En [Este enlace](https://material.io/components/navigation-drawer) podemos leer acerca de las Navigation Drawers.

Sigue los pasos para lograr los objetivos:
	
#### App bar

1. Abre __Android Studio__ y crea un nuevo proyecto con Activity Vacía (Empty Activity).

2. Copiaremos todos los recursos que se encuentran en [Esta carpeta](AppBarAndNavigationDrawer/app/src/main/res/drawable) y las pegamos en nuestro directorio ___drawable___, para utilizarlos posteriormente.

3. En **values/colors.xml** agregamos los siguientes colores:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="purple_200">#FFBB86FC</color>
    <color name="purple_500">#FF6200EE</color>
    <color name="purple_700">#FF3700B3</color>
    <color name="teal_200">#FF03DAC5</color>
    <color name="teal_700">#FF018786</color>
    <color name="black">#FF000000</color>
    <color name="white">#FFFFFFFF</color>
    <color name="colorPrimary">#6200EE</color>
    <color name="colorPrimaryDark">#3700B3</color>
    <color name="colorAccent">#03DAC5</color>
    <color name="textColorPrimary">#FFFFFF</color>
    <color name="toolbarIconColor">@color/textColorPrimary</color>
    <color name="productGridBackgroundColor">#FFFBFA</color>
</resources>
```

EN **values/strings.xml** declaramos las siguietes cadenas

```xml
<resources>
    <string name="app_name">App Bar</string>
    <string name="delete">Eliminar</string>
    <string name="share">Compartir</string>
    <string name="open_drawer">Abrir</string>
    <string name="close_drawer">Cerrar</string>
    <string name="delete_element">Deleting element</string>
    <string name="sharing_element">Sharing element</string>
    <string name="user">Usuario</string>
    <string name="email">Correo electrónico</string>
    <string name="drawer.home">Home</string>
    <string name="drawer.account">Cuenta</string>
    <string name="drawer.payments">Pago</string>
    <string name="drawer.settings">Configuración</string>
    <string name="drawer.extra">Adicional</string>
    <string name="drawer.about">Acerca de</string>
    <string name="drawer.privacy">Privacidad</string>
</resources>
```

y en **values/themes** declaramos los siguientes estilos

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">
    <item
        android:id="@+id/delete"
        android:icon="@drawable/delete"
        android:title="@string/delete"
        app:showAsAction="always" />
    <item
        android:id="@+id/share"
        android:icon="@drawable/share"
        android:title="@string/share"
        app:showAsAction="always" />
</menu>
```

Por último cambiaremos la fuente de los estilos en el **AndroidManifest** en la etiqueta de `aplication` cambiaremos el valor del atributo `android:theme`.

```xml
android:theme="@style/AppTheme">
```


4. Ahora insertaremos nuestro AppBar en nuestro _main_activity.xml_. Para esto, utilizaremos un `AppBarLayout` que en realidad es un `LinearLayout` que implementa varios conceptos del [App Bar de Material design](https://material.io/components/app-bars-top). Dentro de esta, contenemos nuestro `widget Toolbar`, que es realmente la barra superior. el `flag navigationIcon` es el elemento gráfico al lado izquierdo, y en este caso pondremos el ícono de menú hamburguesa.

```xml
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".MainActivity">

        <com.google.android.material.appbar.AppBarLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content">

            <androidx.appcompat.widget.Toolbar
                app:navigationIcon="@drawable/menu"
                android:id="@+id/app_bar"
                style="@style/Widget.Toolbar"
                android:layout_width="match_parent"
                android:layout_height="?attr/actionBarSize"
                app:title="@string/app_name" />
        </com.google.android.material.appbar.AppBarLayout>
    </LinearLayout>
```

5. Para agregar opciones a nuestra `AppBar`, creamos un directorio _menú_.

<img src="images/1.png" width="35%">

dentro de este, creamos _toolbar_menu.xml_ y agregamos los `items` que compondrán a nuestro menú:

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">
    <item
        android:id="@+id/delete"
        android:icon="@drawable/delete"
        android:title="@string/delete"
        app:showAsAction="always" />
    <item
        android:id="@+id/share"
        android:icon="@drawable/share"
        android:title="@string/share"
        app:showAsAction="always" />
</menu>
```


6. Asignamos nuestro `Toolbar` como `ActionBar`. Esto lo hacemos en el `onCreate` de nuestra `MainActivity`.

```kotlin
        val appBar = findViewById<Toolbar>(R.id.app_bar)
        this.setSupportActionBar(appBar)
```

Y asociamos nuestra `AppBar` al menú que creamos con anterioridad:

```kotlin
    override fun onCreateOptionsMenu(menu: Menu?): Boolean {
        menuInflater.inflate(R.menu.toolbar_menu, menu)
        return super.onCreateOptionsMenu(menu)
    }
```

#### Navigation drawer

8. Comenzaremos por crear el menú que irá dentro del layout, creando el archivo  ___drawer_menu.xml___ dentro del directorio _menu_. Este archivo será el layout de nuestro menu, en donde definiremos todos los views que lo conforman.

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <group>
        <item
            android:id="@+id/nav_home"
            android:icon="@drawable/home"
            android:title="@string/drawer.home" />
    </group>

    <item android:title="Cuenta">

        <menu>

            <group android:checkableBehavior="single">

                <item
                    android:id="@+id/nav_payment"
                    android:icon="@drawable/payment"
                    android:title="@string/drawer.payments" />

                <item
                    android:id="@+id/nav_settings"
                    android:icon="@drawable/settings"
                    android:title="@string/drawer.settings" />
            </group>
        </menu>
    </item>

    <item android:title="@string/drawer.extra">
        <menu>
            <item
                android:id="@+id/nav_about"
                android:icon="@drawable/info"
                android:title="@string/drawer.about" />

            <item
                android:id="@+id/nav_privacy"
                android:icon="@drawable/privacy"
                android:title="@string/drawer.privacy" />
        </menu>
    </item>
</menu>
```

8. Ahora, crearemos el `layout` ___drawer_header.xml___ del _header_ de nuestro Drawer.

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:paddingStart="24dp"
    android:paddingTop="48dp"
    android:layout_width="match_parent"
    android:layout_height="wrap_content">
    <ImageView
        android:layout_width="72dp"
        android:layout_height="72dp"
        android:src="@drawable/default_user" />

    <TextView
        android:layout_marginTop="8dp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/user"
        android:textSize="24sp" />

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/email"
        android:textSize="14sp" />
</LinearLayout>
```

10. Nuestro _activity_main.xml_ será modificado de tal forma que el `LinearLayout` quede envuelto por nuestra clase `DrawerLayout`

```xml
<androidx.drawerlayout.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/drawer_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    tools:openDrawer="start"
    android:fitsSystemWindows="true">
	...
</androidx.drawerlayout.widget.DrawerLayout>
```

Sin embargo, es necesario implementar el menú de Navegación y el header, por lo que agregaremos la clase `NavigationView` al final del interior de nuestro `DrawerLayout`.

```xml
  <com.google.android.material.navigation.NavigationView
        app:headerLayout="@layout/drawer_header"
        android:id="@+id/nav_view"
        android:layout_gravity="start"
        android:layout_height="match_parent"
        android:layout_width="wrap_content"
        app:menu="@menu/drawer_menu" />
```
<details>
<summary>El código final de _main_activity.xml_ se puede consultar aquí</summary>

```xml
<?xml version="1.0" encoding="utf-8"?>

<androidx.drawerlayout.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/drawer_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    tools:openDrawer="start"
    android:fitsSystemWindows="true">

    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".MainActivity">

        <com.google.android.material.appbar.AppBarLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content">

            <androidx.appcompat.widget.Toolbar
                app:navigationIcon="@drawable/menu"
                android:id="@+id/app_bar"
                style="@style/Widget.Toolbar"
                android:layout_width="match_parent"
                android:layout_height="?attr/actionBarSize"
                app:title="@string/app_name" />
        </com.google.android.material.appbar.AppBarLayout>
    </LinearLayout>

    <com.google.android.material.navigation.NavigationView
        app:headerLayout="@layout/drawer_header"
        android:id="@+id/nav_view"
        android:layout_gravity="start"
        android:layout_height="match_parent"
        android:layout_width="wrap_content"
        app:menu="@menu/drawer_menu" />
</androidx.drawerlayout.widget.DrawerLayout>
```
</details>

11. Ahora es necesario relacionar nuestro `AppBar` con el `NavigationDrawer`, por lo que definiremos un método para hacer la configuración necesaria:

```kotlin
    
    private fun setupDrawer(toolbar: Toolbar){
        val drawerLayout = findViewById<DrawerLayout>(R.id.drawer_layout)
        val drawerToggle = ActionBarDrawerToggle(this,drawerLayout,toolbar,R.string.open_drawer,R.string.close_drawer)
    }
```

esta función se llama en el método `onCreate`:

```kotlin
setupDrawer(appBar)
```

Corremos nuestra app y finalmente, abriremos nuestro _Drawer_ al hacer click sobre el menú hamburguesa (o hacer slide a la derecha en el borde izquierdo).

<img src="images/4.png" width="35%">


[`Anterior`](../Reto-01/Readme.md) | [`Siguiente`](../Ejemplo-03/Readme.md)




</div>
