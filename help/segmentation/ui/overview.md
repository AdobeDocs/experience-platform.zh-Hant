---
solution: Experience Platform
title: Segmentation Service UI指南
description: 瞭解如何在Adobe Experience Platform UI中建立和管理對象和區段定義。
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: acfe91144175e136955ffd9f0cdae2c351217c16
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---

# Segmentation Service UI指南

[!DNL Adobe Experience Platform Segmentation Service] 提供使用者介面，用於建立和管理對象和區段定義。

## 快速入門

使用對象和區段定義需要瞭解各種 [!DNL Experience Platform] 與細分有關的服務。 閱讀本使用手冊前，請先檢閱以下服務的檔案：

- [[!DNL Segmentation Service]](../home.md)： [!DNL Segmentation Service] 可讓您對儲存在中的資料進行分段 [!DNL Experience Platform] 和歸入較小群組的個人（例如客戶、潛在客戶、使用者或組織）相關的資訊。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md)：可透過橋接正在被擷取到的不同資料來源的身分，以建立客戶設定檔 [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Platform] 組織客戶體驗資料。 為善用分段，請確保您的資料已根據 [資料模型化的最佳實務](../../xdm/schema/best-practices.md).

您也應該瞭解在本檔案中使用的以下主要辭彙，並瞭解它們之間的差異：

- **對象**：一組具有類似行為和/或特徵的人。 此人員集合可透過Adobe Experience Platform使用區段定義（平台產生的對象）、對象構成產生，或從外部來源（例如自訂上傳） （外部產生的對象）產生。
- **區段定義**：Adobe Experience Platform用來說明目標對象之關鍵特性或行為的規則。
- **區段**：將設定檔分隔為對象的動作。

## 概觀

在Experience Platform UI中，選取 **[!UICONTROL 受眾]** 在左側導覽以開啟 **[!UICONTROL 概觀]** 標籤顯示 [!UICONTROL 受眾] 儀表板。

>[!NOTE]
>
>如果您的組織剛開始使用Platform，但尚未建立作用中的設定檔資料集或合併原則， [!UICONTROL 受眾] 儀表板不可見。 而是 [!UICONTROL 概觀] 索引標籤會顯示連結和檔案，以幫助您開始使用對象。

### [!UICONTROL 受眾] 儀表板 {#segments-dashboard}

此 **[!UICONTROL 受眾]** 控制面板會概述與貴組織受眾資料相關的關鍵量度。

若要進一步瞭解，請造訪 [受眾控制面板指南](../../dashboards/guides/audiences.md).

![畫面隨即顯示對象控制面板。 它會顯示各種Widget，包括對象規模、依身分割槽分的設定檔、身分重疊，以及對象規模變更趨勢。](../../dashboards/images/segments/dashboard-overview.png)

## 瀏覽 {#browse}

選取 **[!UICONTROL 瀏覽]** 索引標籤以檢視對象入口網站。 Audience Portal提供屬於您組織和沙箱的所有受眾清單，並包含設定檔計數、來源、建立日期、上次修改日期、標籤和劃分等詳細資訊。

此外，Audience Portal可讓您使用「區段產生器」或「對象構成」建立新對象，以及將外部產生的對象匯入Platform。

如需對象入口網站的詳細資訊，請參閱 [Audience Portal概述](./audience-portal.md).

## 組合 {#compositions}

選取 **[!UICONTROL 組合]** 索引標籤以檢視透過對象構成為您的組織產生的所有對象清單。

![在對象構成中為您組織建立的對象清單。](../images/ui/overview/compositions.png)

依預設，此檢視會列出對象的相關資訊，包括名稱、狀態、建立日期、建立者、上次更新日期和上次更新者。

每個對象旁都會顯示一個省略符號圖示。 選取此專案會顯示對象可用的快速動作清單。

| 動作 | 說明 |
| ------ | ----------- |
| 複製 | 複製選取的對象。 |
| 管理存取權 | 管理屬於對象的存取標籤。 如需存取標籤的詳細資訊，請參閱以下檔案： [管理標籤](../../access-control/abac/ui/labels.md). |
| 刪除 | 刪除選取的對象。 用於下游目的地或為其他對象相依對象的對象 **無法** 都會被刪除。 如需有關刪除對象的詳細資訊，請參閱 [區段常見問題集](../faq.md#lifecycle-states). |

您可以選取 ![自訂表格](../images/ui/overview/customize-table.png) 圖示可變更要顯示的欄位。

![自訂表格按鈕會反白顯示。 選取此按鈕可讓您自訂對象組合頁面上顯示的欄位。](../images/ui/overview/compositions-select-customize-table.png)

此時會出現一個彈出視窗，其中列出可顯示在表格中的所有欄位。

![可針對「構成」區段顯示的屬性。](../images/ui/overview/compositions-customize-table.png)

| 欄位 | 說明 |
| ----- | ----------- | 
| [!UICONTROL 名稱] | 對象名稱。 |
| [!UICONTROL 狀態] | 對象的狀態。 此欄位可能的值包括 `Draft`， `Inactive`、和 `Published`. |
| [!UICONTROL 已建立] | 建立對象的時間和日期。 |
| [!UICONTROL 建立者] | 建立對象的人員名稱。 |
| [!UICONTROL 已更新] | 上次更新對象的時間和日期。 |
| [!UICONTROL 更新者] | 上次更新對象的人員名稱。 |

若要檢視對象的構成方式，請在「 」中選取對象名稱， [!UICONTROL 受眾] 標籤。

將會顯示「對象構成」頁面，其中包含構成對象的建置區塊。 如需如何使用對象構成的詳細資訊，請參閱 [對象構成UI指南](./audience-composition.md).

## 串流區段 {#streaming-segmentation}

串流區段是執行下列作業的能力： [!DNL Platform] 近乎即時，同時著重於資料豐富度。 有了串流區段，現在只要資料進入區段，即可取得區段的資格 [!DNL Platform]，減少排程和執行分段工作的需求。

如需串流區段的詳細資訊，請參閱 [串流區段使用手冊](./streaming-segmentation.md).

>[!NOTE]
>
>為了讓串流細分發揮作用，您需要為組織啟用已排程的分段。 如需啟用已排程分段的詳細資訊，請參閱 [本使用手冊中的串流細分割槽段](#scheduled-segmentation).

## 邊緣分段 {#edge-segmentation}

Edge區段能夠在邊緣即時評估Platform中的受眾，啟用相同頁面和下一頁個人化使用案例。

有關邊緣區段的詳細資訊，請參閱 [邊緣分段UI指南](./edge-segmentation.md)

## 原則違規

>[!NOTE]
>
>原則違規僅適用於建立已指派給目的地的對象。

在您建立完對象後，Adobe Experience Platform資料控管將會分析對象，以確保對象內沒有原則違規。 請參閱 [資料控管概觀](../../data-governance/home.md) 以取得詳細資訊。

![會顯示對象的原則違規。](../images/ui/overview/audience-dule-policy-violations.png)

## 後續步驟和其他資源 {#next-steps}

此 [!DNL Segmentation Service] UI提供豐富的工作流程，允許您從以下來源建立可行銷對象 [!DNL Real-Time Customer Profile] 資料。

若要深入瞭解 [!DNL Segmentation Service]，請繼續閱讀檔案。 若要瞭解如何使用 [!DNL Segmentation Service] API，請閱讀 [[!DNL Segmentation Service] 開發人員指南](../api/overview.md).
