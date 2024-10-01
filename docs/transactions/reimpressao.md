O processo para realizar qualquer transação, tem como premissa que a ativação do SDK foi previamente realizada. 
Para realizar uma Transação de *Reimpressão*, utilize o exemplo abaixo. Ela realizará o desfazimento da última transação.


```kotlin
import android.os.Bundle
import android.util.Log
import androidx.appcompat.app.AppCompatActivity
import com.linx.paykit.common.Callback
import com.linx.paykit.common.Paykit
import com.linx.paykit.common.PaymentResult
import com.linx.paykit.common.builder.Parameters
import com.linx.paykit.common.parameter.ReprintParameters
import com.linx.paykit.core.PaykitFactory
import java.math.BigDecimal

class MainActivity : AppCompatActivity() {

    private lateinit var paykit: Paykit

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)


        val reprintParameter = ReprintParameters(
            receiptParameter.MERCHANT,  // Ou receiptParameter.CLIENT
            reprintParameters.nsu = "NSU_DA_TRANSACAO"
        )

        paykit = PaykitFactory().build(Parameters(this.applicationContext, "Transacao de Reimpressão"))

        paykit.reprint(reprintParameter, object : Callback<PaymentResult> {
            override fun execute(result: PaymentResult) {
                Log.i("PaymentResult", "Status: ${result.status}")
                onPaymentResult(result.transaction)
            }
        })
    }

    private fun onPaymentResult(transaction: PaymentResult) {
        // Implementar a lógica para lidar com o resultado da reversão
    }
}
```

## Explicação do PaymentResult

No `callBack` da transação, é possível capturar detalhes da adquirente, como detalhado a seguir.

 - transactionType: Tipo de processador de pagamento utilizado (STONE, TEF, REDE, GETNET, PAGSEGURO).
 - status: Status da transação.
 - message: Mensagem de sucesso ou erro, se houver.


