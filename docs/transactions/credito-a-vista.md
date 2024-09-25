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

### Configurar uma transação

Para realizar uma transação de pagamento, utilize a `PaymentParameters` definindo os parâmetros de acordo com o tipo da transação.

#### Parâmetros:

| Campo                    | Tipo           | Descrição                                                                                  |
|--------------------------|----------------|--------------------------------------------------------------------------------------------|
| **automaticConfirmation** | `Boolean`      | Indica se a confirmação da transação deve ser automática.                                 |
| **amount**               | `BigDecimal`   | O valor total da transação.                                                               |
| **installments**         | `Int`         | O número de parcelas para pagamento. O valor .                                |
| **cpf**                  | `String?`      | CPF do cliente, se aplicável. Este campo é opcional.                                      |
| **financialType**        | `FinancialType` | O tipo de financiamento da transação. Possíveis valores:            |
|                          |                | - `FinancialType.ISSUER`: Parcelado pelo cliente.                                        |
|                          |                | - `FinancialType.ONE_INSTALMENT`: Pagamento em uma única parcela.                        |
|                          |                | - `FinancialType.MERCHANT`: Parcelado pelo lojista.                                      |
|                          |                | - `FinancialType.PRE_DATED`: Pagamento pré-datado.                                       |
| **billOfSale**           | `String?`      | Documento de venda associado à transação. Este campo é opcional.                          |
| **dateTimeOfSale**      | `Date?`        | Data e hora em que a venda foi realizada. Este campo é opcional.                         |
| **externalId**           | `String?`      | Identificador externo para a transação, se necessário. Este campo é opcional.            |
| **deadline**             | `Int?`         | Data de expiração da primeira parcela, em dias. Este campo é opcional.                   |



### Retorno da transação

O objeto `PaymentResult`, retornado no callback da transação, contém informações essenciais da adquirente. Abaixo estão os principais campos disponíveis:

| Campo      | Tipo     | Descrição                                                            |
|------------|----------|----------------------------------------------------------------------|
| **id**     | `String` | Identificador único da transação (NSU).                             |
| **processor** | `Enum`  | Indica o processador da transação. Valores possíveis:               |
|            |          | - `STONE`                                                           |
|            |          | - `TEF`                                                             |
|            |          | - `REDE`                                                            |
|            |          | - `GETNET`                                                          |
|            |          | - `PAGSEGURO                                                        |
|            |          | - `VERO`                                                            |
| **status** | `Enum`   | Representa o status da transação. Valores possíveis:                |
|            |          | - `PENDING`: Aguardando processamento.                               |
|            |          | - `APPROVED`: Transação aprovada.                                   |
|            |          | - `CANCELLED`: Transação cancelada.                                 |
|            |          | - `ERROR`: Ocorreu um erro na transação.                            |
|            |          | - `DECLINED`: Transação recusada.                                   |
| **transactionData** | `Map<String, String>` | Inclui os dados da transação da adquirente.               |
| **message** | `String` | Mensagem de sucesso ou erro, caso aplicável.  