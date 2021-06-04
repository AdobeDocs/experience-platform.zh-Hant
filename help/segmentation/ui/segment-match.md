---
keywords: Experience Platform；首頁；熱門主題；分段；分段符合；區段符合
solution: Experience Platform
title: 區段符合概述
topic: 概述
description: 區段比對是Adobe Experience Platform中的區段共用服務，可讓兩位或多位Platform使用者以安全、受控且符合隱私權的方式來交換區段資料。
source-git-commit: 481160f83e82c80ea5b73e9b56003dc625a34b5e
workflow-type: tm+mt
source-wordcount: '1901'
ht-degree: 1%

---


# (Alpha)[!DNL Segment Match]概述

>[!IMPORTANT]
>
>[!DNL Segment Match] 目前位於alpha中。文件和功能可能會有所變更。

Adobe Experience Platform區段比對是區段共用服務，可讓兩位或多位Platform使用者以安全、受控且符合隱私權的方式交換區段資料。 [!DNL Segment Match] 使用平台隱私標準和個人識別碼，例如雜湊電子郵件、雜湊電話號碼，以及IDFA和GAID等裝置識別碼。

使用[!DNL Segment Match]，您可以：

* 管理身分重疊程式。
* 檢視預先共用估計。
* 套用資料使用量標籤，以控制是否可與合作夥伴共用資料。
* 在發佈摘要後維護共用的受眾生命週期管理，並透過新增、刪除和取消共用的功能繼續進行資料的動態交換。

[!DNL Segment Match] 使用身分重疊程式，確保以安全且以隱私權為中心的方式共用區段。**重疊身分**&#x200B;是您的區段和所選合作夥伴的區段中都相符的身分。 在傳送者與接收者之間共用區段之前，身分重疊程式會檢查命名空間中的重疊，以及傳送者與接收者之間的同意檢查。 必須傳遞兩個重疊檢查才能共用區段。

以下各節提供有關[!DNL Segment Match]的詳細資訊，包括有關設定及其端對端工作流的詳細資訊。

## 設定

以下各節將概述如何設定和配置[!DNL Segment Match]:

### 設定身分資料和命名空間 {#namespaces}

開始使用[!DNL Segment Match]的第一步，是確定您要根據支援的身分識別命名空間擷取資料。

身分識別命名空間是[Adobe Experience Platform Identity Service](../../identity-service/home.md)的元件。 每個客戶身分識別都包含指出身分識別內容的相關命名空間。 例如，命名空間可以將&quot;name<span>@email.com&quot;值區分為電子郵件地址，或將&quot;443522&quot;區分為數值CRM ID。

完全限定的身分包括ID值和命名空間。 在設定檔片段間比對記錄資料時（例如[!DNL Real-time Customer Profile]合併設定檔資料時），身分值和命名空間都必須符合。

在[!DNL Segment Match]的內容中，共用資料時，重疊程式會使用命名空間。

支援的命名空間清單如下：

| 命名空間 | 說明 |
| --------- | ----------- |
| 電子郵件（SHA256，小寫） | 預先雜湊電子郵件地址的命名空間。 此命名空間中提供的值在以SHA256進行雜湊處理前會轉換為小寫。 在標準化電子郵件地址之前，需要先裁剪開頭和結尾空格。 無法回溯變更此設定。 如需詳細資訊，請參閱以下關於[SHA256雜湊支援](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support)的檔案。 |
| 電話(SHA256_E.164) | 表示需要同時使用SHA256和E.164格式雜湊的原始電話號碼的命名空間。 |
| ECID | 代表Experience CloudID(ECID)值的命名空間。 此命名空間也可由下列別名引用：&quot;Adobe Marketing Cloud ID&quot;、&quot;Adobe Experience Cloud ID&quot;、&quot;Adobe Experience Platform ID&quot;。 如需詳細資訊，請參閱[ECID概述](../../identity-service/ecid.md) 。 |
| Apple IDFA（廣告商的ID） | 代表廣告商Apple ID的命名空間。 如需詳細資訊，請參閱以下關於[以興趣為基礎的廣告](https://support.apple.com/en-us/HT202074)的檔案。 |
| Google廣告ID | 代表Google廣告ID的命名空間。 如需詳細資訊，請參閱[Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en)上的下列檔案。 |

### 設定同意設定

您必須提供同意設定，並將其預設值設為`opt-in`或`opt-out`，才能進行同意檢查。

選擇加入和選擇退出同意檢查會決定您是否可以以同意的方式操作，以依預設共用使用者資料。 如果同意配置預設設定為`opt-in`，則可以共用用戶資料，除非用戶明確選擇退出。 如果預設值設為`opt-out`，則無法共用使用者資料，除非使用者明確選擇加入。

[!DNL Segment Match]的預設同意配置設定為`opt-out`。 若要對您的資料強制執行選擇加入模型，請傳送電子郵件要求給您的Adobe客戶經理。

有關用於設定資料共用同意值的`share`屬性的詳細資訊，請參閱有關[隱私和同意欄位組](../../xdm/field-groups/profile/consents.md)的以下文檔。 如需用於擷取消費者同意以收集和使用與隱私權、個人化和行銷偏好設定相關資料之特定欄位群組的資訊，請參閱下列[隱私權、個人化和行銷偏好設定的同意GitHub範例](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/consent-preferences.schema.md)。

### 設定資料使用量標籤

您必須建立的最後一個先決條件是設定新的資料使用量標籤，以防止資料共用。 您可以透過資料使用標籤管理哪些資料可透過[!DNL Segment Match]共用。

資料使用量標籤可讓您根據套用至該資料的使用量原則，對資料集和欄位進行分類。 標籤可隨時套用，提供您選擇控管資料的彈性。 最佳實務鼓勵在資料內嵌至Experience Platform時，或資料可供Platform使用時，立即加上標籤。

[!DNL Segment Match] 使用C11標籤，此合約標籤專供您 [!DNL Segment Match] 手動新增至任何資料集或屬性，以確保這些資料集或屬性不會列入合作 [!DNL Segment Match] 夥伴共用程式。C11標籤表示不應在[!DNL Segment Match]進程中使用的資料。 在您決定要從[!DNL Segment Match]排除的資料集和/或欄位，並據此新增C11標籤後， [!DNL Segment Match]工作流程會自動強制執行標籤。 [!DNL Segment Match] 自動啟用「限 [!UICONTROL 制資料共] 用」核心原則。如需如何將資料使用量標籤套用至資料集的特定指示，請參閱UI](../../data-governance/labels/user-guide.md)中[管理資料使用量標籤的教學課程。

如需資料使用量標籤及其定義的清單，請參閱[資料使用量標籤字彙表](../../data-governance/labels/reference.md)。 有關資料使用策略的資訊，請參閱[資料使用策略概述](../../data-governance/policies/overview.md)。

## [!DNL Segment Match] 端對端工作流程

設定身分資料和命名空間、同意設定和資料使用標籤後，您就可以開始使用[!DNL Segment Match]及其功能。

### 管理合作夥伴

在Platform UI中，從左側導覽中選取&#x200B;**[!UICONTROL 區段]**，然後從頂端標題中選取&#x200B;**[!UICONTROL 摘要]**。

![segments-feed.png](../images/ui/segment-match/segments-feed.png)

[!UICONTROL 摘要]頁面包含從合作夥伴收到的摘要清單以及您已共用的摘要。 要查看現有合作夥伴的清單或與新合作夥伴建立連接，請選擇&#x200B;**[!UICONTROL 管理合作夥伴]**。

![manage-partners.png](../images/ui/segment-match/manage-partners.png)

兩個合作夥伴之間的連線是「雙向交握」，可做為使用者在沙箱層級將其Platform組織連結在一起的自助方法。 需要連線，才能通知Platform已建立合約，且Platform可協助您與合作夥伴共用服務。

>[!NOTE]
>
>你和你的伴侶之間的「雙向握手」嚴格說來就是一種聯繫。 此過程中不會交換任何資料。

您可以在[!UICONTROL 管理合作夥伴]螢幕的主介面中查看與現有合作夥伴的連接清單。 在右側邊欄上是「[!UICONTROL 共用設定]」面板，它提供您產生新[!UICONTROL 連接ID]的選項，以及可在其中輸入合作夥伴的[!UICONTROL 連接ID]的輸入框。

![suteling-connection.png](../images/ui/segment-match/establish-connection.png)

要建立新的[!UICONTROL 連接ID]，請在[!UICONTROL 共用設定]下選擇&#x200B;**[!UICONTROL 重新生成]**，然後選擇新生成的ID旁邊的複製表徵圖。

![share-setting.png](../images/ui/segment-match/share-setting.png)

要使用其[!UICONTROL 連接ID]連接合作夥伴，請在[!UICONTROL 連接合作夥伴]下的輸入框中輸入其唯一ID值，然後選擇&#x200B;**[!UICONTROL 請求]**。

![connect-partner.png](../images/ui/segment-match/connect-partner.png)

### 建立摘要

**feed**&#x200B;是資料（區段）的分組、資料公開或使用方式的規則，以及決定資料與合作夥伴資料相符的設定。 摘要可以獨立管理，並透過[!DNL Segment Match]與其他Platform使用者交換。

若要建立新摘要，請從[!UICONTROL 摘要]控制面板選取&#x200B;**[!UICONTROL 建立摘要]**。

![create-feed.png](../images/ui/segment-match/create-feed.png)

摘要的基本設定包含有關行銷使用案例和身分設定的名稱、說明和設定。 提供摘要的名稱和說明，然後套用您希望排除資料的行銷使用案例。 您可以從清單中選取多個使用案例，其中包括：

* [!UICONTROL Analytics]
* [!UICONTROL 與PII結合]
* [!UICONTROL 跨網站定位]
* [!UICONTROL 資料科學]
* [!UICONTROL 電子郵件目標定位]
* [!UICONTROL 匯出至第三方]
* [!UICONTROL 站上廣告]
* [!UICONTROL 站上個人化]
* [!UICONTROL 區段符合]
* [!UICONTROL 單一身分個人化]

最後，為您的摘要選取適當的身分識別命名空間。 有關[!DNL Segment Match]支援的特定命名空間的資訊，請參閱[身分資料和命名空間表](#namespaces)。 完成後，選擇&#x200B;**[!UICONTROL Next]**。

![audience-sharing.png](../images/ui/segment-match/audience-sharing.png)

建立摘要的設定後，從第一方區段清單中選取您要共用的區段。 您可以從清單中選取多個區段，並可使用右側邊欄來管理所選區段的清單。 完成後，選擇&#x200B;**[!UICONTROL Next]**。

![select-segments.png](../images/ui/segment-match/select-segments.png)

此時會出現「[!UICONTROL 共用]」頁面，提供您一個介面以選取您要與其共用動態消息的合作夥伴。 在此步驟中，您也可以檢視預先共用重疊估計報表，並依您與合作夥伴之間的命名空間查看重疊身分的數量，以及同意共用資料的重疊身分數。

選取「**[!UICONTROL 依區段分析]**」以查看估計報表。

![analyze.png](../images/ui/segment-match/analyze.png)

重疊估計報表可讓您在共用摘要前，管理每個合作夥伴和每個區段的重疊和同意檢查。

| 量度 | 說明 |
| ------- | ----------- |
| 經同意的預估身分 | 符合貴組織所設定同意要求的重疊身分總數。 |
| 估計的重疊身份 | 符合所選區段資格且與所選合作夥伴相符的身分數。 這些身分識別會依命名空間顯示，不代表個別設定檔身分識別。 重疊估計基於配置檔案草圖。 |

完成後，選擇&#x200B;**[!UICONTROL Close]**。

![overlap-report.png](../images/ui/segment-match/overlap-report.png)

選擇合作夥伴並查看重疊估計報告後，選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![share.png](../images/ui/segment-match/share.png)

此時會顯示[!UICONTROL 檢閱]步驟，讓您在共用及發佈新摘要之前先檢閱。 此步驟包含您所套用之身分設定的詳細資訊，以及您所選行銷使用案例、區段和合作夥伴的相關資訊。

選擇&#x200B;**[!UICONTROL 完成]**&#x200B;以繼續。

![review.png](../images/ui/segment-match/review.png)

### 更新摘要

若要新增或移除區段，請從[!UICONTROL 摘要]頁面選取&#x200B;**[!UICONTROL 建立摘要]**，然後選取&#x200B;**[!UICONTROL 現有摘要]**。 在顯示的現有摘要清單中，選取您要更新的摘要，然後選取&#x200B;**[!UICONTROL Next]**。

![摘要清單](../images/ui/segment-match/feed-list.png)

區段清單隨即顯示。 從這裡，您可以新增區段至動態消息，也可以使用右側邊欄來移除您不再需要的任何區段。 完成摘要中區段的管理後，請選取&#x200B;**[!UICONTROL Next]**，然後依照上述步驟完成更新的摘要。

![更新](../images/ui/segment-match/update.png)

>[!NOTE]
>
>當您從共用摘要新增或移除區段時，接收合作夥伴必須在收到的摘要清單中重新啟用[!DNL Profile]切換，以確認變更。

### 接受傳入的摘要

若要檢視傳入的摘要，請從[!UICONTROL 摘要]頁面的標題中選取&#x200B;**[!UICONTROL 已接收]**，然後從清單中選取您要檢視的摘要。 若要接受摘要，請選取「**[!UICONTROL 啟用設定檔]**」，並允許在幾分鐘內將狀態從[!UICONTROL 擱置中]更新為[!UICONTROL 啟用]。

![received.png](../images/ui/segment-match/received.png)

接受共用摘要後，您就可以開始使用共用資料來建立新區段。

## 後續步驟

閱讀本檔案，您便對[!DNL Segment Match]、其功能及其端對端工作流程有了了解。 請參閱下列檔案，深入了解其他Platform服務：

* [[!DNL Segmentation Service]](../home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!DNL Real-time Customer Profile] 概觀](../../profile/home.md)
