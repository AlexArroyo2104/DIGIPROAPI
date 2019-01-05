# Api formatos electrónicos

"Formatos electrónicos" es un API (Application programming interface) desarrollada por DIgipro - The digital evolution company para la generación, edición, visualización y envío de todo tipo de formatos (documentos de tipo formulario) para el procesamiento de datos adecuado sin la necesidad de utilizar papel (paperless), solamente con el uso de un dispositivo móvil IOS (iPhone / iPad) podrá generar formularios que se adecuen a las necesidades de su empresa.

[TOC]

## API DGFmwrk

El API es público y gratuito para su uso comercial, pero para poder usar el API es necesario tener una licencia. Deberá de ponerse en contacto con uno de nuestros asesores de venta y ellos le proporcionarán la licencia y todo lo que debe de saber para la configuración de sus formatos electrónicos.

### Requerimientos

El API "DGFmwrk.framework" hace uso diferentes herramientas y utilizades que facilitan la creación de los formatos electrónicos y por ende se necesita que se desarrolle la aplicaci´n bajo los requerimientos mínimos:

- Swift 4.2
- IOS 11.0
- Un bundle id registrado para hacer uso de los módulos especializados

### Instalación

Arrastrar el archivo "DGFmwrk.framework" a tu proyecto en Xcode, depués dirígete a la parte de Targets en tu proyecto y agrega en el apartado de "Embedded Binaries" y "Linked Frameworks and Libraries" el framework que acabas de arrastrar a tu proyecto. Deberás de usar el icono de + para agregar el framework a cada uno de los apartados, justo como se muestra en la siguiente imagen.

![alt text](https://github.com/jviloriam/DIGIPROAPI/blob/master/images/embedded-binaries.digipro.png?raw=true)

Ahora podrá hacer uso de cada uno de los componentes y funciones que tiene la aplicación pero antes de poderlo usar deberá de hacer unas configuraciones previas para que el API funcione adecuadamente.

### Configuración básica

#### Settings

Crear un nuevo archivo de "Settings.bundle" para la aplicación, si su aplicación ya contiene un "Settings.bundle" deberá de agregar los nuevos parámetros, estos parámetros los encontrará en el archivo ubicado en "adicionales/settings/Root.plist" o puede copiarlo desde el siguiente código:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>StringsTable</key>
	<string>Root</string>
	<key>PreferenceSpecifiers</key>
	<array>
		<dict>
			<key>Type</key>
			<string>PSGroupSpecifier</string>
			<key>Title</key>
			<string>Version App</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTitleValueSpecifier</string>
			<key>Title</key>
			<string>Versión</string>
			<key>Key</key>
			<string>version_preference</string>
			<key>DefaultValue</key>
			<string>1.0</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTitleValueSpecifier</string>
			<key>Title</key>
			<string>Paquete</string>
			<key>Key</key>
			<string>bundle_preference</string>
			<key>DefaultValue</key>
			<string>2</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSGroupSpecifier</string>
			<key>Title</key>
			<string>Data</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTitleValueSpecifier</string>
			<key>Title</key>
			<string>Datos almacenados</string>
			<key>Key</key>
			<string>data_preference</string>
			<key>DefaultValue</key>
			<string>0.0 MB</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSToggleSwitchSpecifier</string>
			<key>Title</key>
			<string>Borrar datos almacenados</string>
			<key>Key</key>
			<string>delete_data_preference</string>
			<key>DefaultValue</key>
			<false/>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSGroupSpecifier</string>
			<key>Title</key>
			<string>Anexos</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTitleValueSpecifier</string>
			<key>Title</key>
			<string>Imágenes guardadas</string>
			<key>Key</key>
			<string>img_saved</string>
			<key>DefaultValue</key>
			<string>0</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTitleValueSpecifier</string>
			<key>Title</key>
			<string>Huellas digitales guardadas</string>
			<key>Key</key>
			<string>huellas_saved</string>
			<key>DefaultValue</key>
			<string>0</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTitleValueSpecifier</string>
			<key>Title</key>
			<string>Firmas guardadas</string>
			<key>Key</key>
			<string>firm_saved</string>
			<key>DefaultValue</key>
			<string>0</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTitleValueSpecifier</string>
			<key>Title</key>
			<string>Videos guardados</string>
			<key>Key</key>
			<string>video_saved</string>
			<key>DefaultValue</key>
			<string>0</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTitleValueSpecifier</string>
			<key>Title</key>
			<string>Audios guardados</string>
			<key>Key</key>
			<string>audio_saved</string>
			<key>DefaultValue</key>
			<string>0</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTitleValueSpecifier</string>
			<key>Title</key>
			<string>Mapas guardados</string>
			<key>Key</key>
			<string>map_saved</string>
			<key>DefaultValue</key>
			<string>0</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTitleValueSpecifier</string>
			<key>Title</key>
			<string>Rostros guardados</string>
			<key>Key</key>
			<string>face_saved</string>
			<key>DefaultValue</key>
			<string>0</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSGroupSpecifier</string>
			<key>Title</key>
			<string>Acceso</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTitleValueSpecifier</string>
			<key>Title</key>
			<string>Código de empresa</string>
			<key>Key</key>
			<string>codigo_preference</string>
			<key>DefaultValue</key>
			<string>codigo</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTitleValueSpecifier</string>
			<key>Title</key>
			<string>Usuario</string>
			<key>Key</key>
			<string>usuario_preference</string>
			<key>DefaultValue</key>
			<string>Nombre de usuario</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSGroupSpecifier</string>
			<key>Title</key>
			<string>Proceso de Validación</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTitleValueSpecifier</string>
			<key>Title</key>
			<string>Nombre</string>
			<key>Key</key>
			<string>nombre_validacion</string>
			<key>DefaultValue</key>
			<string></string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTitleValueSpecifier</string>
			<key>Title</key>
			<string>Apellido Paterno</string>
			<key>Key</key>
			<string>apellido_paterno_validacion</string>
			<key>DefaultValue</key>
			<string></string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTitleValueSpecifier</string>
			<key>Title</key>
			<string>Apellido Materno</string>
			<key>Key</key>
			<string>apellido_materno_validacion</string>
			<key>DefaultValue</key>
			<string></string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTitleValueSpecifier</string>
			<key>Title</key>
			<string>Correo electrónico</string>
			<key>Key</key>
			<string>correo_electronico_validacion</string>
			<key>DefaultValue</key>
			<string></string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTitleValueSpecifier</string>
			<key>Title</key>
			<string>Teléfono celular</string>
			<key>Key</key>
			<string>telefono_celular_validacion</string>
			<key>DefaultValue</key>
			<string></string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTitleValueSpecifier</string>
			<key>Title</key>
			<string>Estado de cuenta</string>
			<key>Key</key>
			<string>estado_validacion</string>
			<key>DefaultValue</key>
			<string>Por Validar</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSGroupSpecifier</string>
			<key>Title</key>
			<string>Adicionales</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSToggleSwitchSpecifier</string>
			<key>Title</key>
			<string>Tutorial (Ayuda)</string>
			<key>Key</key>
			<string>data_tutorial</string>
			<key>DefaultValue</key>
			<true/>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSToggleSwitchSpecifier</string>
			<key>Title</key>
			<string>Autenticación TouchID</string>
			<key>Key</key>
			<string>touchid_auth</string>
			<key>DefaultValue</key>
			<false/>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTitleValueSpecifier</string>
			<key>Title</key>
			<string>Logs almacenados</string>
			<key>Key</key>
			<string>data_log</string>
			<key>DefaultValue</key>
			<string>0.0 MB</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSGroupSpecifier</string>
			<key>Title</key>
			<string>Modo desarrollador</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTextFieldSpecifier</string>
			<key>Title</key>
			<string>Serial</string>
			<key>Key</key>
			<string>serial_developer</string>
			<key>DefaultValue</key>
			<string>Vacio</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSGroupSpecifier</string>
			<key>Title</key>
			<string>Licencia</string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTextFieldSpecifier</string>
			<key>Title</key>
			<string>Licencia código</string>
			<key>Key</key>
			<string>licence_code</string>
			<key>DefaultValue</key>
			<string></string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSTextFieldSpecifier</string>
			<key>Title</key>
			<string>Licencia usuario</string>
			<key>Key</key>
			<string>licence_user</string>
			<key>DefaultValue</key>
			<string></string>
		</dict>
		<dict>
			<key>Type</key>
			<string>PSMultiValueSpecifier</string>
			<key>Title</key>
			<string>Modalidad</string>
			<key>Key</key>
			<string>mode_app</string>
			<key>DefaultValue</key>
			<string>Normal</string>
			<key>Titles</key>
			<array>
				<string>Normal</string>
				<string>Kiosco</string>
				<string>SDK</string>
				<string>Licencia</string>
			</array>
			<key>Values</key>
			<array>
				<string>Normal</string>
				<string>Kiosco</string>
				<string>SDK</string>
				<string>Licencia</string>
			</array>
		</dict>
	</array>
</dict>
</plist>
```

#### Google y Firebase

Deberás de agregar un nuevo archivo llamado "GoogleService-Info.plist" este archivo es el que configura a Firebase y Google Maps, es de vital importancia que esté configurado y presente este archivo ya que es uno de los componentes principales en el API.

Deberás de hacer uso de nuestra configuración para Google, esta configuración la encontrarás en el archivo ubicado en "adicionales/settings/GoogleService-Info.plist" o puede copiarlo desde el siguiente código:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>AD_UNIT_ID_FOR_BANNER_TEST</key>
	<string>ca-app-pub-3940256099942544/2934735716</string>
	<key>AD_UNIT_ID_FOR_INTERSTITIAL_TEST</key>
	<string>ca-app-pub-3940256099942544/4411468910</string>
	<key>CLIENT_ID</key>
	<string></string>
	<key>REVERSED_CLIENT_ID</key>
	<string></string>
	<key>API_KEY</key>
	<string></string>
	<key>GCM_SENDER_ID</key>
	<string>539654860154</string>
	<key>PLIST_VERSION</key>
	<string>1</string>
	<key>BUNDLE_ID</key>
	<string></string>
	<key>PROJECT_ID</key>
	<string>digipro-fct-elect</string>
	<key>STORAGE_BUCKET</key>
	<string>digipro-fct-elect.appspot.com</string>
	<key>IS_ADS_ENABLED</key>
	<true/>
	<key>IS_ANALYTICS_ENABLED</key>
	<false/>
	<key>IS_APPINVITE_ENABLED</key>
	<false/>
	<key>IS_GCM_ENABLED</key>
	<true/>
	<key>IS_SIGNIN_ENABLED</key>
	<true/>
	<key>GOOGLE_APP_ID</key>
	<string></string>
	<key>DATABASE_URL</key>
	<string></string>
	<key>FIRAnalyticsDebugEnabled</key>
	<true/>
</dict>
</plist>

```

Por motivos de seguridad los datos relacionados al API_KEY de Google fueron borrados, puedes usar tus datos o pedirlos a tu asesor de ventas.

Si usa tus propias llaves para Google deberás de usar el siguiente código:

```swift
ConfigurationManager.shared.configure(googlePlacesKey: "AIzaSyCCyxWE5JZcZKkmEYX7ejSVmivsH4OoQ94", googleServicesKey: "AIzaSyCCyxWE5JZcZKkmEYX7ejSVmivsH4OoQ94")
```

Si no es tu caso deberás de usar la configuración normal o básica como en el siguiente ejemplo:

```swift
ConfigurationManager.shared.configure()
```

#### Info.plist

Para el correcto funcionamiento del API y todas sus funcionalidades es necesario tomar en cuenta algunas configuraciones extra que deben de ir en el archivo "Info.plist" y son las siguientes:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>LSApplicationQueriesSchemes</key>
	<array>
		<string>googlechromes</string>
		<string>comgooglemaps</string>
	</array>
	<key>LSRequiresIPhoneOS</key>
	<true/>
	<key>NSAppTransportSecurity</key>
	<dict>
		<key>NSAllowsArbitraryLoadsInWebContent</key>
		<true/>
	</dict>
	<key>NSCameraUsageDescription</key>
	<string>A Digipro le gustaría hacer uso de su cámara para uso exclusivo en la aplicación, es seguro y privado.</string>
	<key>NSLocationAlwaysAndWhenInUseUsageDescription</key>
	<string>A Digipro le gustaría hacer uso de su ubicación actual para mostrarla en la aplicación, es seguro y privado. Será usada para identificar la ubicación en que fué creado el Formato electrónico.</string>
	<key>NSLocationAlwaysUsageDescription</key>
	<string>A Digipro le gustaría hacer uso de su ubicación actual para mostrarla en la aplicación, es seguro y privado. Será usada para identificar la ubicación en que fué creado el Formato electrónico.</string>
	<key>NSLocationUsageDescription</key>
	<string>A Digipro le gustaría hacer uso de su ubicación actual para mostrarla en la aplicación, es seguro y privado. Será usada para identificar la ubicación en que fué creado el Formato electrónico.</string>
	<key>NSLocationWhenInUseUsageDescription</key>
	<string>A Digipro le gustaría hacer uso de su ubicación actual para mostrarla en la aplicación, es seguro y privado. Será usada para identificar la ubicación en que fué creado el Formato electrónico.</string>
	<key>NSMicrophoneUsageDescription</key>
	<string>A Digipro le gustaría hacer uso del micrófono para grabar audios para uso exclusivo en la aplicación, es seguro y privado.</string>
	<key>NSPhotoLibraryAddUsageDescription</key>
	<string>A Digipro le gustaría acceder a su librería de imágenes y hacer uso exclusivo en la aplicación, es seguro y privado.</string>
	<key>NSPhotoLibraryUsageDescription</key>
	<string>A Digipro le gustaría acceder a su librería de imágenes y hacer uso exclusivo en la aplicación, es seguro y privado.</string>
	<key>UIApplicationShortcutItems</key>
	<array>
		<dict>
			<key>UIApplicationShortcutItemIconFile</key>
			<string>edit-icon-c</string>
			<key>UIApplicationShortcutItemSubtitle</key>
			<string>Crear nuevo formato</string>
			<key>UIApplicationShortcutItemTitle</key>
			<string>Nuevo FE</string>
			<key>UIApplicationShortcutItemType</key>
			<string>nuevo.formato</string>
		</dict>
	</array>
</dict>
</plist>
```



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

