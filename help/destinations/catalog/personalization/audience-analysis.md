---
title: Audience Analysis目的地
description: 檢視客戶在Customer Journey Analytics中符合資格的對象。
badgeLimitedAvailability: label="可用性限制" type="Informative"
source-git-commit: 83b3d40e17f444555769020526bb723265a09eb9
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 2%

---

# Audience Analysis目的地

此 [!UICONTROL 對象分析] 目的地可讓您擴充Adobe Experience Platform受眾資料至 [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=zh-Hant). 您可以選取要納入產生之擴充資料中的對象。 然後，您便可將對象資格作為維度用於 [Analysis Workspace](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html) 報告。

>[!AVAILABILITY]
>
>此目的地處於有限測試階段。 如果您有興趣使用此目的地，請聯絡您的Adobe客戶團隊。

## 先決條件

使用此目的地之前需要下列專案：

* 您必須完成布建才能使用Audience Analysis目的地。 如果您尚未布建使用此目的地，請聯絡您的Adobe帳戶團隊。
* 您必須布建才能使用Customer Journey Analytics。
* 您必須在Adobe Experience Platform中建立至少一個對象。

## 支援的身分

Audience Analysis支援下表所述的身分啟用。 進一步瞭解 [身分](/help/identity-service/features/namespaces.md). 通常會使用Experience CloudID (ECID)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | Google廣告ID | 當您的來源身分是GAID名稱空間時，請選取GAID目標身分。 |
| IDFA | 廣告商適用的Apple ID | 當您的來源身分是IDFA名稱空間時，請選取IDFA目標身分。 |
| ECID | Experience Cloud ID | 代表ECID的名稱空間。 此名稱空間也可以以下列别名表示：「Adobe Marketing Cloud ID」、「Adobe Experience Cloud ID」、「Adobe Experience Platform ID」。 請參閱以下檔案： [ECID](/help/identity-service/features/ecid.md) 以取得詳細資訊。 |
| phone_sha256 | 使用SHA256演演算法雜湊的電話號碼 | Adobe Experience Platform同時支援純文字和SHA256雜湊電話號碼。 當來源欄位包含未雜湊屬性時，請核取 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 |
| email_lc_sha256 | 使用SHA256演演算法雜湊的電子郵件地址 | Adobe Experience Platform同時支援純文字和SHA256雜湊電子郵件地址。 當來源欄位包含未雜湊屬性時，請核取 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 |
| extern_id | 自訂使用者ID | 當您的來源身分是自訂名稱空間時，請選取此目標身分。 |

{style="table-layout:auto"}

## 支援的對象

使用此目的地時，支援下列型別的對象：

| 對象來源 | 支援 | 說明 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | ✓ | 受眾 [已匯入](../../../segmentation/ui/overview.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

## 匯出型別和頻率

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 對象匯出]** | 您正在匯出具有Audience Analysis目的地中所使用識別碼（名稱、電話號碼或其他）的對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 當根據對象評估在Experience Platform中更新設定檔時，聯結器會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 設定新目的地

>[!IMPORTANT]
> 
>若要建立目的地，您需要 **[!UICONTROL 檢視目的地]** 和 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要建立此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

### 目的地詳細資料

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：目的地名稱。
* **[!UICONTROL 說明]**：目的地說明。
* **[!UICONTROL 資料串流ID]**：您要以合格對象擴充的資料串流ID。 您可以在下列位置取得此ID： [資料串流管理員](/help/datastreams/overview.md).
* **[!UICONTROL 整合別名]**：整合別名。

### 警報

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

* **[!UICONTROL 超過啟用略過率]**：當啟用略過率超過臨界值時收到通知。

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

### 治理原則與執行動作

此選擇性區段可讓您定義資料治理原則，並確保使用的資料在傳送及啟用受眾時符合要求。

完成選取目的地所需的行銷動作後，選取「 」 **[!UICONTROL 建立]**.

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

建立目的地後，您就可以針對目的地啟用所需的對象。

1. 如果您尚未位於建立的目的地，您可以導覽至「 」以再次尋找該目的地 **[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]**.
1. 選取 **[!UICONTROL 啟用對象]**.
1. 選取您要分析資格的所需對象。 完成後，選取 **[!UICONTROL 下一個]**.
1. 檢閱目的地組態和對象設定，然後選取「 」 **[!UICONTROL 完成]**.

您可以導覽回「 」，新增更多對象以供日後分析 **[!UICONTROL 啟用對象]** 頁面。 對象啟動後，您就無法移除對象。
