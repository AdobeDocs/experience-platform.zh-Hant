---
title: Kevel Connection
description: 使用Kevel串流目的地，直接在Kevel的UserDB和區段管理API中啟用對象，並支援在決策時的即時鎖定目標。
source-git-commit: d820485fd81efd08d8626f8476338558c4585c20
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 3%

---


# [!DNL Kevel] 連線 {#kevel}

## 概觀 {#overview}

[[!DNL Kevel]](https://www.kevel.com/)提供啟用AI的技術和專家指引，協助創新的商務領導在零售媒體中啟動、擴展和成功。 [!DNL Kevel]的Retail Media Cloud功能可針對站上和站外廣告提供針對性、可歸因、可自訂的廣告格式。

Adobe Experience Platform的[!DNL Kevel]串流目的地可讓客戶直接在[!DNL Kevel]的UserDB和區段管理API中啟用Adobe對象，以支援在廣告決策時的即時鎖定目標。

>[!IMPORTANT]
> 
>如果您有問題或想要請求有關[!DNL Kevel]目的地或其檔案的更新，請傳送電子郵件至[!DNL Kevel]support@kevel.com[，寄給](mailto:support@kevel.com)團隊。

## 使用案例 {#use-cases}

您可以在零售媒體體驗中啟用豐富的第一方行為對象，以提供更相關的廣告和更強大的效能。 在Experience Platform中，您可以建立高價值、以意圖為基礎的受眾，例如經常光顧的類別購物者或具有最近產品興趣的使用者，並即時將這些會籍同步至[!DNL Kevel]。 [!DNL Kevel]會立即讓這些區段可用於廣告決策，在搜尋、瀏覽和應用程式體驗中啟用贊助產品和其他格式的精確目標定位。 使用者一旦符合資格，您就可以根據這些訊號採取行動，提高相關曝光數、改善鎖定目標，並改善測量和ROAS。

## 先決條件 {#prerequisites}

若要準備使用[!DNL Kevel]目的地，請確定符合下列必要條件：

- 您必須擁有使用中的&#x200B;**[!DNL Kevel]網路**&#x200B;和API存取權。
- 您需要具有許可權的&#x200B;**[!DNL Kevel]API金鑰**，才能建立區段和更新UserDB記錄。
- 您必須在Experience Platform中設定身分識別名稱空間，將對應到您的網站或應用程式在[!DNL Kevel]廣告請求期間傳送的身分識別（例如ECID、GAID、IDFA、忠誠度ID等）。
- Adobe客戶應僅對應即時廣告請求期間使用的身分，因為每個身分都會產生UserDB記錄。

## 支援的身分 {#supported-identities}

[!DNL Kevel]目的地支援啟用您的應用程式在傳送廣告要求給[!DNL Kevel]時可能使用的任何身分。 您最多可以對應三個身分識別名稱空間來產生對應的UserDB記錄。

[!DNL Kevel]支援下列Experience Platform身分識別名稱空間：

| 身分識別命名空間 | 說明 | 一般用途 |
|--------------------|---------------------------------|----------------------------------------------------------------|
| **ECID** | Experience Cloud ID | 用於網站上的個人化和跨Adobe識別。 |
| **GAID** | GOOGLE ADVERTISING ID | 用於Android應用程式/裝置流量。 |
| **IDFA** | APPLE ADVERTISING ID | 用於iOS應用程式/裝置流量（需經ATT同意）。 |
| **外部識別碼** | 外部ID （自訂識別碼） | 傳遞專有或後端產生的ID。 |

{style="table-layout:auto"}

### 支援自訂身分名稱空間

[!DNL Kevel]目的地&#x200B;**也接受自訂名稱空間** (如您的Experience Platform實作中所定義)。

這表示：

- 您可以對應&#x200B;**客戶特定的身分識別名稱空間** （例如： `loyalty_id`、`gigya_id`，或您在Identity Service中定義的任何自訂身分）。
- 這些名稱空間可指派給`kevel_user_key1`、`kevel_user_key2`或`kevel_user_key3`，方式與全域名稱空間相同。
- [!DNL Kevel]將為每個對應的識別碼&#x200B;**的每個執行個體產生**&#x200B;一個UserDB記錄，允許系統傳送的每個識別碼在廣告決定時間即時比對。

### 身分對應行為

- 您最多可以將&#x200B;**個三個**&#x200B;個Experience Platform身分識別名稱空間對應到[!DNL Kevel]的三個身分識別槽。
- 對於每個已啟用的設定檔，[!DNL Kevel]會收到每個對應識別&#x200B;**的每個執行個體一個UserDB記錄**。
- 客戶應僅將其實際傳送廣告要求的身分對應至[!DNL Kevel]，以避免不必要的UserDB儲存空間。

Kevel目的地![的](/help/destinations/assets/catalog/advertising/kevel-destination-mappings.png)對應範例

## 支援的對象 {#supported-audiences}

| 對象來源 | 支援 | 說明 |
|-----------------------|-----------|---------------------------------------------------------- |
| 細分服務 | 是 | 由細分引擎評估的Adobe設定檔對象。 |
| 自訂上傳 | 無 | 目前不支援。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

| 項目 | 類型 | 附註 |
|------|------|-------|
| 匯出類型 | **區段匯出** | 每當設定檔符合或退出對象時，[!DNL Kevel]就會收到更新。 |
| 匯出頻率 | **串流** | 更新會使用Destination SDK串流框架即時傳送。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

遵循標準Experience Platform [連線目的地](../../ui/connect-destination.md)工作流程。

>[!IMPORTANT]
> 
>您必須擁有&#x200B;**檢視目的地**&#x200B;和&#x200B;**管理目的地**&#x200B;許可權。

### 驗證目標 {#authenticate}

連線到[!DNL Kevel]時，請提供下列欄位：

- **持有人權杖** — 您的[!DNL Kevel] API金鑰。

Kevel目的地的![驗證選項](/help/destinations/assets/catalog/advertising/kevel-destination-authentication.png)

### 填寫目標詳細資料 {#destination-details}

驗證之後，請設定：

- **名稱** — 識別此目的地執行個體的標籤。
- **描述** — 描述此目的地執行個體的選擇性文字。
- **[!DNL Kevel]網路識別碼** — 您的[!DNL Kevel]網路識別碼。

Kevel目的地![的](/help/destinations/assets/catalog/advertising/kevel-destination-details.png)目的地詳細資料

## 啟用此目的地的區段 {#activate}

若要將對象傳送至[!DNL Kevel]，請遵循中的工作流程\
[啟用串流區段匯出目的地的設定檔和區段](/help/destinations/ui/activate-segment-streaming-destinations.md)。

### 停用對象 {#deactivate}

停用對象或從Experience Platform中的[!DNL Kevel]目的地移除對象時，Experience Platform會停止傳送該對象的進一步設定檔資格更新。 在[!DNL Kevel]中建立的任何現有區段仍然可用，且不會自動刪除。

如果[!DNL Kevel]區段目前正在使用中的行銷活動中使用，[!DNL Kevel]可防止刪除以避免中斷即時傳遞。 在這種情況下，在Experience Platform中停用會導致以下結果：

- Experience Platform資料流停止
- [!DNL Kevel]區段繼續存在，且可能一直附加至行銷活動，直到手動移除或更新行銷活動為止

若要完全停止[!DNL Kevel]中的目標定位，請確定已從[!DNL Kevel]的行銷活動管理系統中的任何作用中行銷活動中移除此區段。

### 對應屬性和身分 {#map}

[!DNL Kevel]需要：

- **身分識別名稱空間** — 最多有三個身分識別名稱空間對應到[!DNL Kevel]個身分識別槽。
- **區段成員資格** — 不需要手動對應；Experience Platform會自動傳遞區段成員資格識別碼和別名。

啟用期間，請選取您為[!DNL Kevel]設定的身分識別名稱空間。 每個身分都會產生自己的UserDB更新呼叫。

## 匯出的資料/驗證資料匯出 {#exported-data}

當設定檔符合或退出對象時，Experience Platform會傳送串流更新給[!DNL Kevel]。

### [!DNL Kevel] UserDB收到的範例裝載

```json
PUT /udb/{networkId}/segments?userKey=ECID-12345
{
  "segments": [1723, 3344, 9988]
}
```

| 參數 | 說明 |
|-----------|-------------|
| **userKey** | 衍生自對應的Adobe身分。 |
| **區段** | 與目前已實現設定檔之Adobe對象相對應的[!DNL Kevel]區段ID集。 |

{style="table-layout:auto"}

### 匯出期間使用的Experience Platform設定檔範例 {#sample-profile}

將對象啟用至[!DNL Kevel]目的地時，Experience Platform會將包含&#x200B;**區段資格**&#x200B;和客戶&#x200B;**對應之**&#x200B;身分的設定檔片段傳送至[!DNL Kevel]的身分槽。

以下是匯出的設定檔範例，其中顯示：

- 多個身分名稱空間對應至`kevel_user_key1`、`kevel_user_key2`和`kevel_user_key3`
- `ups`名稱空間中的單一已啟動區段

```json
{
  "segmentMembership": {
    "ups": {
      "9d161bbb-c785-474a-965b-7d7bc2adf879": {
        "status": "realized",
        "lastQualificationTime": "2025-12-10T21:43:38.541076Z"
      }
    }
  },
  "identityMap": {
    "kevel_user_key1": [
      {
        "id": "ECID-fN1zo"
      },
      {
        "id": "ECID-9Xr2p"
      }
    ],
    "kevel_user_key2": [
      {
        "id": "GAID-4oic4"
      }
    ],
    "kevel_user_key3": [
      {
        "id": "IDFA-nB5fU"
      }
    ]
  }
}
```

#### [!DNL Kevel]如何解譯此設定檔

透過[!DNL Kevel]目的地組態，每個對應的識別都會產生不同的UserDB記錄，表示[!DNL Kevel]會接收：

- `ECID-fN1zo`的一次更新
- `ECID-9Xr2p`的一次更新
- `GAID-4oic4`的一次更新
- `IDFA-nB5fU`的一次更新

這可讓您在廣告決策時，使用任何可用的身分來識別相同的人員，每個身分都有一組相同的區段會籍。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

- [[!DNL Kevel] UserDB參考](https://dev.kevel.com/reference/userdb)
- [[!DNL Kevel] 使用者區段鎖定目標](https://dev.kevel.com/docs/segment-targeting)
