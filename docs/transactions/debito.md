O processo para realizar qualquer transação, tem como premissa que a ativação do SDK foi previamente realizada. 
Para realizar uma Transação de *Débito*, utilize o exemplo abaixo. 

!!! Atenção 

    Verifique os parametros da transação. Os atributos devem seguir os critérios: <br/>
    - amount: MAIOR ou igual a 1

```kotlin
import android.os.Bundle
import android.util.Log
import androidx.appcompat.app.AppCompatActivity
import com.linx.paykit.common.Callback
import com.linx.paykit.common.Paykit
import com.linx.paykit.common.PaymentResult
import com.linx.paykit.common.builder.Parameters
import com.linx.paykit.common.parameter.PaymentParameters
import com.linx.paykit.core.PaykitFactory
import java.math.BigDecimal

class MainActivity : AppCompatActivity() {

    private lateinit var paykit: Paykit

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        paykit = PaykitFactory().build(Parameters(this.applicationContext, "Transacao de Debito"))

        val debitParameter = PaymentParameters(
            amount = BigDecimal("100.00"),  // Valor da transação
            automaticConfirmation = true  // Confirmação automática
        )

        paykit.credit(debitParameter, object : Callback<PaymentResult> {
            override fun execute(result: PaymentResult) {
                Log.i("PaymentResult", "ID: ${result.transactionId}, Transaction: ${result.transaction}")
                onPaymentResult(result.transactionId, result.transaction)
            }
        })
    }

    private fun onPaymentResult(transactionId: String, transaction: PaymentResult) {
        // Implementar a lógica para lidar com o resultado do pagamento
    }
}
```

## Explicação do PaymentResult

No `callBack` da transação, é possível capturar detalhes da adquirente, como detalhado a seguir.

 - transactionId: Identificador único da transação (NSU).
 - transaction: Objeto contendo o resultado detalhado da transação da adquirente, útil para deserialização.
 - transactionType: Tipo de processador de pagamento utilizado (STONE, TEF, REDE, GETNET, PAGSEGURO, VERO).
 - status: Status da transação.
 - message: Mensagem de sucesso ou erro, se houver.


