---
title: 發佈流程
description: 瞭解建立程式庫、測試組建以及核准它們以在Adobe Experience Platform中生產的流程。
exl-id: 4885f60b-6401-4ec7-aa1a-29c135087847
source-git-commit: 2d71eafb00098d958c8cff9350caa27bd3f0260d
workflow-type: tm+mt
source-wordcount: '1407'
ht-degree: 66%

---

# 發佈流程 {#publishing-flow}

>[!CONTEXTUALHELP]
>id="platform_tags_publishing_flow"
>title="發佈流程"
>abstract="了解發佈流程所需的使用者權限層級，包括開發、核准和發佈權限。"

>[!NOTE]
>
>Adobe Experience Platform Launch 已進行品牌重塑，現在是 Adobe Experience Platform 中的一套資料彙集技術。 因此，這些產品文件都推出多項幾術語變更。如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

Adobe Experience Platform中的標籤發佈流程是指建立程式庫、測試組建及核准以供生產的程式。

您可以對程式庫採取的可用動作取決於程式庫的狀態和您擁有的權限層級。此外，視發佈流程的上游而定，程式庫的狀態也會影響其內含的資源 (規則、資料元素和擴充功能)。

以下各節說明屬於發佈流程的權限、程式庫狀態和上游詳細資訊。

## 權限 {#permissions}

發佈流程有不同的重要用戶權限層級；尤其是 [!UICONTROL Develop]、[!UICONTROL Approve] 和 [!UICONTROL Publish] 屬性權限：

* **[!UICONTROL Develop]**：包括建立程式庫、組建以進行開發，並提交核准的功能。
* **[!UICONTROL Approve]**：包括建置中繼用並核准中繼組建的功能。
* **[!UICONTROL Publish]**：包括發佈已核准程式庫的功能。

這些權限並未包括在內。若要讓一個人員從頭到尾執行工作流程，該人員必須在指定屬性內被授予所有這三項權限。

如需管理標籤許可權的詳細資訊，請參閱[使用者許可權指南](../administration/user-permissions.md)。

## 程式庫狀態 {#state}

就發佈流程而言，程式庫所處的狀態共有四種基本狀態：

* [[!UICONTROL Development]](#development)
* [[!UICONTROL Submitted]](#submitted)
* [[!UICONTROL Approved]](#approved)
* [[!UICONTROL Published]](#published)

這四種狀態在 **[!UICONTROL Publishing Flow]** 標籤內會以欄的形式呈現。

![](./images/approval-workflow/flow-ui.png)

您必須執行特定動作，才能讓程式庫在這些狀態之間移動。下圖概述讓資料庫在狀態之間切換的各動作：

![](./images/approval-workflow/library-state.png)

### [!UICONTROL Development] {#development}

建立新程式庫時，它們會以 [!UICONTROL Development] 狀態啟動。必須在程式庫處於 [!UICONTROL Development] 時才能對程式庫進行任何變更。完成開發和測試後，即提交程式庫進行核准。

下表概述處於 [!UICONTROL Development] 狀態的程式庫可用的動作：

| 動作 | 說明 |
| --- | --- |
| [!UICONTROL Edit] | 使用 [!UICONTROL Edit Library] 畫面新增或移除程式庫的元件。 |
| [!UICONTROL Build to Development] | 為程式庫建立組建。編譯組建並將組建部署到指派該程式庫的環境。如果該程式庫並未指派給環境或包含已在上游中定義的變更，此步驟則會失敗。 |
| [!UICONTROL Submit for Approval] | 請從開發環境解除指派該程式庫，然後將程式庫移至 [!UICONTROL Submitted] 欄，以供擁有核准權限的用戶作業。程式庫的最新組建必須成功，才能啟用此選項。 |
| [!UICONTROL Submit & Build to Staging] | 這只能由同時具有開發及核准許可權的使用者執行。 此動作會從開發環境中取消指派程式庫、將程式庫移動到[!UICONTROL Submitted]狀態，並將程式庫建置到中繼環境。 程式庫的最新組建必須成功，才能啟用此選項。 |
| [!UICONTROL Approve for Publishing] | 這只能由同時具有開發及核准許可權的使用者執行。 此動作會從開發環境中取消指派程式庫，並將其移至[!UICONTROL Approved]狀態 — 完全略過預備環境和[!UICONTROL Submitted]狀態。 程式庫的最新組建必須成功，才能啟用此選項。 |
| [!UICONTROL Approve & Publish to Production] | 這只能由擁有開發、核准和發佈許可權的使用者執行。 此動作會從開發環境中取消指派程式庫，將其移動到[!UICONTROL Approved]狀態，然後發佈到生產環境。 生產組建完成後，程式庫將會移至[!UICONTROL Published]狀態。 程式庫的最新組建必須成功，才能啟用此選項。 |
| [!UICONTROL Delete] | 從系統中移除程式庫。 這不會將組建從環境移除。 |

### [!UICONTROL Submitted] {#submitted}

程式庫處於 [!UICONTROL Submitted] 狀態時，擁有核准權限的用戶可以在中繼環境中測試程式庫。測試完成後，則可核准或拒絕程式庫。已拒絕的組建會回到 [!UICONTROL Development]，以便於在重新啟動發佈流程前進行其他變更。

下表概述處於 [!UICONTROL Submitted] 狀態的程式庫可用的動作：

| 動作 | 說明 |
| --- | --- |
| [!UICONTROL Open] | 檢視程式庫的內容。在 [!UICONTROL Development] 欄以外的程式庫不允許變更。如果需要變更，則應拒絕程式庫，以便在 [!UICONTROL Development] 中進行變更。 |
| [!UICONTROL Build for Staging] | 在中繼環境中建置程式庫以進行部署。 |
| [!UICONTROL Approve for Publishing] | 將程式庫移至 [!UICONTROL Approved] 欄，以便擁有發佈權限的用戶進行作業。 |
| [!UICONTROL Approve & Publish to Production] | 這只能由同時具有核准和發佈許可權的使用者執行。 此動作會從預備環境中取消指派程式庫，將其移動到[!UICONTROL Approved]狀態，然後發佈到生產環境。 生產組建完成後，程式庫將會移至[!UICONTROL Published]狀態。 不需要在中繼環境中成功建置，即可使用我們的來執行。 |
| [!UICONTROL Reject] | 從中繼環境解除程式庫的指派，並將程式移回 [!UICONTROL Development] 欄，進行進一步的變更。 |

### [!UICONTROL Approved] {#approved}

核准程式庫後，擁有發佈權限的用戶可以發佈或拒絕程式庫。已拒絕的組建會回到 [!UICONTROL Development]，以便於在發佈流程再次開始前進行進一步的變更。

下表概述處於 [!UICONTROL Approved] 狀態的程式庫可用的動作：

| 動作 | 說明 |
| --- | --- |
| [!UICONTROL Open] | 檢視程式庫的內容。在 [!UICONTROL Development] 欄以外的程式庫不允許變更。如果需要變更，則應拒絕程式庫，以便在 [!UICONTROL Development] 中進行變更。 |
| [!UICONTROL Build and Publish to Production] | 從中繼環境解除程式庫的指派、指派程式庫至生產環境，然後進行部署。<br><br>**重要**：選取此選項時，您的程式庫會在生產環境中上線。請確保在選取此選項前，程式庫包含您想要的變更。 |
| [!UICONTROL Reject] | 從中繼環境解除程式庫的指派，並將程式移至 [!UICONTROL Development] 欄，進行進一步的變更。 |

### [!UICONTROL Published] {#published}

[!UICONTROL Published]欄顯示已發佈哪些程式庫及其發佈日期。 目前發佈的程式庫旁邊會顯示一個綠色圓點。 除非您已在先前的程式庫上執行重新發佈，否則這永遠是欄頂端的程式庫。

| 動作 | 說明 |
| --- | --- |
| [!UICONTROL Open] | 檢視程式庫的內容。在 [!UICONTROL Development] 欄以外的程式庫不允許變更。如果您想要變更生產環境中的內容，則須建立一個新的程式庫並透過完整的發佈程序移動。 |
| [!UICONTROL Republish] | 此動作僅適用於最近發佈的五個程式庫，且僅限於生產環境(A)已設定關閉「封存」選項，且(b)在建置時使用[!UICONTROL Managed by Adobe]主機時。 |
| [!UICONTROL Download] | 此動作僅適用於最近發佈的五個程式庫，且僅當生產環境為(A)在設定了「封存」選項，且(b)在建置時使用[!UICONTROL Managed by Adobe]主機時，才可使用。 |

## 上游 {#upstream}

發佈第一個程式庫後，在透過發佈流程移動較新的程式庫時，應了解上游的角色。

如果程式庫目前處於 [!UICONTROL Development]、[!UICONTROL Submitted] 或 [!UICONTROL Approved] 階段，該程式庫將會繼承上游任一程式庫的規則、資料元素和擴充功能。這些繼承的資源構成各程式庫行經發佈流程時的「基準」。基本上，您可以將每個新程式庫想成是對於上游所建立的基準所進行的一系列變更。如此即可確保在發佈新的迭代時，不會遭到上一個程式庫意外覆寫。

上游中的內容取決於程式庫目前的階段。例如，處於 [!UICONTROL Approved] 欄中的程式庫僅會繼承來自於 [!UICONTROL Published] 程式庫的資源，而在 [!UICONTROL Development] 下方的程式庫則會繼承所有其他欄的資源。

![](./images/approval-workflow/upstream.png)

在UI中編輯程式庫時，從上游繼承的所有資源都會在&#x200B;**[!UICONTROL Resources Upstream]**&#x200B;區段中呈現。 若要檢視這些資源，請選取區段標題下方的展開標籤。

![](./images/approval-workflow/upstream-collapse.png)

此區段隨即展開，顯示從上游繼承的個別資源。您可以使用左邊欄來篩選 [!UICONTROL Rules], [!UICONTROL Data Elements] 與 [!UICONTROL Extensions]，或使用搜尋列依名稱查詢特定資源。

![](./images/approval-workflow/upstream-resources.png)

## 後續步驟

本指南提供Adobe Experience Platform中程式庫發佈流程的整體概觀。 若要了解更多如何發佈程式庫的資訊，請參閱[發佈概觀](./overview.md)。
