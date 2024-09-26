# Configuração do SDK

## Primeiros passos

Para iniciar a configuração do SDK único, o seu projeto precisa incluir as bibliotecas do SDK Único.
A solicitação da `Senha de Acesso` deve ser realizada a partir [deste formulário](https://forms.office.com/r/ThvGGXDuq4).

Esta senha é intransferível e é de responsabilidade de cada vertical solicitar para o seu time.


## Passo 1 - Configurar o repositório

Adicione as variáveis do Artifacts em seu `gradle.properties`

```
azureUsername=stndtef
azurePassword=YOUR_PASSWORD_HERE
```

Adicione ou edite o arquivo `settings.gradle.kts` do projeto principal.

```groovy
val azureUsername: String? = findProperty("azureUsername") as String?
val azurePassword: String? = findProperty("azurePassword") as String?

dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        google()
        mavenCentral()
        maven {
            name = "SDK_UNICO"
            url = uri("https://pkgs.dev.azure.com/stndtef/SmartPOS/_packaging/SDK_UNICO/maven/v1")
            credentials {
                username = azureUsername ?: "default_username"
                password = azurePassword ?: "default_password"
            }
        }
    }
}
```

!!! Atenção 

    Faz-se necessário, para cada SDK de adquirente, configurar as respectivas dependências de adquirentes. Sendo de utilização excludente utilizar dois SDKs simultaneamente.

## Passo 2 - Configurar as dependências da app

Adicione as dependências de implementação do SDK no `build.gradle` da app.
O SDK Único possui três dependências principais: `commons`, `config` e `core` , que encapsulam os comportamentos das adquirentes.
Todas estas são necessárias para a compilação do projeto.

- Core library

=== "Maven"

    ```xml
    <dependency>
        <groupId>SDKPayServices</groupId>
        <artifactId>core</artifactId>
        <version>1.0.3</version>
    </dependency>
    ```
=== "Gradle"    

    ```groovy
    compile(group: 'SDKPayServices', name: 'core', version: '1.0.3')
    ```
- Commons library 

=== "Maven"

    ```groovy
    <dependency>
        <groupId>SDKPayServices</groupId>
        <artifactId>common</artifactId>
        <version>1.1.1</version>
    </dependency>
    ```
=== "Gradle"    

    ```groovy
    compile(group: 'SDKPayServices', name: 'common', version: '1.1.1')
    ```

- Config library 

=== "Maven"

    ```xml
    <dependency>
        <groupId>SDKPayServices</groupId>
        <artifactId>config</artifactId>
        <version>1.1.1</version>
    </dependency>
    ```
=== "Gradle"    

    ```groovy
    compile(group: 'SDKPayServices', name: 'config', version: '1.1.1')
    ```


Para adicionar o SDK da adquirente ao projeto, selecione a versão apropriada de release.


- Stone

=== "Maven"

    ```xml
        <dependency>
            <groupId>SDKPayServices</groupId>
            <artifactId>stone</artifactId>
            <version>1.1.1</version>
        </dependency>
    ```
=== "Gradle"

    ```groovy
        compile(group: 'SDKPayServices', name: 'stone', version: '1.1.1')
    ```

- PagSeguro

=== "Maven"

    ```xml
        <dependency>
            <groupId>SDKPayServices</groupId>
            <artifactId>pagseguro</artifactId>
            <version>1.1.1</version>
        </dependency>
    ```
=== "Gradle"

    ```groovy
        compile(group: 'SDKPayServices', name: 'pagseguro', version: '1.1.1')
    ```

- Getnet

=== "Maven"

    ```xml
        <dependency>
            <groupId>SDKPayServices</groupId>
            <artifactId>getnet</artifactId>
            <version>0.1.3.15529</version>
        </dependency>
    ```
=== "Gradle"

    ```groovy
   compile(group: 'SDKPayServices', name: 'getnet', version: '0.1.3.15529')
    ```
- Vero

=== "Maven"

    ```xml
    <dependency>
        <groupId>SDKPayServices</groupId>
        <artifactId>vero</artifactId>
        <version>0.1.3.15529</version>
    </dependency>
    ```
=== "Gradle"

    ```groovy
        compile(group: 'SDKPayServices', name: 'vero', version: '0.1.3.15529')
    ```

!!! Atenção 

    Faz-se necessário, para cada SDK de adquirente, configurar as respectivas dependências de adquirentes. Sendo de utilização excludente utilizar dois SDKs simultaneamente.

Dependências da **Vero**

=== "Gradle"

    ```groovy
    android {
        productFlavors {
        create("linxtef")
        create("stone") {
            minSdk = 22
            targetSdk = 34
        }
        create("pagseguro") {
            minSdk = 23
        }
        create("rede")
        create("getnet") {
            minSdk = 22
        }
        create("vero"){
            minSdk = 22
        }
    }
    ```    

## Passo 3 - Verificação de dependências

Realize a build do projeto e verifique se as dependências foram resolvidas.
