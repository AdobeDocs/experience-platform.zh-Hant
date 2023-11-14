---
solution: Experience Platform
title: 在區段中接受同意
description: 瞭解如何在區段作業中遵循個人資料收集和分享的客戶同意偏好設定。
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

# 在區段中接受同意

>[!NOTE]
>
>本指南說明如何在中遵循同意 **區段定義**.

法律隱私權法規，例如 [!DNL California Consumer Privacy Act] (CCPA)為消費者提供選擇退出的權利，拒絕收集他們的個人資料或與第三方共用。 Adobe Experience Platform提供標準Experience Data Model (XDM)元件，其用意是在即時客戶個人檔案資料中擷取這些客戶同意偏好設定。

如果客戶撤回或拒絕同意分享其個人資料，貴組織在產生行銷活動的受眾時，務必遵守該偏好設定。 本檔案說明如何使用Experience Platform使用者介面，將客戶同意值整合到您的區段定義中。

## 快速入門

接受客戶同意值需要瞭解各種 [!DNL Adobe Experience Platform] 涉及的服務。 開始進行本教學課程之前，請確定您熟悉下列服務：

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md)：Platform組織客戶體驗資料的標準化架構。
* [[!DNL Real-Time Customer Profile]](../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的客戶設定檔。
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md)：可讓您從建立對象 [!DNL Real-Time Customer Profile] 資料。

## 同意結構描述欄位

為了遵循客戶同意和偏好設定，屬於您的其中一種結構描述 [!UICONTROL XDM個別設定檔] 聯合結構描述必須包含標準欄位群組 **[!UICONTROL 同意和偏好設定]**.

有關欄位群組提供的每個屬性的結構和預期使用案例的詳細資訊，請參閱 [同意和偏好設定參考指南](../xdm/field-groups/profile/consents.md). 有關如何將欄位群組新增到結構描述的逐步指示，請參閱 [XDM UI指南](../xdm/ui/resources/schemas.md#add-field-groups).

將欄位群組新增至後 [啟用設定檔的結構描述](../xdm/ui/resources/schemas.md#profile) 及其欄位已用來從體驗應用程式中擷取同意資料，您可以在區段規則中使用收集的同意屬性。

## 在區段中處理同意

為了確保區段定義中不包含選擇退出的設定檔，必須在現有區段定義中新增特殊欄位，並在建立任何新區段定義時包含這些欄位。

以下步驟示範如何為兩種型別的選擇退出標幟新增適當的欄位：

1. [!UICONTROL 資料收集]
1. [!UICONTROL 共用資料]

>[!NOTE]
>
>雖然本指南著重於上述兩個選擇退出標幟，您可以設定區段定義以一併納入其他同意訊號。 此 [同意和偏好設定參考指南](../xdm/field-groups/profile/consents.md) 提供這些選項及其預期使用案例的詳細資訊。

在UI中建立區段定義時，位於 **[!UICONTROL 屬性]**，導覽至 **[!UICONTROL XDM個別設定檔]**，然後選取 **[!UICONTROL 同意和偏好設定]**. 從這裡，您可以檢視的選項 **[!UICONTROL 資料彙集]** 和 **[!UICONTROL 共用資料]**.

![](./images/opt-outs/consents.png)

首先，選取 **[!UICONTROL 資料彙集]** 類別，然後拖曳 **[!UICONTROL 選擇值]** 放入區段產生器中。 將屬性新增至區段定義時，您可以指定 [同意值](../xdm/field-groups/profile/consents.md#choice-values) 必須包含或排除的專案。

![](./images/opt-outs/consent-values.png)

一種方式是排除選擇退出收集其資料的任何客戶。 若要這麼做，請將運運算元設為 **[!UICONTROL 不等於]**，然後選擇下列值：

* **[!UICONTROL 否（選擇退出）]**
* **[!UICONTROL 「否」的預設值（選擇退出）]**
* **[!UICONTROL 未知]** （若不明，則假設將拒絕同意）

![](./images/opt-outs/collect.png)

在 **[!UICONTROL 屬性]** 在左側邊欄中，導覽回 **[!UICONTROL 同意和偏好設定]** 區段，然後選取 **[!UICONTROL 共用資料]**. 拖曳其對應的 **[!UICONTROL 選擇值]** ，並選取與相同的值 [!UICONTROL 資料彙集] 選擇值。 確保 **[!UICONTROL 或]** 兩個屬性之間的關係已建立。

![](./images/opt-outs/share.png)

同時使用 **[!UICONTROL 資料彙集]** 和 **[!UICONTROL 共用資料]** 將同意值新增至區段定義，則任何選擇退出使用其資料的客戶，都會從產生的對象中排除。 從這裡，您可以繼續自訂區段定義，然後再選取 **[!UICONTROL 儲存]** 以完成程式。

## 後續步驟

依照本教學課程進行，您現在應該更瞭解在Experience Platform中建立區段定義時，如何遵循客戶同意和偏好設定。

如需在Platform中管理同意的詳細資訊，請參閱下列檔案：

* [使用Adobe標準進行同意處理](../landing/governance-privacy-security/consent/adobe/overview.md)
* [使用IAB TCF 2.0標準進行同意處理](../landing/governance-privacy-security/consent/iab/overview.md)