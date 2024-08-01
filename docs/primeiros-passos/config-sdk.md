# Configuração do SDK

## Primeiros passos

Para iniciar a configuração do SDK único, o seu projeto precisa incluir as bibliotecas do SDK Único.
A solicitação do `Token de Acesso` deve ser realizada a partir [deste formulário](https://forms.office.com/r/ThvGGXDuq4).


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


## Passo 3 - Verificar as permissões necessárias

Adicione as seguintes permissões ao seu arquivo `AndroidManifest.xml`:

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.seuapp">

    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
    <uses-permission android:name="android.permission.CHANGE_WIFI_STATE"/>
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.BLUETOOTH"/>
    <uses-permission android:name="android.permission.BLUETOOTH_ADMIN"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.WRITE_OWNER_DATA"/>
    <uses-permission android:name="android.permission.READ_OWNER_DATA"/>
    <uses-permission android:name="android.permission.READ_PHONE_STATE"/>


    <application
        android:allowBackup="true"
        android:label="@string/app_name"
        android:icon="@mipmap/ic_launcher"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>
```