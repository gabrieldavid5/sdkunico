# Primeira Integração

O SDK único, em sua definição, simplifica a integração com os SDKs das adquirentes, a partir de sua interface única. <br/>

Para integrar sua aplicação com o SDK Único, siga os passos abaixo. Certifique-se de adicionar os devidos imports e configurar os parâmetros corretamente.

```kotlin
import android.util.Log
import com.linx.paykit.common.Callback
import com.linx.paykit.common.Paykit
import com.linx.paykit.common.activation.ActivationParameters
import com.linx.paykit.common.activation.ActivationResult
import com.linx.paykit.common.builder.Parameters
import com.linx.paykit.core.PaykitFactory

val TAG = "SDKUnicoExample"
var paykit: Paykit? = null

fun setupPaykit() {

    paykit = PaykitFactory().build()

    //Defina os parâmetros de acordo com a adquirente
    val params = ActivationParameters().apply {
        
    }

    paykit?.activate(p, object : Callback<ActivationResult> {
        override fun execute(result: ActivationResult) {
            Log.d(TAG, "SDK Ativado com sucesso")
        }
    })
}
```

A classe `ActivationParameters` possui parâmetros de acordo com o SDK da Adquirente.

=== "Linx DTEF"

    ```kotlin
        val params = ActivationParameters().apply {
            tef.cnpj = "CNPJ"
            tef.production = false
            tef.token = "TOKEN"
        }
    ```

=== "Stone"

    ```kotlin
        val params = ActivationParameters().apply {
            stone.stoneCode = "CODIGO_STONE"
            stone.context = this.applicationContext
            stone.dialogMessage = "Dialog Message"
            stone.dialogTitle = "Dialog Title"
        }
    ```

=== "PagSeguro"

    ```kotlin
        val params = ActivationParameters().apply {
            pagSeguro.activationCode = "CODIGO_PAG_SEGURO"
        }
    ```

=== "Rede"

    ```kotlin
        val params = ActivationParameters().apply {
            rede.activationCode = "CODIGO_REDE"
        }
    ```

!!! Atenção 

    Verifique na lista de dependências do Android Studio a correta adição do SDK da adquirente, de acordo com a versão solicitada no formulário de acesso ao SDK.
