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

En el "Build Settings" de tu aplicación busca la propiedad **Enable Bitcode** y cámbialo a NO ya que ningúno de los frameworks soporta por el momento reconstruir el código Bitcode.

![Bitcode](https://github.com/jviloriam/DIGIPROAPI/blob/master/images/bitcode.png?raw=true)

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

### AppDelegate

Así es como debería de quedar tu AppDelegate con la configuración básica del SDK
```swift

import UIKit

// PODS
import Firebase
import GoogleMaps
import GooglePlaces

// DIGIPROSDK
import DIGIPROSDK

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {

    var window: UIWindow?


    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        // Override point for customization after application launch.
        
        // Initilization of DigiproSDK
        configureDigipro()
        ConfigurationManager.shared.uiapplication = application
        ConfigurationManager.shared.launchOptions = launchOptions
        configure4F()
        
        return true
    }

    func applicationWillResignActive(_ application: UIApplication) {
        // Sent when the application is about to move from active to inactive state. This can occur for certain types of temporary interruptions (such as an incoming phone call or SMS message) or when the user quits the application and it begins the transition to the background state.
        // Use this method to pause ongoing tasks, disable timers, and invalidate graphics rendering callbacks. Games should use this method to pause the game.
    }

    func applicationDidEnterBackground(_ application: UIApplication) {
        // Use this method to release shared resources, save user data, invalidate timers, and store enough application state information to restore your application to its current state in case it is terminated later.
        // If your application supports background execution, this method is called instead of applicationWillTerminate: when the user quits.
    }

    func applicationWillEnterForeground(_ application: UIApplication) {
        // Called as part of the transition from the background to the active state; here you can undo many of the changes made on entering the background.
    }

    func applicationDidBecomeActive(_ application: UIApplication) {
        // Restart any tasks that were paused (or not yet started) while the application was inactive. If the application was previously in the background, optionally refresh the user interface.
    }

    func applicationWillTerminate(_ application: UIApplication) {
        // Called when the application is about to terminate. Save data if appropriate. See also applicationDidEnterBackground:.
    }


}

extension AppDelegate{
    
    func configureDigipro(){
        // Google And Facebook Init
        
        #warning("Set Google API KEY for Google Maps nad Places.")
        // This confi
        GMSPlacesClient.provideAPIKey("")
        GMSServices.provideAPIKey("")
        
        #warning("Set Firebase configuration, you need \"GoogleService-Info.plist\" with your product bundle ID.")
        FirebaseApp.configure()
        
        _ = ConfigurationManager.shared
        _ = FormularioUtilities.shared
        ConfigurationManager.shared.configure()
        
        // Here you can launch any Splash Screen/Loading Screen/Login Screen
        // By default you can let Xcode laund the Storyboard
    }
    
    func configure4F(){
        // Here is the 4F Licence and Configuration, the code is provided only if the licence is provided.
    }
    
}
```

#### Inicio de la aplicación

Para poder empezar a usar el SDK y todos los componentes es necesario hacer dos tipos de login:
1: Logearse al código de empresa o código de aplicación.
2: Logearse a nivel usuario

Para poder logearse con un código empresarial es necesario utilizar el siguiente código, este código únicamente sirve como ejemplo de como realizar el login.

```swift

import UIKit

// DIGIPROSDK
import DIGIPROSDK

class ViewController: UIViewController, APIDelegate {
    func sendStatus(message: String, error: String, isLog: Bool, isNotification: Bool) {
        
    }
    
    func sendStatusCompletition(initial: Float, current: Float, final: Float) {
        
    }
    
    func sendStatusCodeMessage(message: String, error: String) {
        
    }
    
    func didSendError(message: String, error: String) {
        
    }
    
    func didSendResponse(message: String, error: String) {
        
    }
    
    func didSendResponseHUD(message: String, error: String, porcentage: Int) {
        
    }
    

    var sdkAPI : APIManager<ViewController>?
    
    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view.
        
        // Init SDK Protocol
        self.sdkAPI = APIManager<ViewController>()
        self.sdkAPI?.delegate = self
        
        // This is the user input code, you need to uppercased the input.
        ConfigurationManager.shared.codigoUIAppDelegate.Codigo = "abc".uppercased()
        
        // This is a usual or common Promise to get the answer for every action from the server.
        self.sdkAPI?.validCodeOnlinePromise(delegate: self)
            .then{ response in
                print(response)
                print("Código validado.")
                // Realizar acción al validar el código
            }
            .catch{ error in
                print(error)
                print("There was an error.")
            }
        
    }


}

```
