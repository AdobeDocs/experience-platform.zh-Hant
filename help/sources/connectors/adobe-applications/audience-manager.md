---
keywords: Experience Platform；首頁；熱門主題；Audience Manager聯結器；Audience Manager；Audience Manager
solution: Experience Platform
title: Audience Manager來源概觀
description: Adobe Audience Manager來源會將在Audience Manager中收集的第一方資料串流至Adobe Experience Platform。
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: 8ef9fedcc77f39707ef5191988a5b7360e1118cc
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 0%

---

# Audience Manager來源

>[!IMPORTANT]
>
>初次設定時，Adobe Audience Manager來源會傳回錯誤訊息，說明具有指定之身分名稱空間 `namespaceCode={VALUE}` 不存在。 **注意**：在後端， `namespaceCode` 用於表示身分符號。 若要完成整合，您必須：
>
>- [在Identity Service中建立自訂名稱空間](../../../identity-service/features/namespaces.md#create-custom-namespaces) 具有指定的身分符號(`VALUE`) 。
>- 重新內嵌資料。

Adobe Audience Manager來源會串流在Adobe Audience Manager中收集的第一方資料，以在Adobe Experience Platform中啟用。 Audience Manager來源會擷取兩種型別的資料至Platform：

- **即時資料：** 在Audience Manager的資料收集伺服器上即時擷取的資料。 此資料會用於Audience Manager以填入規則型特徵，並會在最短延遲時間內出現在Platform中。
- **設定檔資料：** Audience Manager使用即時和已上線的資料來匯出客戶設定檔。 這些設定檔用於在區段實現時填入身分圖表和特徵。

Audience Manager來源將這些資料型別對應至Experience Data Model (XDM)結構，然後傳送給Platform。 即時資料會以XDM ExperienceEvent資料傳送，而設定檔資料會以XDM個別設定檔資料傳送。

如需詳細資訊，請閱讀以下指南： [在使用者介面中建立Audience Manager來源連線](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## 什麼是Experience Data Model (XDM)？

XDM是公開記錄的規格，提供平台組織客戶體驗資料的標準化架構。

遵守XDM標準可讓客戶體驗資料統一整合，讓您更輕鬆地提供資料及收集資訊。

如需如何在Experience Platform中使用XDM的詳細資訊，請參閱 [XDM系統概覽](../../../xdm/home.md). 若要深入瞭解設定檔與事件之間XDM結構描述的結構方式，請參閱 [結構描述組合的基本面](../../../xdm/schema/composition.md).

## XDM結構描述範例

以下範例為對應至Platform中XDM ExperienceEvent和XDM Individual Profile的Audience Manager結構。

### ExperienceEvent — 適用於即時資料和已上線的資料

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM個別設定檔 — 適用於設定檔資料

![](images/aam-profile-xdm-for-profile-data.png)

如需欄位如何從Audience Manager對應至XDM的詳細資訊，請參閱以下檔案： [Audience Manager對應欄位](./mapping/audience-manager.md).

## 平台上的資料管理

### 資料集

資料集是資料集合的儲存和管理結構，通常是表格，包含結構（欄）和欄位（列），並可透過資料連線使用。 Audience Manager資料包含即時資料、傳入資料和設定檔資料。 若要尋找Audience Manager資料集，請使用UI中的搜尋函式，並針對每種資料型別提供命名慣例。

依預設，設定檔的Audience Manager資料集會停用，使用者可以根據自己的使用案例啟用或停用資料集。 不建議停用用於設定檔中區段成員資格的資料集。

>[!NOTE]
>
>AAM即時是前往資料湖的唯一資料集。 所有其他的Audience Manager資料集都會移至 [!DNL Profile]，若已針對 [!DNL Profile]. 如果它們未啟用 [!DNL Profile]，則不會收到任何資料，且會顯示為空白。

| 資料集名稱 | 說明 | 類別 |
| --- | --- | --- |
| AAM Real-time | 此資料集包含直接點選Audience ManagerDCS端點所收集的資料，以及Audience Manager設定檔的身分對應。 將此資料集保留為設定檔擷取啟用。 | 體驗事件 |
| AAM即時設定檔更新 | 此資料集可讓您即時鎖定Audience Manager特徵和區段。 其中包括Edge區域路由、特徵和區段會籍的相關資訊。 將此資料集保留為設定檔擷取啟用。 資料在資料集中不會顯示為批次。 您可以啟用 **[!UICONTROL 個人資料]** 切換，以直接將資料內嵌至設定檔。 | 記錄 |
| AAM裝置資料 | 具有ECID的裝置資料以及在Audience Manager中彙總的對應區段實現。 資料在資料集中不會顯示為批次。 您可以啟用 **[!UICONTROL 個人資料]** 切換，以直接將資料內嵌至設定檔。 | 記錄 |
| AAM裝置設定檔資料 | 用於Audience Manager聯結器診斷。 資料在資料集中不會顯示為批次。 您可以啟用 **[!UICONTROL 個人資料]** 切換，以直接將資料內嵌至設定檔。 | 記錄 |
| AAM已驗證的設定檔 | 此資料集包含Audience Manager已驗證的設定檔。 資料在資料集中不會顯示為批次。 您可以啟用 **[!UICONTROL 個人資料]** 切換，以直接將資料內嵌至設定檔。 | 記錄 |
| AAM已驗證的設定檔中繼資料 | 用於Audience Manager聯結器診斷。 資料在資料集中不會顯示為批次。 您可以啟用 **[!UICONTROL 個人資料]** 切換，以直接將資料內嵌至設定檔。 | 記錄 |
| AAM裝置資料回填 | 資料集，避免將過去的裝置資料帶入。 這包含Audience Manager中彙總的ECID和對應區段實現。 資料在資料集中不會顯示為批次。 您可以啟用 **[!UICONTROL 個人資料]** 切換以直接將資料內嵌至設定檔。 | 記錄 |
| AAM已驗證的設定檔回填 | 資料集，以免納入過去已驗證的資料。 這包含Audience Manager已驗證的設定檔。 資料在資料集中不會顯示為批次。 您可以啟用 **[!UICONTROL 個人資料]** 切換以直接將資料內嵌至設定檔。 | 記錄 |

### 連線

Adobe Audience Manager會在「目錄：Audience Manager連線」中建立一個連線。 目錄是Adobe Experience Platform中資料位置和歷程的記錄系統。 連線是目錄物件，是客戶特定的聯結器例項。 請閱讀 [目錄服務總覽](../../../catalog/home.md) 有關目錄、連線和聯結器的詳細資訊。

### 區段母體對設定檔影響

當您首次將Audience Manager區段傳送至Platform時，區段母體大小會直接影響設定檔號碼。 這表示選取所有區段可能會造成設定檔使用量超過授權使用權益。 Platform也會將新資料與設定檔擷取的歷史資料區分開來。 具有100個第一方身分的區段將會建立100個設定檔。 不過，如果該區段的母體數量增加至150個且已內嵌至Platform，則設定檔的數量只會增加50個，因為只有50個新設定檔。

您也可以透過檢視您的帳戶可用的設定檔使用情形。 [授權使用情況儀表板](../../../dashboards/guides/license-usage.md).

## 在Platform上Audience Manager資料的預期延遲為何？

| Audience Manager資料 | 類型 | 延遲性 | 附註 |
| --- | --- | --- | --- |
| 即時資料 | 活動 | &lt;25分鐘 | 從Audience Manager邊緣節點擷取到出現在資料湖中的時間。 |
| 即時資料 | 設定檔更新 | &lt;10分鐘 | 登入即時客戶個人檔案的時間。 |
| 即時和已上線的資料 | 設定檔更新 | 24到36小時 | 從透過DCS/PCS Edge資料擷取和上線資料、處理至使用者設定檔，再到出現在即時客戶設定檔中的時間。 目前，此資料不會直接進入資料湖。 可以為Audience Manager設定檔資料集啟用設定檔切換，以便將此資料直接擷取到即時客戶設定檔中。 |
