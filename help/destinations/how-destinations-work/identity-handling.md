---
title: 目的地啟用工作流程中的身分處理
description: 瞭解在啟用工作流程中如何根據目的地型別處理身分匯出
exl-id: f4894a08-c7a9-4d57-a6d3-660c49206d6a
source-git-commit: f9917d6a6de81f98b472cff9b41f1526ea51cdae
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 0%

---

# 目的地啟用工作流程中的身分處理

此頁面說明身分識別如何匯出至不同目的地型別的特殊性，並教導您如何根據目的地找到哪些身分識別可供匯出。

>[!TIP]
>
> 如需身分識別、身分識別名稱空間及身分識別相關辭彙定義的詳細資訊，請閱讀[身分識別服務概觀](/help/identity-service/home.md)。

[目錄](/help/destinations/catalog/overview.md)中的每個目的地都略有不同，因此沒有針對所有目的地進行一刀切的設定。 不過，有一些模式可指導目的地的設定及其身分需求，如下節所述。

## 以檔案為基礎的目的地 {#file-based}

針對[以檔案為基礎的目的地](/help/destinations/destination-types.md#file-based) （例如[!DNL Amazon S3]、SFTP、大部分的電子郵件行銷目的地，例如[!DNL Adobe Campaign]、[!DNL Oracle Eloqua]、[!DNL Salesforce Marketing Cloud]），這些目的地中的身分設定大多是開啟的，這表示您不需要在批次啟用工作流程的[選取屬性](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)步驟中選取任何身分。

如果您選擇將身分新增至檔案匯出，請注意，在匯出中只能選取[身分名稱空間](/help/identity-service/features/identity-graph-viewer.md#access-identity-graph-viewer)中的單一身分。 當您選取要匯出的身分時，會自動選取它作為[必要屬性](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes)和[重複資料刪除索引鍵](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys)。

![選取為必要屬性和重複資料刪除索引鍵的身分。](/help/destinations/assets/how-destinations-work/selected-identity.png)

作為因應措施，如果這些身分已作為屬性擷取到Experience Platform中，則可以將更多身分新增到匯出。 請參閱以下範例，其中除了身分名稱空間`Phone_E.164`之外，還選取要匯出的XDM屬性電子郵件地址。

![選取要匯出的電子郵件地址屬性範例。](/help/destinations/assets/how-destinations-work/email-selected.png)

## 從身分對應匯出身分與將身分匯出為XDM屬性 — 差異 {#identity-map-or-attribute}

根據您是從身分對應中選取匯出身分識別，還是從已當作屬性擷取到Experience Platform中的身分識別，匯出記錄的數目可能有所不同。 當您從身分對應選取身分時，[合併原則](/help/profile/merge-policies/overview.md)在匯出的記錄數目中也扮演重要角色。

例如，假設您從兩個不同的資料集中有下列設定檔片段，這些片段將合併到單一客戶設定檔中：

**設定檔片段一**

| 身分對應 | 名字 | 姓氏 | 電子郵件屬性 |
|---------|----------|---------|--------|
| 電子郵件1，忠誠度ID1 | John | 完成 | 電子郵件1 |


**設定檔片段二**

| 身分對應 | 名字 | 姓氏 | 電子郵件屬性 |
|---------|----------|---------|--------|
| 電子郵件2，忠誠度ID1 | John | 完成 | 電子郵件2 |

合併的設定檔如下所示：

| 身分對應 | 名字 | 姓氏 | 電子郵件屬性 |
|---------|----------|---------|--------|
| 電子郵件1、電子郵件2、忠誠度ID1 | John | 完成 | 電子郵件2 |

匯出行為會因您選取匯出`IdentityMap: Email`或`xdm: personalEmail.address`而有所不同。

如果客戶啟用`IdentityMap: Email`，匯出的檔案中將有兩個記錄，一個用於email1，另一個用於email2。

但是，如果客戶啟用`xdm: personalEmail.address`，則記錄中只會出現email2，因為email attribute欄位只包含email2。 這些情況可以解決不同的使用案例，您可能會想要啟用某個客戶檔案中的所有電子郵件地址，或僅啟用該客戶檔案中最新的電子郵件地址。

結果是，您匯出的記錄數量取決於您選擇的合併原則，以及您在匯出中是否選取身分或屬性。

## API型串流目的地 {#streaming-destinations}

[以[Destination SDK](/help/destinations/destination-sdk/overview.md)建置的API型串流目的地](/help/destinations/destination-types.md#streaming-destination) （例如[!DNL Facebook]、[!DNL Google Customer Match]、[!DNL Pinterest]、[!DNL Braze]及其他）只支援匯出的特定ID。 如需可匯出至每個目的地的特定身分詳細資訊，請閱讀每個目的地檔案頁面中的&#x200B;*支援的身分*&#x200B;區段（例如，請參閱[!DNL Pinterest]目的地頁面中的[支援的身分割槽段](/help/destinations/catalog/advertising/pinterest.md)）。

但是請注意，您可以彈性地使用來自[私人圖形](/help/profile/merge-policies/overview.md#id-stitching)或屬性中的資料做為身分。 這表示您可以將XDM屬性對應至目的地所需的身分欄位。 請參閱以下的[!DNL Pinterest]目的地範例，其中XDM屬性`personalEmail.address`對應到必要的[!DNL Pinterest]身分`pinterest_audience`。

>[!TIP]
>
>當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項，讓Experience Platform在啟動時自動雜湊資料。 深入瞭解[串流目的地啟用教學課程](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation)中的&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項。

![對應到Pinterest目的地之身分欄位的電子郵件地址屬性範例。](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### 依賴協力廠商Cookie整合的Advertising目的地 {#third-party-cookie-destinations}

依賴第三方Cookie的Advertising目的地（例如： [!DNL Google Ads]、[!DNL Google Ad Manager]、[!DNL Google DV360]、[!DNL Bing]、[!DNL The Trade Desk]）不需要客戶在啟用工作流程中選取ID。 對於這些目的地，在設定啟用工作流程時，Experience Platform會自動尋找由[[!UICONTROL Experience CloudID服務]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hant)建構的身分比對資料表，並匯出所有適用於設定檔且受目的地支援的身分。

這些目的地需要透過[!UICONTROL Experience CloudID服務]或[!UICONTROL Experience PlatformWeb SDK]進行ID同步。

如果您使用[!UICONTROL Experience PlatformWeb SDK]，但頁面上未實作舊版[!UICONTROL Experience CloudID服務]，則您必須確保已啟用相關網站的資料流，以允許同步協力廠商ID，如[設定資料流檔案](/help/datastreams/configure.md#create)中所述。

如上述連結的檔案所述，在設定資料串流時，您必須確定已啟用&#x200B;**[!UICONTROL 協力廠商ID同步]**&#x200B;滑桿。 大部分客戶會將`container_id`欄位保留空白（預設為0）。 如果您的舊版Audience Manager實作使用特定容器ID （但請注意，這將是極少數的客戶），則您只需變更此值。

>[!NOTE]
>
>Audience Manager支援這些廣告目的地的絕大部分(這些目的地型別在Audience Manager中稱為以裝置為基礎的目的地)。 檢視Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html)中所有支援的以裝置為基礎的目的地的[清單。 Experience Platform中只列出少數幾個。 如需在Experience Platform和Audience Manager之間共用資料的資訊，請閱讀[啟用從Experience Platform到Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#enable-aep-to-aam-data)的資料共用的區段。 目前沒有支援更多協力廠商Cookie目的地的計畫。

## 企業目的地 {#enterprise-destinations}

[Enterprise目的地](/help/destinations/destination-types.md#streaming-profile-export) ([!DNL Amazon Kinesis]、[!DNL Azure Event Hubs]、HTTP API)不需要資料匯出中的特定ID，因為這些是專為企業整合使用案例所設計。 不過，您可以視需要從身分對應將身分匯出為XDM屬性或來自身分對應。 檢視匯出至HTTP目的地](/help/destinations/catalog/streaming/http-destination.md#exported-data)的[資料範例，其中包含`personalEmail.address` XDM屬性，以及身分對應中的身分`ECID`和`email_lc_sha256` （雜湊電子郵件地址）。

## Personalization目的地 {#personalization-destinations}

[Personalization （或edge）目的地](/help/destinations/destination-types.md#edge-personalization-destinations) (例如：Adobe Target、[!DNL Custom Personalization])不需要在啟用工作流程中選擇任何身分，因為整合是設定檔查詢。 使用者端（[!DNL Target]、[!DNL Web SDK]或其他）會查詢[[!UICONTROL Edge]](/help/collection/home.md#edge)，並提取它需要的設定檔資訊以進行站上個人化。

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在瞭解如何找出個別目的地支援或所需的身分識別。 您現在也知道身分選取如何適用於每個目的地型別。

接下來，您可以閱讀目的地型別中哪些[匯出設定](/help/destinations/how-destinations-work/destinations-configurations.md)是共有的、開發人員可以在個別目的地層級進行設定，以及使用者可以在啟動工作流程中編輯哪些設定。

您也可以簽出[目錄](/help/destinations/catalog/overview.md)中的所有可用目的地。
