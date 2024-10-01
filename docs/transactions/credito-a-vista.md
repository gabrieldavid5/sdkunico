O processo para realizar qualquer transação, tem como premissa que a ativação do SDK foi previamente realizada. 
Para realizar uma Transação de *Crédito à vista*, utilize o exemplo abaixo.

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

        PaykitFactory().build(Parameters(context, APP_NAME))

        paykit = PaykitFactory().build(Parameters(this.applicationContext, "Credito à Vista"))

        val creditParameter = PaymentParameters(
            installments = 1,  // Número de parcelas (1 para crédito à vista)
            amount = BigDecimal("100.00"),  // Valor da transação
            automaticConfirmation = true  // Confirmação automática
        )

        paykit.credit(creditParameter, object : Callback<PaymentResult> {
            override fun execute(result: PaymentResult) {
                Log.i("PaymentResult", "ID: ${result.id}, Transaction: ${result.transactionData}")
                onPaymentResult(result.id, result.transaction)
            }
        })
    }

    private fun onPaymentResult(id: String, transaction: PaymentResult) {
        // Implementar a lógica para lidar com o resultado do pagamento
    }
}
```
