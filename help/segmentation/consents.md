---
keywords: Experience Platform；首頁；熱門主題；選擇退出；分段；分段服務；分段服務；榮譽退出；選擇退出；選擇退出；選擇退出；同意；共用；收集；
solution: Experience Platform
title: 遵循區段中的同意
topic-legacy: overview
description: 了解如何遵循客戶同意偏好設定，以收集個人資料並在區段作業中共用。
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: 6d11a94d45b4a089ca6960aaf1ce78ae654ebc3f
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 0%

---

# 遵守區段中的同意

[!DNL California Consumer Privacy Act](CCPA)等法律隱私權法規為消費者提供選擇退出其個人資料的收集或與第三方共用的權利。 Adobe Experience Platform提供標準的Experience Data Model(XDM)元件，用於在即時客戶設定檔資料中擷取這些客戶同意偏好設定。

如果客戶因共用其個人資料而撤回或隱匿同意，貴組織在產生行銷活動受眾時，務必遵守該偏好。 本檔案說明如何使用Experience Platform使用者介面，將客戶同意值整合在區段定義中。

## 快速入門

要執行客戶同意值，必須了解所涉的各種[!DNL Adobe Experience Platform]服務。 開始本教學課程之前，請務必熟悉下列服務：

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md):Platform用來組織客戶體驗資料的標準化架構。
* [[!DNL Real-time Customer Profile]](../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的客戶設定檔。
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md):可讓您從資料建立受眾 [!DNL Real-time Customer Profile] 區段。

## 同意結構欄位

為了遵守客戶同意和偏好設定，屬於[!UICONTROL XDM個別設定檔]聯合結構的其中一個結構必須包含標準欄位群組&#x200B;**[!UICONTROL 隱私權/個人化/行銷偏好設定（同意）]**。

有關欄位組提供的每個屬性的結構和預期使用案例的詳細資訊，請參閱[同意和首選項參考指南](../xdm/field-groups/profile/consents.md)。 有關如何將欄位組添加到架構的逐步說明，請參閱[XDM UI指南](../xdm/ui/resources/schemas.md#add-field-groups)。

將欄位群組新增至[啟用設定檔的架構](../xdm/ui/resources/schemas.md#profile)及其欄位已用來從體驗應用程式內嵌同意資料後，您就可以在區段規則中使用收集的同意屬性。

## 處理細分中的同意

為了確保退出設定檔不包含在區段中，必須在建立任何新區段時，將特殊欄位新增至現有區段並納入。

下列步驟示範如何為兩種選擇退出標幟新增適當欄位：

1. [!UICONTROL 資料收集]
1. [!UICONTROL 共用資料]

>[!NOTE]
>
>雖然本指南著重於上述的兩個選擇退出標幟，您也可以設定區段以併入其他同意訊號。 [同意和偏好設定參考指南](../xdm/field-groups/profile/consents.md)提供了有關這些選項及其預定使用案例的詳細資訊。

在UI中建立區段時，在&#x200B;**[!UICONTROL Attributes]**&#x200B;下，導覽至&#x200B;**[!UICONTROL XDM個別設定檔]**，然後選取&#x200B;**[!UICONTROL Consents and Preferences]**。 從這裡，您可以看到&#x200B;**[!UICONTROL 資料收集]**&#x200B;和&#x200B;**[!UICONTROL 共用資料]**&#x200B;的選項。

![](./images/opt-outs/consents.png)

首先選取&#x200B;**[!UICONTROL 資料收集]**&#x200B;類別，然後將&#x200B;**[!UICONTROL 選擇值]**&#x200B;拖曳至區段產生器。 將屬性新增至區段時，您可以指定必須包含或排除的[同意值](../xdm/field-groups/profile/consents.md#choice-values)。

![](./images/opt-outs/consent-values.png)

一種方法是排除選擇退出並收集其資料的任何客戶。 要執行此操作，請將運算子設為&#x200B;**[!UICONTROL 不等於]**，然後選擇以下值：

* **[!UICONTROL 否（選擇退出）]**
* **[!UICONTROL 預設為否（選擇退出）]**
* **[!UICONTROL 未知]** （若未知，則假設不同意）

![](./images/opt-outs/collect.png)

在左側邊欄的&#x200B;**[!UICONTROL Attributes]**&#x200B;下，導覽回&#x200B;**[!UICONTROL Consensts and Preferences]**&#x200B;區段，然後選取&#x200B;**[!UICONTROL Share Data]**。 將其對應的&#x200B;**[!UICONTROL 選擇值]**&#x200B;拖曳至畫布，並選取與[!UICONTROL 資料收集]選擇值相同的值。 請確定兩個屬性之間已建立&#x200B;**[!UICONTROL 或]**&#x200B;關係。

![](./images/opt-outs/share.png)

區段中同時新增了&#x200B;**[!UICONTROL 資料收集]**&#x200B;和&#x200B;**[!UICONTROL 共用資料]**&#x200B;同意值後，任何選擇退出使用其資料的客戶將從產生的受眾中排除。 在此處，您可以在選取&#x200B;**[!UICONTROL Save]**&#x200B;以完成此程式之前，繼續自訂區段定義。

## 後續步驟

依照本教學課程，您現在應該能更清楚了解在Experience Platform中建立區段時，如何遵守客戶同意和偏好設定。

如需在Platform中管理同意的詳細資訊，請參閱下列檔案：

* [使用Adobe標準進行同意處理](../landing/governance-privacy-security/consent/adobe/overview.md)
* [使用IAB TCF 2.0標準的同意處理](../landing/governance-privacy-security/consent/iab/overview.md)