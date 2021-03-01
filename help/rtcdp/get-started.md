---
keywords: RTCDP;CDP；即時客戶資料平台；即時客戶資料平台；即時cdp;cdp;rtcdp
title: 即時客戶資料平台快速入門
description: 設定 Real-time Customer Data Platform 實作時使用此範本案例作為的範例。
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '2326'
ht-degree: 1%

---


# 即時客戶資料平台快速入門

本入門指南引導您完成即時客戶資料平台（即時CDP）的示例實施。 您可以在設定自己的實作時，將它當做範例。 雖然本指南會顯示特定範例，但會連結至您建立設定時可使用的其他資訊。

此範例說明由Adobe Experience Platform提供支援的即時客戶資料平台對下列產品的強大功能：

* 從多個來源收錄資料
* 將它們合併為單一[!DNL real-time customer profile]
* 跨裝置提供一致、相關且個人化的體驗。

## 使用案例

運動服裝公司Luma一直在努力改善客戶體驗。 他們有新的計畫來增加禮品相關的銷售。 他們還希望減少過度曝光，例如關注客戶的煩人廣告。

目前，他們在媒體上花了太多錢，針對訪客未來不會購買的項目重新設定目標。 例如，Luma不想將某個項目重新鎖定在某人的目標位置，而該項目原本是為其他人一次性購買。

目前，Luma的資料分散在多個來源。 因此，他們面臨著重大挑戰：

* 行銷組織必須與各自擁有資料來源的不同團隊合作，包括網站、行動應用程式、忠誠度系統、CRM等。
* 當行銷團隊存取資料時，資料通常已過時，而且與他們對時間敏感的促銷活動不再相關。
* 他們需要統一資料，以鎖定個人而非通道。

因此，Luma有下列業務目標：

* 從不同的資料來源建立消費者的即時單一檢視。
* 運用跨不同通道和裝置的相關訊息，個人化行銷宣傳。

為達成這些目標，行銷團隊必須能夠大規模管理客戶資料。

借助由Adobe Experience Platform提供支援的即時CDP,Luma的營銷組織可以：

1. 從分散的平台收集資料，並確保資料在下游可供其他行銷活動使用。
1. 建立其消費者的單一即時檢視，不受資料來源的影響。
1. 在每個觸點上提供一致、相關且個人化的體驗。

## 步驟

本教學課程包含下列步驟：

1. 建立[客戶個人檔案](#customer-profile)。
1. [個](#personalizing-the-user-experience) 人化使用者體驗。
1. 使用[多個資料來源](#using-multiple-data-sources)。
1. [設定資料來源](#configuring-a-data-source)。
1. [收集特](#bringing-the-data-together-for-a-specific-customer) 定客戶的資料。
1. 設定[區段](#segments)。
1. 設定[目標](#destinations)。
1. [將描述檔接合在各種裝置上](#cross-device-identity-stitching)。
1. [分析描述檔](#analyzing-the-profile)。

## 客戶個人檔案

當客戶第一次瀏覽您的網站時，您對他們一無所知。

![image](assets/luma-site.png)

資料在導覽時即時擷取，不僅會傳送至Adobe Analytics的報表套裝，還會直接傳送至Adobe Experience Platform。 在收集資料時，您會開始根據[!DNL Experience Platform's real-time customer profile]中的行為資料，對消費者形成單一檢視。

許多網站的訪客可能是舊有從Luma購買的客戶。  Luma必須個人化訊息傳遞和產品，以解決新訪客和回頭訪客以及已知客戶的問題。

### 新客戶的首次造訪

例如，獨立身份的訪客導覽至Luma網站的「男」區段，並檢視兩對穿運動衫的訪客。

![影像](assets/luma-sweatshirts.png)

當客戶導覽以進一步瞭解這些產品時，這些產品檢視會收集在Adobe Analytics，並傳送至[!DNL Experience Platform]。

<!--![image](assets/luma-shirt-detail.png)-->

Luma可將訪客的行為對應至Adobe Experience Platform的使用者個人檔案，並開始匯整該消費者行為的更豐富檢視。

### 取得更詳細的客戶檢視

當客戶繼續與網站互動時，會呈現更清楚的畫面。 例如，假設訪客新增產品至購物車並登入。

當客戶登入時，她把自己稱為莎拉·羅斯。

![影像](assets/luma-login.png)

將合併兩個標識：

* 匿名瀏覽資料
* 與Sarah Rose帳戶相關的現有資料

這兩個識別碼都會結合為[!DNL Experience Platform]中的單一描述檔。 Luma現在對這個消費者有統一的看法。

根據網站「男性」區段中匿名訪客的瀏覽行為，可能假設該客戶為男性。 現在她登入後，Luma就認識Sarah Rose。 Luma運用[!DNL Real-time Customer Profile]的強大功能來調整跨通道傳遞給她的訊息。

## 個人化使用者體驗

Sarah受到了忠誠的歡迎，並感謝她成為銅牌會員，獲得了更多關於福利以及如何提高她的地位和分數的資訊。

她導覽至首頁以瀏覽更多內容。

![影像](assets/luma-personal.png)

Sarah會根據她在Adobe Experience Platform的[!DNL Real-time Customer Profile]，獲得動態傳遞的個人化首頁體驗。

她看到了相關內容，這要歸功於Adobe TargetAdobe Sensei推動的個人化，這個個人化考慮了她過去購買的服裝和服裝的親和力。 Luma還根據她最近的瀏覽，為男性量身訂做男性跑步器材的目錄內容。

在下一頁，Sarah會看到精選產品，並根據她最近檢視的項目提供新的建議托盤。

此個人化內容可協助Sarah快速找到相關項目。 這可提升轉化率，並提供更愉快的客戶體驗。

### 將客戶帶回來

莎拉分心了，離開了網站，結束了她的工作。 盧瑪可以利用她在Adobe Experience Platform的資料幫助她回到網站。

由Adobe Experience Platform提供支援的即時客戶資料平台，專為客戶體驗管理而打造。 它可讓組織：

* 簡化資料整合與啟動
* 控制已知和未知的資料使用
* 大規模加速行銷使用案例

## 使用多個資料來源

Luma團隊在單一位置擁有所有行為和客戶資料。

![影像](assets/luma-dash.png)

他們可以從下列所有來源擷取資料：

* 現有Adobe Experience Cloud解決方案資料
* 非Adobe來源，例如Luma的忠誠度計畫、客服中心和銷售點系統資料
* 從Luma資料來源即時串流資料
* 來自Adobe解決方案的即時資料（不需要新標籤）

所有這些來自不同來源的資料都會合併為單一統一的客戶個人檔案。

## 設定資料來源

使用[!DNL Real-time Customer Data Platform]將新的資料來源帶入平台。 即時CDP包括一個資料源目錄，可以快速方便地添加到配置檔案中。

![影像](assets/luma-source-cat.png)

例如，若要收錄Luma的CRM資料，請依&#x200B;*CRM*&#x200B;篩選目錄，並列出包含&#x200B;*CRM*&#x200B;的所有現成連接器。 要添加[!DNL Microsoft Dynamics CRM]資料：

1. 授權連線。

   ![影像](assets/luma-source-auth.png)

1. 從建議的XDM預映射表清單中選擇要導入的內容。

   <!--    ![image](assets/luma-source-import.png) -->

   例如，選擇&#x200B;**[!UICONTROL Contacts]**。 預覽的連絡人資料會自動載入，因此您可以確保一切如預期般呈現。

   Adobe Experience Platform會將標準欄位自動對應至[!DNL Experience Data Model](XDM)描述檔架構，讓此程式耗費大量的人工工作。

1. 檢閱欄位對應。

   <!--    ![image](assets/luma-source-mapping.png) -->

   例如，請再次檢查聯繫人的電子郵件欄位是否已正確映射。\
   您可以選擇預覽資料並執行進階對應。

1. 設定排程。

   ![影像](assets/luma-source-sched.png)

都搞定了。 您剛剛將[!DNL Microsoft CRM]新增為[!DNL Experience Platform]的資料來源。

### 為使用策略的收錄資料加標籤

Luma有許多內部政策限制使用特定種類收集到的資訊，而且還必須遵守與資料使用相關的法律和隱私權相關的顧慮。 使用Adobe Experience Platform[!DNL Data Governance]，可將預先定義的資料使用標籤套用至資料集（以及這些資料集內的特定欄位），讓Luma根據特定的使用限制來分類其資料。

![](assets/governance-labels.png)

在套用資料使用標籤後，Luma就可以使用[!DNL Data Governance]來建立資料使用原則。 資料使用原則是描述允許您對包含特定標籤的資料執行動作種類的規則。 嘗試在構成策略違規的即時CDP中執行操作時，會阻止該操作，並發出警報以顯示違反了哪些策略以及原因。

## 為特定客戶整合資料

在此案例中，請搜尋Sarah Rose的設定檔。 她的個人檔案隨即出現，並附上她用來登入的電子郵件。

<!-- ![image](assets/luma-find-profile.png) -->

Luma擁有的關於Sarah的所有個人檔案資訊都會顯示出來。 這包括她的個人資訊，例如地址和電話號碼、通訊偏好設定，以及她符合的區段。

| 類別 | 說明 |
|---|---|
| 身份 | 顯示在[!DNL Platform]中，Sarah與Luma之間跨通道和裝置的互動所連結的身分。 會顯示她來自網站的ECID。 她的身分識別也包含其行動應用程式的ECID、電子郵件ID、最近新增[!DNL Microsoft Dynamics]資料集的CRM ID，以及從Luma忠誠度系統傳入Adobe Experience Platform的忠誠度ID。 |
| 事件 | 顯示Sarah與Luma品牌的所有互動資料。 這包括她剛剛檢視的項目、她過去檢視的任何內容、她收到的電子郵件、她與客服中心的互動，以及每個互動的通道和裝置。 |

Real-time CDP配置檔案將Luma營銷團隊的工作流程從數週縮減為幾分鐘，並基於此360度客戶視圖，為個人化開啟可能性。 此描述檔會合併她登入前瀏覽網站時的行為資料，以及她現有的客戶描述檔，以建立Sarah的完整檢視。

行銷團隊可運用此增強的[!DNL Real-time Customer Profile]，更個人化Sarah的體驗，並提高她對Luma的品牌忠誠度。

## 區段

強大的Adobe Experience Platform區段功能可讓行銷人員根據[!DNL Real-time Customer Profile]中擷取的資料，結合屬性、事件和現有區段。

<!-- ![image](assets/luma-segments.png) -->

在這種情況下，Sarah最近在網站上的互動行為與她過去的行為不同。 她通常買女裝。 不過，她購物車中的項目是男性的大型運動衫。

Luma資料科學團隊已經建立了關於購買傾向的模型。 一個模型可識別現有消費者服飾類別（例如男性／女性）或大小的突然變化。 Sarah的購買行為改變表明，她不是在為自己購物。

<!-- ![image](assets/luma-gift.png) -->

### 定義區段

修改或建立區段，以代表購物車放棄者，而放棄者似乎正在購買禮品：

```sql
Profile: Category != Preferred Category 
AND 
Product Size != Preferred Size 
in last 7 days.  
AND 
Abandoned Cart 
AND 
Loyalty member 
```

<!-- ![image](assets/luma-abandon.png)-->

由於Sarah在購物車中加入了明顯的禮品項目，並放棄了它，所以Luma可以透過免費的禮品包裝方案鎖定她。

## 目的地

當您新增「贈送購物車放棄者」區段時，您可以大致瞭解有多少人加入此區段。 您可以採取行動，讓它跨通道個人化。

選擇&#x200B;**[!UICONTROL 發送到目標]**。

在即時CDP中，Luma可以順暢地根據受眾細分採取行動，實現個人化。\
在此，我們看到Luma將此目標(包括Adobe和非Adobe解決方案)發送到的所有目標：

![影像](assets/luma-dest.png)

### 選擇目標

在此案例中，Luma想透過這些目標的個人化重新鎖定此受眾：

* Google，用於顯示

   <!--* Facebook -->
* Adobe Campaign，請寄電子郵件

<!-- ![image](assets/luma-sched-dest.png) -->

### 計畫目標

您也可以排程區段在特定時間開始或結束。 區段會在排程日期的設定平台中張貼並自動更新。

>[!NOTE]
>
>（可選）如果選擇日期欄位，它將自動計畫90天外。

選擇&#x200B;**[!UICONTROL 保存]**&#x200B;以轉至下一頁。

當此觀眾中的客戶進行購買時，他們對此觀眾的會籍會即時抑制。 由於狀態已改變，他們不再符合資格。

如此，Luma媒體團隊的主管就可省下數十萬美元，因為沒有針對不合格的觀眾使用庫存。

### 強制目標的資料使用策略

Adobe Experience Platform包含隱私權和安全性控制，以判斷區段是否可啟動至特定目的地。 啟用或限制啟動的依據是建立時指派給目的地的行銷目的，以及貴組織定義的資料使用政策。

如果您的活動違反原則，會出現警告。 此警告包含資料世系資訊，可協助您識別違反原則的原因，以及您可以採取哪些措施來解決違規問題。

通過這些控制，[!DNL Experience Platform]幫助Luma以負責任的態度遵守法規和市場。 這些控制項是有彈性的，可加以修改，以符合Luma的安全性和管理團隊的需求，讓他們能夠放心地處理管理已知和未知客戶資料的地區和組織需求。

### 資料流畫布

儲存時，視覺化資料流畫布會顯示從統一描述檔映射至您選取的三個目的地的區段。

![影像](assets/luma-flow.png)

## 跨裝置身分識別

Sarah在自己的行動裝置上瀏覽社交媒體網站，然後看到Luma廣告。 這讓她想起了她在購物車裡留下的物品。

之後，她開啟電子郵件，看到重新定向的電子郵件。 她從電子郵件中選擇Luma的連結。

這條連結將Sarah帶到移動Luma首頁，她在那裡看到了由Adobe Target提供的高度個性化的體驗。

* 她受到銅獎的歡迎。
* 她看到了&quot;禮物&quot;的訊息。
* 她還看到「免費禮品包裝」訊息，這是其銅像會籍權益的一部分。
* 她仍然以自己對跑步的親和力為目標。

她買毛衣，加上禮物包裝，並寫上禮券。 她還可以選擇記住這個活動，並在明年收到提醒，以便在此時獲得禮物。 她說是的，第二年，她被安排進電子郵件宣傳活動，提醒她再買一件禮物。

由於觀眾抑制能力，莎拉不會被那些男人的毛衣所鎖定。

## 分析配置檔案

Luma行銷人員使用Adobe Experience Platform來查看即時CDP儀表板上的禮品贈送部分。 他們看到這項計畫的成果，並看到它在不斷增長。 客戶會回應優惠，並投入更多資金。

這些洞見讓行銷人員能夠對此信號採取行動，而CDP中提供此資料並讓像Sarah這樣的客戶加入此細分，也為此提供了動力。

Luma使用此CDP資料來提升忠誠度和客戶滿意度。
