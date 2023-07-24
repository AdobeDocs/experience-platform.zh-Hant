---
title: 在使用者介面中建立SAP Commerce來源連線
description: 瞭解如何使用Adobe Experience Platform UI建立SAP Commerce來源連線。
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 99edb8b2bcd4225235038e966a367d91375c961a
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 1%

---

# 建立 [!DNL SAP Commerce] ui中的來源連線

>[!NOTE]
>
>此 [!DNL SAP Commerce] 來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

下列教學課程將逐步引導您完成建立 [!DNL SAP Commerce] 要帶來的來源連線 [[!DNL SAP] 訂閱帳單](https://www.sap.com/products/financial-management/subscription-billing.html) 使用Adobe Experience Platform使用者介面的聯絡人和客戶資料。

## 快速入門 {#getting-started}

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有有效的 [!DNL SAP Commerce] 帳戶，您可以略過本檔案的其餘部分，並前往上的教學課程 [設定資料流](../../dataflow/ecommerce.md).

### 收集必要的認證 {#gather-credentials}

為了連線 [!DNL SAP Commerce] 若要Experience Platform，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| --- | --- |
| 使用者端ID | 的值 `clientId` 服務金鑰。 |
| 使用者端密碼 | 的值 `clientSecret` 服務金鑰。 |
| 權杖端點 | 的值 `url` 從服務金鑰，它將類似於 `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| 地區 | 您的資料中心位置。 區域出現在 `url` 且其值類似於 `eu10` 或 `us10`. 例如，如果 `url` 是 `https://eu10.revenue.cloud.sap/api` 您將需要 `eu10`. |

如需詳細資訊，請參閱 [[!DNL SAP Commerce] 檔案](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/c5fcaf96daff4c7a8520188e4d8a1843.html).

### 建立Platform結構描述 {#create-platform-schema}

建立之前 [!DNL SAP Commerce] 來源連線，您也必須確保先建立Experience Platform結構描述以用於您的來源。 請參閱教學課程，位置如下： [建立平台結構描述](../../../../../xdm/schema/composition.md) 有關如何建立方案的完整步驟。

展開下列區段以檢視結構描述範例。

+++ 檢視結構描述範例

```
{
  "_extconndev": {
    "addresses": [
      {
        "addressUUID": "{ADDRESS_UUID}",
        "city": "Burnaby",
        "country": "Canada",
        "email": "chandni@acme.com",
        "houseNumber": "27",
        "isDefault": false,
        "phone": "123-456-7890",
        "postalCode": "V3J 1X9",
        "state": "British Columbia",
        "street": "Beresford"
      }
    ],
    "changedAt": "1687204041",
    "changedBy": "vero@acme.com",
    "contactNumber": "123-456-7980",
    "corporateInfo": {
      "company": "acme"
    },
    "createAt": "1687204041",
    "createdBy": "vero@acme.com",
    "customReferences": [
      {
        "id": "Sample value",
        "typeCode": "Sample value"
      }
    ],
    "customerNumber": "Sample value",
    "customerType": "Sample value",
    "defaultAddress": {
      "addressUUID": "Sample value",
      "city": "North Vancouver",
      "country": "Canada",
      "email": "chandni@acme.come",
      "houseNumber": "34",
      "isDefault": false,
      "phone": "123-456-7890",
      "postalCode": "V7H 2P1",
      "state": "British Columbia",
      "street": "Maple"
    },
    "externalObjectReferences": [
      {
        "externalId": "{EXTERNAL_ID}",
        "externalIdTypeCode": "{EXTERNAL_ID_TYPE_CODE}",
        "externalSystemId": "{EXTERNAL_SYSTEM_ID}"
      }
    ],
    "markets": [
      {
        "active": false,
        "country": "USA",
        "currency": "USD",
        "marketId": "Sample value",
        "priceinfo": {
          "incoterms": "{INCO_TERMS}",
          "incotermsLocation": "{INCO_TERMS_LOCATION}",
          "priceGroup": "{PRICE_GROUP}",
          "priceListType": "{PRICE_LIST_TYPE}"
        },
        "salesArea": {
          "distributionChannel": "{DISTRIBUTION_CHANNEL}",
          "division": "{DIVISION}",
          "salesOrganization": "{SALES_ORGANIZATION}"
        }
      }
    ],
    "personalInfo": {
      "firstName": "Chandni",
      "lastName": "Kaur"
    }
  },
  "_id": "/uri-reference",
  "_repo": {
    "createDate": "2004-10-23T12:00:00-06:00",
    "modifyDate": "2004-10-23T12:00:00-06:00"
  },
  "createdByBatchID": "/uri-reference",
  "modifiedByBatchID": "/uri-reference",
  "personID": "{PERSON_ID}",
  "repositoryCreatedBy": "kevin@acme.com",
  "repositoryLastModifiedBy": "kevin@acme.com"
}
```

+++

## 連線您的 [!DNL SAP Commerce] 帳戶 {#connect-account}

在Platform UI中選取 **[!UICONTROL 來源]** 以存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 *電子商務* 類別，選取 **[!UICONTROL SAP商務]**，然後選取 **[!UICONTROL 新增資料]**.

![具有SAP Commerce卡片目錄的平台UI熒幕擷圖](../../../../images/tutorials/create/ecommerce/sap-commerce/catalog-card.png)

此 **[!UICONTROL 連線SAP Commerce帳戶]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶 {#existing-account}

若要使用現有帳戶，請選取 [!DNL SAP Commerce] 要用來建立新資料流的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![連線SAP Commerce帳戶與現有帳戶的Platform UI熒幕擷圖](../../../../images/tutorials/create/ecommerce/sap-commerce/existing.png)

### 新帳戶 {#new-account}

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、選擇性說明和您的認證。 完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![連線SAP Commerce帳戶與新帳戶的Platform UI熒幕擷圖](../../../../images/tutorials/create/ecommerce/sap-commerce/new.png)

### 選擇資料 {#select-data}

最後，您必須選取要擷取至Platform的物件型別。

| 物件型別 | 說明 |
| --- | --- |
| `Customers` | 擁有訂閱的實體。 |
| `Contacts` | 客戶的聯絡詳細資料。 |

>[!BEGINTABS]

>[!TAB 客戶]

若要內嵌客戶資料，請選取「 」 **[!UICONTROL 客戶]** 作為物件型別，然後選取 **[!UICONTROL 下一個]**.

![SAP Commerce平台UI熒幕擷取畫面，顯示已選取「客戶」選項的設定](../../../../images/tutorials/create/ecommerce/sap-commerce/configuration-customers.png)

>[!TAB 連絡人]

若要內嵌連絡人資料，請選取 **[!UICONTROL 連絡人]** 作為物件型別，然後選取 **[!UICONTROL 下一個]**.

![SAP Commerce平台UI熒幕擷取畫面，顯示已選取連絡人選項的設定](../../../../images/tutorials/create/ecommerce/sap-commerce/configuration-contacts.png)

>[!ENDTABS]

## 後續步驟 {#next-steps}

依照本教學課程，您已建立與的連線， [!DNL SAP Commerce] 帳戶。 您現在可以繼續下一節教學課程和 [設定資料流以將資料匯入Platform](../../dataflow/ecommerce.md).

## 其他資源 {#additional-resources}

以下各節提供其他資源，您可在使用時參照 [!DNL SAP Commerce] 來源。

### 映射 {#mapping}

Platform會根據您選取的目標結構描述或資料集，為自動對應的欄位提供智慧型建議。 您可以手動調整對應規則以符合您的使用案例。 您可以視需要選擇直接對應欄位，或使用資料準備函式來轉換來源資料，以衍生計算值或計算值。 如需使用對應程式介面和計算欄位的完整步驟，請參閱 [資料準備UI指南](../../../../../data-prep/ui/mapping.md).

資料流的對應設定會因您的結構描述和您選取要內嵌的物件型別而異。

>[!BEGINTABS]

>[!TAB 客戶]

若為客戶資料， [!DNL SAP Commerce] 使用 [客戶](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers) 和 [客戶 — 聯絡人關係](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) 的端點 [!DNL SAP Business Partners] 用於擷取資料的API

以下是對映設定的範例 [!DNL SAP Commerce] 客戶資料的資料流：

| 目標欄位 | 說明 |
| --- | --- |
| `customerNumber` | 客戶編號。 |
| `corporateInfo` | 客戶編號。 |
| `customerType` | 客戶型別。 |
| `createdAt` | 指出客戶建立時間的時間戳記。 |
| `changedAt` | 表示上次更新客戶的時間戳記。 |
| `markets[*].country` | 客戶市場，擷取為陣列物件。 |
| `addresses[*].email` | 與客戶多個地址相關聯的電子郵件，以陣列物件的形式擷取。 |
| `addresses[*].city` | 與客戶多個地址相關聯的城市，以陣列物件的形式擷取。 |
| `addresses[*].addressUUID` | 與客戶多個地址相關聯的ID，以陣列物件的形式擷取。 |
| `externalObjectReferences[*].externalSystemId` | 其他資料，擷取為陣列物件。 |
| `externalObjectReferences[*].externalId` | 其他資料，擷取為陣列物件。 |
| `customReferences[*].id` | 其他資料，擷取為陣列物件。 |
| `customReferences[*].typeCode` | 其他資料，擷取為陣列物件。 |

![來源工作流程的對應步驟。](../../../../images/tutorials/create/ecommerce/sap-commerce/mapping-customers.png)

>[!TAB 連絡人]

若為聯絡資料， [!DNL SAP Commerce] 使用 [連絡人](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts) 的端點 [!DNL SAP Business Partners] 用於擷取資料的API。

以下是對映設定的範例 [!DNL SAP Commerce] 連絡人資料的資料流：

| 目標欄位 | 說明 |
| --- | --- |
| `contactNumber` | 連絡人的號碼。 |
| `createdAt` | 表示聯絡人建立時間的時間戳記。 |
| `changedAt` | 表示上次更新連絡人的時間戳記。 |
| `personalInfo.lastName` | 連絡人的姓氏。 |
| `personalInfo.firstName` | 連絡人的名字。 |
| `externalObjectReferences[*].externalSystemId` | 其他資料，擷取為陣列物件。 |
| `externalObjectReferences[*].externalId` | 其他資料，擷取為陣列物件。 |
| `externalObjectReferences[*].externalIdTypeCode` | 其他資料，擷取為陣列物件。 |

![來源工作流程的對應步驟。](../../../../images/tutorials/create/ecommerce/sap-commerce/mapping-contacts.png)

>[!ENDTABS]

