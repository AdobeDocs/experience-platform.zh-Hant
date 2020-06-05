---
title: 將描述檔和區段啟用至目標
seo-title: 將描述檔和區段啟用至目標
description: 將區段對應至目標，以啟用您在Adobe即時客戶資料平台中擁有的資料。 若要完成此作業，請遵循下列步驟。
seo-description: 將區段對應至目標，以啟用您在Adobe即時客戶資料平台中擁有的資料。 若要完成此作業，請遵循下列步驟。
translation-type: tm+mt
source-git-commit: 24e4746b28620210c138a1e803b6afadff79ab30
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---


# 將描述檔和區段啟用至目標

將區段對應至目標，以啟用您在Adobe即時客戶資料平台中擁有的資料。 若要完成此作業，請遵循下列步驟。

## 先決條件 {#prerequisites}

要將資料激活到目標，必須已成功 [連接目標](/help/rtcdp/destinations/assets/connect-destination-1.png)。 如果您尚未這麼做，請前往目標目錄 [](/help/rtcdp/destinations/destinations-catalog.md)，瀏覽支援的目標，並設定一或多個目標。

## 啟動資料 {#activate-data}

1. 在「 **[!UICONTROL 目標>瀏覽]**」中，選取您要啟用區段的目標。
2. 按一下目標的名稱。 這會帶您進入「啟動」流程。
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)請注意，如果目的地已有啟動流程，您可以看到目前傳送至目的地的區段。 選取 **[!UICONTROL 右側邊欄]** 「編輯啟動」，然後依照下列步驟修改啟動詳細資訊。
3. 選擇 **[!UICONTROL 激活]**;
4. 在「啟 **[!UICONTROL 動目標]** 」工作流程的「選 **** 取區段」頁面上，選取要傳送至目標的區段。
   ![區段到目的地](/help/rtcdp/destinations/assets/select-segments.png)
5. *有條件*. 此步驟會依您要啟用區段的目的地類型而有所不同。 <br> 對於 *電子郵件目標**和雲端儲存目標*，在「選取屬性」頁面上，選 ******** 取「新增欄位Marketing」，並選取您要傳送至目標的屬性。
我們建議其中一個屬性作為聯合 [架構的唯一](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 標識符。 如需必要屬性的詳細資訊，請參閱「電子郵件行銷目標」 [文章中的「身分](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 」。
   ![目標屬性](/help/rtcdp/destinations/assets/select-attributes-step.png)

   <br> 

   對於 *社交目標*，在「身分對 **[!UICONTROL 應」步驟中]** ，您可以選取來源屬性，將其映射為目標身分。 此步驟為可選或必選步驟，具體取決於您在架構中使用的主要身份。 <br> 

   *電子郵件地址作為主要身份*: 如果您在架構中使用電子郵件地址作為主要身份，則可以跳過「身份映射」步驟，如下所示：

   ![身分識別的電子郵件地址](/help/rtcdp/destinations/assets/email-as-identity.gif)

   <br> 

   *另一個ID作為主要身份*: 如果您使用其他ID(例如 *Rewards ID* 或 *Loyalty ID*)作為架構中的主要身分識別，您必須手動將您身分識別架構中的電子郵件地址映射為社交目標中的目標身分，如下所示：

   ![忠誠度ID身分](/help/rtcdp/destinations/assets/rewardsid-as-identity.gif)


   如果 `Email_LC_SHA256` 您根據Facebook電子郵件雜湊要求，將資料擷取的客戶電子郵件地址雜湊到Adobe Experience Platform中，請選 [為目標身分](/help/rtcdp/destinations/facebook-destination.md#email-hashing-requirements)。 <br> 如果 `Email` 您使用的電子郵件地址未雜湊，請選取為目標身分。 Adobe即時CDP會雜湊電子郵件地址，以符合Facebook的要求。

   ![填入欄位後的身分對應](/help/rtcdp/destinations/assets/identity-mapping.png)

6. 在「區 **[!UICONTROL 段排程]** 」頁面上，您可以看到傳送資料至目的地的開始日期，以及傳送資料至目的地的頻率。

   >[!IMPORTANT]
   >
   >對於社交目的地，您必須在此步驟中選取對象的來源。 您只能在選取下圖中的其中一個選項後，才可繼續下一步。

   ![選擇資料來源](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. 在「審 **[!UICONTROL 閱]** 」頁面上，您可以看到您所選項目的摘要。 選擇 **[!UICONTROL 取消]** ，以劃分流程，選擇 **[!UICONTROL 返回]** ，修改設定，或選擇完 **[!UICONTROL 成]** ，確認選擇並開始向目標發送資料。

![確認選擇](/help/rtcdp/destinations/assets/confirm-selection.png)

## 編輯啟動 {#edit-activation}

請依照下列步驟，在即時CDP中編輯現有的啟動流程：

1. 在左 **[!UICONTROL 側導覽列中選取]** 「目標」，然後按一下「 **[!UICONTROL 瀏覽]** 」標籤，然後按一下目標名稱。
2. 選取 **[!UICONTROL 右側欄]** 「編輯啟動」，以變更要傳送至目的地的區段。

## 確認區段啟動成功 {#verify-activation}

### 電子郵件行銷目的地和雲端儲存空間目的地

對於電子郵件行銷目標和雲端儲存目標，Adobe即時CDP會在您提供的儲存位置 `.txt` 中 `.csv` 建立以定位點分隔或檔案。 希望每天在您的儲存位置中建立一個新檔案。 The file format is:
`<destination name>id<destination id><timestamp-yyyymmddhhmmss>`

您在連續三天收到的檔案可能如下所示：

```
Salesforce_id3544_20191120110000.csv
Salesforce_id3544_20191121123000.csv
Salesforce_id3544_20191122124530.csv
```

這些檔案在您的儲存位置即表示確認是否成功啟動。

### 廣告目的地

檢查您要啟動資料的各個廣告目的地。 如果啟動成功，您的廣告平台會填入受眾。

### 社交網路目的地

對於Facebook，成功的啟動表示Facebook自訂對象會以程式設計方式在 [Facebook廣告管理員中建立](https://www.facebook.com/adsmanager/manage/)。 當使用者符合已啟用區段的資格或被取消資格時，會新增及移除觀眾中的區段成員資格。

>[!TIP]
>
>Adobe即時CDP與Facebook的整合可支援歷史觀眾回填。 當您將區段啟動至目標時，所有歷史區段資格都會傳送至Facebook。

## 停用啟動 {#disable-activation}

若要停用現有的啟動流程，請遵循下列步驟：

1. 在左 **[!UICONTROL 側導覽列中選取]** 「目標」，然後按一下「 **[!UICONTROL 瀏覽]** 」標籤，然後按一下目標名稱。
2. 按一下 **[!UICONTROL 右邊欄]** 中的「已啟用」控制項，以變更啟動流程狀態。
3. 在「更 **新資料流狀態** 」視窗中，選 **取「確認** 」以停用啟動流程。

在AWS Kinesis中，生成訪問密鑰——秘密訪問密鑰對，以授予Adobe Real-time CDP對AWS Kinesis帳戶的訪問權。 從 [AWS Kinesis文檔瞭解更多資訊](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。