# SDK Formatos Electrónicos - Digipro

&copy;**DIGIPRO S.A de C.V. Todos los derechos reservados**

"Formatos Electrónicos" (FE conocido por sus siglas en español) es un KDS (Kit de Desarrollo de Software también conocido como SDK por sus siglas en inglés) desarrollado por &copy;**DIGIPRO S.A de C.V.** para la generación, edición, visualización y envío de formatos electrónicos. Y para su procesamiento de datos adecuado sin la necesidad de utilizar papel (paperless), solamente con el uso de un dispositivo móvil IOS (iPhone/iPad) podrá generar formularios electrónicos que se adecuen a las necesidades de su empresa.

## ¿Qué es un Formato Electrónico?

Para &copy;**DIGIPRO** un formato electrónico es un conjunto de datos que necesitan ser procesados y valorados para cumplir un objetivo o requisito necesario para que la empresa pueda completar una serie de procesos y cumplir con una finalidad.

El conjunto de datos pueden ser de los siguientes grupos:

* Tipo Lineales:
	* Texto
	* Fecha
	* Moneda
	* Número
	* Rango de Fecha
	* Area de Texto
	* Leyenda
	* Logo
	* Botón
	* Wizard
	* Lista
* Tipo Anexos:
	* Escaneo de Documentos
	* Toma de Fotografía
	* Toma de Video
	* Toma de Audio
	* Toma de Geolocalización
	* Reconocimiento de Texto
	* Firma Autografa Digital (FDA)
* Tipo Biométricos:
	* Escaneao de Huellas
	* Escaneo de Rostro y verificación de rostro en vivo (livenessface)
* Tipo Especiales:
	* Elementos contenedores y de tipo tabla

[TOC]

## SDK DIGIPRO

EL SDK es público y gratuito para su instalación y uso comercial, pero para poder usar el SDK adecuadamente es necesario tener una licencia y deberá de ponerse en [contacto](https://digipro.com.mx/contacto/) con uno de nuestros asesores de venta y ellos le proporcionarán la licencia y todo lo que debe de saber para la configuración de sus formatos electrónicos.
[DiGIPRO Sitio Oficial](https://digipro.com.mx/)

### Requerimientos

El SDK hace uso diferentes herramientas que facilitan la creación de los formatos electrónicos y la aplicación se desarrolló bajo los siguientes requerimientos mínimos:

- Swift 4.2
- IOS 11.0

### Previsualización

Aquí te damos una prueba muy significativa de como se visualiza un formato electrónico usando el SDK.

![alt text](https://github.com/jviloriam/DIGIPROAPI/blob/master/videos/intro.gif?raw=true)

Ahora, para hacer uso de cada uno de los componentes y funciones que tiene la aplicación deberá de instalarlo y hacer unas configuraciones básicas para que el SDK funcione adecuadamente.

### Instalación

El SDK está compuesto por 7 módulos que son los que abren las posibilidades de crear formatos electrónicos mucho más complejos, a continuación se dará una breve explicación de cada módulo.

Por el momento alguno de los frameworks no funcionan usando el simulador de Xcode y solamente funcionan usando un dispositivo IOS.

**Módulo - DIGIPROSDK:** *Este framework es el CORE del SDK, es necesario tener este instalado para poder iniciar la aplicación.*

**Módulo - DIGIPROSDKSO:** *Contiene los elementos básicos y lineales de formatos electrónicos.*

**Módulo - DIGIPROSDKSSO:** *Contiene los elementos de servicios y métodos de formatos electrónicos.*

**Módulo - DIGIPROSDKATO:** *Contiene los elementos de tipo anexos de formatos electrónicos.*

**Módulo - DIGIPROSDKVO:** *Contiene el elemento biométrico de escaneo de huella.*

**Módulo - DIGIPROSDKFO:** *Contiene el elemento biométrico de detección de rostro.*

**Módulo - DIGIPROSDKUI:** *Contiene las interfaces de toda la aplicación.*

### Configuración básica

Deberás de agregar los frameworks que necesitas a tu aplicación en la parte de "Embedded Binaries" en los ajustes de la aplicación. Justo como se muestra en la siguiente imagen. (Dependerá de cada framework de Digipro agregado el número de frameworks adicionales a usar).

![Frameworks](https://github.com/jviloriam/DIGIPROAPI/blob/master/images/frameworks.png?raw=true)

### Uso básico

Deberás de inicializar el API en tu "AppDelegate.swift" escribiendo el siguiente código:

```swift

import DIGIPROSDK

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        // Override point for customization after application launch.
        _ = ConfigurationManager.shared
        _ = FormularioUtilities.shared
        ConfigurationManager.shared.window = window
        ConfigurationManager.shared.appDelegate = self
        ConfigurationManager.shared.configure()
        return true
    }

func applicationDidBecomeActive(_ application: UIApplication) {
        // Restart any tasks that were paused (or not yet started) while the application was inactive. If the application was previously in the background, optionally refresh the user interface.
        ConfigurationManager.shared.utilities.checkPreferences()
    }
```

Este código lo que configura es toda la estructura de archivos, datos, funciones y utilidades que se van a hacer uso en la aplicación.

Y verifica si utiliza frameworks que ya utiliza el API y manda mensajes de advertencia para que el desarrollador pueda tomar una decisión de quitar o desinstalar el framework.

