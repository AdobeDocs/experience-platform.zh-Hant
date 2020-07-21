---
title: Google廣告管理員目標
seo-title: Google廣告管理員目標
description: 'Google Ad Manager之前稱為DoubleClick for Publishers或DoubleClick AdX，是來自谷歌的廣告服務平台，可讓出版業者透過視訊和行動應用程式管理其網站上的廣告展示。 '
seo-description: 'Google Ad Manager之前稱為DoubleClick for Publishers或DoubleClick AdX，是來自谷歌的廣告服務平台，可讓出版業者透過視訊和行動應用程式管理其網站上的廣告展示。 '
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---


# [!DNL Google Ad Manager Destination]

## 概述

[!DNL Google Ad Manager]此廣告服務平台之前 [!DNL DoubleClick] 稱為「發佈者」或「 [!DNL DoubleClick AdX][!DNL Google] 」，可讓發佈者透過視訊和行動應用程式，管理其網站上廣告的顯示。

## 目標規格

請注意以下特定於目標的詳細 [!DNL Google Ad Manager] 資訊：

* 您可以傳送下列身 [分](../../identity-service/namespaces.md) ，到 [!DNL Google Ad Manager] 目的地： **Google Cookie ID、IDFA、GAID、Roku ID、Microsoft ID、Amazon Fire TV ID**。
* 在平台中以程式設計方式建立啟用的 [!DNL Google] 觀眾。
* Adobe即時CDP目前不包含測量量度，以驗證啟動是否成功。 請參閱Google中的觀眾計數，以驗證整合併瞭解觀眾鎖定規模。

>[!IMPORTANT]
>
>如果您想要建立第一個目標，但 [!DNL Google Ad Manager] Experience Cloud ID服務過去（使用Audience Manager或其他應用程式）未啟用 [](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID同步功能，請聯絡Adobe諮詢或客戶服務以啟用ID同步。 如果您先前在Audience Manager中 [!DNL Google] 設定整合，您設定的ID同步化會延續至Adobe即時CDP。

## 必要條件

### 允許清單

>[!NOTE]
>
>在Adobe即時CDP中設定您的第一個目 [!DNL Google Ad Manager] 標之前，允許清單是必填的。 在建立目標之前，請確保已完成下面所述的允 [!DNL Google] 許清單進程。

在Adobe [!DNL Google Ad Manager] 即時CDP中建立目標之前，您必須聯絡 [!DNL Google] Adobe，才能將Adobe列入允許的資料提供者清單，並將您的帳戶新增至允許清單。 請聯 [!DNL Google] 絡並提供下列資訊：

* **帳戶ID** : 這是Adobe的帳戶ID [!DNL Google]。 請聯絡Adobe客戶服務或您的Adobe代表以取得此ID。
* **客戶ID** : 這是Adobe的客戶帳戶ID [!DNL Google]。 請聯絡Adobe客戶服務或您的Adobe代表以取得此ID。
* **網路ID** : 這是您的帳戶， [!DNL Google Ad Manager]
* **對象連結ID** : 這是您的帳戶， [!DNL Google Ad Manager]
* 您的帳戶類型。 **DFP，由Google** 或 **AdX購買者提供**。

## 建立目標

1. 在「連 **[!UICONTROL 接」>「目標]**」中，選 [!DNL Google Ad Manager]擇並選擇「創 **[!UICONTROL 建目標」]**。
   ![Connect Google Ad Manager目標](/help/rtcdp/destinations/assets/google-1-destination.png)

2. 在建立 **目標工作流的** 「設定」步驟中，填寫目標的 [!UICONTROL 「基本資訊] 」。 <br>

   ![基本資訊Google廣告管理員](/help/rtcdp/destinations/assets/google-1-destination-setup-step.png)
* **[!UICONTROL 名稱]**: 填寫此目標的首選名稱。
* **[!UICONTROL 說明]**: 可選。 例如，您可以提及您使用此目的地的促銷活動。
* **[!UICONTROL 帳戶類型]**: 根據您使用Google的帳戶，選取一個選項：
   * 用於 `DFP by Google` 發佈 [!DNL DoubleClick] 者
   * 用 `AdX buyer` 於 [!DNL Google AdX]
* **[!UICONTROL 帳戶ID]**: 在您的帳戶ID中填入 [!DNL Google]。 這可以是您的網路ID或對象連結ID。 通常，這是8位數的ID。
* **[!UICONTROL 行銷使用案例]**: 行銷使用案例會指出將資料匯出至目的地的方式。 您可以從Adobe定義的行銷使用案例中選擇，也可以建立自己的行銷使用案例。 有關行銷使用案例的詳細資訊，請參 [閱即時CDP中的資料治理頁](/help/rtcdp/privacy/data-governance-overview.md#destinations) 。 如需個別Adobe定義之行銷使用案例的詳細資訊，請參閱「資 [料使用政策」概觀](/help/data-governance/policies/overview.md#core-actions)。

> [!NOTE]
>
> 設定目的地時， [!DNL Google Ad Manager] 請與您或Adobe代表 [!DNL Google Account Manager] 合作，以瞭解您擁有的帳戶類型。

## 啟用區段至 [!DNL Google Ad Manager]

如需如何啟用區段至目的地的指示 [!DNL Google Ad Manager]，請參 [閱啟用資料至目的地](/help/rtcdp/destinations/activate-destinations.md)。