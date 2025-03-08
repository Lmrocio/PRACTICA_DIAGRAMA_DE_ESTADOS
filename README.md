# DIAGRAMAS DE ESTADOS

La actividad consiste en realizar un diagrama de estados, que refleje los distintos estados y transiciones en los que se encuentra un cajero en cada momento.

> Requisitos del sistema:
>  - El sistema en un estado stand-by hasta que un usuario introduce una tarjeta.
>  - El usuario introduce la tarjeta en el sistema y el sistema valida la tarjeta. Si la tarjeta no es correcta, el sistema expulsará la tarjeta y quedará en estado stand-by. En el caso de ser una tarjeta válida, el sistema solicita al usuario que se valide mediante un pin.
>  - Si hay error en el pin, el sistema volverá al usuario que vuelva a intentar validarse hasta completar el proceso 3 veces, en cuyo caso, si el usuario no se ha validado correctamente finalizará el proceso, quedándose con la tarjeta. El usuario podrá cancelar el proceso de identificación en cualquier momento antes de cumplir los 3 intentos.
>  - Una vez el usuario se ha validado correctamente, el sistema ofrecerá al sistema las distintas transacciones que puede realizar. Cuando una transacción sea elegida, se llevará a cabo, y, al finalizarla, el sistema dará la opción de poder elegir una nueva transacción o cancelar la interacción con el cajero y por tanto finalizar sesión. La interacción con el cajero podrá ser cancelada, finalizada la sesión, en cualquier momento siempre y cuando no esté en proceso de ejecución de una transacción.

<hr>

## Diseñar el diagrama de estados del sistema. 

![diagrama diseñado](https://github.com/Lmrocio/PRACTICA_DIAGRAMA_DE_ESTADOS/blob/main/Diagrama_estados.png?raw=true)

<details> <summary>Código empleado para realizar el diagrama</summary>

@startuml
[*] --> StandBy

StandBy --> TarjetaInsertada : Insertar tarjeta

TarjetaInsertada --> TarjetaValida : Validar tarjeta

TarjetaInsertada --> TarjetaExpulsada : Tarjeta inválida

TarjetaValida --> SolicitarPIN : Solicitar PIN

TarjetaExpulsada --> StandBy : Expulsar tarjeta

SolicitarPIN --> PINCorrecto : Validar PIN

SolicitarPIN --> PINIncorrecto : PIN incorrecto

PINIncorrecto --> SolicitarPIN : Reintentar PIN

PINIncorrecto --> FinSesion : 3 intentos fallidos

PINCorrecto --> MenuTransacciones : Acceso al menú de transacciones

FinSesion --> [*] : Finalizar sesión

MenuTransacciones --> ElegirTransaccion : Elegir transacción

ElegirTransaccion --> RealizarTransaccion : Realizar transacción

RealizarTransaccion --> MenuTransacciones : Nueva transacción

RealizarTransaccion --> FinalizarSesion : Cancelar interacción

FinalizarSesion --> [*] : Fin de la sesión

@enduml
  
</details>

<hr>

## Describir el diagrama realizado, interpretando cada uno de los elementos que aparecen en él.

### Estados:
> Se consideran como ``estados`` a los diferentes momentos que un sistema puede tomar, es decir, serían los instantes de un proceso en el que el sistema ha cambiado.

- StandBy: el cajero está esperando a que el usuario inserte una tarjeta. Se trata del estado inicial, en el cual no se está realizando ninguna acción activa.
  
- TarjetaInsertada: el cajero detecta una tarjeta que ha sido introducida por un usuario.
  
- TarjetaValida: el sistema ha validado la tarjeta introducida y procede a solicitar el pin.
  
- TarjetaExpulsada: la tarjeta introducida no es válida, por lo que será expulsada y se volverá al estado inicial.
  
- SolicitarPin: el sistema solicita al usuario que introduzca el pin de la tarjeta, una vez que esta ha sido validada.
  
- PinCorrecto: el sistema valida el pin introducido por el usuario para una tarjeta determinada, pasando al siguiente estado del sistema.
  
- PinIncorrecto: el sistema permite que el usuario vuelva a intentar ingresar el pin de la tarjeta.
  
- MenuTransacciones: muestra las opciones de transacciones que ofrece el cajero.
  
- ElegirTransaccion: el usuario eligue una de las transacciones del cajero.
  
- RealizarTransaccion: el sistema realiza la transacción elegida por el usuario.
  
- FinalizarSesion: el usuario decide cancelar la sesión y salir del cajero.
  
### Transiciones:
> Las ``transiciones`` indican cambios entre los distintos estados de un sistema. Estos cambios tendrán condiciones que apelen a los requisitos necesarios para que dicho cambio tenga lugar.

- StandBy --> TarjetaInsertada: se activa cuando el usuario inserta una tarjeta en el cajero.
  
- TarjetaInsertada --> TarjetaValida: la tarjeta introducida es válida.
  
- TarjetaInsertada --> TarjetaExpulsada: la tarjeta es inválida, por lo que se expulsa y el sistema regresa a StandBy.
  
- TarjetaValida --> SolicitarPIN: después de que la tarjeta es validada correctamente, el sistema solicita al usuario que ingrese el PIN.
  
- SolicitarPIN --> PINCorrecto: se produce cuando el usuario ingresa el PIN correctamente.
  
- SolicitarPIN --> PINIncorrecto: se activa cuando el usuario ingresa un PIN incorrecto, permitiendo reintentos.
  
- PINIncorrecto --> FinSesion: si el usuario falla tres veces en ingresar el PIN correctamente, el sistema termina la sesión.
  
- PINCorrecto --> MenuTransacciones: después de un PIN correcto, el sistema muestra el menú de transacciones disponibles.
  
- MenuTransacciones --> ElegirTransaccion: el usuario elige una de las transacciones ofrecidas.
  
- ElegirTransaccion --> RealizarTransaccion: el sistema lleva a cabo la transacción elegida.
  
- RealizarTransaccion --> MenuTransacciones: después de realizar una transacción, el sistema ofrece la opción de elegir otra transacción.
  
- RealizarTransaccion --> FinalizarSesion: si el usuario decide cancelar la sesión después de realizar una transacción, el sistema finaliza la interacción.
  
- FinalizarSesion --> [*]: el sistema finaliza la sesión, regresando al estado inicial de StandBy

### Pseudoestados:
> Existen momentos en el sistema que no representan un estado en sí, pero que nos permite manejar o exponer con mayor claridad las transiciones del sistema. Esto son los ``pseudoestados``.

- [*]: representa el punto de inicio y fin del diagrama, pero no representa un estado en sí, ya que podríamos decir que el estado es StandBy. Este punto nos ayuda a comprender mejor el flujo del sistema.
  
### Condiciones:
> Las ``condiciones`` son los requisitos que deben tener lugar para que se realice una transición entre estados.

- Tarjeta válida: la tarjeta es válida para proceder con la validación del PIN.
  
- Tarjeta inválida: la tarjeta no es válida y es expulsada.
  
- PIN correcto: el PIN ingresado por el usuario es correcto.
  
- PIN incorrecto: el PIN ingresado por el usuario es incorrecto.
  
- 3 intentos fallidos: después de tres intentos fallidos para ingresar el PIN, el sistema cancela o suspende la sesión.
  
- Transacción elegida: el usuario elige una transacción.
  
- Cancelar sesión: el usuario decide terminar la interacción.

### Comportamientos:
> Se tratan de acciones o actividades que se ejecutan durante las transiciones o estados. Es decir, son procesos que ocurren mientras un estado o transición está teniendo lugar en el sistema.

En este caso, he considerado que no hay ningún comportamiento según el enunciado planteado. El diagrama se centra más en el flujo de los estados y las condiciones necesarias para que sucedan las transiciones que se plantean.
