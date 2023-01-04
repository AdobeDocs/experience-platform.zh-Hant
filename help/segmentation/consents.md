---
keywords: Experience Platform；首頁；熱門主題；選擇退出；分段；分段服務；分段服務；榮譽退出；選擇退出；選擇退出；選擇退出；同意；共用；收集；
solution: Experience Platform
title: 遵循區段中的同意
topic-legacy: overview
description: 了解如何遵循客戶同意偏好設定，以收集個人資料並在區段作業中共用。
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# 遵守區段中的同意

法律隱私權法規，例如 [!DNL California Consumer Privacy Act] (CCPA)提供消費者選擇退出其個人資料的收集或分享權利給第三方。 Adobe Experience Platform提供標準的Experience Data Model(XDM)元件，用於在即時客戶設定檔資料中擷取這些客戶同意偏好設定。

如果客戶因共用其個人資料而撤回或隱匿同意，貴組織在產生行銷活動受眾時，務必遵守該偏好。 本檔案說明如何使用Experience Platform使用者介面，將客戶同意值整合在區段定義中。

## 快速入門

遵循客戶同意值需要了解 [!DNL Adobe Experience Platform] 服務。 開始本教學課程之前，請務必熟悉下列服務：

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md):Platform用來組織客戶體驗資料的標準化架構。
* [[!DNL Real-Time Customer Profile]](../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的客戶設定檔。
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md):可讓您從 [!DNL Real-Time Customer Profile] 資料。

## 同意結構欄位

為了遵守客戶同意和偏好，您的 [!UICONTROL XDM個別設定檔] 聯合架構必須包含標準欄位組 **[!UICONTROL 同意和偏好設定]**.

如需欄位群組所提供每個屬性的結構和預期使用案例的詳細資訊，請參閱 [同意和偏好參考指南](../xdm/field-groups/profile/consents.md). 如需如何將欄位群組新增至架構的逐步指示，請參閱 [XDM UI指南](../xdm/ui/resources/schemas.md#add-field-groups).

欄位群組新增至 [啟用設定檔的結構](../xdm/ui/resources/schemas.md#profile) 而其欄位已用於從體驗應用程式內嵌同意資料，則您可以在區段規則中使用收集的同意屬性。

## 處理細分中的同意

為了確保退出設定檔不包含在區段中，必須在建立任何新區段時，將特殊欄位新增至現有區段並納入。

下列步驟示範如何為兩種選擇退出標幟新增適當欄位：

1. [!UICONTROL 資料收集]
1. [!UICONTROL 共用資料]

>[!NOTE]
>
>雖然本指南著重於上述的兩個選擇退出標幟，您也可以設定區段以併入其他同意訊號。 此 [同意和偏好參考指南](../xdm/field-groups/profile/consents.md) 提供這些選項及其預定使用案例的詳細資訊。

在UI中建立區段時，請在 **[!UICONTROL 屬性]**，導覽至 **[!UICONTROL XDM個別設定檔]**，然後選取 **[!UICONTROL 同意和偏好設定]**. 從這裡，您可以看到 **[!UICONTROL 資料收集]** 和 **[!UICONTROL 共用資料]**.

![](./images/opt-outs/consents.png)

從選取 **[!UICONTROL 資料收集]** 類別，然後拖曳 **[!UICONTROL 選擇值]** 填入區段產生器。 將屬性新增至區段時，您可以指定 [同意值](../xdm/field-groups/profile/consents.md#choice-values) 必須包含或排除。

![](./images/opt-outs/consent-values.png)

一種方法是排除選擇退出並收集其資料的任何客戶。 若要這麼做，請將運算子設為 **[!UICONTROL 不等於]**，並選擇下列值：

* **[!UICONTROL 否（選擇退出）]**
* **[!UICONTROL 預設為否（選擇退出）]**
* **[!UICONTROL 未知]** （若未知，則假設不予同意）

![](./images/opt-outs/collect.png)

在 **[!UICONTROL 屬性]** 在左側邊欄中，導覽回 **[!UICONTROL 同意和偏好設定]** 區段，然後選取 **[!UICONTROL 共用資料]**. 拖曳其對應的 **[!UICONTROL 選擇值]** 並選取與 [!UICONTROL 資料收集] 選項值。 確保 **[!UICONTROL 或]** 在兩個屬性之間建立關係。

![](./images/opt-outs/share.png)

同時使用 **[!UICONTROL 資料收集]** 和 **[!UICONTROL 共用資料]** 新增至區段的同意值，則任何選擇退出使用其資料的客戶，都將從產生的受眾中排除。 您可以在此處繼續自訂區段定義，再選取 **[!UICONTROL 儲存]** 來完成這個過程。

## 後續步驟

依照本教學課程，您現在應該能更清楚了解在Experience Platform中建立區段時，如何遵守客戶同意和偏好設定。

如需在Platform中管理同意的詳細資訊，請參閱下列檔案：

* [使用Adobe標準進行同意處理](../landing/governance-privacy-security/consent/adobe/overview.md)
* [使用IAB TCF 2.0標準的同意處理](../landing/governance-privacy-security/consent/iab/overview.md)