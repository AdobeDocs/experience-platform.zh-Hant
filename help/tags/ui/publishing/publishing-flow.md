---
title: 發佈流
description: 瞭解建立庫、測試構建以及批准它們在Adobe Experience Platform生產的過程。
exl-id: 4885f60b-6401-4ec7-aa1a-29c135087847
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 36%

---

# 發佈流程

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

Adobe Experience Platform的標籤發佈流是指建立庫、測試生成並批准它們以用於生產的過程。

您可以對程式庫採取的可用動作取決於程式庫的狀態和您擁有的權限層級。此外，視發佈流程的上游而定，程式庫的狀態也會影響其內含的資源 (規則、資料元素和擴充功能)。

以下各節說明屬於發佈流程的權限、程式庫狀態和上游詳細資訊。

## 權限 {#permissions}

對於發佈流程而言，用戶權限的級別不同；具體而言， [!UICONTROL 開發]。 [!UICONTROL 批准], [!UICONTROL 發佈] 產權：

* **[!UICONTROL 開發]**:包括建立庫、構建以供開發和提交以供審批的能力。
* **[!UICONTROL 批准]**:包括生成用於轉移和批准轉移生成的能力。
* **[!UICONTROL 發佈]**:包括發佈已批准的庫的功能。

這些權限並未包括在內。若要讓一個人員從頭到尾執行工作流程，該人員必須在指定屬性內被授予所有這三項權限。

查看 [用戶權限指南](../administration/user-permissions.md) 的子菜單。

## 程式庫狀態 {#state}

就發佈流程而言，程式庫所處的狀態共有四種基本狀態：

* [[!UICONTROL 開發]](#development)
* [[!UICONTROL 已提交]](#submitted)
* [[!UICONTROL 已核准]](#approved)
* [[!UICONTROL 已發佈]](#published)

這四個狀態在 **[!UICONTROL 發佈流]** 頁籤。

![](./images/approval-workflow/flow-ui.png)

您必須執行特定動作，才能讓程式庫在這些狀態之間移動。下圖概述讓資料庫在狀態之間切換的各動作：

![](./images/approval-workflow/library-state.png)

### [!UICONTROL 開發] {#development}

建立新庫時，它們將在 [!UICONTROL 開發] 狀態。 必須在庫位於 [!UICONTROL 開發]。 完成開發和測試後，即提交程式庫進行核准。

下表概述了中的庫的可用操作 [!UICONTROL 開發] 狀態：

| 動作 | 說明 |
| --- | --- |
| [!UICONTROL 編輯] | 使用 [!UICONTROL 編輯庫] 的子菜單。 |
| [!UICONTROL 構建到開發] | 為程式庫建立組建。編譯組建並將組建部署到指派該程式庫的環境。如果該程式庫並未指派給環境或包含已在上游中定義的變更，此步驟則會失敗。 |
| [!UICONTROL 提交以進行核准] | 從開發環境中取消分配庫，並將庫移到 [!UICONTROL 已提交] 列，用於具有要處理的批准權限的用戶。 庫的最新生成必須成功才能啟用此選項。 |
| [!UICONTROL 提交並生成到暫存] | 只能由具有「開發」和「批准」權限的用戶執行。 此操作將從開發環境中取消分配庫，將庫移到 [!UICONTROL 已提交] 並將庫構建到暫存環境。 庫的最新生成必須成功才能啟用此選項。 |
| [!UICONTROL 核准以發佈] | 只能由具有「開發」和「批准」權限的用戶執行。 此操作將從開發環境中取消分配庫並將其移到 [!UICONTROL 已批准] 狀態 — 跳過暫存環境和 [!UICONTROL 已提交] 完全歸州。 庫的最新生成必須成功才能啟用此選項。 |
| [!UICONTROL 批准並發佈到生產] | 只能由具有「開發」、「批准」和「發佈」權限的用戶執行。 此操作將從開發環境中取消分配庫，並將其移到 [!UICONTROL 已批准] 並發佈到製作中。 在完成生產構建後，庫將移至 [!UICONTROL 已發佈] 狀態。 庫的最新生成必須成功才能啟用此選項。 |
| [!UICONTROL 刪除] | 從系統中刪除庫。 這不會將組建從環境移除。 |

### [!UICONTROL 已提交] {#submitted}

當庫位於 [!UICONTROL 已提交] 狀態，具有批准權限的用戶可以test暫存環境中的庫。 測試完成後，則可核准或拒絕程式庫。已拒絕的生成返回 [!UICONTROL 開發] 這樣，在重新啟動發佈流之前可以進行其他更改。

下表概述了中的庫的可用操作 [!UICONTROL 已提交] 狀態：

| 動作 | 說明 |
| --- | --- |
| [!UICONTROL 開啟] | 檢視程式庫的內容。不允許對外部的庫進行更改 [!UICONTROL 開發] 的雙曲餘切值。 如果需要更改，應拒絕庫，以便可以在 [!UICONTROL 開發]。 |
| [!UICONTROL 為測試環境建置] | 在中繼環境中建置程式庫以進行部署。 |
| [!UICONTROL 核准以發佈] | 將庫移到 [!UICONTROL 已批准] 列，用於具有要處理的發佈權限的用戶。 |
| [!UICONTROL 批准並發佈到生產] | 只能由具有「批准」和「發佈」權限的用戶執行。 此操作將從暫存環境中取消分配庫，並將其移到 [!UICONTROL 已批准] 並發佈到製作中。 在完成生產構建後，庫將移至 [!UICONTROL 已發佈] 狀態。 在過渡環境中不成功構建，就可以使用我們的系統執行此操作。 |
| [!UICONTROL 拒絕] | 從轉移環境中取消分配庫並將庫移回 [!UICONTROL 開發] 的子菜單。 |

### [!UICONTROL 已核准] {#approved}

核准程式庫後，擁有發佈權限的用戶可以發佈或拒絕程式庫。已拒絕的生成返回 [!UICONTROL 開發] 以便在發佈流再次開始之前進行進一步更改。

下表概述了中的庫的可用操作 [!UICONTROL 已批准] 狀態：

| 動作 | 說明 |
| --- | --- |
| [!UICONTROL 開啟] | 檢視程式庫的內容。不允許對外部的庫進行更改 [!UICONTROL 開發] 的雙曲餘切值。 如果需要更改，應拒絕庫，以便可以在 [!UICONTROL 開發]。 |
| [!UICONTROL 建置並發佈到生產環境] | 從中繼環境解除程式庫的指派、指派程式庫至生產環境，然後進行部署。<br><br>**重要**：選取此選項時，您的程式庫會在生產環境中上線。請確保在選取此選項前，程式庫包含您想要的變更。 |
| [!UICONTROL 拒絕] | 從轉移環境取消分配庫並將庫移動到 [!UICONTROL 開發] 的子菜單。 |

### [!UICONTROL 已發佈] {#published}

的 [!UICONTROL 已發佈] 列顯示已發佈的庫及其發佈日期。 當前發佈的庫旁邊將顯示一個綠點。 除非您對前一個庫執行了重新發佈，否則它將始終是列頂部的庫。

| 動作 | 說明 |
| --- | --- |
| [!UICONTROL 開啟] | 檢視程式庫的內容。不允許對外部的庫進行更改 [!UICONTROL 開發] 的雙曲餘切值。 如果您想要變更生產環境中的內容，則須建立一個新的程式庫並透過完整的發佈程序移動。 |
| [!UICONTROL 重新發佈] | 此操作僅在最近發佈的五個庫上可用，並且僅當生產環境(A)配置了「存檔」選項關閉，(b)使用 [!UICONTROL 按Adobe管理] 主機。 |
| [!UICONTROL 下載] | 此操作僅在最近發佈的五個庫上可用，並且僅當生產環境(A)配置了「存檔」選項，(b)使用 [!UICONTROL 按Adobe管理] 主機。 |

## 上游 {#upstream}

發佈第一個程式庫後，在透過發佈流程移動較新的程式庫時，應了解上游的角色。

如果庫當前位於 [!UICONTROL 開發]。 [!UICONTROL 已提交]或 [!UICONTROL 已批准] 階段，該庫將繼承上游所有庫的規則、資料元素和擴展。 這些繼承的資源構成各程式庫行經發佈流程時的「基準」。基本上，您可以將每個新程式庫想成是對於上游所建立的基準所進行的一系列變更。如此即可確保在發佈新的迭代時，不會遭到上一個程式庫意外覆寫。

上游中的內容取決於程式庫目前的階段。例如， [!UICONTROL 已批准] 列僅從繼承資源 [!UICONTROL 已發佈] 庫，而庫位於 [!UICONTROL 開發] 從所有其他列繼承資源。

![](./images/approval-workflow/upstream.png)

在UI中編輯庫時，從上游繼承的所有資源都在 **[!UICONTROL 上游資源]** 的子菜單。 若要檢視這些資源，請選取區段標題下方的展開標籤。

![](./images/approval-workflow/upstream-collapse.png)

此區段隨即展開，顯示從上游繼承的個別資源。可以使用左滑軌在 [!UICONTROL 規則]。 [!UICONTROL 資料元素], [!UICONTROL 擴展]或使用搜索欄按名稱查找特定資源。

![](./images/approval-workflow/upstream-resources.png)

## 後續步驟

本指南概要介紹了Adobe Experience Platform圖書館的出版流程。 若要了解更多如何發佈程式庫的資訊，請參閱[發佈概觀](./overview.md)。
