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


##### Login Código
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

##### Login User

Este es el código utilizado para poder logear al usuario

```swift

import UIKit

// DIGIPROSDK
import DIGIPROSDK
import DIGIPROSDKUI

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
    
    public func didSendResponseStatus(title: String, subtitle: String, porcentage: Float){
        // This is for get every single format status.
    }

    var sdkAPI : APIManager<ViewController>?
    var arrayPlantillaData = Array<(String, Array<FEPlantillaData>)>()
    
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
                // Futher code to login the user
                // You do not need to login the code and the user in the same view controller, that depends of your app flow or your needs.
                
                
                // User Login
                let lUser = "arturog"
                let lPassword = "tester"
                
                var password = Array(lPassword.utf8)
                password = password.sha512()
                let passwordString = password.toBase64()
                ConfigurationManager.shared.usuarioUIAppDelegate.Password = passwordString!
                
                let pass = Array(lPassword.utf8)
                let passwordBase = pass.toBase64()
                ConfigurationManager.shared.usuarioUIAppDelegate.PasswordEncoded = passwordBase!
                ConfigurationManager.shared.usuarioUIAppDelegate.User = lUser
                ConfigurationManager.shared.usuarioUIAppDelegate.IP = ConfigurationManager.shared.utilities.getIPAddress()
                ConfigurationManager.shared.usuarioUIAppDelegate.AplicacionID = ConfigurationManager.shared.codigoUIAppDelegate.AplicacionID
                ConfigurationManager.shared.usuarioUIAppDelegate.ProyectoID = ConfigurationManager.shared.codigoUIAppDelegate.ProyectoID
                
                
                self.sdkAPI?.validUserOnlinePromise(delegate: self)
                    .then{ response in
                        print(response)
                        print("User logged")
                        
                    }
                    .catch{ error in
                        print(error)
                        print("There was an error.")
                    }
            }
            .catch{ error in
                print(error)
                print("There was an error.")
            }
        
    }


}

```

Ya que se obtienen los accesos a cada uno de los login, ahora procederemos a descargar los datos adicionales para la aplicación y mandar a visualizar nuestra primera plantilla o formato vacio.

Este es el código final para poder obtener la primera plantilla encontrada y visualizarla.

```swift

import UIKit

// DIGIPROSDK
import DIGIPROSDK
import DIGIPROSDKUI

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
    
    public func didSendResponseStatus(title: String, subtitle: String, porcentage: Float){
        // This is for get every single format status.
    }

    var sdkAPI : APIManager<ViewController>?
    var arrayPlantillaData = Array<(String, Array<FEPlantillaData>)>()
    
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
                // Futher code to login the user
                // You do not need to login the code and the user in the same view controller, that depends of your app flow or your needs.
                
                
                // User Login
                let lUser = "arturog"
                let lPassword = "tester"
                
                var password = Array(lPassword.utf8)
                password = password.sha512()
                let passwordString = password.toBase64()
                ConfigurationManager.shared.usuarioUIAppDelegate.Password = passwordString!
                
                let pass = Array(lPassword.utf8)
                let passwordBase = pass.toBase64()
                ConfigurationManager.shared.usuarioUIAppDelegate.PasswordEncoded = passwordBase!
                ConfigurationManager.shared.usuarioUIAppDelegate.User = lUser
                ConfigurationManager.shared.usuarioUIAppDelegate.IP = ConfigurationManager.shared.utilities.getIPAddress()
                ConfigurationManager.shared.usuarioUIAppDelegate.AplicacionID = ConfigurationManager.shared.codigoUIAppDelegate.AplicacionID
                ConfigurationManager.shared.usuarioUIAppDelegate.ProyectoID = ConfigurationManager.shared.codigoUIAppDelegate.ProyectoID
                
                
                self.sdkAPI?.validUserOnlinePromise(delegate: self)
                    .then{ response in
                        print(response)
                        print("User logged")
                        
                        // Now we need to download all data reated to the user (formats, template and data related)
                        ConfigurationManager.shared.isInitiated = true
                        // Step 1 Check "PLANTILLAS"
                        self.sdkAPI?.validaPlantillasOnlinePromise(delegate: self)
                            .then{ response in
                                print(response)
                                print("Plantillas validadas")
                                
                                self.sdkAPI?.validaVariablesOnlinePromise(delegate: self)
                                    .then { response in
                                        
                                        print(response)
                                        print("Variables validadas")
                                        
                                         self.sdkAPI?.validFormatosOnlinePromise(delegate: self)
                                            .then { response in

                                                print(response)
                                                print("Formatos validados")
                                                
                                                // Now you can load a single template, if you know the data.
                                                // If not you can load or call different functions to get every data storaged on the device.
                                                self.popNewForm()
                                                
                                            }
                                            .catch { error in
                                                print(error)
                                                print("There was an error.")
                                            }
                                    }
                                    .catch { error in
                                        print(error)
                                        print("There was an error.")
                                    }
                            }
                            .catch{ error in
                                print(error)
                                print("There was an error.")
                            }
                    }
                    .catch{ error in
                        print(error)
                        print("There was an error.")
                    }
            }
            .catch{ error in
                print(error)
                print("There was an error.")
            }
        
    }


}


extension ViewController{
    
    func popNewForm(){
        
        
        self.sdkAPI?.validFlujosAndProcesosPromise(delegate: self)
            .then { response in
                print(response)
                print("Templates obtenidos")
                FormularioUtilities.shared.globalFlujo = ConfigurationManager.shared.flujosOrdered[0].FlujoID
                // Get all Template in Array
                self.arrayPlantillaData = (self.sdkAPI?.getPlantillasBySections(String(FormularioUtilities.shared.globalFlujo)))!
                
                let destination = NuevaPlantillaViewController.init(nibName: "NuevaPlantillaViewController", bundle: Cnstnt.Path.ui)
                destination.modalTransitionStyle = .coverVertical
                destination.modalPresentationStyle = .overFullScreen
                let navigation = UINavigationController(rootViewController: destination)
                FormularioUtilities.shared.currentFormato = FEFormatoData()
                FormularioUtilities.shared.currentFormato.FlujoID = self.arrayPlantillaData[0].1[0].FlujoID
                FormularioUtilities.shared.currentFormato.TipoDocID = self.arrayPlantillaData[0].1[0].TipoDocID
                FormularioUtilities.shared.currentFormato.ExpID = self.arrayPlantillaData[0].1[0].ExpID
                destination.index = 0
                destination.flujo = self.arrayPlantillaData[0].1[0].FlujoID
                destination.proceso = 0
                destination.navigation = navigation
                destination.arrayPlantillaData = self.arrayPlantillaData[0].1[0]
                
                self.present(navigation, animated: true, completion: nil)
            }
            .catch { error in
                print(error)
                print("There was an error.")
            }
        
        
    }
    
}

```

### DEMO

Si tienes problemas con el código puedes descargar el proyecto "Demo" para que puedas ver el funcionamiento sin necesidad de copiar y pegar. Solamente deberás de ir a la carpeta de "demo" y descargar el proyecto.

# Flujo Login Genérico SDK - Digipro

##### Implementación del flujo en nuestra aplicación.

###### Primera vista a configurar para el flujo genérico.

El primer paso es importar a nuestro proyecto las siguientes librerias:
``` swift
import DIGIPROSDK
import DIGIPROSDKUI
```

Una vez importadas las librerias en el viewController a utilizar, escribimos el siguiente código para dar inicio a nuestra aplicación:


``` swift
import UIKit
import DIGIPROSDK
import DIGIPROSDKUI

class SplashSDKViewController: UIViewController {
    
    //Variables de controlador
    var sdkAPI : APIManager<SplashSDKViewController>?
    var splashView: SplashSDK?

    override func viewDidLoad() {
        super.viewDidLoad()
        self.navigationController?.isNavigationBarHidden = true
        //se inicializan variables con el protocolo generico del framework en nuestro viewController
        self.splashView?.sdkAPI.delegate = self.sdkAPI?.delegate
        self.sdkAPI = APIManager<SplashSDKViewController>()
        self.sdkAPI?.delegate = self

        // Do any additional setup after loading the view.
    }
```

###### En esta parte de nuestro controlador, en el viewDidAppear inicializamos el view genérico desde el SDK, configuramos la vista y lo agregamos a la vista padre de nuestro controlador
_
``` swift
    
    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(true)
        
        self.splashView = SplashSDK(frame: self.view.bounds)
        self.splashView!.center.x = view.center.x
        self.splashView!.center.y = view.center.y
        self.splashView?.centerXAnchor.constraint(equalTo: self.view.centerXAnchor)
        self.splashView?.centerYAnchor.constraint(equalTo: self.view.centerYAnchor)
        self.splashView!.sdkAPI.delegate = self.sdkAPI?.delegate!
        view.addSubview(self.splashView!)
        
    }
    
    //removemos la vista de nuestro controlador para que no consuma memoria.
    override func viewWillDisappear(_ animated: Bool) {
        super.viewWillDisappear(true)
        self.splashView?.removeFromSuperview()
    }

}
```
###### Se hace un extension en nuestra clase al delegado APIDelegate, el cual nos pedira que agreguemos los metodos para obtener las respuestas de los servicios
_

``` swift
extension SplashSDKViewController: APIDelegate{
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
    
    ///// En este metodo es donde recibimos la respuesta del servicio y hacemos la navegación al siguiente controlador
    
    func responseSplash(message: String) {
        self.navigationController?.pushViewController(CodeNewLoginViewController(), animated: true)
    }
    
}

```

###### Segunda vista a configurar para el flujo genérico.
_

``` swift
import UIKit
import DIGIPROSDK
import DIGIPROSDKUI

class CodeNewLoginViewController: UIViewController {
    
    var sdkAPI : APIManager<CodeNewLoginViewController>?
    var codeView: CodeView?


    override func viewDidLoad() {
        super.viewDidLoad()
        self.navigationController?.isNavigationBarHidden = false
        self.navigationItem.hidesBackButton = true
        self.navigationController?.navigationBar.topItem?.title = "Proveedor"
        self.codeView?.sdkAPI.delegate = self.sdkAPI?.delegate
        self.sdkAPI = APIManager<CodeNewLoginViewController>()
        self.sdkAPI?.delegate = self
        
    }
```
_
```swift
    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(true)
        
        
        self.codeView = CodeView(frame: self.view.bounds)
        self.codeView!.center.x = view.center.x
        self.codeView!.center.y = view.center.y
        self.codeView?.centerXAnchor.constraint(equalTo: view.centerXAnchor)
        self.codeView?.centerYAnchor.constraint(equalTo: view.centerYAnchor)
        self.codeView!.sdkAPI.delegate = self.sdkAPI?.delegate!
        view.addSubview(self.codeView!)
    }
    
    //removemos la vista de nuestro controlador para que no consuma memoria.
    override func viewWillDisappear(_ animated: Bool) {
        super.viewWillDisappear(true)
        self.codeView?.removeFromSuperview()
    }

```
###### Se hace un extension en nuestra clase al delegado APIDelegate, el cual nos pedira que agreguemos los metodos para obtener las respuestas de los servicios
_
```swift

extension CodeNewLoginViewController: APIDelegate{
    func sendStatus(message: String, error: String, isLog: Bool, isNotification: Bool) {
    }
    
    func sendStatusCompletition(initial: Float, current: Float, final: Float) {
    }
    
    func didSendError(message: String, error: String) {
    }
    
    func didSendResponse(message: String, error: String) {
    }
    
    func didSendResponseHUD(message: String, error: String, porcentage: Int) {
    }
  ```
   En este metodo es donde recibimos la respuesta del servicio y manejamos la respuesta si fue erronea o satisfactoria, para las acciones a realizar.
  _
```swift
    func sendStatusCodeMessage(message: String, error: String) {
        print("Message: \(message)\n Error: \(error)")
        if message.isEmpty{
            print("Error: \(error)")
        }else{
            self.navigationController?.pushViewController(UserNewLoginViewController(), animated: true)
        }
    }
}

```

###### Tercera y última vista a configurar para el flujo genérico.
_

```swift
import UIKit
import DIGIPROSDK
import DIGIPROSDKUI

class UserNewLoginViewController: UIViewController {
    
    //Variables de controlador
    var sdkAPI : APIManager<UserNewLoginViewController>?
    var loginView: LoginView?

    override func viewDidLoad() {
        super.viewDidLoad()
        //se inicializan variables con el protocolo generico del framework en nuestro
        self.loginView?.sdkAPI.delegate = self.sdkAPI?.delegate
        self.sdkAPI = APIManager<UserNewLoginViewController>()
        self.sdkAPI?.delegate = self
    }
    
    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(true)
        
        self.loginView = LoginView(frame: self.view.bounds)
        self.loginView!.center.x = view.center.x
        self.loginView!.center.y = view.center.y
        let downloadImage = UIImage(named: "logo-digipro") ?? UIImage()
        self.loginView!.set(image: downloadImage)
        self.loginView!.set(title: "¡Bienvenido!\n\nPor favor escriba su usuario y contraseña para ingresar")
        self.loginView?.sdkAPI.delegate = self.sdkAPI?.delegate!
        view.addSubview(loginView!)
        
        
    }

}
```

###### Se hace un extension en nuestra clase al delegado APIDelegate, el cual nos pedira que agreguemos los metodos para obtener las respuestas de los servicios
_
```swift
extension UserNewLoginViewController: APIDelegate{
    func sendStatus(message: String, error: String, isLog: Bool, isNotification: Bool) {
        
    }
    
    func sendStatusCompletition(initial: Float, current: Float, final: Float) {
        
    }
    
    func didSendError(message: String, error: String) {
        
    }
    
    func didSendResponse(message: String, error: String) {
        
    }
    
    func didSendResponseHUD(message: String, error: String, porcentage: Int) {
        
    }
  
```
   En este metodo es donde recibimos la respuesta del servicio y manejamos la respuesta si fue erronea o satisfactoria, para las acciones a realizar.
  _
```swift
    
    func sendStatusCodeMessage(message: String, error: String) {
        print("Message: \(message)\n Error: \(error)")
        guard let navController = self.parent else {
            return
        }
        AlertNewViewController.show(in: navController, title: "Bienvenido", subtitle: "Acceso Correcto", completion: nil)
    }
    
    
}
```

