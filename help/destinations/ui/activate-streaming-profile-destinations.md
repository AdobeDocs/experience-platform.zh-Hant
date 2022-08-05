---
keywords: 激活配置檔案目標；激活目標；激活資料激活電子郵件營銷目標；激活雲儲存目標
title: 激活受眾資料以流式處理配置檔案導出目標
type: Tutorial
description: 瞭解如何通過將段發送到基於配置檔案的流式傳輸目的地來激活您在Adobe Experience Platform擁有的受眾資料。
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: af761155bc510d96cea2b0bd475ee4a3bc4abe16
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 0%

---

# 激活受眾資料以流式處理配置檔案導出目標

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

## 總覽 {#overview}

本文介紹在Adobe Experience Platform流式基於配置檔案的目標(如AmazonKinesis)激活觀眾資料所需的工作流。

## 先決條件 {#prerequisites}

要將資料激活到目標，必須已成功 [連接到目標](./connect-destination.md)。 如果尚未執行此操作，請轉至 [目標目錄](../catalog/overview.md)，瀏覽支援的目標，並配置要使用的目標。

## 選擇目標 {#select-destination}

1. 轉到 **[!UICONTROL 連接>目標]**，然後選擇 **[!UICONTROL 目錄]** 頁籤。

   ![顯示目標目錄頁籤的影像。](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. 選擇 **[!UICONTROL 激活段]** 在與要激活段的目標相對應的卡上，如下圖所示。

   ![在目標目錄頁籤中突出顯示激活段控制項的影像。](../assets/ui/activate-streaming-profile-destinations/activate-segments-button.png)

1. 選擇要用於激活段的目標連接，然後選擇 **[!UICONTROL 下一個]**。

   ![該影像顯示可連接到的兩個目標的選擇。](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. 移至下一節 [選擇段](#select-segments)。

## 選擇段 {#select-segments}

使用段名稱左側的複選框選擇要激活到目標的段，然後選擇 **[!UICONTROL 下一個]**。

![在激活工作流的「選擇段」步驟中突出顯示選中的複選框的影像。](../assets/ui/activate-streaming-profile-destinations/select-segments.png)

## 選擇配置檔案屬性 {#select-attributes}

在 **[!UICONTROL 映射]** 步驟，選擇要發送到目標目標的配置檔案屬性。

>[!NOTE]
>
> Adobe Experience Platform用您的架構中的四個推薦的常用屬性來預先填充您的選擇： `person.name.firstName`。 `person.name.lastName`。 `personalEmail.address`。 `segmentMembership.status`。

檔案導出方式將因以下方式而異，具體取決於 `segmentMembership.status` 已選中：
* 如果 `segmentMembership.status` 欄位，導出的檔案包括 **[!UICONTROL 活動]** 初始完整快照中的成員和 **[!UICONTROL 活動]** 和 **[!UICONTROL 已過期]** 後續增量導出中的成員。
* 如果 `segmentMembership.status` 欄位未選中，導出的檔案僅包括 **[!UICONTROL 活動]** 初始完整快照和後續增量導出中的成員。

![顯示映射步驟中預填充的建議屬性的影像。](../assets/ui/activate-streaming-profile-destinations/attributes-default.png)

1. 在 **[!UICONTROL 選擇屬性]** ，選擇 **[!UICONTROL 添加新欄位]**。

   ![在映射步驟中突出顯示「添加新欄位」控制項的影像。](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. 選擇右側的箭頭 **[!UICONTROL 架構欄位]** 的子菜單。

   ![在映射步驟中突出顯示如何選擇源欄位的影像。](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. 在 **[!UICONTROL 選擇欄位]** 頁，選擇要發送到目標的XDM屬性，然後選擇 **[!UICONTROL 選擇]**。

   ![該影像顯示可選擇作為源欄位的XDM欄位的選擇。](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)


1. 要添加更多映射，請重複步驟1至3，然後選擇 **[!UICONTROL 下一個]**。

## 審閱 {#review}

在 **[!UICONTROL 審閱]** 的子菜單。 選擇 **[!UICONTROL 取消]** 分解流， **[!UICONTROL 後退]** 修改設定，或 **[!UICONTROL 完成]** 確認選擇並開始向目標發送資料。

>[!IMPORTANT]
>
>在此步驟中，Adobe Experience Platform檢查資料使用策略違規。 下面顯示的示例違反了策略。 在解決違規之前，無法完成段激活工作流。 有關如何解決策略違規的資訊，請參見 [策略執行](../../rtcdp/privacy/data-governance-overview.md#enforcement) 資料治理文檔部分。

![在審閱步驟中顯示違反資料策略的影像。](../assets/common/data-policy-violation.png)

如果未檢測到任何策略違規，請選擇 **[!UICONTROL 完成]** 確認選擇並開始向目標發送資料。

![顯示激活工作流的審閱步驟的影像。](../assets/ui/activate-streaming-profile-destinations/review.png)

## 驗證段激活 {#verify}

已導出 [!DNL Experience Platform] 資料以JSON格式降落到目標目標中。 例如，以下事件包含已限定某個段並退出另一個段的受眾的電子郵件地址配置檔案屬性。 此潛在客戶的標識為ECID和電子郵件。

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
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
