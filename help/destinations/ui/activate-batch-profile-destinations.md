---
keywords: 啟用設定檔目的地；啟用目的地；啟用資料；啟用電子郵件行銷目的地；啟用雲端儲存目的地
title: 啟用受眾資料以批次設定檔匯出目的地
type: Tutorial
seo-title: Activate audience data to batch profile export destinations
description: 了解如何將區段傳送至批次設定檔式型目的地，以啟動Adobe Experience Platform中的受眾資料。
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by sending segments to batch profile-based destinations.
exl-id: 82ca9971-2685-453a-9e45-2001f0337cda
source-git-commit: b4810dfef7b0d437744ca14a32bd4f5746e8d002
workflow-type: tm+mt
source-wordcount: '1958'
ht-degree: 0%

---

# 啟用受眾資料以批次設定檔匯出目的地

## 總覽 {#overview}

本文說明在Adobe Experience Platform批次設定檔型目的地（例如雲端儲存空間和電子郵件行銷目的地）中啟用受眾資料所需的工作流程。

## 先決條件 {#prerequisites}

若要將資料啟用至目的地，您必須成功 [連接到目的地](./connect-destination.md). 如果尚未這麼做，請前往 [目的地目錄](../catalog/overview.md)，瀏覽支援的目的地，並設定您要使用的目的地。

## 選取您的目的地 {#select-destination}

1. 前往 **[!UICONTROL 連線>目的地]**，然後選取 **[!UICONTROL 目錄]** 標籤。

   ![目標目錄索引標籤](../assets/ui/activate-batch-profile-destinations/catalog-tab.png)

1. 選擇 **[!UICONTROL 啟用區段]** 在與您要啟用區段的目的地對應的卡片上，如下圖所示。

   ![「啟用區段」按鈕](../assets/ui/activate-batch-profile-destinations/activate-segments-button.png)

1. 選取您要用來啟用區段的目的地連線，然後選取 **[!UICONTROL 下一個]**.

   ![選擇目標](../assets/ui/activate-batch-profile-destinations/select-destination.png)

1. 移至下一節，以 [選取區段](#select-segments).

## 選取您的區段 {#select-segments}

使用區段名稱左側的核取方塊，選取您要啟用至目的地的區段，然後選取 **[!UICONTROL 下一個]**.

![選取區段](../assets/ui/activate-batch-profile-destinations/select-segments.png)


## 排程區段匯出 {#scheduling}

[!DNL Adobe Experience Platform] 以 [!DNL CSV] 檔案。 在 **[!UICONTROL 排程]** 頁面，您可以為要匯出的每個區段設定排程和檔案名稱。 必須設定排程，但設定檔案名稱為選用。

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] 會自動分割每個檔案500萬筆記錄（列）的匯出檔案。 每一列代表一個設定檔。
>
>拆分檔案名後附加一個數字，表示該檔案是較大導出的一部分，例如： `filename.csv`, `filename_2.csv`, `filename_3.csv`.

選取 **[!UICONTROL 建立排程]** 按鈕（與您要傳送至目的地的區段對應）。

![建立計畫按鈕](../assets/ui/activate-batch-profile-destinations/create-schedule-button.png)

### 導出完整檔案 {#export-full-files}

選擇 **[!UICONTROL 導出完整檔案]** 觸發匯出檔案，該檔案包含所選區段之所有設定檔資格的完整快照。

![導出完整檔案](../assets/ui/activate-batch-profile-destinations/export-full-files.png)

1. 使用 **[!UICONTROL 頻率]** 選取器以選取匯出頻率：

   * **[!UICONTROL 一次]**:排程一次性的隨選完整檔案匯出。
   * **[!UICONTROL 每日]**:在您指定的時間，每天排程完整檔案匯出一次。

1. 使用 **[!UICONTROL 時間]** 選取器以選擇一天中的時間，位於 [!DNL UTC] 格式，導出時間。

   >[!IMPORTANT]
   >
   >由於內部Experience Platform進程的配置方式，第一個增量或完整檔案導出可能不包含所有回填資料。 <br> <br> 為確保完整檔案和增量檔案都能匯出完整且最新的回填資料，Adobe建議在次日中午12點後設定第一次檔案匯出時間。 未來版本將會解決此限制。

1. 使用 **[!UICONTROL 日期]** 選取器，以選擇應進行匯出的日期或間隔。
   >[!TIP]
   >
   > 若是每日匯出，請設定您的開始和結束日期，以符合下游平台中促銷活動的持續時間。
1. 選擇 **[!UICONTROL 建立]** 以儲存排程。


### 導出增量檔案 {#export-incremental-files}

選擇 **[!UICONTROL 導出增量檔案]** 觸發導出，其中第一個檔案是選定段的所有配置檔案資格的完整快照，而後續檔案是自上次導出以來的增量配置檔案資格。

>[!IMPORTANT]
>
>第一個匯出的增量檔案包含所有符合區段資格的設定檔，可作為回填。

![導出增量檔案](../assets/ui/activate-batch-profile-destinations/export-incremental-files.png)

1. 使用 **[!UICONTROL 頻率]** 選取器以選取匯出頻率：

   * **[!UICONTROL 每日]**:在您指定的時間，每天計劃一次增量檔案導出。
   * **[!UICONTROL 每小時]**:計畫每3、6、8或12小時導出增量檔案。

1. 使用 **[!UICONTROL 時間]** 選取器以選擇一天中的時間，位於 [!DNL UTC] 格式，導出時間。

   >[!IMPORTANT]
   >
   >由於內部Experience Platform進程的配置方式，第一個增量或完整檔案導出可能不包含所有回填資料。 <br> <br> 為確保完整檔案和增量檔案都能匯出完整且最新的回填資料，Adobe建議在次日中午12點後設定第一次檔案匯出時間。 未來版本將會解決此限制。

1. 使用 **[!UICONTROL 日期]** 選取器，以選擇應進行匯出的日期或間隔。
   >[!TIP]
   >
   >設定您的開始和結束日期，以符合下游平台中促銷活動的持續時間。
1. 選擇 **[!UICONTROL 建立]** 以儲存排程。

### 配置檔案名 {#file-names}

預設檔案名稱包含目的地名稱、區段ID以及日期和時間指標。 例如，您可以編輯匯出的檔案名稱以區分不同的促銷活動，或將資料匯出時間附加至檔案。

選取鉛筆圖示以開啟強制回應視窗並編輯檔案名稱。 檔案名限制為255個字元。

![配置檔案名](../assets/ui/activate-batch-profile-destinations/configure-name.png)

在檔案名稱編輯器中，可以選取不同的元件以新增至檔案名稱。

![編輯檔案名選項](../assets/ui/activate-batch-profile-destinations/activate-workflow-configure-step-2.png)

無法從檔案名稱中移除目的地名稱和區段ID。 除了這些外，您還可以新增下列項目：

* **[!UICONTROL 區段名稱]**:您可以將區段名稱附加至檔案名稱。
* **[!UICONTROL 日期和時間]**:在新增 `MMDDYYYY_HHMMSS` 格式或Unix 10位數的檔案生成時間時間戳。 如果希望檔案在每次增量導出時都生成動態檔案名，請選擇以下選項之一。
* **[!UICONTROL 自訂文字]**:將自訂文字新增至檔案名稱。

選擇 **[!UICONTROL 套用變更]** 以確認您的選取。

>[!IMPORTANT]
> 
>如果您未選取 **[!UICONTROL 日期和時間]** 元件，則檔案名將為靜態，而新導出的檔案將用每次導出覆蓋儲存位置中以前的檔案。 將循環匯入工作從儲存位置執行至電子郵件行銷平台時，建議使用此選項。

完成所有區段的設定後，請選取 **[!UICONTROL 下一個]** 繼續。

## 選取設定檔屬性 {#select-attributes}

針對以設定檔為基礎的目的地，您必須選取要傳送至目標目的地的設定檔屬性。


1. 在 **[!UICONTROL 選擇屬性]** 頁面，選取 **[!UICONTROL 新增欄位]**.

   ![新增對應](../assets/ui/activate-batch-profile-destinations/add-new-field.png)

1. 選取 **[!UICONTROL 結構欄位]** 的下界。

   ![選擇源欄位](../assets/ui/activate-batch-profile-destinations/select-target-field.png)

1. 在 **[!UICONTROL 選擇欄位]** 頁，選擇要發送到目標的XDM屬性，然後選擇 **[!UICONTROL 選擇]**.

   ![「選擇源欄位」頁](../assets/ui/activate-batch-profile-destinations/target-field-page.png)

1. 要添加更多映射，請重複步驟1到3。

>[!NOTE]
>
> Adobe Experience Platform會從您的架構中，使用四個建議且常用的屬性來填入您的選取項目： `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

檔案匯出會依下列方式而異，具體取決於 `segmentMembership.status` 已選取：
* 若 `segmentMembership.status` 欄位，導出的檔案包括 **[!UICONTROL 作用中]** 初始完整快照和 **[!UICONTROL 作用中]** 和 **[!UICONTROL 過期]** 成員。
* 若 `segmentMembership.status` 欄位未選中，導出的檔案僅包括 **[!UICONTROL 作用中]** 初始完整快照和後續增量導出中的成員。

![建議的屬性](../assets/ui/activate-batch-profile-destinations/mandatory-deduplication.png)

### 強制屬性 {#mandatory-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_mandatorykey"
>title="關於必要屬性"
>abstract="選取所有匯出的設定檔都應包含的XDM結構屬性。 不含強制鍵的設定檔不會匯出至目的地。 不選取強制索引鍵會匯出所有符合資格的設定檔（無論其屬性為何）。"
>additional-url="http://www.adobe.com/go/destinations-mandatory-attributes-en" text="進一步了解檔案"

強制屬性是使用者啟用的核取方塊，可確保所有設定檔記錄都包含選取的屬性。 例如：所有匯出的設定檔都包含電子郵件地址&#x200B;。

您可以將屬性標示為必填，以確保 [!DNL Platform] 僅匯出包含特定屬性的設定檔。 因此，它可作為額外的篩選形式使用。 將屬性標示為必要屬性 **not** 必填。

不選擇強制屬性會匯出所有符合資格的設定檔（無論其屬性為何）。

建議其中一個屬性是 [唯一識別碼](../../destinations/catalog/email-marketing/overview.md#identity) 從您的架構。 如需強制屬性的詳細資訊，請參閱 [電子郵件行銷目的地](../../destinations/catalog/email-marketing/overview.md#identity) 檔案。

### 重複資料刪除密鑰 {#deduplication-keys}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_deduplicationkey"
>title="關於重複資料刪除金鑰"
>abstract="選取重複資料刪除金鑰，即可在匯出檔案中消除相同設定檔的多個記錄。 選取單一命名空間或最多兩個XDM架構屬性作為重複資料刪除索引鍵。 未選取重複資料刪除金鑰可能會導致匯出檔案中出現重複的設定檔項目。"
>additional-url="http://www.adobe.com/go/destinations-deduplication-keys-en" text="進一步了解檔案"

重複資料刪除金鑰是使用者定義的主金鑰，可決定使用者要依此身分對其設定檔進行重複資料刪除的&#x200B;身分。

重複資料刪除索引鍵消除了在一個匯出檔案中有多個相同設定檔記錄的可能性。

在中，有三種使用重複資料刪除密鑰的方式 [!DNL Platform]:

* 使用單一身分命名空間作為 [!UICONTROL 去重複化金鑰]
* 使用 [!DNL XDM] 設定檔作為 [!UICONTROL 去重複化金鑰]
* 使用 [!DNL XDM] 設定檔作為複合鍵

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

### 重複資料刪除使用案例1:無重複資料消除 {#deduplication-use-case-1}

若不使用重複資料刪除，匯出檔案將包含下列項目。

| personalEmail | firstName | lastName |
|---|---|---|
| johndoe@example.com | 約翰 | Doe |
| johndoe@example.com | 約翰 | D |


### 重複資料刪除使用案例2:基於身份命名空間的重複資料消除 {#deduplication-use-case-2}

假設重複資料刪除由 [!DNL Email] 命名空間，匯出檔案將包含下列項目。 設定檔B是符合區段資格的最新一個，因此是唯一一個匯出的設定檔。

| 電子郵件* | personalEmail | firstName | lastName |
|---|---|---|---|
| johndoe_1@example.com | johndoe@example.com | 約翰 | D |
| johndoe_2@example.com | johndoe@example.com | 約翰 | D |

### 重複資料刪除使用案例3:基於單一設定檔屬性的重複資料刪除 {#deduplication-use-case-3}

假設重複資料刪除由 `personal Email` 屬性，則匯出檔案將包含下列項目。 設定檔B是符合區段資格的最新一個，因此是唯一一個匯出的設定檔。

| personalEmail* | firstName | lastName |
|---|---|---|
| johndoe@example.com | 約翰 | D |


### 重複資料刪除使用案例4:基於兩個配置檔案屬性的重複資料消除 {#deduplication-use-case-4}

假設使用複合鍵重複資料刪除 `personalEmail + lastName`，則匯出檔案將包含下列項目。

| personalEmail* | lastName* | firstName |
|---|---|---|
| johndoe@example.com | D | 約翰 |
| johndoe@example.com | Doe | 約翰 |


Adobe建議您選取身分命名空間，例如 [!DNL CRM ID] 或電子郵件地址作為重複資料刪除金鑰，以確保所有設定檔記錄都經過唯一識別。

>[!NOTE]
> 
>如果資料集（而非整個資料集）中的某些欄位已套用任何資料使用標籤，則在啟用時，會在下列條件下強制執行這些欄位層級標籤：
>
>* 欄位會用於區段定義中。
>* 欄位會設定為目標目的地的預計屬性。

>
> 例如，如果欄位 `person.name.firstName` 具有與目的地的行銷動作相衝突的特定資料使用標籤，則您會在審核步驟中顯示資料使用政策違規。 如需詳細資訊，請參閱 [Adobe Experience Platform中的資料控管](../../rtcdp/privacy/data-governance-overview.md#destinations).

## 檢閱 {#review}

在 **[!UICONTROL 檢閱]** 頁面，您可以看到您所選內容的摘要。 選擇 **[!UICONTROL 取消]** 來分解流， **[!UICONTROL 返回]** 修改設定，或 **[!UICONTROL 完成]** 確認您的選擇並開始將資料傳送至目的地。

>[!IMPORTANT]
>
>在此步驟中，Adobe Experience Platform會檢查資料使用政策是否違反。 以下顯示違反原則的範例。 除非您解決違規，否則無法完成區段啟用工作流程。 有關如何解決策略違規的資訊，請參見 [政策執行](../../rtcdp/privacy/data-governance-overview.md#enforcement) （位於資料控管檔案一節）。

![資料策略違規](../assets/common/data-policy-violation.png)

如果未檢測到任何違反策略的情況，請選擇 **[!UICONTROL 完成]** 確認您的選擇並開始將資料傳送至目的地。

![檢閱](../assets/ui/activate-batch-profile-destinations/review.png)

## 驗證區段啟用 {#verify}


對於電子郵件行銷目的地和雲端儲存空間目的地，Adobe Experience Platform會建立 `.csv` 檔案。 預期每天會在儲存位置中建立新檔案。 預設檔案格式為：
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

您連續三天收到的檔案可能如下所示：

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

儲存位置中是否存在這些檔案是成功激活的確認。 若要了解匯出的檔案的結構，您可以 [下載範例.csv檔案](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). 此範例檔案包含設定檔屬性 `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`，和 `personalEmail.address`.
