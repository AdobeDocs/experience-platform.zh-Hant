---
solution: Experience Platform
title: 在區段定義中遵循同意
description: 瞭解如何在細分操作中遵循個人資料收集和分享的客戶同意偏好設定。
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---

# 在區段定義中遵循同意

>[!NOTE]
>
>本指南說明如何在&#x200B;**區段定義**&#x200B;中遵循同意。

法律隱私權法規(例如[!DNL California Consumer Privacy Act] (CCPA))賦予消費者權利，可選擇退出收集其個人資料或與第三方共用資料。 Adobe Experience Platform提供標準Experience Data Model (XDM)元件，其用意是在即時客戶個人檔案資料中擷取這些客戶同意偏好設定。

如果客戶撤回或拒絕同意分享其個人資料，貴組織在產生行銷活動的受眾時，務必遵守該偏好設定。 本檔案說明如何使用Experience Platform使用者介面，將客戶同意值整合到您的區段定義中。

## 快速入門

接受客戶同意值需要瞭解所涉及的各種[!DNL Adobe Experience Platform]服務。 開始進行本教學課程之前，請確定您熟悉下列服務：

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： Experience Platform組織客戶體驗資料的標準化架構。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的客戶設定檔。
* [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：可讓您從[!DNL Real-Time Customer Profile]資料建立對象。

## 同意結構描述欄位

為了遵循客戶同意和偏好設定，屬於您[!UICONTROL XDM個人設定檔]聯合結構描述之一的結構描述必須包含標準欄位群組&#x200B;**[!UICONTROL 同意和偏好設定]**。

有關欄位群組所提供的每個屬性的結構和預期使用案例的詳細資訊，請參閱[同意和偏好設定參考指南](../../xdm/field-groups/profile/consents.md)。 如需如何將欄位群組新增到結構描述的逐步指示，請參閱[XDM UI指南](../../xdm/ui/resources/schemas.md#add-field-groups)。

將欄位群組新增至[啟用設定檔的結構描述](../../xdm/ui/resources/schemas.md#profile)後，其欄位已用來從您的體驗應用程式中擷取同意資料，您可以在區段規則中使用收集的同意屬性。

## 在區段中處理同意

為了確保區段定義中不包含選擇退出的設定檔，必須在現有區段定義中新增特殊欄位，並在建立任何新區段定義時包含這些欄位。

以下步驟示範如何為兩種型別的選擇退出標幟新增適當的欄位：

1. [!UICONTROL 資料收集]
1. [!UICONTROL 共用資料]

>[!NOTE]
>
>雖然本指南著重於上述兩個選擇退出標幟，您可以設定區段定義以一併納入其他同意訊號。 [同意和偏好設定參考指南](../../xdm/field-groups/profile/consents.md)提供這些選項及其預期使用案例的詳細資訊。

在UI中建置區段定義時，請在&#x200B;**[!UICONTROL 屬性]**&#x200B;下方導覽至&#x200B;**[!UICONTROL XDM個別設定檔]**，然後選取&#x200B;**[!UICONTROL 同意和偏好設定]**，接著選取&#x200B;**[!UICONTROL 識別碼特定]**。 從這裡，您可以看到&#x200B;**[!UICONTROL 資料彙集]**&#x200B;和&#x200B;**[!UICONTROL 共用資料]**&#x200B;的選項。

![](../images/tutorials/opt-outs/consents.png)

從選取&#x200B;**[!UICONTROL 資料集合]**&#x200B;類別開始，然後將&#x200B;**[!UICONTROL 選擇值]**&#x200B;拖曳至區段產生器。 將屬性新增至區段定義時，您可以指定必須包含或排除的[同意值](../../xdm/field-groups/profile/consents.md#choice-values)。

![](../images/tutorials/opt-outs/consent-values.png)

一種方式是排除選擇退出收集其資料的任何客戶。 若要這麼做，請將運運算元設為&#x200B;**[!UICONTROL 不等於]**，然後選擇下列值：

* **[!UICONTROL 否（選擇退出）]**
* **[!UICONTROL 預設為否（選擇退出）]**
* **[!UICONTROL 未知]** （若其他未知則假設拒絕同意）

![](../images/tutorials/opt-outs/collect.png)

在左側邊欄的&#x200B;**[!UICONTROL 屬性]**&#x200B;下，導覽回&#x200B;**[!UICONTROL 同意和偏好設定]**&#x200B;區段，然後選取&#x200B;**[!UICONTROL 共用資料]**。 將其對應的&#x200B;**[!UICONTROL 選擇值]**&#x200B;拖曳到畫布中，並選取與[!UICONTROL 資料集合]選擇值相同的值。 確定兩個屬性之間已建立&#x200B;**[!UICONTROL 或]**&#x200B;關係。

![](../images/tutorials/opt-outs/share.png)

新增&#x200B;**[!UICONTROL 資料收集]**&#x200B;和&#x200B;**[!UICONTROL 共用資料]**&#x200B;同意值至區段定義後，任何選擇退出使用其資料的客戶，都會從產生的對象中排除。 從這裡，您可以繼續自訂區段定義，然後再選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以完成程式。

## 後續步驟

依照本教學課程進行，您現在應該能更清楚瞭解在Experience Platform中建立區段定義時，如何遵循客戶同意和偏好設定。

如需在Experience Platform中管理同意的詳細資訊，請參閱下列檔案：

* [使用Adobe標準進行同意處理](../../landing/governance-privacy-security/consent/adobe/overview.md)
* [使用IAB TCF 2.0標準進行同意處理](../../landing/governance-privacy-security/consent/iab/overview.md)