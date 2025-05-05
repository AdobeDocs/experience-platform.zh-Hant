---
title: Demandbase連線
description: 使用此目標來啟用 Account-Based Marketing (ABM) 使用案例的帳戶客群。透過 DemandBase 的 B2B Demand Side Platform (DSP) 向目標帳戶中的相關人物誌和角色投放廣告。還可以利用 Demandbase 第三方資料來擴充目標帳戶，以用於行銷和銷售中的其他下游使用案例。
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=zh-Hant#rtcdp-editions newtab=true"
badgeB2P: label="B2P版本" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=zh-Hant#rtcdp-editions newtab=true"
last-substantial-update: 2024-09-30T00:00:00Z
exl-id: a84609a2-f1d3-4998-9db4-ad59c0a0b631
source-git-commit: 08c2c7f5080f0e6afb7be53aad9f88ba0fccf923
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 17%

---

# Demandbase連線 {#demandbase}

>[!AVAILABILITY]
>
>&#x200B;>購買[企業對企業](/help/rtcdp/overview.md#rtcdp-b2b)和[企業對個人](/help/rtcdp/overview.md#rtcdp-b2p)版Real-Time Customer Data Platform的公司，皆可透過Demandbase目的地啟用帳戶對象。

為您的Demandbase行銷活動啟用設定檔，以根據[帳戶對象](/help/segmentation/types/account-audiences.md)進行對象目標定位、個人化和隱藏。

## 使用實例 {#use-case}

使用此目標來啟用 Account-Based Marketing (ABM) 使用案例的帳戶客群。透過 DemandBase 的 B2B Demand Side Platform (DSP) 向目標帳戶中的相關人物誌和角色投放廣告。還可以利用 Demandbase 第三方資料來擴充目標帳戶，以用於行銷和銷售中的其他下游使用案例。

例如，運用Demandbase的廣告技術DSP，針對關鍵客戶中的特定角色或角色，以創造漏斗頂端的銷售機會，或建立並擴大購買群組。 使用Demandbase目的地來探索其他使用案例，以有效鎖定您的帳戶。

透過這項整合，您也可以使用即時帳戶資訊查詢來個人化網站體驗，以最佳化參與情形。

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | X | 對象[從CSV檔案匯入](../../../segmentation/ui/overview.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-and-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|--------------|-----------|---------------------------|
| 匯出型別 | 對象匯出 | 所有對象成員將會匯出包含金鑰識別碼，例如姓名、電話號碼等。 |
| 頻率 | 串流 | 「隨時待命」API型連線。 設定檔變更後，更新會立即傳送到下游。 |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

若要將帳戶對象匯出至Demandbase，您需要下列專案：

1. Demandbase帳戶。
2. Demandbase API權杖。 您可以在Demandbase中和使用者產生API Token。 若要產生Token，請在登入您的Demandbase帳戶後，導覽至[我的設定檔> API Token](https://web.demandbase.com/o/ad/at)。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填入必填欄位，然後選取&#x200B;**[!UICONTROL 連線到目的地]**。

![新增持有人權杖](/help/destinations/assets/catalog/advertising/demandbase/add-bearer-token.png)

* **[!UICONTROL 持有人權杖]**：填入持有人權杖以驗證目的地。 檢視[必要條件](#prerequisites)以取得權杖的相關資訊。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![新增目的地連線的相關資訊](/help/destinations/assets/catalog/advertising/demandbase/name-and-description.png)

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL 實體型別]**：選取&#x200B;**[!UICONTROL 帳戶]**&#x200B;作為實體型別。

現在您已準備好在Demandbase中啟用對象。

## 啟動此目標的客群 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[啟用帳戶對象](/help/destinations/ui/activate-account-audiences.md)以取得啟用此目的地的帳戶對象的指示。

## 其他附註和重要圖說文字 {#additional-notes}

* 如果先前已將具有相同名稱的帳戶對象啟動至Demandbase，則無法透過與Demandbase目的地不同的資料流再次啟動該對象。
* 如果您已將對象匯出至Demandbase，且在Experience Platform中成功匯出，但並非所有資料都會送達Demandbase，您可能會在Demandbase端遇到API節流。 如需進一步說明，請洽詢他們。
