---
keywords: Experience Platform；主題；熱門主題；選擇退出；分段；分段服務；分段服務；榮譽退出；選擇退出；選擇退出；同意；共用；收集；
solution: Experience Platform
title: 尊重段內的同意
description: 瞭解如何在段操作中遵守客戶同意首選項以收集和共用個人資料。
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# 遵守段內的同意

法律隱私法規，如 [!DNL California Consumer Privacy Act] (CCPA)規定消費者有權選擇不收集或與第三方共用其個人資料。 Adobe Experience Platform提供標準體驗資料模型(XDM)元件，這些元件旨在在即時客戶配置檔案資料中捕獲這些客戶同意偏好。

如果客戶因共用其個人資料而撤回或拒絕同意，那麼在為市場營銷活動吸引受眾時，貴組織必須遵守這一偏好。 本文檔介紹如何使用Experience Platform用戶介面在段定義中整合客戶同意值。

## 快速入門

遵守客戶同意價值需要瞭解 [!DNL Adobe Experience Platform] 服務。 開始本教程之前，請確保您熟悉以下服務：

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md):平台組織客戶體驗資料的標準化框架。
* [[!DNL Real-Time Customer Profile]](../profile/home.md):根據來自多個來源的聚合資料即時提供統一的客戶配置檔案。
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md):允許您從 [!DNL Real-Time Customer Profile] 資料。

## 同意架構欄位

為了遵守客戶同意和首選項，您的 [!UICONTROL XDM個人配置檔案] union架構必須包含標準欄位組 **[!UICONTROL 同意和首選項]**。

有關欄位組提供的每個屬性的結構和預期使用情形的詳細資訊，請參閱 [同意和首選項參考指南](../xdm/field-groups/profile/consents.md)。 有關如何將欄位組添加到架構的逐步說明，請參閱 [XDM UI指南](../xdm/ui/resources/schemas.md#add-field-groups)。

將欄位組添加到 [啟用配置檔案的架構](../xdm/ui/resources/schemas.md#profile) 並且其欄位已用於從您的體驗應用程式中接收同意資料，您可以使用段規則中收集的同意屬性。

## 在分割中處理同意

為了確保在段中不包括已選取的配置檔案，必須在建立任何新段時將特殊欄位添加到現有段並包括在內。

以下步驟演示如何為兩種類型的opt-out標誌添加相應欄位：

1. [!UICONTROL 資料收集]
1. [!UICONTROL 共用資料]

>[!NOTE]
>
>本指南重點介紹上面的兩個選擇退出標誌，但您也可以配置段以同時包含附加同意信號。 的 [同意和首選項參考指南](../xdm/field-groups/profile/consents.md) 提供了有關這些選項及其預期使用情形的詳細資訊。

在UI中生成段時，在 **[!UICONTROL 屬性]**，導航 **[!UICONTROL XDM個人配置檔案]**，然後選擇 **[!UICONTROL 同意和首選項]**。 從這裡，您可以看到 **[!UICONTROL 資料收集]** 和 **[!UICONTROL 共用資料]**。

![](./images/opt-outs/consents.png)

從選擇 **[!UICONTROL 資料收集]** 類別，然後拖動 **[!UICONTROL 選擇值]** 到段生成器。 將屬性添加到段時，可以指定 [同意值](../xdm/field-groups/profile/consents.md#choice-values) 必須包括或排除的。

![](./images/opt-outs/consent-values.png)

一種方法是排除選擇不收集資料的任何客戶。 要執行此操作，請將運算子設定為 **[!UICONTROL 不等於]**，然後選擇以下值：

* **[!UICONTROL 否（選擇退出）]**
* **[!UICONTROL 預設值為「否」（選擇退出）]**
* **[!UICONTROL 未知]** （假定在未知的情況下不予同意）

![](./images/opt-outs/collect.png)

下 **[!UICONTROL 屬性]** 在左欄中，導航回 **[!UICONTROL 同意和首選項]** ，然後選擇 **[!UICONTROL 共用資料]**。 拖動其對應 **[!UICONTROL 選擇值]** 到畫布中，並選擇與 [!UICONTROL 資料收集] 選項值。 確保 **[!UICONTROL 或]** 建立了兩個屬性之間的關係。

![](./images/opt-outs/share.png)

同時使用 **[!UICONTROL 資料收集]** 和 **[!UICONTROL 共用資料]** 添加到該段的同意值後，任何選擇不使用其資料的客戶將被排除在結果受眾之外。 在此處，您可以在選擇 **[!UICONTROL 保存]** 完成該過程。

## 後續步驟

通過學完本教程，您現在應更瞭解在Experience Platform中構建段時如何遵守客戶同意和首選項。

有關在平台中管理同意的詳細資訊，請參閱以下文檔：

* [使用Adobe標準的同意處理](../landing/governance-privacy-security/consent/adobe/overview.md)
* [使用IAB TCF 2.0標準的同意處理](../landing/governance-privacy-security/consent/iab/overview.md)