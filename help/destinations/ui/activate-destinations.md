---
keywords: 啟動目的地；啟動目的地；啟動資料
title: 將設定檔和區段啟用至目的地
type: Tutorial
seo-title: 將設定檔和區段啟用至目的地
description: 將區段對應至目的地，以啟動您在Adobe Experience Platform中的資料。 若要完成此操作，請遵循下列步驟。
seo-description: 將區段對應至目的地，以啟動您在Adobe Experience Platform中的資料。 若要完成此操作，請遵循下列步驟。
exl-id: c3792046-ffa8-4851-918f-98ced8b8a835
source-git-commit: a670823139eab37d319e834de5e3025d44e9c9b4
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 將設定檔和區段啟用至目的地

## 總覽 {#overview}

將區段對應至目的地，以啟動您在[!DNL Adobe Experience Platform]中擁有的資料。 若要完成此操作，請遵循下列步驟。

## 先決條件 {#prerequisites}

若要將資料激活到目標，必須已成功[連接目標](./connect-destination.md)。 如果尚未這麼做，請前往[目的地目錄](../catalog/overview.md)，瀏覽支援的目的地，並設定一或多個目的地。

## 啟動資料 {#activate-data}

啟動工作流程中的步驟因目的地類型而異。 所有目標類型的完整工作流程概述如下。

## 選擇要激活資料的目標 {#select-destination}

適用於：所有目的地

在Adobe Experience Platform使用者介面中，導覽至&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Browse]**，然後按一下與您要啟用區段之目的地對應的&#x200B;**[!UICONTROL Activate]**&#x200B;按鈕，如下圖所示。

![啟用至目的地](../assets/ui/activate-destinations/browse-tab-activate.png)

請依照下一節中的步驟，選取您要啟用的區段。

## [!UICONTROL 選取] 區段步驟 {#select-segments}

適用於：所有目的地

![選取區段步驟](../assets/ui/activate-destinations/select-segments-icon.png)

在&#x200B;**[!UICONTROL 啟動目標]**&#x200B;工作流程中，在&#x200B;**[!UICONTROL 選取區段]**&#x200B;頁面上，選取一或多個要啟動至目標的區段。 選擇&#x200B;**[!UICONTROL Next]**&#x200B;以繼續執行下一步。

![區段至目的地](../assets/ui/activate-destinations/email-select-segments.png)

##  對應步驟 {#mapping}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="套用轉換"
>abstract="使用未雜湊的來源欄位時，請核取此選項，讓Adobe Experience Platform在啟動時自動雜湊這些欄位。"

適用於：社交目的地和Google Customer Match廣告目的地

![身分對應步驟](../assets/ui/activate-destinations/identity-mapping-icon.png)

對於社交目的地，您必須選取來源屬性或身分識別命名空間，以對應為目的地中的目標身分識別。

## 範例：在[!DNL Facebook Custom Audience]中啟用受眾資料 {#example-facebook}

以下是在[!DNL Facebook]中啟用受眾資料時正確身分對應的範例。

選擇源欄位：

* 如果您使用的電子郵件地址未雜湊，請選取`Email`命名空間作為來源身分。
* 如果您根據[!DNL Facebook] [電子郵件雜湊要求](../catalog/social/facebook.md#email-hashing-requirements)將客戶電子郵件地址雜湊到[!DNL Platform]中，請選取`Email_LC_SHA256`命名空間作為來源身分。
* 如果您的資料包含非雜湊電話號碼，請選取`PHONE_E.164`命名空間作為來源身分。 [!DNL Platform] 會雜湊電話號碼以符合 [!DNL Facebook] 要求。
* 如果您根據[!DNL Facebook] [電話號碼雜湊要求](../catalog/social/facebook.md#phone-number-hashing-requirements)將資料擷取時的電話號碼雜湊至[!DNL Platform]，請選取`Phone_SHA256`命名空間作為來源身分。
* 如果您的資料包含[!DNL Apple]裝置ID，請選取`IDFA`命名空間作為來源識別。
* 如果您的資料包含[!DNL Android]裝置ID，請選取`GAID`命名空間作為來源識別。
* 如果您的資料包含其他類型的識別碼，請選取`Custom`命名空間作為來源識別碼。

選擇目標欄位：

* 當來源命名空間為`Email`或`Email_LC_SHA256`時，請選取`Email_LC_SHA256`命名空間作為目標身分。
* 當來源命名空間為`PHONE_E.164`或`Phone_SHA256`時，請選取`Phone_SHA256`命名空間作為目標身分。
* 當來源命名空間為`IDFA`或`GAID`時，請選取`IDFA`或`GAID`命名空間作為目標身分識別。
* 如果源命名空間是自定義命名空間，請選擇`Extern_ID`命名空間作為目標標識。

![身分對應](../assets/ui/activate-destinations/identity-mapping.png)

啟動後，[!DNL Platform]會自動雜湊來自未雜湊命名空間的資料。

屬性來源資料不會自動雜湊。 當源欄位包含未雜湊屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Platform]在啟動時自動雜湊資料。
![身分對應轉換](../assets/ui/activate-destinations/identity-mapping-transformation.png)

 

## 範例：在[!DNL Google Customer Match]中啟用受眾資料 {#example-gcm}

以下是在[!DNL Google Customer Match]中啟用受眾資料時正確身分對應的範例。

選擇源欄位：

* 如果您使用的電子郵件地址未雜湊，請選取`Email`命名空間作為來源身分。
* 如果您根據[!DNL Google Customer Match] [電子郵件雜湊要求](../catalog/social/../advertising/google-customer-match.md)將客戶電子郵件地址雜湊到[!DNL Platform]中，請選取`Email_LC_SHA256`命名空間作為來源身分。
* 如果您的資料包含非雜湊電話號碼，請選取`PHONE_E.164`命名空間作為來源身分。 [!DNL Platform] 會雜湊電話號碼以符合 [!DNL Google Customer Match] 要求。
* 如果您根據[!DNL Facebook] [電話號碼雜湊要求](../catalog/social/../advertising/google-customer-match.md)將資料擷取時的電話號碼雜湊至[!DNL Platform]，請選取`Phone_SHA256_E.164`命名空間作為來源身分。
* 如果您的資料包含[!DNL Apple]裝置ID，請選取`IDFA`命名空間作為來源識別。
* 如果您的資料包含[!DNL Android]裝置ID，請選取`GAID`命名空間作為來源識別。
* 如果您的資料包含其他類型的識別碼，請選取`Custom`命名空間作為來源識別碼。

選擇目標欄位：

* 當來源命名空間為`Email`或`Email_LC_SHA256`時，請選取`Email_LC_SHA256`命名空間作為目標身分。
* 當來源命名空間為`PHONE_E.164`或`Phone_SHA256_E.164`時，請選取`Phone_SHA256_E.164`命名空間作為目標身分。
* 當來源命名空間為`IDFA`或`GAID`時，請選取`IDFA`或`GAID`命名空間作為目標身分識別。
* 如果源命名空間是自定義命名空間，請選擇`User_ID`命名空間作為目標標識。

![身分對應](../assets/ui/activate-destinations/identity-mapping-gcm.png)

啟動後，[!DNL Platform]會自動雜湊來自未雜湊命名空間的資料。

屬性來源資料不會自動雜湊。 當源欄位包含未雜湊屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Platform]在啟動時自動雜湊資料。
![身分對應轉換](../assets/ui/activate-destinations/identity-mapping-gcm-transformation.png)

## **** 排程步驟 {#scheduling}

適用於：電子郵件行銷目的地和雲端儲存空間目的地

![排程步驟](../assets/ui/activate-destinations/scheduling-icon.png)

[!DNL Adobe Experience Platform] 以檔案形式匯出電子郵件行銷和雲端儲存目的地的 [!DNL CSV] 資料。在&#x200B;**[!UICONTROL 排程]**&#x200B;步驟中，您可以設定要匯出之每個區段的排程和檔案名稱。 必須設定排程，但設定檔案名稱為選用。

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] 會自動分割每個檔案500萬筆記錄（列）的匯出檔案。每一列代表一個設定檔。
>
>拆分檔案名後附加一個數字，表示該檔案是較大導出的一部分，例如：`filename.csv`、`filename_2.csv`、`filename_3.csv`。

選取與您要傳送至目的地之區段對應的&#x200B;**[!UICONTROL 建立排程]**&#x200B;按鈕。

![建立計畫按鈕](../assets/ui/activate-destinations/create-schedule-button.png)

### 導出完整檔案 {#export-full-files}

選擇&#x200B;**[!UICONTROL 導出完整檔案]**&#x200B;以使導出的檔案包含所有符合該段資格的配置檔案的完整快照。

![導出完整檔案](../assets/ui/activate-destinations/export-full-files.png)

1. 使用&#x200B;**[!UICONTROL Frequency]**&#x200B;選擇器在一次性(**[!UICONTROL Once]**)或&#x200B;**[!UICONTROL Daily]**&#x200B;匯出之間進行選擇。 匯出完整檔案&#x200B;**[!UICONTROL Daily]**&#x200B;會每天從開始日期到結束日期的12:00 AM UTC（東部標準時間晚上7:00）匯出檔案。
2. 使用&#x200B;**[!UICONTROL Time]**&#x200B;選擇器，選擇應在何時進行導出的[!DNL UTC]格式。 匯出檔案&#x200B;**[!UICONTROL Daily]**&#x200B;會每天將檔案從開始日期匯出到您選取的結束日期。

   >[!IMPORTANT]
   >
   >在特定時間匯出檔案的選項目前為測試版，僅適用於特定數量的客戶。
   ><br> <br> 由於內部Experience Platform程式的設定方式，第一個增量或完整檔案匯出可能不包含所有必要的回填資料。  <br> <br> 為確保完整檔案和增量檔案都能匯出完整且最新的回填資料，建議您在次日中午12點(GMT)後設定第一次檔案匯出時間。這是將在未來版本中解決的限制。

3. 使用&#x200B;**[!UICONTROL Date]**&#x200B;選取器來選擇應進行匯出的日期或間隔。
4. 選擇&#x200B;**[!UICONTROL 建立]**&#x200B;以保存計畫。


### 導出增量檔案 {#export-incremental-files}

選擇「**[!UICONTROL 導出增量檔案]**」，使導出的檔案僅包含自上次導出後符合該段資格的配置檔案。

>[!IMPORTANT]
>
>第一個匯出的增量檔案包含所有符合區段資格的設定檔，可作為回填。

![導出增量檔案](../assets/ui/activate-destinations/export-incremental-files.png)

1. 使用&#x200B;**[!UICONTROL Frequency]**&#x200B;選擇器，在&#x200B;**[!UICONTROL Daily]**&#x200B;或&#x200B;**[!UICONTROL Hourly]**&#x200B;匯出之間進行選擇。 導出增量檔案&#x200B;**[!UICONTROL Daily]**&#x200B;每天從開始日期到結束日期（UTC時）12:00 PM（EST時間7:00 AM）導出檔案。
   * 選擇&#x200B;**[!UICONTROL 每小時]**&#x200B;時，使用&#x200B;**[!UICONTROL Every]**&#x200B;選擇器在&#x200B;**[!UICONTROL 3]**、**[!UICONTROL 6]**、**[!UICONTROL 8]**&#x200B;和&#x200B;**[!UICONTROL 12]**&#x200B;小時選項之間進行選擇。

      >[!IMPORTANT]
      >
      >每3、6、8或12小時導出增量檔案的選項當前處於測試狀態，並且僅對特定數量的客戶可用。 非測試版客戶每天可匯出一次增量檔案。

2. 使用&#x200B;**[!UICONTROL Time]**&#x200B;選擇器，選擇應在何時進行導出的[!DNL UTC]格式。

   >[!IMPORTANT]
   >
   >為匯出選取一天中時間的選項，僅適用於選取數量的客戶。<br> <br> 由於內部Experience Platform程式的設定方式，第一個增量或完整檔案匯出可能不包含所有必要的回填資料。  <br> <br> 為確保完整檔案和增量檔案都能匯出完整且最新的回填資料，建議您在次日中午12點(GMT)後設定第一次檔案匯出時間。這是將在未來版本中解決的限制。

3. 使用&#x200B;**[!UICONTROL Date]**&#x200B;選取器來選擇應進行匯出的日期或間隔。
4. 選擇&#x200B;**[!UICONTROL 建立]**&#x200B;以保存計畫。

### 配置檔案名 {#file-names}

預設檔案名稱包含目的地名稱、區段ID以及日期和時間指標。 例如，您可以編輯匯出的檔案名稱以區分不同的促銷活動，或將資料匯出時間附加至檔案。

選取鉛筆圖示以開啟強制回應視窗並編輯檔案名稱。 檔案名限制為255個字元。

![配置檔案名](../assets/ui/activate-destinations/configure-name.png)

在檔案名稱編輯器中，可以選取不同的元件以新增至檔案名稱。

![編輯檔案名選項](../assets/ui/activate-destinations/activate-workflow-configure-step-2.png)

無法從檔案名稱中移除目的地名稱和區段ID。 除了這些外，您還可以新增下列項目：

* **[!UICONTROL 區段名稱]**:您可以將區段名稱附加至檔案名稱。
* **[!UICONTROL 日期和時間]**:在添加格 `MMDDYYYY_HHMMSS` 式或生成檔案時的Unix 10位時間戳之間進行選擇。如果希望檔案在每次增量導出時都生成動態檔案名，請選擇以下選項之一。
* **[!UICONTROL 自訂文字]**:將自訂文字新增至檔案名稱。

選擇&#x200B;**[!UICONTROL 應用更改]**&#x200B;以確認您的選擇。

>[!IMPORTANT]
> 
>如果未選擇&#x200B;**[!UICONTROL 日期和時間]**&#x200B;元件，則檔案名將為靜態，新導出的檔案將用每次導出覆蓋儲存位置中的上一個檔案。 將循環匯入工作從儲存位置執行至電子郵件行銷平台時，建議使用此選項。

完成所有區段的設定後，請選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

## **[!UICONTROL 區段排]** 程 {#segment-schedule}

適用於：廣告目的地，社交目的地

![區段排程步驟](../assets/ui/activate-destinations/segment-schedule-icon.png)

在&#x200B;**[!UICONTROL 區段排程]**&#x200B;頁面上，您可以設定傳送資料至目的地的開始日期以及傳送資料至目的地的頻率。

>[!IMPORTANT]
>
>針對社交目的地，您必須在此步驟中選取對象的來源。 您必須先在下圖中選取其中一個選項，才能繼續下一步。

![Facebook受眾來源](../assets/catalog/social/facebook/facebook-origin-audience.png)

>[!IMPORTANT]
>
>針對Google Customer Match，在啟動[!DNL IDFA]或[!DNL GAID]區段時，您必須在此步驟中提供[!UICONTROL 應用程式ID]。

![輸入應用程式id](../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

## **[!UICONTROL 選擇屬]** 性步驟 {#select-attributes}

適用於：電子郵件行銷目的地和雲端儲存目的地

![選擇屬性步驟](../assets/ui/activate-destinations/select-attributes-icon.png)

在&#x200B;**[!UICONTROL 選擇屬性]**&#x200B;頁上，選擇&#x200B;**[!UICONTROL 添加新欄位]**&#x200B;並選擇要發送到目標的屬性。

>[!NOTE]
>
> Adobe Experience Platform會從您的架構中，使用四個建議且常用的屬性來填入您的選取項目：`person.name.firstName`、`person.name.lastName`、`personalEmail.address`、`segmentMembership.status`。

檔案導出將以下方式有所不同，具體取決於是否選擇了`segmentMembership.status`:
* 如果選擇了`segmentMembership.status`欄位，則導出的檔案包括初始完整快照中的&#x200B;**[!UICONTROL 活動]**&#x200B;成員，以及後續增量導出中的&#x200B;**[!UICONTROL 活動]**&#x200B;和&#x200B;**[!UICONTROL 過期]**&#x200B;成員。
* 如果未選擇`segmentMembership.status`欄位，則導出的檔案在初始完整快照和後續增量導出中僅包含&#x200B;**[!UICONTROL 活動]**&#x200B;成員。

![建議的屬性](../assets/ui/activate-destinations/mandatory-deduplication.png)

### 強制屬性 {#mandatory-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_mandatorykey"
>title="關於必要屬性"
>abstract="選取所有匯出的設定檔都應包含的XDM結構屬性。 不含強制鍵的設定檔不會匯出至目的地。 不選取強制索引鍵會匯出所有符合資格的設定檔（無論其屬性為何）。"
>additional-url="http://www.adobe.com/go/destinations-mandatory-attributes-en" text="進一步了解檔案"

您可以將屬性標示為必填，以確保[!DNL Platform]僅匯出包含特定屬性的設定檔。 因此，它可作為額外的篩選形式使用。 將屬性標示為必要屬性是&#x200B;**不需要**。

不選擇強制屬性會匯出所有符合資格的設定檔（無論其屬性為何）。

建議您將結構中的一個屬性設為[唯一識別碼](../../destinations/catalog/email-marketing/overview.md#identity)。 如需強制屬性的詳細資訊，請參閱[電子郵件行銷目的地](../../destinations/catalog/email-marketing/overview.md#identity)檔案中的身分區段。

### 重複資料刪除密鑰 {#deduplication-keys}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_deduplicationkey"
>title="關於重複資料刪除金鑰"
>abstract="選取重複資料刪除金鑰，即可在匯出檔案中消除相同設定檔的多個記錄。 選取單一命名空間或最多兩個XDM架構屬性作為重複資料刪除索引鍵。 未選取重複資料刪除金鑰可能會導致匯出檔案中出現重複的設定檔項目。"
>additional-url="http://www.adobe.com/go/destinations-deduplication-keys-en" text="進一步了解檔案"

>[!IMPORTANT]
>
>使用重複資料刪除金鑰的選項目前處於測試階段，僅適用於特定數量的客戶。

重複資料刪除索引鍵消除了在一個匯出檔案中有多個相同設定檔記錄的可能性。

在[!DNL Platform]中，有三種使用重複資料刪除密鑰的方式：

* 使用單一身分命名空間作為[!UICONTROL 重複資料刪除索引鍵]
* 從[!DNL XDM]設定檔使用單一設定檔屬性作為[!UICONTROL 重複資料刪除索引鍵]
* 使用[!DNL XDM]配置檔案中兩個配置檔案屬性的組合作為複合鍵

>[!IMPORTANT]
>
> 您可以將單一身分命名空間匯出至目的地，命名空間會自動設為重複資料刪除索引鍵。 不支援將多個命名空間傳送至目的地。
> 
> 您無法使用身分命名空間和設定檔屬性的組合作為重複資料刪除索引鍵。

### 重複資料刪除範例 {#deduplication-example}

此示例說明重複資料消除的工作方式，具體取決於所選的重複資料消除密鑰。

讓我們考慮下列兩個設定檔。

**設定檔A**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "existing",
        "lastQualificationTime": "2021-03-10 10:03:08"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "Doe",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

**設定檔B**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "existing",
        "lastQualificationTime": "2021-04-10 11:33:28"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "D",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

### 重複資料刪除使用案例1:無重複資料消除

若不使用重複資料刪除，匯出檔案將包含下列項目。

| personalEmail | firstName | lastName |
|---|---|---|
| johndoe@example.com | 約翰 | Doe |
| johndoe@example.com | 約翰 | D |


### 重複資料刪除使用案例2:基於身份命名空間的重複資料消除

假設使用[!DNL Email]命名空間執行重複資料刪除，則匯出檔案將包含下列項目。 設定檔B是符合區段資格的最新一個，因此是唯一一個匯出的設定檔。

| 電子郵件* | personalEmail | firstName | lastName |
|---|---|---|---|
| johndoe_1@example.com | johndoe@example.com | 約翰 | D |
| johndoe_2@example.com | johndoe@example.com | 約翰 | D |

### 重複資料刪除使用案例3:基於單一設定檔屬性的重複資料刪除

假設使用`personal Email`屬性重複資料刪除，則匯出檔案將包含下列項目。 設定檔B是符合區段資格的最新一個，因此是唯一一個匯出的設定檔。

| personalEmail* | firstName | lastName |
|---|---|---|
| johndoe@example.com | 約翰 | D |


### 重複資料刪除使用案例4:基於兩個配置檔案屬性的重複資料消除（複合重複資料消除密鑰）

假設複合鍵`personalEmail + lastName`重複資料刪除，則導出檔案將包含以下項。

| personalEmail* | lastName* | firstName |
|---|---|---|
| johndoe@example.com | D | 約翰 |
| johndoe@example.com | Doe | 約翰 |


Adobe建議選取身分命名空間（例如[!DNL CRM ID]或電子郵件地址）作為重複資料刪除金鑰，以確保所有設定檔記錄都經過唯一識別。

>[!NOTE]
> 
>如果資料集（而非整個資料集）中的某些欄位已套用任何資料使用標籤，則在啟用時，會在下列條件下強制執行這些欄位層級標籤：
>
>* 欄位會用於區段定義中。
>* 欄位會設定為目標目的地的預計屬性。

>
> 
例如，如果欄位`person.name.firstName`具有與目的地的行銷動作相衝突的特定資料使用標籤，則在審核步驟中將顯示資料使用策略違規。 如需詳細資訊，請參閱Adobe Experience Platform中的[資料控管](../../rtcdp/privacy/data-governance-overview.md#destinations)。

## **** 檢視步驟 {#review}

適用於：所有目的地

![檢閱步驟](../assets/ui/activate-destinations/review-icon.png)

在&#x200B;**[!UICONTROL 檢閱]**&#x200B;頁面上，您會看到您所選項目的摘要。 選擇&#x200B;**[!UICONTROL 取消]**&#x200B;以分解流，選擇&#x200B;**[!UICONTROL 返回]**&#x200B;以修改設定，或選擇&#x200B;**[!UICONTROL 完成]**&#x200B;以確認您的選擇並開始向目標發送資料。

>[!IMPORTANT]
>
>在此步驟中，Adobe Experience Platform會檢查資料使用政策是否違反。 以下顯示違反原則的範例。 除非您解決違規，否則無法完成區段啟用工作流程。 有關如何解決策略違規的資訊，請參閱資料控管文檔部分中的[策略實施](../../rtcdp/privacy/data-governance-overview.md#enforcement)。

![資料策略違規](../assets/common/data-policy-violation.png)

如果未檢測到任何違反策略的情況，請選擇&#x200B;**[!UICONTROL 完成]**&#x200B;以確認您的選擇並開始向目標發送資料。

![確認選取](../assets/ui/activate-destinations/confirm-selection.png)

## 確認區段啟動成功 {#verify-activation}

### 電子郵件行銷目的地和雲端儲存空間目的地 {#esp-and-cloud-storage}

對於電子郵件行銷目的地和雲端儲存空間目的地，Adobe Experience Platform會在您提供的儲存位置中建立以定位點分隔的`.csv`檔案。 預期每天會在儲存位置中建立新檔案。 預設檔案格式為：
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

您連續三天收到的檔案可能如下所示：

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

儲存位置中是否存在這些檔案是成功激活的確認。 若要了解匯出的檔案的結構，您可以[下載範例.csv檔案](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv)。 此範例檔案包含設定檔屬性`person.firstname`、`person.lastname`、`person.gender`、`person.birthyear`和`personalEmail.address`。

## 廣告目的地

檢查您要啟用資料的個別廣告目的地的帳戶。 如果啟動成功，則廣告平台會填入對象。

## 社交目的地

對於[!DNL Facebook]，成功的啟動表示將以程式設計方式在[[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/)中建立[!DNL Facebook]自訂對象。 當使用者符合已啟動區段的資格或取消資格時，會新增及移除對象中的區段成員資格。

>[!TIP]
>
>Adobe Experience Platform與[!DNL Facebook]之間的整合支援歷史受眾回填。 當您將區段啟用至目的地時，所有歷史區段資格都會傳送至[!DNL Facebook]。

## 停用啟用 {#disable-activation}

若要停用現有的啟動流程，請遵循下列步驟：

1. 在左側導航欄中選擇&#x200B;**[!UICONTROL 目標]**，然後按一下&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤，然後按一下目標名稱。
2. 按一下右側邊欄中的&#x200B;**[!UICONTROL 啟用]**&#x200B;控制項，以變更啟動流程狀態。
3. 在&#x200B;**更新資料流狀態**&#x200B;窗口中，選擇&#x200B;**確認**&#x200B;以禁用激活流。
