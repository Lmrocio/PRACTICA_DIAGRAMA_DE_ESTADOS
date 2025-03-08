# DIAGRAMAS DE ESTADOS

La actividad consiste en realizar un diagrama de estados, que refleje los distintos estados y transiciones en los que se encuentra un cajero en cada momento.

> Requisitos del sistema:
>  - El sistema en un estado stand-by hasta que un usuario introduce una tarjeta.
>  - El usuario introduce la tarjeta en el sistema y el sistema valida la tarjeta. Si la tarjeta no es correcta, el sistema expulsará la tarjeta y quedará en estado stand-by. En el caso de ser una tarjeta válida, el sistema solicita al usuario que se valide mediante un pin.
>  - Si hay error en el pin, el sistema volverá al usuario que vuelva a intentar validarse hasta completar el proceso 3 veces, en cuyo caso, si el usuario no se ha validado correctamente finalizará el proceso, quedándose con la tarjeta. El usuario podrá cancelar el proceso de identificación en cualquier momento antes de cumplir los 3 intentos.
>  - Una vez el usuario se ha validado correctamente, el sistema ofrecerá al sistema las distintas transacciones que puede realizar. Cuando una transacción sea elegida, se llevará a cabo, y, al finalizarla, el sistema dará la opción de poder elegir una nueva transacción o cancelar la interacción con el cajero y por tanto finalizar sesión. La interacción con el cajero podrá ser cancelada, finalizada la sesión, en cualquier momento siempre y cuando no esté en proceso de ejecución de una transacción.

<hr>

## Diseñar el diagrama de estados del sistema. (Entrega: Diagrama de estados y código para generarlo)

