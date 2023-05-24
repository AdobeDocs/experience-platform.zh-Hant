---
title: AWS分機概述
description: 瞭解AWS在Adobe Experience Platform的事件轉發擴展。
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 3%

---

# [!DNL AWS] 擴展概述

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) 雲計算平台提供多種服務，如分佈式計算、資料庫儲存、內容交付和軟體即服務(SaaS)整合服務，用於客戶關係管理(CRM)和企業資源規劃(ERP)。

的 [!DNL AWS] [事件轉發](../../../ui/event-forwarding/overview.md) 擴展 [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) 將事件從Adobe Experience Platform邊緣網路發送到 [!DNL AWS] 進行進一步處理。 本指南介紹如何安裝擴展並在事件轉發規則中使用其功能。

## 先決條件

您必須 [!DNL AWS] 現有帳戶 [!DNL Kinesis] 資料流，以便使用此擴展。 如果沒有預先存在的資料流，請參見 [!DNL AWS] 文檔 [使用 [!DNL AWS] 管理控制台](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html)。

## 安裝擴展 {#install}

安裝 [!DNL AWS] 擴展，導航到資料收集UI或Experience PlatformUI並選擇 **[!UICONTROL 事件轉發]** 的上界。 在此處，選擇要向其添加副檔名的屬性，或改為建立新屬性。

選擇或建立所需屬性後，選擇 **[!UICONTROL 擴展]** 在左側導航中，選擇 **[!UICONTROL 目錄]** 頁籤。 搜索 [!UICONTROL AWS] 卡，然後選擇 **[!UICONTROL 安裝]**。

![的 [!UICONTROL 安裝] 按鈕 [!UICONTROL AWS] 資料收集UI中的擴展。](../../../images/extensions/server/aws/install.png)

在下一個螢幕上，必須提供您的連接憑據 [!DNL AWS] 帳戶。 具體來說，您必須 [!DNL AWS] 訪問密鑰ID和密鑰訪問密鑰。 如果您不知道這些值，請參閱 [!DNL AWS] 文檔 [如何獲取您的訪問密鑰ID和機密訪問密鑰](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html)。

![在擴展配置視圖中添加的訪問密鑰ID和秘密訪問密鑰。](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>訪問策略需要附加到 [!DNL AWS] 用於生成訪問憑據的帳戶。 必須配置此策略以授予將資料發送到 [!DNL Kinesis] 資料流。 請參閱 **示例2** 的 [!DNL AWS] 文檔 [示例策略 [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) 查看策略的定義。

完成後，選擇 **[!UICONTROL 保存]** 並安裝擴展。

## 配置事件轉發規則 {#rule}

安裝擴展後，建立新事件轉發 [規則](../../../ui/managing-resources/rules.md) 並根據需要配置其條件。 配置規則的操作時，選擇 **[!UICONTROL AWS]** 擴展，然後選擇 **[!UICONTROL 將資料發送到Kinesis資料流]** 按鈕。

![的 [!UICONTROL 將資料發送到Kinesis資料流] 正在為資料收集UI中的規則選擇操作類型。](../../../images/extensions/server/aws/select-action-type.png)

右面板將更新，以顯示應如何發送資料的配置選項。 具體來說，您必須 [資料元素](../../../ui/managing-resources/data-elements.md) 到代表您 [!DNL Event Hub] 配置。

![的配置選項 [!UICONTROL 將資料發送到Kinesis資料流] UI中顯示的操作類型。](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Kinesis資料流詳細資訊]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 流名稱] | 此事件轉發規則將向其發送資料記錄的流的名稱。 |
| [!UICONTROL AWS州] | 的 [!DNL AWS] 區域 [!DNL Kinesis] 建立資料流。 |
| [!UICONTROL 分區密鑰] | 的 [分區鍵](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) 擴展在向資料流發送資料時使用。<br><br>[!DNL Kinesis Data Streams] 將屬於流的資料記錄分割成多個分片。 它使用與每個資料記錄一起發送的分區密鑰來確定給定資料記錄所屬的分片。<br><br>分發客戶的一個好分區密鑰可能是客戶編號，因為每個客戶的編號不同。 分區密鑰不好可能是他們的郵遞區號，因為他們可能都住在附近的同一區域。 通常，您應選擇具有不同潛在值最高範圍的分區鍵。 查看 [!DNL AWS] 文章 [縮放 [!DNL Kinesis] 資料流](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) 用於管理分區鍵的最佳做法。 |

{style="table-layout:auto"}

**[!UICONTROL 資料]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 負載] | 此欄位包含將轉發到 [!DNL Kinesis] 資料流，採用JSON格式。<br><br>在 **[!UICONTROL 原始]** 選項，您可以將JSON對象直接貼上到提供的文本欄位中，或者選擇資料元素表徵圖(![資料集表徵圖](../../../images/extensions/server/aws/data-element-icon.png))以從現有資料元素清單中選擇以表示負載。<br><br>您還可以使用 **[!UICONTROL JSON鍵值對編輯器]** 選項通過UI編輯器手動添加每個鍵值對。 每個值都可以用原始輸入來表示，或者可以選擇資料元素。 |

{style="table-layout:auto"}

完成後，選擇 **[!UICONTROL 保留更改]** 將操作添加到規則配置。 對規則滿意後，選擇 **[!UICONTROL 保存到庫]**。

最後，發佈新事件轉發 [構建](../../../ui/publishing/builds.md) 以啟用對庫的更改。

## 後續步驟

本指南介紹了如何將資料發送到 [!DNL Kinesis Data Streams] 使用 [!DNL AWS] 事件轉發擴展。 有關Experience Platform中事件轉發功能的詳細資訊，請參閱 [事件轉發概述](../../../ui/event-forwarding/overview.md)。
