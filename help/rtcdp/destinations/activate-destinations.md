---
title: 將描述檔和區段啟用至目標
seo-title: 將描述檔和區段啟用至目標
description: 將區段對應至目標，以啟用您在Adobe即時客戶資料平台中擁有的資料。 若要完成此作業，請遵循下列步驟。
seo-description: 將區段對應至目標，以啟用您在Adobe即時客戶資料平台中擁有的資料。 若要完成此作業，請遵循下列步驟。
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# 將描述檔和區段啟用至目標

將區段對應至目標，以啟用您在Adobe即時客戶資料平台中擁有的資料。 若要完成此作業，請遵循下列步驟。

## 先決條件 {#prerequisites}

要將資料激活到目標，必須已成功 [連接目標](/help/rtcdp/destinations/assets/connect-destination.png)。 如果您尚未這麼做，請前往目標目錄 [](/help/rtcdp/destinations/destinations-catalog.md)，瀏覽支援的目標，並設定一或多個目標。

## 啟動資料 {#activate-data}

1. 在 **[!UICONTROL Destinations > Browse]**&#x200B;中，選取您要啟用區段的目標。
2. 按一下目標的名稱。 這會帶您進入「啟動」流程。
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)請注意，如果目的地已有啟動流程，您可以看到目前傳送至目的地的區段。 在右 **[!UICONTROL Edit activation]** 側導軌中選擇，然後依照下列步驟修改啟動詳細資訊。
3. 選擇 **[!UICONTROL Activate]**;
4. 在工作 **[!UICONTROL Activate destination]** 流程中，在頁 **[!UICONTROL Select Segments]** 面上，選取要傳送至目的地的區段。
   ![區段到目的地](/help/rtcdp/destinations/assets/select-segments.png)
5. *有條件*. 此步驟僅適用於對應至電子郵件行銷目的地的區段。 <br> 在頁面 **[!UICONTROL Destination Attributes]** 上，選 **[!UICONTROL Add new field]** 擇並選擇要發送到目標的屬性。
我們建議其中一個屬性作為聯合 [架構的唯一](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 標識符。 如需必要屬性的詳細資訊，請參閱「電子郵件行銷目標」 [文章中的「身分](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 」。
   ![目標屬性](/help/rtcdp/destinations/assets/destination-attributes.png)
6. 在頁面 **[!UICONTROL Schedule]** 上，您可以看到傳送資料至目的地的開始日期，以及傳送資料至目的地的頻率。
7. 在頁面 **[!UICONTROL Review]** 上，您可以看到您所選取項目的摘要。 選 **[!UICONTROL Cancel]** 擇以劃分流程、 **[!UICONTROL Back]** 修改設定，或確 **[!UICONTROL Finish]** 認您的選擇並開始傳送資料至目的地。

![確認選擇](/help/rtcdp/destinations/assets/confirm-selection.png)

## 編輯啟動 {#edit-activation}

請依照下列步驟，在即時CDP中編輯現有的啟動流程：

1. 在左 **[!UICONTROL Destinations]** 側導覽列中選取，然後按一下標 **[!UICONTROL Browse]** 簽，然後按一下目標名稱。
2. 在右 **[!UICONTROL Edit activation]** 側欄中選取以變更要傳送至目的地的區段。

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

## 停用啟動 {#disable-activation}

若要停用現有的啟動流程，請遵循下列步驟：

1. 在左 **[!UICONTROL Destinations]** 側導覽列中選取，然後按一下標 **[!UICONTROL Browse]** 簽，然後按一下目標名稱。
2. 按一下 **[!UICONTROL Enabled]** 右側導軌中的控制項，以變更啟動流程狀態。
3. 在「更 **新資料流狀態** 」視窗中，選 **取「確認** 」以停用啟動流程。

