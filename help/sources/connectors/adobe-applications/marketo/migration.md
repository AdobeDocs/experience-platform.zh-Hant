---
title: 使用Marketo Engage來源將ECID對應從人員移轉至活動
description: 瞭解如何使用Marketo Engage來源，將ECID對應從人員資料集移轉至活動資料集。
source-git-commit: 0c695e11e7d7c14ef7e047cd007668e1099bf127
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 將ECID對應從移轉 [!DNL Person] 資料集至 [!DNL Activity] 資料集

您可以將ECID對應從您的 [!DNL Marketo Engage Person] 將資料集新增至 [!DNL Activity] 資料集，以提供更穩定的資料擷取和身分管理行為。 此外，此移轉會處理下列問題：

| 問題 | 解決方案 |
| --- | --- |
| 當 [!DNL Marketo Person] 資料集具有多個ECID的連結，資料擷取會在 [Experience Data Model (XDM)記錄中的身分總數超過20](../../../../identity-service/guardrails.md). | 透過將ECID欄位對應移轉至 [!DNL Activity]，您可確定來自 [!DNL Marketo Person] 資料流會維持在限制內，因此可讓資料擷取成功。 |
| 每當 [!DNL Marketo Person] 資料集是使用ECID擷取的，其中所有ECID上的時間戳記皆來自 [!DNL Marketo Person] 資料集會以人員記錄的上次更新時間戳記更新。 這可能會導致 [從身分圖表刪除較新的身分是不正確的](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). | 將ECID欄位對應移轉至 [!DNL Activity]，Identity Service可正確反映ECID的時間戳記，而Identity Service的「先進先出」機制可提供較穩定的行為。 |
| 透過擷取ECID時 [!DNL Marketo Person] 資料流中，新新增的ECID不會擷取到Experience Platform，除非 [!DNL Person] 記錄位置 [!DNL Marketo]. | 當新的ECID連結至 [!DNL Person] 記錄位置 [!DNL Marketo]，您可透過擷取 [!DNL Marketo Activity] 資料流並在Experience Platform時立即提示身分圖表更新。 |

基本上，您必須：

* 更新您的 [!DNL Marketo Activity] 資料流。
* 更新您的 [!DNL Marketo Person] 資料流。

## 更新 [!DNL Marketo Activity] 資料流 {#update-activity-dataflow}

請依照下列步驟更新您的 [!DNL Marketo Activity] 資料流：

* 在Experience PlatformUI中，導覽至 *來源* workspace並尋找您現有的資料流 [!DNL Marketo Activity] 資料。
* 資料流已啟用，請選取省略符號(`...`)，然後選取「 」 **[!UICONTROL 更新資料流]**.
* 然後，選取 **[!UICONTROL 下一個]** 直到您到達 *對應* 介面。
* 在 *對應* 介面，選取 **[!UICONTROL 新欄位]** 然後選取 **[!UICONTROL 新增計算欄位]**. 您必須從此新增下列專案：

| 來源資料集 | xdm目標欄位 |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>如果您更新至現有的 [!DNL Marketo] 資料流僅包含新增或移除ECID對應欄位，然後資料流會自動略過歷史回填作業。 只有在發生「造訪網頁」和「點按網頁」等活動型別時，才會發生新資料擷取。

## 更新 [!DNL Marketo Person] 資料流 {#update-person-dataflow}

請依照下列步驟更新您的 [!DNL Marketo Person] 資料流：

* 在Experience PlatformUI中，導覽至 *來源* workspace並尋找您現有的資料流 [!DNL Marketo Person] 資料。
* 資料流已啟用，請選取省略符號(`...`)，然後選取「 」 **[!UICONTROL 更新資料流]**.
* 然後，選取 **[!UICONTROL 下一個]** 直到您到達 *對應* 介面。
* 在 *對應* 介面，移除對應至的計算欄位 `identityMap` 然後選取 **[!UICONTROL 下一個]** 和 **[!UICONTROL 儲存並擷取]**.

>[!NOTE]
>
>如果您更新至現有的 [!DNL Marketo] 資料流僅包含新增或移除ECID對應欄位，然後資料流會自動略過歷史回填作業。 先前已擷取的ECID時間戳記將維持不變。 只有在擷取與現有ECID對應的新資料時，才會更新這些ID。

## 後續步驟

閱讀本檔案後，您現在瞭解如何將ECID對應從 [!DNL Marketo Person] 資料集至 [!DNL Marketo Activity] 資料集。 如需詳細資訊，請閱讀以下內容 [!DNL Marketo] 檔案：

* [建立資料流以進行內嵌 [!DNL Marketo] 要Experience Platform的資料](../../../tutorials/ui/create/adobe-applications/marketo.md).
* [欄位對應指南](../mapping/marketo.md).