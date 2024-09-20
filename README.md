En el Contract PrivateBank.sol encontramos 

1 Una vulnerabilidad de reentrada ( Reentracy )
Basicamente en mi entender un contrato que tiene una determinada función es llamado por otro contrato externo llamando nuevamente a la función original antes  que la primera se ejecute. Por ejemplo en la misma línea de pensamiento en este caso tenemos un contrato (PrivateBank.sol) que tiene la función de Withdraw..me imagino un atacante que llama la función de Withdraw en el contrato y antes que finalice la transacción realiza otra llamada antes que se actualice el saldo del usuario. El atacante para realizar esto ejecuta su propio código. 
Es el famoso drenacion de fondos que lo que hace en otras palabras es manipular el contrato original.
Una posible solución seria actualizar el estado del contrato antes de hacer cualquier llamada externa
Lo que pude investigar también existen guardianes que bloquean la reentrada (Reentrancyguard) el modificador de OppenZeppelin podría ayudar a mitigar esto.
Siguiendo con la consigna en la línea 11 tenemos la función Withdraw. El atacante podría hacer que el msg.sender.call{value: balance} llame nuevamente la función Withdraw antes que el balances[msg.sender] = 0 se ejecute

2 En el contrato podemos observar la función getuserbalance ( línea 27)que lo que hace es devolver el saldo de un usuario..en este caso esta declarado como publico  lo que implica que puede ser llamado por otros usuario o otros contratos. Si quiero que solo los usuarios puedan consultar sus propios saldos podemos declarar la función en privada o interna

