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



## Permissões Necessárias

Adicione as seguintes permissões ao seu arquivo `AndroidManifest.xml`:

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.yourcompany.sdkunico">

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