# Configuração do SDK

## Primeiros passos

Para iniciar a configuração do SDK único, o seu projeto precisa incluir as bibliotecas do SDK Único.
A solicitação da `Senha de Acesso` deve ser realizada a partir [deste formulário](https://forms.office.com/r/ThvGGXDuq4).

Esta senha é intransferível e é de responsabilidade de cada vertical solicitar a senha para o seu time.


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

Adicione as dependências de implementação do SDK no `build.gradle` da app


=== "SDK"

    ```groovy
    dependencies {
        implementation("SDKPayServices:core:0.1.3.15458")
        implementation("SDKPayServices:config:0.1.3.15458")
        implementation("SDKPayServices:common:0.1.3.15458")
    }
    ```


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
