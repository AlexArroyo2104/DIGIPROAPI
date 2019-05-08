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

### Instalación

Arrastrar el archivo "DGFmwrk.framework" a tu proyecto en Xcode, depués dirígete a la parte de Targets en tu proyecto y agrega en el apartado de "Embedded Binaries" y "Linked Frameworks and Libraries" el framework que acabas de arrastrar a tu proyecto. Deberás de usar el icono de + para agregar el framework a cada uno de los apartados, justo como se muestra en la siguiente imagen.

![alt text](https://github.com/jviloriam/DIGIPROAPI/blob/master/videos/intro.gif?raw=true)

Ahora podrá hacer uso de cada uno de los componentes y funciones que tiene la aplicación pero antes de poderlo usar deberá de hacer unas configuraciones previas para que el API funcione adecuadamente.

### Configuración básica

#### Settings

Crear un nuevo archivo de "Settings.bundle" para la aplicación, si su aplicación ya contiene un "Settings.bundle" deberá de agregar los nuevos parámetros, estos parámetros los encontrará en el archivo ubicado en "adicionales/settings/Root.plist" o puede copiarlo desde el siguiente código:

### Uso básico

Deberás de inicializar el API en tu "AppDelegate.swift" escribiendo el siguiente código:

```swift
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

