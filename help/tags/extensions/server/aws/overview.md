---
title: AWS擴充功能概述
description: 了解Adobe Experience Platform中用於事件轉送的AWS擴充功能。
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
source-git-commit: b4ff3dbc9c62dceefdf2b842cafa65132dde41fc
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 4%

---

# [!DNL AWS] 擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) 是雲計算平台，為客戶關係管理(CRM)和企業資源規劃(ERP)提供多種服務，如分佈式計算、資料庫儲存、內容交付和軟體即服務(SaaS)整合服務。

此 [!DNL AWS] [事件轉送](../../../ui/event-forwarding/overview.md) 擴充功能可運用 [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) 從Adobe Experience Platform邊緣網路將事件傳送至 [!DNL AWS] 供進一步處理。 本指南說明如何安裝擴充功能，並在事件轉送規則中運用其功能。

## 先決條件

您必須有 [!DNL AWS] 具有現有 [!DNL Kinesis] 資料流，以便使用此擴充功能。 如果您沒有預先存在的資料流，請參閱 [!DNL AWS] 檔案 [使用 [!DNL AWS] 管理控制台](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## 安裝擴充功能 {#install}

若要安裝 [!DNL AWS] 擴充功能，請導覽至資料收集UI或Experience PlatformUI，然後選取 **[!UICONTROL 事件轉送]** 從左側導覽。 從此處，選取要新增擴充功能的屬性，或改為建立新屬性。

選取或建立所需屬性後，請選取 **[!UICONTROL 擴充功能]** 在左側導覽器中，選取 **[!UICONTROL 目錄]** 標籤。 搜尋 [!UICONTROL AWS] 卡片，然後選取 **[!UICONTROL 安裝]**.

![此 [!UICONTROL 安裝] 按鈕 [!UICONTROL AWS] 擴充功能。](../../../images/extensions/server/aws/install.png)

在下一個畫面中，您必須提供 [!DNL AWS] 帳戶。 具體來說，您必須提供 [!DNL AWS] 存取金鑰ID和秘密存取金鑰。 如果您不知道這些值，請參閱 [!DNL AWS] 檔案 [如何取得您的存取金鑰ID和機密存取金鑰](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![擴充功能組態檢視中新增的存取金鑰ID和機密存取金鑰。](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>訪問策略需要附加到 [!DNL AWS] 用於生成訪問憑據的帳戶。 必須配置此策略以授予將資料發送到 [!DNL Kinesis] 資料流。 請參閱 **範例2** 在 [!DNL AWS] 文檔 [範例原則 [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) 以了解應如何定義原則。

完成後，請選取 **[!UICONTROL 儲存]** 且已安裝擴充功能。

## 設定事件轉送規則 {#rule}

安裝擴充功能後，建立新的事件轉送 [規則](../../../ui/managing-resources/rules.md) 並視需要設定其條件。 設定規則的動作時，請選取 **[!UICONTROL AWS]** 擴充功能，然後選取 **[!UICONTROL 傳送資料至Kinesis資料流]** （針對動作類型）。

![此 [!UICONTROL 傳送資料至Kinesis資料流] 在資料收集UI中為規則選取的動作類型。](../../../images/extensions/server/aws/select-action-type.png)

右側面板會更新，顯示應如何傳送資料的設定選項。 具體來說，您必須指派 [資料元素](../../../ui/managing-resources/data-elements.md) 到代表您 [!DNL Event Hub] 設定。

![的設定選項 [!UICONTROL 傳送資料至Kinesis資料流] UI中顯示的動作類型。](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Kinesis資料流詳細資料]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 資料流名稱] | 此事件轉送規則會將資料記錄傳送至的資料流名稱。 |
| [!UICONTROL AWS地區] | 此 [!DNL AWS] 地區， [!DNL Kinesis] 資料流已建立。 |
| [!UICONTROL 分區密鑰] | 此 [分區密鑰](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) 擴充功能在傳送資料至資料流時使用的欄位。<br><br>[!DNL Kinesis Data Streams] 將屬於資料流的資料記錄分隔到多個分區中。 它使用與每個資料記錄一起發送的分區密鑰來確定給定資料記錄屬於哪個分區。<br><br>分發客戶的好分區密鑰可能是客戶編號，因為每個客戶的編號都不同。 分區密鑰不好，可能是郵遞區號，因為它們都可能住在附近的同一區域。 通常，您應選擇具有不同潛在值最大範圍的分區鍵。 請參閱 [!DNL AWS] 文章 [縮放 [!DNL Kinesis] 資料流](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) 以了解有關管理分區密鑰的最佳做法。 |

{style=&quot;table-layout:auto&quot;}

**[!UICONTROL 資料]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 裝載] | 此欄位包含要轉送至 [!DNL Kinesis] 資料流，格式為JSON。<br><br>在 **[!UICONTROL 原始]** 選項，您可以直接將JSON物件貼到提供的文字欄位，或選取資料元素圖示(![資料集圖示](../../../images/extensions/server/aws/data-element-icon.png))，以從現有資料元素清單中選取以表示裝載。<br><br>您也可以使用 **[!UICONTROL JSON索引鍵值配對編輯器]** 選項，透過UI編輯器手動新增每個機碼 — 值組。 每個值都可由原始輸入來表示，或可以改為選取資料元素。 |

{style=&quot;table-layout:auto&quot;}

完成後，請選取 **[!UICONTROL 保留變更]** 將動作新增至規則設定。 對規則感到滿意時，請選取 **[!UICONTROL 儲存至程式庫]**.

最後，發佈新的事件轉送 [建置](../../../ui/publishing/builds.md) 啟用程式庫的變更。

## 後續步驟

本指南說明如何將資料傳送至 [!DNL Kinesis Data Streams] 使用 [!DNL AWS] 事件轉送擴充功能。 如需Experience Platform中事件轉送功能的詳細資訊，請參閱 [事件轉送概觀](../../../ui/event-forwarding/overview.md).
