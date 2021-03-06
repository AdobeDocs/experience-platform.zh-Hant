---
title: Marketo Engage目標
description: Marketo Engage是用於營銷、廣告、分析和商業的唯一端到端客戶體驗管理(CXM)解決方案。 它使您能夠自動化和管理從CRM主管管理和客戶參與到基於客戶的市場營銷和收入分配中的活動。
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 3%

---

# Marketo Engage目標 {#beta-marketo-engage-destination}

## 總覽 {#overview}

Marketo Engage是用於營銷、廣告、分析和商業的唯一端到端客戶體驗管理(CXM)解決方案。 它使您能夠自動化和管理從CRM主管管理和客戶參與到基於客戶的市場營銷和收入分配中的活動。

目標使營銷商能夠將在Adobe Experience Platform建立的段推送到Marketo，在那裡它們將顯示為靜態清單。

## 支援的身份 {#supported-identities}

| 目標標識 | 說明 |
|---|---|
| ECID | 表示ECID的命名空間。 以下別名也可以引用此命名空間：&quot;Adobe Marketing CloudID&quot;,&quot;Adobe Experience CloudID&quot;,&quot;Adobe Experience PlatformID&quot; 請參閱以下文檔 [ECID](/help/identity-service/ecid.md) 的子菜單。 |
| 電子郵件 | 表示電子郵件地址的命名空間。 此類型的命名空間通常與單個人關聯，因此可用於跨不同渠道標識該人。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>在 [映射步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 在激活目標工作流中 *強制* 映射標識和 *可選* 按鈕。 從「標識名稱空間」頁籤映射電子郵件和/或ECID是確保在Marketo匹配該人員的最重要工作。 映射電子郵件可確保最高的匹配率。

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 區段匯出]** | 您正在導出段（受眾）的所有成員，其中包含Marketo Engage目標中使用的標識符（電子郵件、ECID）。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style=&quot;table-layout:auto&quot;&quot;

## 設定目標並激活段 {#set-up}

>[!IMPORTANT]
> 
>* 要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。
>* 要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。


有關如何設定目標和激活段的詳細說明，請閱讀 [將Adobe Experience Platform段推入Marketo靜態清單](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) 在Marketo檔案里。

下面的視頻還演示了配置Marketo目標和激活段的步驟。

>[!NOTE]
>
>Experience Platform用戶介面頻繁更新，自此視頻記錄後可能已更改。 有關最新資訊，請參閱上面連結的指南。

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)。

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->
