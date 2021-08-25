---
keywords: 啟用設定檔目的地；啟用目的地；啟用資料；啟用電子郵件行銷目的地；啟用雲端儲存目的地
title: 對串流設定檔匯出目的地啟用受眾資料
type: Tutorial
seo-title: Activate audience data to streaming profile export destinations
description: 了解如何將區段傳送至以設定檔為基礎的串流目的地，以啟動Adobe Experience Platform中您擁有的受眾資料。
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by sending segments to streaming profile-based destinations.
source-git-commit: d13920250fafd2ba4ff37dd5d4a45d417ed3ecc7
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# 對串流設定檔匯出目的地啟用受眾資料

## 概覽 {#overview}

本文說明在Adobe Experience Platform串流設定檔型目的地(例如Amazon Kinesis)中啟用受眾資料所需的工作流程。

## 先決條件 {#prerequisites}

若要將資料激活到目的地，您必須已成功[連接到目標](./connect-destination.md)。 如果尚未這麼做，請前往[目標目錄](../catalog/overview.md)，瀏覽支援的目標，並設定您要使用的目標。

## 選取您的目的地 {#select-destination}

1. 前往&#x200B;**[!UICONTROL 連線>目的地]**，然後選取&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤。

   ![目標目錄索引標籤](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. 在與您要啟用區段的目的地對應的卡片上，選取「啟用區段」**[!UICONTROL ，如下圖所示。]**

   ![「啟用區段」按鈕](../assets/ui/activate-streaming-profile-destinations/activate-segments-button.png)

1. 選取您要用來啟用區段的目的地連線，然後選取&#x200B;**[!UICONTROL Next]**。

   ![選擇目標](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. 移至下一個區段至[選取您的區段](#select-segments)。

## 選取您的區段 {#select-segments}

使用區段名稱左側的核取方塊，選取您要啟用至目的地的區段，然後選取&#x200B;**[!UICONTROL Next]**。

![選取區段](../assets/ui/activate-streaming-profile-destinations/select-segments.png)

## 選取設定檔屬性 {#select-attributes}

選取您要傳送至目標目的地的設定檔屬性。

>[!NOTE]
>
> Adobe Experience Platform會從您的架構中，使用四個建議且常用的屬性來填入您的選取項目：`person.name.firstName`、`person.name.lastName`、`personalEmail.address`、`segmentMembership.status`。

檔案導出將以下方式有所不同，具體取決於是否選擇了`segmentMembership.status`:
* 如果選擇了`segmentMembership.status`欄位，則導出的檔案包括初始完整快照中的&#x200B;**[!UICONTROL 活動]**&#x200B;成員，以及後續增量導出中的&#x200B;**[!UICONTROL 活動]**&#x200B;和&#x200B;**[!UICONTROL 過期]**&#x200B;成員。
* 如果未選擇`segmentMembership.status`欄位，則導出的檔案在初始完整快照和後續增量導出中僅包含&#x200B;**[!UICONTROL 活動]**&#x200B;成員。

![建議的屬性](../assets/ui/activate-streaming-profile-destinations/attributes-default.png)

1. 在&#x200B;**[!UICONTROL 選擇屬性]**&#x200B;頁中，選擇&#x200B;**[!UICONTROL 添加新欄位]**。

   ![新增對應](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. 選擇&#x200B;**[!UICONTROL 架構欄位]**&#x200B;條目右側的箭頭。

   ![選擇源欄位](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. 在&#x200B;**[!UICONTROL 選擇欄位]**&#x200B;頁中，選擇要發送到目標的XDM屬性，然後選擇&#x200B;**[!UICONTROL 選擇]**。

   ![「選擇源欄位」頁](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)


1. 要添加更多映射，請重複步驟1到3，然後選擇&#x200B;**[!UICONTROL Next]**。

## 檢閱 {#review}

在&#x200B;**[!UICONTROL 檢閱]**&#x200B;頁面上，您會看到您所選項目的摘要。 選擇&#x200B;**[!UICONTROL 取消]**&#x200B;以分解流，選擇&#x200B;**[!UICONTROL 返回]**&#x200B;以修改設定，或選擇&#x200B;**[!UICONTROL 完成]**&#x200B;以確認您的選擇並開始向目標發送資料。

>[!IMPORTANT]
>
>在此步驟中，Adobe Experience Platform會檢查資料使用政策是否違反。 以下顯示違反原則的範例。 除非您解決違規，否則無法完成區段啟用工作流程。 有關如何解決策略違規的資訊，請參閱資料控管文檔部分中的[策略實施](../../rtcdp/privacy/data-governance-overview.md#enforcement)。

![資料策略違規](../assets/common/data-policy-violation.png)

如果未檢測到任何違反策略的情況，請選擇&#x200B;**[!UICONTROL 完成]**&#x200B;以確認您的選擇並開始向目標發送資料。

![檢閱](../assets/ui/activate-streaming-profile-destinations/review.png)

## 驗證區段啟用 {#verify}

匯出的[!DNL Experience Platform]資料會以JSON格式登陸目標目的地。 例如，以下事件包含已符合特定區段資格並退出其他區段之對象的電子郵件地址設定檔屬性。 此潛在客戶的身分識別為ECID和電子郵件。

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```
