---
title: Salesforce Source聯結器總覽
description: 瞭解如何使用API或使用者介面將Salesforce連線至Adobe Experience Platform。
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1593'
ht-degree: 0%

---

# [!DNL Salesforce]

>[!IMPORTANT]
>
>您現在可以在Amazon Web Services (AWS)上執行Adobe Experience Platform時使用[!DNL Salesforce]來源。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../landing/multi-cloud.md)。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Experience Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從協力廠商CRM系統擷取資料。 CRM提供者的支援包括[!DNL Salesforce]。

## 在Azure上設定Experience Platform的[!DNL Salesforce]來源 {#azure}

請依照下列步驟，瞭解如何在Azure上為Experience Platform設定[!DNL Salesforce]帳戶。

### IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

### 從[!DNL Salesforce]到XDM的欄位對應

若要在[!DNL Salesforce]與Experience Platform之間建立來源連線，[!DNL Salesforce]來源資料欄位必須先對應到適當的目標XDM欄位，才能內嵌到Experience Platform中。

請參閱下列內容，以取得有關[!DNL Salesforce]資料集與Experience Platform之間的欄位對應規則的詳細資訊：

- [連絡人](../adobe-applications/mapping/salesforce.md#contact)
- [銷售機會](../adobe-applications/mapping/salesforce.md#lead)
- [帳戶](../adobe-applications/mapping/salesforce.md#account)
- [機會](../adobe-applications/mapping/salesforce.md#opportunity)
- [機會聯絡人角色](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [行銷活動](../adobe-applications/mapping/salesforce.md#campaign)
- [行銷活動成員](../adobe-applications/mapping/salesforce.md#campaign-member)
- [帳戶聯絡人關係](../adobe-applications/mapping/salesforce.md#account-contact-relation)

### 設定[!DNL Salesforce]名稱空間和結構描述自動產生公用程式

若要使用[!DNL Salesforce]來源做為[!DNL B2B-CDP]的一部分，您必須先設定[!DNL Postman]公用程式來自動產生[!DNL Salesforce]名稱空間和結構描述。 下列檔案提供有關設定[!DNL Postman]公用程式的額外資訊：

- 您可以從此[GitHub存放庫](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility)下載名稱空間和結構描述自動產生公用程式集合和環境。
- 如需有關使用Experience Platform API的資訊，包括如何收集必要標題的值以及讀取範例API呼叫的詳細資訊，請參閱[Experience Platform API快速入門](../../../landing/api-guide.md)指南。
- 如需如何產生Experience Platform API認證的詳細資訊，請參閱[驗證及存取Experience Platform API](../../../landing/api-authentication.md)教學課程。
- 如需如何為Experience Platform API設定[!DNL Postman]的詳細資訊，請參閱[設定開發人員主控台和 [!DNL Postman]](../../../landing/postman.md)上的教學課程。

透過Experience Platform開發人員主控台和[!DNL Postman]設定，您現在可以開始將適當的環境值套用至您的[!DNL Postman]環境。

+++檢視變數表格指南

下表包含範例值，以及有關填入[!DNL Postman]環境的其他資訊：

| 變數 | 說明 | 範例 |
| --- | --- | --- |
| `CLIENT_SECRET` | 用來產生`{ACCESS_TOKEN}`的唯一識別碼。 如需如何擷取`{CLIENT_SECRET}`的詳細資訊，請參閱有關[驗證及存取Experience Platform API](../../../landing/api-authentication.md)的教學課程。 | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web權杖(JWT)是用於產生{ACCESS_TOKEN}的驗證認證。 如需如何產生`{JWT_TOKEN}`的相關資訊，請參閱有關[驗證及存取Experience Platform API](../../../landing/api-authentication.md)的教學課程。 | `{JWT_TOKEN}` |
| `API_KEY` | 用於驗證Experience Platform API呼叫的唯一識別碼。 如需如何擷取`{API_KEY}`的詳細資訊，請參閱有關[驗證及存取Experience Platform API](../../../landing/api-authentication.md)的教學課程。 | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | 完成對Experience Platform API的呼叫所需的授權權杖。 如需如何擷取`{ACCESS_TOKEN}`的詳細資訊，請參閱有關[驗證及存取Experience Platform API](../../../landing/api-authentication.md)的教學課程。 | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | 關於[!DNL Marketo]，此值是固定的，並且一律設定為： `ent_dataservices_sdk`。 | `ent_dataservices_sdk` |
| `CONTAINER_ID` | `global`容器保有所有標準Adobe和Experience Platform合作夥伴提供的類別、結構描述欄位群組、資料型別和結構描述。 關於[!DNL Marketo]，此值是固定的，且一律設為`global`。 | `global` |
| `PRIVATE_KEY` | 用於向Experience Platform API驗證您的[!DNL Postman]執行個體的認證。 請參閱有關設定開發人員主控台和[設定開發人員主控台和 [!DNL Postman]](../../../landing/postman.md)的教學課程，以瞭解如何擷取{PRIVATE_KEY}的說明。 | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | 用來整合至Adobe I/O的認證。 | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management系統(IMS)提供驗證Adobe服務的架構。 關於[!DNL Marketo]，此值是固定的，且一律設為： `ims-na1.adobelogin.com`。 | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 企業實體，可以擁有或授權產品及服務並允許存取其成員。 如需如何擷取`{ORG_ID}`資訊的說明，請參閱[設定開發人員主控台和 [!DNL Postman]](../../../landing/postman.md)的教學課程。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 您正在使用的虛擬沙箱分割的名稱。 | `prod` |
| `TENANT_ID` | ID，用來確保您建立的資源已正確命名且包含在您的組織內。 | `b2bcdpproductiontest` |
| `PLATFORM_URL` | 您對其進行API呼叫的URL端點。 此值是固定的，且一律設為： `http://platform.adobe.io/`。 | `http://platform.adobe.io/` |
| `munchkinId` | 您的[!DNL Marketo]帳戶的唯一識別碼。 如需如何擷取`munchkinId`的詳細資訊，請參閱[驗證您的 [!DNL Marketo] 執行個體](../adobe-applications/marketo/marketo-auth.md)的教學課程。 | `123-ABC-456` |
| `sfdc_org_id` | 您的[!DNL Salesforce]帳戶的組織識別碼。 請參閱下列[[!DNL Salesforce] 指南](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1)，以取得您[!DNL Salesforce]組織ID的詳細資訊。 | `00D4W000000FgYJUA0` |
| `has_abm` | 表示您是否訂閱[!DNL Marketo Account-Based Marketing]的布林值。 | `false` |
| `has_msi` | 表示您是否訂閱[!DNL Marketo Sales Insight]的布林值。 | `false` |

{style="table-layout:auto"}

+++

### 執行指令碼

設定好[!DNL Postman]集合和環境後，您現在可以透過[!DNL Postman]介面執行指令碼。

在[!DNL Postman]介面中，選取自動產生器公用程式的根資料夾，然後從頂端標題選取&#x200B;**[!DNL Run]**。

![根資料夾](../../images/tutorials/create/salesforce/root-folder.png)

[!DNL Runner]介面出現。 從這裡，確定已選取所有核取方塊，然後選取&#x200B;**[!DNL Run Namespaces and Schemas Autogeneration Utility]**。

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

成功的請求會根據測試版規格建立B2B名稱空間和結構描述。

## 在Amazon Web Services上設定Experience Platform的[!DNL Salesforce]來源 {#aws}

>[!AVAILABILITY]
>
>本節適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../landing/multi-cloud.md)。

請依照下列步驟，瞭解如何在Amazon Web Services (AWS)上為Experience Platform設定[!DNL Salesforce]帳戶。

### 先決條件

若要將您的[!DNL Salesforce]帳戶連線至AWS地區的Experience Platform，您必須具備下列條件：

- 具有API存取許可權的[!DNL Salesforce]帳戶。
- [!DNL Salesforce Connected App]可供您用來啟用JWT_BEARER OAuth流程。
- [!DNL Salesforce]中存取資料的必要許可權。

### AWS上連線的IP位址允許清單

您必須先將地區特定的IP位址新增至允許清單，才能將您的來源連線到AWS上的Experience Platform。 如需詳細資訊，請參閱[允許清單IP位址以連線至AWS](../../ip-address-allow-list.md)上的Experience Platform的指南。

### 建立[!DNL Salesforce Connected App]

首先，使用以下專案來建立PEM檔案的憑證/金鑰組。

```shell
openssl req -newkey rsa:4096 -new -nodes -x509 -days 3650 -keyout key.pem -out cert.pem  
```

1. 在[!DNL Salesforce]儀表板中，選取設定(![設定圖示。](/help/images/icons/settings.png))，然後選取&#x200B;**[!DNL Setup]**。
2. 導覽至[!DNL App Manager]，然後選取&#x200B;**[!DNL New Connection App]**。
3. 為您的應用程式命名，並允許自動填寫其餘欄位。
4. 為[!DNL Enable OAuth Settings]啟用此方塊。
5. 設定回呼URL。 由於這不會用於JWT，因此您可以使用`https://localhost`。
6. 為[!DNL Use Digital Signatures]啟用此方塊。
7. 上傳先前建立的cert.pem檔案。

#### 新增必要許可權

新增下列許可權：

1. 透過API (API)管理使用者資料
2. 存取自訂許可權(custom_permissions)
3. 存取身分URL服務（識別碼、設定檔、電子郵件、地址、電話）
4. 存取唯一識別碼(openid)
5. 隨時執行請求(refresh_token、offline_access)

在新增您的許可權後，請確定您已啟用&#x200B;**[!DNL Issue JSON Web Token (JWT)-based access tokens for named user]**&#x200B;的方塊。

接著，選取&#x200B;**[!DNL Save]**、**[!DNL Continue]**，然後選取&#x200B;**[!DNL Manage Customer Details]**。 使用消費者詳細資訊面板來擷取下列內容：

- **消費者金鑰**：您稍後在向Experience Platform驗證[!DNL Salesforce]帳戶時，會使用此消費者金鑰作為使用者端ID。
- **消費者機密**：您稍後在向Experience Platform驗證[!DNL Salesforce]帳戶時，會使用此消費者機密作為使用者端ID。

### 授權您的[!DNL Salesforce]使用者使用連線應用程式

請依照下列步驟，取得使用連線應用程式的授權：

1. 瀏覽至&#x200B;**[!DNL Manage Connected Apps]**。
2. 選擇「**[!DNL Edit]**」。
3. 將&#x200B;**[!DNL Permitted Users]**&#x200B;設定為&#x200B;**[!DNL Admin approved users are pre-authorized]**，然後選取&#x200B;**[!DNL Save]**。
4. 導覽至&#x200B;**[!DNL Settings]> [!DNL Manage Users] >[!DNL Profiles]**。
5. 編輯與使用者相關聯的設定檔。
6. 導覽至&#x200B;**[!DNL Connected App Access]**，然後選取您在先前步驟中建立的應用程式。

### 產生JWT持有人權杖

請依照下列步驟產生您的JWT持有人權杖。

#### 將索引鍵配對轉換為pkcs12

若要產生JWT持有人權杖，您必須先使用以下命令將您的憑證/金鑰組轉換為pkcs12格式。 在此步驟中，您還必須在系統提示時&#x200B;**設定匯出密碼**。

```shell
openssl pkcs12 -export -in cert.pem -inkey key.pem -name jwtcert >jwtcert.p12
```

#### 根據pkcs12建立Java金鑰存放區

接下來，使用以下命令，根據您剛產生的pkcs12建立Java金鑰儲存區。 在此步驟中，當出現提示時，您也必須設定&#x200B;**目的地金鑰存放區密碼**。 此外，您必須提供先前的匯出密碼作為來源金鑰存放區密碼。

```shell
keytool -importkeystore -srckeystore jwtcert.p12 -destkeystore keystore.jks -srcstoretype pkcs12 -alias jwtcert
```

#### 確認您的keystroke.jks包含jwtcert別名

接下來，使用下列命令確認您的`keystroke.jks`包含`jwtcert`別名。 在此步驟中，系統會提示您提供上一步驟中產生的目的地金鑰存放區密碼。

```shell
keytool -keystore keystore.jks -list
```

#### 產生已簽署的權杖

最後，使用下列java類別JWTExample產生您的簽署權杖。

```java
package org.example;
 
import org.apache.commons.codec.binary.Base64;
 
import java.io.*;
import java.security.*;
import java.text.MessageFormat;
 
public class Main {
 
    public static void main(String[] args) {
 
        String header = "{\"alg\":\"RS256\"}";
        String claimTemplate = "'{'\"iss\": \"{0}\", \"sub\": \"{1}\", \"aud\": \"{2}\", \"exp\": \"{3}\"'}'";
 
        try {
            StringBuffer token = new StringBuffer();
 
            //Encode the JWT Header and add it to our string to sign
            token.append(Base64.encodeBase64URLSafeString(header.getBytes("UTF-8")));
 
            //Separate with a period
            token.append(".");
 
            //Create the JWT Claims Object
            String[] claimArray = new String[5];
            claimArray[0] = "{CLIENT_ID}";
            claimArray[1] = "{AUTHORIZED_SALESFORCE_USERNAME}";
            claimArray[2] = "{SALESFORCE_LOGIN_URL}";
            claimArray[3] = Long.toString((System.currentTimeMillis() / 1000) + 2629746*4);
            MessageFormat claims;
            claims = new MessageFormat(claimTemplate);
            String payload = claims.format(claimArray);
 
            //Add the encoded claims object
            token.append(Base64.encodeBase64URLSafeString(payload.getBytes("UTF-8")));
 
            //Load the private key from a keystore
            KeyStore keystore = KeyStore.getInstance("JKS");
            keystore.load(new FileInputStream("path/to/keystore"), "keystorepassword".toCharArray());
            PrivateKey privateKey = (PrivateKey) keystore.getKey("jwtcert", "privatekeypassword".toCharArray());
 
            //Sign the JWT Header + "." + JWT Claims Object
            Signature signature = Signature.getInstance("SHA256withRSA");
            signature.initSign(privateKey);
            signature.update(token.toString().getBytes("UTF-8"));
            String signedPayload = Base64.encodeBase64URLSafeString(signature.sign());
 
            //Separate with a period
            token.append(".");
 
            //Add the encoded signature
            token.append(signedPayload);
 
            System.out.println(token.toString());
 
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

| 屬性 | 設定 |
| --- | --- |
| `claimArray[0]` | 以您的使用者端識別碼更新`claimArray[0]`。 |
| `claimArray[1]` | 以針對應用程式授權的[!DNL Salesforce]使用者名稱更新`claimArray[1]`。 |
| `claimArray[2]` | 以您的[!DNL Salesforce]登入URL更新`claimArray[2]`。 |
| `claimArray[3]` | 以自epoch時間以來的毫秒格式來更新到期日期的`claimArray[3]`。 例如，`3660624000000`是12-31-2085。 |
| `/path/to/keystore` | 將`/path/to/keystore`取代為您keystore.jks的正確路徑 |
| `keystorepassword` | 將`keystorepassword`取代為您的目的地金鑰存放區密碼。 |
| `privatekeypassword` | 以您的來源金鑰存放區密碼取代`privatekeypassword`。 |

## 後續步驟

完成[!DNL Salesforce]帳戶的先決條件設定後，您就可以繼續將您的[!DNL Salesforce]帳戶連線至Experience Platform並內嵌您的CRM資料。 如需詳細資訊，請閱讀以下檔案：

### 使用API連線[!DNL Salesforce]至Experience Platform

以下檔案提供如何使用API或使用者介面將[!DNL Salesforce]連線至Experience Platform的資訊：

- [使用流量服務API連線Salesforce至Experience Platform](../../tutorials/api/create/crm/salesforce.md)
- [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流程服務API為CRM來源建立資料流](../../tutorials/api/collect/crm.md)

### 使用UI連線[!DNL Salesforce]至Experience Platform

- [在UI中建立Salesforce來源連線](../../tutorials/ui/create/crm/salesforce.md)
- [在UI中為CRM連線建立資料流](../../tutorials/ui/dataflow/crm.md)