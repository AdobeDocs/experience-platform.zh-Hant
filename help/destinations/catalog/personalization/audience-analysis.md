---
title: Audience Analysis目的地
description: 在Customer Journey Analytics中檢視客戶符合資格的對象。
badgeLimitedAvailability: label="可用性限制" type="Informative"
exl-id: 81437237-d746-4ce9-b938-7d2541f0ed32
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 3%

---

# Audience Analysis目的地

[!UICONTROL Audience Analysis]目的地可讓您將Adobe Experience Platform對象資料擴充至[Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=zh-Hant)。 您可以選取要納入產生之擴充資料中的對象。 然後，受眾資格便可在[Analysis Workspace](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html?lang=zh-Hant)報表中作為維度使用。

>[!AVAILABILITY]
>
>此目的地處於有限測試階段。 如果您有興趣使用此目的地，請聯絡您的Adobe客戶團隊。

## 先決條件

使用此目的地之前需要下列專案：

* 您必須完成布建才能使用Audience Analysis目的地。 如果您尚未布建使用此目的地，請聯絡您的Adobe客戶團隊。
* 您必須完成布建才能使用Customer Journey Analytics。
* 您必須在Adobe Experience Platform中建立至少一個對象。

## 支援的身分

Audience Analysis支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。 通常會使用Experience Cloud ID (ECID)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | 當您的來源身分是GAID名稱空間時，請選取GAID目標身分。 |
| IDFA | 廣告商適用的Apple ID | 當您的來源身分是IDFA名稱空間時，請選取IDFA目標身分。 |
| ECID | Experience Cloud ID | 代表ECID的名稱空間。 此名稱空間也可以以下列别名表示：「Adobe Marketing Cloud ID」、「Adobe Experience Cloud ID」、「Adobe Experience Platform ID」。 如需詳細資訊，請參閱[ECID](/help/identity-service/features/ecid.md)上的下列檔案。 |
| phone_sha256 | 使用SHA256演演算法雜湊的電話號碼 | Adobe Experience Platform同時支援純文字和SHA256雜湊電話號碼。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |
| email_lc_sha256 | 使用SHA256演演算法雜湊的電子郵件地址 | Adobe Experience Platform同時支援純文字和SHA256雜湊電子郵件地址。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |
| extern_id | 自訂使用者ID | 當您的來源身分是自訂名稱空間時，請選取此目標身分。 |

{style="table-layout:auto"}

## 支援的對象

使用此目的地時，支援下列型別的對象：

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在匯出具有Audience Analysis目的地中所使用識別碼（名稱、電話號碼或其他）的對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 當根據對象評估在Experience Platform中更新設定檔時，聯結器會將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 設定新的目的地

>[!IMPORTANT]
> 
>若要建立目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要建立此目的地，請依照[目的地設定教學課程](../../ui/connect-destination.md)中所述的步驟進行。

### 目的地詳細資料

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：目的地名稱。
* **[!UICONTROL 描述]**：目的地描述。
* **[!UICONTROL 資料串流ID]**：您要與合格對象擴充的資料串流ID。 您可以在[資料串流管理員](/help/datastreams/overview.md)中取得此識別碼。
* **[!UICONTROL 整合別名]**：整合別名。

### 警示

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

* **[!UICONTROL 啟用略過率超過]**：當啟用略過率超過臨界值時會收到通知。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

### 治理原則與執行動作

此選擇性區段可讓您定義資料治理原則，並確保使用的資料在傳送及啟用受眾時符合要求。

當您完成選取目的地所需的行銷動作時，請選取&#x200B;**[!UICONTROL 建立]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

建立目的地後，您就可以針對目的地啟用所需的對象。

1. 如果您尚未位於建立的目的地，您可以導覽至&#x200B;**[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]**，再次找到該目的地。
1. 選取&#x200B;**[!UICONTROL 啟用對象]**。
1. 選取您要分析資格的所需對象。 完成後，選取&#x200B;**[!UICONTROL 下一步]**。
1. 檢閱目的地組態和對象設定，然後選取&#x200B;**[!UICONTROL 完成]**。

您可以導覽回&#x200B;**[!UICONTROL 啟用對象]**&#x200B;頁面，新增更多對象以供日後分析。 對象啟動後，您就無法移除對象。
