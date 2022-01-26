---
keywords: 個性化；目標；目的地；目的地個性化；配置個性化目標；同一頁；下一頁；
title: 配置同頁和下一頁個性化的個性化目標
type: Tutorial
seo-title: Configure personalization destinations for same-page and next-page personalization
description: 瞭解如何為同一頁和下一頁個性化配置個性化目標
seo-description: Configure personalization destinations for same-page and next-page personalization
source-git-commit: 628e7a993a3566322e0249a5a9864cf6b3fe4493
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 1%

---


# 配置同頁和下一頁個性化的個性化目標

## 總覽 {#overview}

Adobe Experience Platform用途 [邊緣分割](../../segmentation/ui/edge-segmentation.md) 使客戶能夠即時、高規模地建立和瞄準受眾群。

此功能可幫助您配置同頁和下一頁個性化使用案例。

本文提供了有關如何為這些使用案例配置Experience Platform和個性化目標的逐步說明。

## 步驟1:配置Experience PlatformWeb SDK資料流 {#configure-datastream}

配置個性化用例的第一步是配置 [!DNL Web SDK datastream]。

按照 [資料流配置](../../edge/fundamentals/datastreams.md) 文檔。

## 步驟2:配置個性化目標 {#configure-destination}

配置資料流後，可以開始配置個性化目標。

關注 [目標連接建立教程](../ui/connect-destination.md) 有關如何建立新目標連接的詳細說明。

根據您正在配置的目標，請參閱以下文章以瞭解特定於目標的先決條件和相關資訊：

* [Adobe Target](../catalog/personalization/adobe-target-connection.md)
* [自定義個性化連接](../catalog/personalization/custom-personalization.md)

## 第3步：建立 [!DNL Active-On-Edge] 合併策略 {#create-merge-policy}

建立目標連接後，必須建立 [!DNL Active-On-Edge] 合併策略。

按照 [建立合併策略](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)，並確保啟用 **[!UICONTROL 活動 — 邊緣合併策略]** 切換。

## 第4步：在平台中建立新段 {#create-segment}

建立後 [!DNL Active-On-Edge] 合併策略，必須在平台中建立新段。

關注 [段構建器](../../segmentation/ui/segment-builder.md) 指南，確保 [分配](../../segmentation/ui/segment-builder.md#merge-policies) 這樣 [!DNL Active-On-Edge] 合併您在步驟3中建立的策略。

## 第5步：將段激活到目標

配置過程的最後一步是將您在步驟4中建立的段激活到您在步驟2建立的目標。

要執行此操作，請遵循此操作 [激活教程](../ui/activate-profile-request-destinations.md)。

## 驗證設定 {#validate-configuration}

成功執行上述步驟後，您應在個性化目標中看到新段。