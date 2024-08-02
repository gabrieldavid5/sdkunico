# Pre-requisitos para Integração com o SDK Único

Para integrar o SDK Único na sua aplicação, é necessário atender a determinados requisitos técnicos.

## Requisitos do Sistema Operacional

O **SDK Único** é desenvolvido nativamente para Android, sendo necessário que sua aplicação também seja Android ou possua uma interface/plugin que permita a comunicação se for híbrida. A versão mínima suportada do Android é a **5.0+ (API 21)** ou superior.

## Versões do S.O. Android dos Terminais

Os terminais compatíveis possuem diferentes versões do sistema operacional, conforme definido pelo fabricante:

|  Stone               | DTEF       | REDE            | Getnet    | PagSeguro |
|----------------------|------------|-----------------|-----------|-----------|
| SUNMI P2  v7.1       |  SUNMI P2  | Positivo L400   | SUNMI P2  | SUNMI P2  |
| GPOS 700X: v8.1      |  AA        | AA              | AA        | AA        |
| Positivo L400 : v11  |  AA        | AA              | AA        | AA        |
| Positivo L300 : v7.1 |  AA        | AA              | AA        | AA        |
| APOS A8: v5.1        |  AA        | AA              | AA        | AA        |




É essencial desenvolver com retrocompatibilidade para a versão mínima (5.0) a fim de garantir o funcionamento em todos os modelos.

## Tamanho do APK

Para manter boas práticas de gerenciamento de espaço e uso de banda larga (3G/4G) nos terminais SmartPOS, o aplicativo deve ter no máximo <b>70MB</b>



