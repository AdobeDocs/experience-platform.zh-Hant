---
keywords: Experience Platform；首頁；熱門主題；Audience Manager連接器；受眾管理器；受眾管理器
solution: Experience Platform
title: Audience Manager源概述
description: Adobe Audience Manager資料來源收集了Audience ManagerAdobe Experience Platform的第一方資料。
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 0%

---

# Audience Manager源

Adobe Audience Manager資料來源對在Adobe Audience Manager收集的第一方資料進行匯總，以便在Adobe Experience Platform激活。 Audience Manager源向平台接收兩種類型的資料：

- **即時資料：** 在Audience Manager的資料收集伺服器上即時捕獲的資料。 此資料用於Audience Manager以填充基於規則的特徵，並將在最短的延遲時間內在平台中顯示。
- **配置檔案資料：** Audience Manager使用即時資料和附加資料來導出客戶配置檔案。 這些配置檔案用於填充段實現上的身份圖和特徵。

Audience Manager源將這些資料類型映射到體驗資料模型(XDM)架構，然後將它們發送到平台。 即時資料以XDM ExperienceEvent資料形式發送，而配置檔案資料以XDM Individual Profile資料形式發送。

有關詳細資訊，請閱讀上的指南 [在UI中建立Audience Manager源連接](../../tutorials/ui/create/adobe-applications/audience-manager.md)。

## 什麼是體驗資料模型(XDM)?

XDM是一個公開記錄的規範，它提供了一個標準化框架，平台通過該框架組織客戶體驗資料。

遵守XDM標準可以統一整合客戶體驗資料，使資料傳輸和資訊收集更加容易。

有關XDM在Experience Platform中的使用方式的詳細資訊，請閱讀 [XDM系統概述](../../../xdm/home.md)。 要詳細瞭解XDM架構在配置檔案和事件之間的結構化方式，請閱讀 [架構組合基礎](../../../xdm/schema/composition.md)。

## XDM架構示例

下面是映射到平台中XDM ExperienceEvent和XDM Individual Profile的Audience Manager結構示例。

### ExperienceEvent — 用於即時資料和已載入資料

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM個人配置檔案 — 用於配置檔案資料

![](images/aam-profile-xdm-for-profile-data.png)

有關如何將欄位從Audience Manager映射到XDM的資訊，請閱讀上的文檔 [Audience Manager映射欄位](./mapping/audience-manager.md)。

## 平台上的資料管理

### 資料集

資料集是用於資料集合（通常是表）的儲存和管理構造，該資料集包含模式（列）和欄位（行），並由資料連接提供。 Audience Manager資料包括即時資料、入站資料和配置檔案資料。 要查找Audience Manager資料集，請使用UI中的搜索函式以及為每種類型的資料提供的命名約定。

預設情況下，Audience Manager資料集會為Profile禁用，並且用戶能夠根據其使用情形啟用或禁用資料集。 建議不要禁用將用於配置檔案中段成員資格的資料集。

>[!NOTE]
>
>實AAM時是資料湖中唯一的資料集。 所有其他Audience Manager資料集 [!DNL Profile]，如果為 [!DNL Profile]。 如果未為 [!DNL Profile]，則它們不會接收任何資料，並且它們將顯示為空。

| 資料集名稱 | 說明 | 類別 |
| --- | --- | --- |
| 實AAM時 | 此資料集包含通過Audience ManagerDCS端點上的直接命中和Audience Manager配置檔案的標識映射收集的資料。 使此資料集處於啟用狀態，以便進行配置檔案接收。 | 體驗活動 |
| 實AAM時配置檔案更新 | 該資料集支援對Audience Manager特徵和片段的即時目標。 它包括Edge區域路由、特性和段成員資格的資訊。 使此資料集處於啟用狀態，以便進行配置檔案接收。 資料集中的資料不作為批處理顯示。 您可以啟用 **[!UICONTROL 配置檔案]** 切換，將資料直接接收到配置檔案。 | 記錄 |
| 設AAM備資料 | 具有ECID的設備資料和在Audience Manager中聚合的相應段實現。 資料集中的資料不作為批處理顯示。 您可以啟用 **[!UICONTROL 配置檔案]** 切換，將資料直接接收到配置檔案。 | 記錄 |
| 設AAM備配置檔案資料 | 用於Audience Manager連接器診斷。 資料集中的資料不作為批處理顯示。 您可以啟用 **[!UICONTROL 配置檔案]** 切換，將資料直接接收到配置檔案。 | 記錄 |
| 已驗AAM證的配置檔案 | 此資料集包含經過Audience Manager驗證的配置檔案。 資料集中的資料不作為批處理顯示。 您可以啟用 **[!UICONTROL 配置檔案]** 切換，將資料直接接收到配置檔案。 | 記錄 |
| 已驗AAM證的配置檔案元資料 | 用於Audience Manager連接器診斷。 資料集中的資料不作為批處理顯示。 您可以啟用 **[!UICONTROL 配置檔案]** 切換，將資料直接接收到配置檔案。 | 記錄 |
| 設AAM備資料回填 | 資料集從過去的設備中導入資料。 這包含ECID和在Audience Manager中聚合的相應段實現。 資料集中的資料不作為批處理顯示。 您可以啟用 **[!UICONTROL 配置檔案]** 切換，將資料直接接收到配置檔案。 | 記錄 |
| 已驗AAM證的配置檔案回填 | 資料集，從而引入過去經過驗證的資料。 這包含經過Audience Manager驗證的配置檔案。 資料集中的資料不作為批處理顯示。 您可以啟用 **[!UICONTROL 配置檔案]** 切換，將資料直接接收到配置檔案。 | 記錄 |

### 連線

Adobe Audience Manager在目錄中建立一個連接：Audience Manager連接。 目錄是Adobe Experience Platform內資料位置和沿襲記錄系統。 連接是Catalog對象，它是特定於客戶的連接器實例。 請閱讀 [目錄服務概述](../../../catalog/home.md) 的子菜單。

### 要分析的段填充影響

首次將Audience Manager段發送到平台時，段填充大小會直接影響配置檔案編號。 這意味著選擇所有段可能會導致配置檔案超出許可證使用權限。 平台還將新資料與歷史資料區分為Profile接收。 具有100個基於第一方身份的段將建立100個配置檔案。 然而，如果同一部門的人口增加到150人，並被納入平台，則資料數將只增加50人，因為只有50個新資料。

您還可以通過以下方式檢查您的帳戶可用的配置檔案使用情況： [許可證使用儀表板](../../../dashboards/guides/license-usage.md)。

## 平台上Audience Manager資料的預期延遲是多少？

| Audience Manager資料 | 類型 | 延遲性 | 附註 |
| --- | --- | --- | --- |
| 即時資料 | 活動 | &lt;25 分鐘 | 從在Audience Manager邊緣節點捕獲到出現在資料湖中的時間。 |
| 即時資料 | 配置檔案更新 | &lt;10 分鐘 | 即時客戶配置檔案的登錄時間。 |
| 即時資料和掛載資料 | 配置檔案更新 | 24至36小時 | 從通過DCS/PCS邊緣資料和已登錄資料捕獲、處理到用戶配置檔案，然後出現在即時客戶配置檔案中的時間。 目前，這些資料並未直接降落在資料湖中。 可以為Audience Manager配置檔案資料集啟用配置檔案切換，以將此資料直接插入即時客戶配置檔案。 |
