## Interface Paykit

A interface `Paykit` define os métodos que cada adquirente deve implementar para realizar transações de pagamento.

### Métodos

| Método                          | Descrição                                                                 | Parâmetros                                                         | Retorno             |
|---------------------------------|---------------------------------------------------------------------------|--------------------------------------------------------------------|---------------------|
| **activate**                    | Ativa o SDK com os parâmetros fornecidos.                | `activationParameters`: Parâmetros de ativação.                                     | `ActivationResult`  |
| **credit**                      | Realiza uma transação de crédito.                        | `paymentParameters`: Parâmetros da transação.                                       | `PaymentResult`     |
| **debit**                       | Realiza uma transação de débito.                         | `paymentParameters`: Parâmetros da transação.                                       | `PaymentResult`     |
| **voucher**                     | Processa um pagamento por meio de voucher.               | `paymentParameters`: Parâmetros da transação.                                       | `PaymentResult`     |
| **pix**                         | Processa um pagamento via PIX.                           | `paymentParameters`: Parâmetros da transação.                                       | `PaymentResult`     |
| **wallet**                      | Processa um pagamento utilizando carteira digital.        | `paymentParameters`: Parâmetros da transação.                                      | `PaymentResult`     |
| **cancel**                      | Cancela uma transação.                                   | `cancelParameter`: Parâmetros de cancelamento.                                      | `PaymentResult`      |
| **confirmPendingTransaction**   | Confirma uma transação pendente.                        | `pendingTransactionParameters`: Parâmetros da transação pendente.                    | `Boolean`           |
| **undoPendingTransaction**      | Desfaz uma transação pendente.                          | `pendingTransactionParameters`: Parâmetros da transação pendente.                    | `Boolean`           |
| **printLastReceipt**           | Imprime o último recibo.                                | `receiptType`: Tipo de recibo a ser impresso.                                         | `Boolean`           |
| **print**                       | Imprime uma imagem bitmap.                              | `bitmap`: A imagem a ser impressa.                                                   | `Boolean`           |
| **retrieveSdkInfo**            | Recupera informações sobre o SDK.                       | `callback`: Callback para receber as informações do SDK.                              | `SdkInfo`           |



### Configurar uma transação de pagamento

Para realizar uma transação de pagamento, utilize a classe `PaymentParameters` definindo os parâmetros de acordo com o tipo da transação.

#### Parâmetros:

| Campo                    | Tipo           | Descrição                                                                                  |
|--------------------------|----------------|--------------------------------------------------------------------------------------------|
| **automaticConfirmation** | `Boolean`      | Indica se a confirmação da transação deve ser automática.                                 |
| **amount**               | `BigDecimal`   | O valor total da transação.                                                                |
| **installments**         | `Int`         | O número de parcelas para pagamento. O valor .                                              |
| **cpf**                  | `String?`      | CPF do cliente, se aplicável. Este campo é opcional.                                       |
| **financialType**        | `FinancialType` | O tipo de financiamento da transação. Possíveis valores:                                  |
|                          |                | - `FinancialType.ISSUER`: Parcelado pelo cliente.                                          |
|                          |                | - `FinancialType.ONE_INSTALMENT`: Pagamento em uma única parcela.                          |
|                          |                | - `FinancialType.MERCHANT`: Parcelado pelo lojista.                                        |
|                          |                | - `FinancialType.PRE_DATED`: Pagamento pré-datado.                                         |
| **billOfSale**           | `String?`      | Documento de venda associado à transação. Este campo é opcional.                           |
| **dateTimeOfSale**      | `Date?`        | Data e hora em que a venda foi realizada. Este campo é opcional.                            |
| **externalId**           | `String?`      | Identificador externo para a transação, se necessário. Este campo é opcional.              |
| **deadline**             | `Int?`         | Data de expiração da primeira parcela, em dias. Este campo é opcional.                     |



### Retorno da transação

O objeto `PaymentResult`, retornado no callback da transação, contém informações essenciais da adquirente. Abaixo estão os principais campos disponíveis:

| Campo      | Tipo     | Descrição                                                            |
|------------|----------|----------------------------------------------------------------------|
| **id**     | `String` | Identificador único da transação (NSU).                              |
| **processor** | `Enum`  | Indica o processador da transação. Valores possíveis:              |
|            |          | - `STONE`                                                            |
|            |          | - `TEF`                                                              |
|            |          | - `REDE`                                                             |
|            |          | - `GETNET`                                                           |
|            |          | - `PAGSEGURO                                                         |
|            |          | - `VERO`                                                             |
| **status** | `Enum`   | Representa o status da transação. Valores possíveis:                 |
|            |          | - `PENDING`: Aguardando processamento.                               |
|            |          | - `APPROVED`: Transação aprovada.                                    |
|            |          | - `CANCELLED`: Transação cancelada.                                  |
|            |          | - `ERROR`: Ocorreu um erro na transação.                             |
|            |          | - `DECLINED`: Transação recusada.                                    |
| **transactionData** | `Map<String, String>` | Inclui os dados da transação da adquirente.    |
| **message** | `String` | Mensagem de sucesso ou erro, caso aplicável.  