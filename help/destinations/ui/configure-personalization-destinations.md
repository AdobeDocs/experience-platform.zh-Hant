---
keywords: 個人化；目標；目的地；個性化目標；設定個人化目的地；同一頁；下一頁；
title: 為同一頁面和下一頁個人化設定個人化目的地
type: Tutorial
description: 了解如何為同一頁面和下一頁個人化設定個人化目的地。
exl-id: 7d7b6869-bd59-4766-a044-f449396f6524
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# 為同一頁面和下一頁個人化設定個人化目的地

## 總覽 {#overview}

>[!NOTE]
>
>當 [設定Adobe Target連線](../catalog/personalization/adobe-target-connection.md) 若不使用datastream ID，則不支援本文所述的使用案例。

Adobe Experience Platform使用 [邊緣分割](../../segmentation/ui/edge-segmentation.md) 讓客戶即時大規模建立和鎖定受眾區段。

此功能可協助您設定同頁和下一頁個人化使用案例。

本文提供如何針對這些使用案例設定Experience Platform和您的個人化目的地的逐步指示。

此外，請觀看以下影片以了解端對端設定程式的概觀。

>[!VIDEO](https://video.tv.adobe.com/v/340091/)

>[!NOTE]
>
>Experience Platform使用者介面經常更新，且自此視訊錄制以來可能已變更。 如需最新資訊，請參閱以下各節所述的設定步驟。

## 步驟1:在資料收集UI中設定資料流 {#configure-datastream}

設定個人化目的地的第一步，是為Experience PlatformWeb SDK設定資料流。 這是在資料收集UI中完成。

設定資料流時，位於 **[!UICONTROL Adobe Experience Platform]** 確保兩者 **[!UICONTROL 邊緣分割]** 和 **[!UICONTROL 個人化目的地]** 中所有規則的URL。

![資料流配置](../assets/ui/configure-personalization-destinations/datastream-config.png)

如需如何設定資料流的詳細資訊，請遵循 [Platform Web SDK檔案](../../edge/datastreams/overview.md).

## 步驟2:設定您的個人化目的地 {#configure-destination}

設定資料流後，您就可以開始設定個人化目的地。

關注 [目的地連線建立教學課程](../ui/connect-destination.md) 以了解如何建立新目的地連線的詳細指示。

請根據您要設定的目的地，參閱下列文章以取得目的地特定的必要條件和相關資訊：

* [Adobe Target連線](../catalog/personalization/adobe-target-connection.md)
* [自訂個人化連線](../catalog/personalization/custom-personalization.md)

## 步驟3:建立 [!DNL Active-On-Edge] 合併策略 {#create-merge-policy}

建立目的地連線後，您必須建立 [!DNL Active-On-Edge] 合併策略。

遵循 [建立合併策略](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)，並確定啟用 **[!UICONTROL 邊緣活動合併策略]** 切換。

## 步驟4:在Platform中建立新區段 {#create-segment}

建立 [!DNL Active-On-Edge] 合併原則，您必須在Platform中建立新區段。

關注 [區段產生器](../../segmentation/ui/segment-builder.md) 指南來建立新區段，並請務必 [指派](../../segmentation/ui/segment-builder.md#merge-policies) the [!DNL Active-On-Edge] 合併您在步驟3中建立的策略。

## 步驟5:啟動區段至您的目的地

設定程式的最後一個步驟是將您在步驟4建立的區段啟動至您在步驟2建立的目的地。

要執行此操作，請遵循此操作 [啟用教學課程](../ui/activate-profile-request-destinations.md).

## 驗證設定 {#validate-configuration}

成功執行上述步驟後，您應該會在個人化目的地中看到新區段。
