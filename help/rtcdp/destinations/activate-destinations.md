---
title: 將描述檔和區段啟用至目標
seo-title: 將描述檔和區段啟用至目標
description: 將區段對應至目標，以啟用您在Adobe即時客戶資料平台中擁有的資料。 若要完成此作業，請遵循下列步驟。
seo-description: 將區段對應至目標，以啟用您在Adobe即時客戶資料平台中擁有的資料。 若要完成此作業，請遵循下列步驟。
translation-type: tm+mt
source-git-commit: 73925aa59f9981d8945fb0be6c4924e1831cf902

---


# 將描述檔和區段啟用至目標

將區段對應至目標，以啟用您在Adobe即時客戶資料平台中擁有的資料。 若要完成此作業，請遵循下列步驟。

## 先決條件 {#prerequisites}

要將資料激活到目標，必須已成功 [連接目標](/help/rtcdp/destinations/assets/connect-destination.png)。 如果您尚未這麼做，請前往目標目錄 [](/help/rtcdp/destinations/destinations-catalog.md)，瀏覽支援的目標，並設定一或多個目標。

## 啟動資料 {#activate-data}

1. 在「 **目標>瀏覽**」中，選取您要啟用區段的目標。
2. 按一下目標的名稱。 這會帶您進入「啟動」流程。
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)請注意，如果目的地已有啟動流程，您可以看到目前傳送至目的地的區段。 選取 **右側邊欄** 「編輯啟動」，然後依照下列步驟修改啟動詳細資訊。
3. 選擇 **激活**;
4. 在「 **啟用目標** 」精靈的「選 **取區段** 」頁面上，選取要傳送至目標的區段。
   ![區段到目的地](/help/rtcdp/destinations/assets/select-segments.png)
5. *有條件*. 此步驟僅適用於對應至電子郵件行銷目的地的區段。 <br> 在「目 **標屬性** 」頁上，選擇「 **添加新欄位** 」並選擇要發送到目標的屬性。
我們建議其中一個屬性作為聯合 [架構的唯一](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 標識符。 如需必要屬性的詳細資訊，請參閱「電子郵件行銷目標」 [文章中的「身分](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 」。
   ![目標屬性](/help/rtcdp/destinations/assets/destination-attributes.png)
6. 在「 **排程** 」頁上，您可以看到傳送資料至目的地的開始日期，以及傳送資料至目的地的頻率。
7. 在「審 **閱** 」頁面上，您可以看到您所選項目的摘要。 選擇 **取消** ，以劃分流程，選擇 **返回** ，修改設定，或選擇完 **成** ，確認選擇並開始向目標發送資料。

![確認選擇](/help/rtcdp/destinations/assets/confirm-selection.png)

## 編輯啟動 {#edit-activation}

請依照下列步驟，在即時CDP中編輯現有的啟動流程：

1. 在左 **側導覽列中選取** 「目標」，然後按一下「 **瀏覽** 」標籤，然後按一下目標名稱。
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

## 停用啟動 {#disable-activation}

若要停用現有的啟動流程，請遵循下列步驟：

1. 在左 **側導覽列中選取** 「目標」，然後按一下「 **瀏覽** 」標籤，然後按一下目標名稱。
2. 按一下 **[!UICONTROL 右邊欄]** 中的「已啟用」控制項，以變更啟動流程狀態。
3. 在「更 **新資料流狀態** 」視窗中，選 **取「確認** 」以停用啟動流程。

