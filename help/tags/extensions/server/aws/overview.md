---
title: AWS擴充功能概觀
description: 瞭解Adobe Experience Platform中用於事件轉送的AWS擴充功能。
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 0%

---

# [!DNL AWS]擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品檔案中出現了幾項術語變更。 請參閱下列[檔案](../../../term-updates.md)，以取得術語變更的彙總參考資料。

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/)是雲端運算平台，提供各種服務，例如分散式運算、資料庫儲存、內容傳遞，以及客戶關係管理(CRM)和企業資源規劃(ERP)的軟體即服務(SaaS)整合服務。

[!DNL AWS] [事件轉送](../../../ui/event-forwarding/overview.md)擴充功能運用[[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)將事件從Adobe Experience PlatformEdge Network傳送至[!DNL AWS]以進行進一步處理。 本指南說明如何安裝擴充功能，以及在事件轉送規則中運用其功能。

## 先決條件

您必須擁有具有現有[!DNL Kinesis]資料流的[!DNL AWS]帳戶，才能使用此擴充功能。 如果您沒有預先存在的資料流，請參閱有關[使用 [!DNL AWS] 管理主控台](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html)建立新資料流的[!DNL AWS]檔案。

## 安裝擴充功能 {#install}

若要安裝[!DNL AWS]擴充功能，請導覽至資料收集UI或Experience PlatformUI，然後從左側導覽中選取&#x200B;**[!UICONTROL 事件轉送]**。 從這裡，選取要新增擴充功能的屬性，或改為建立新屬性。

選取或建立所需的屬性後，在左側導覽中選取&#x200B;**[!UICONTROL 擴充功能]**，然後選取&#x200B;**[!UICONTROL 目錄]**&#x200B;索引標籤。 搜尋[!UICONTROL AWS]卡片，然後選取&#x200B;**[!UICONTROL 安裝]**。

![正在資料收集UI中為[!UICONTROL AWS]擴充功能選取[!UICONTROL 安裝]按鈕。](../../../images/extensions/server/aws/install.png)

在下一個畫面中，您必須提供您[!DNL AWS]帳戶的連線認證。 具體來說，您必須提供您的[!DNL AWS]存取金鑰ID和機密存取金鑰。 如果您不知道這些值，請參閱[上的[!DNL AWS]檔案，瞭解如何取得您的存取金鑰ID和機密存取金鑰](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html)。

![擴充功能組態檢視中新增的存取金鑰識別碼與機密存取金鑰。](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>存取原則必須附加至用來產生存取認證的[!DNL AWS]帳戶。 此原則必須設定為授與存取許可權，才能將資料傳送至[!DNL Kinesis]資料流。 請參考 [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples)之[範例原則的[!DNL AWS]檔案中的&#x200B;**範例2**，瞭解應該如何定義原則。

完成後，選取[儲存]，然後安裝擴充功能。****

## 設定事件轉送規則 {#rule}

安裝擴充功能後，請建立新的事件轉送[規則](../../../ui/managing-resources/rules.md)，並視需要設定其條件。 設定規則的動作時，請選取&#x200B;**[!UICONTROL AWS]**&#x200B;擴充功能，然後針對動作型別選取&#x200B;**[!UICONTROL 將資料傳送至Kinesis資料流]**。

![針對資料收集UI中的規則所選取的[!UICONTROL 傳送資料至Kinesis資料流]動作型別。](../../../images/extensions/server/aws/select-action-type.png)

右側面板會更新，以顯示資料傳送方式的設定選項。 具體來說，您必須將[資料元素](../../../ui/managing-resources/data-elements.md)指派給代表您[!DNL Event Hub]組態的各種屬性。

![ UI中顯示的[!UICONTROL 傳送資料至Kinesis資料流]動作型別的組態選項。](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Kinesis資料流詳細資料]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 資料流名稱] | 此事件轉送規則將傳送資料記錄的目標資料流名稱。 |
| [!UICONTROL AWS地區] | 建立[!DNL Kinesis]資料流的[!DNL AWS]區域。 |
| [!UICONTROL 分割區索引鍵] | 擴充功能將資料傳送至資料流時所使用的[資料分割索引鍵](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key)。<br><br>[!DNL Kinesis Data Streams]會將屬於資料流的資料記錄分割成多個分片。 它會使用隨每個資料記錄傳送的分割區索引鍵，來判斷指定的資料記錄屬於哪個分片。<br><br>分配客戶的正確資料分割金鑰可能是客戶編號，因為每個客戶的資料分割金鑰不同。 不良的資料分割金鑰可能是它們的郵遞區號，因為它們可能都住在附近的同一個區域。 一般而言，您應該選擇具有不同潛在值範圍最大的分割區索引鍵。 如需管理分割區金鑰的最佳實務，請參閱[縮放您的 [!DNL Kinesis] 資料串流](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/)上的[!DNL AWS]文章。 |

{style="table-layout:auto"}

**[!UICONTROL 資料]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 承載] | 此欄位包含將轉送至[!DNL Kinesis]資料流的資料，採用JSON格式。<br><br>在&#x200B;**[!UICONTROL 原始]**&#x200B;選項下，您可以將JSON物件直接貼上到提供的文字欄位中，或者您可以選取資料元素圖示（![資料集圖示](../../../images/extensions/server/aws/data-element-icon.png)）來從現有資料元素清單中選取以代表裝載。<br><br>您也可以使用&#x200B;**[!UICONTROL JSON索引鍵/值組編輯器]**&#x200B;選項，透過UI編輯器手動新增每個索引鍵/值組。 每個值都可表示為原始輸入，或是可改為選取資料元素。 |

{style="table-layout:auto"}

完成後，選取&#x200B;**[!UICONTROL 保留變更]**&#x200B;以將動作新增至規則設定。 如果您對規則感到滿意，請選取&#x200B;**[!UICONTROL 儲存至程式庫]**。

最後，發佈新的事件轉送[組建](../../../ui/publishing/builds.md)，以啟用程式庫的變更。

## 後續步驟

本指南說明如何使用[!DNL AWS]事件轉送擴充功能將資料傳送至[!DNL Kinesis Data Streams]。 如需Experience Platform中事件轉送功能的詳細資訊，請參閱[事件轉送概觀](../../../ui/event-forwarding/overview.md)。
