# Configuração do SDK

## Primeiros passos

Para iniciar a configuração do SDK único, o seu projeto precisa incluir as bibliotecas do SDK Único.
A solicitação do `Token de Acesso` deve ser realizada a partir [deste formulário](https://www.linx.com.br/sdk-access-request).


## Passo 1 - Configurar o repositório

Adicione esta seção ao seu arquivo `build.gradle` nos arquivos `repositories` e `publishing.repositories`.

```groovy
maven {
    url 'https://pkgs.dev.azure.com/stndtef/SmartPOS/_packaging/SDK_UNICO/maven/v1'
    name 'SDK_UNICO'
    authentication {
        basic(BasicAuthentication)
    }
}
```
Adicione ou edite o arquivo `settings.xml`localizado no caminho `${user.home}/.m2`

```groovy
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                              https://maven.apache.org/xsd/settings-1.0.0.xsd">
  <servers>
    <server>
      <id>SDK_UNICO</id>
      <username>stndtef</username>
      <password>[PERSONAL_ACCESS_TOKEN]</password>
    </server>
  </servers>
</settings>
```

!!! Atenção 

    Faz-se necessário, para cada SDK de adquirente, configurar as respectivas dependências. Sendo de utilização excludente utilizar dois SDKs simultaneamente.

## Passo 2 - Configurar o build.gradle da app

Dependências da **Stone**

=== "Maven"

    ```xml
    <dependency>
      <groupId>SDKPayServices</groupId>
      <artifactId>stone</artifactId>
      <version>1.0.3</version>
    </dependency>
    ```

=== "Gradle"

    ```groovy
    compile(group: 'SDKPayServices', name: 'stone', version: '1.0.3')
    ```    


Dependências do **Linx DTEF**

=== "Maven"

    ```xml
    <dependency>
      <groupId>SDKPayServices</groupId>
      <artifactId>tef</artifactId>
      <version>1.0.3</version>
    </dependency>
    ```

=== "Gradle"

    ```groovy
    compile(group: 'SDKPayServices', name: 'tef', version: '1.0.3')
    ```    