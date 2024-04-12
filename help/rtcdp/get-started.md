---
keywords: RTCDP；CDP；Real-time Customer Data Platform；即時客戶資料平台；real time cdp；cdp；rtcdp
title: Real-time Customer Data Platform快速入門
description: 在設定您的 Adobe Real-Time Customer Data Platform 實作時，可使用此範例情境當作範例。
feature: Get Started, Use Cases
exl-id: 9f775d33-27a1-4a49-a4c5-6300726a531b
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '2325'
ht-degree: 1%

---

# Real-time Customer Data Platform快速入門

本快速入門手冊將引導您瞭解Real-time Customer Data Platform (Real-Time CDP)的範例實作。 您可在設定自己的實施作業時加以使用。 雖然本指南會顯示特定範例，但會連結至您建立設定時可使用的其他資訊。

此範例顯示由Adobe Experience Platform提供支援的Real-time Customer Data Platform強大功能，可以：

* 從多個來源擷取資料
* 將它們合併為單一 [!DNL real-time customer profile]
* 跨裝置提供一致、相關和個人化的體驗。

## 使用案例

運動服裝公司Luma一直都在努力改善客戶體驗。 他們推出一項新計畫，以提高與禮品相關的銷售額。 此外也希望減少過度曝光，例如向客戶傳送令人討厭的廣告。

目前，他們在針對訪客日後不會購買的專案重新定位的媒體上花費過多。 例如，Luma不想將原本打算為其他人一次性購買的專案重新鎖定某個人。

目前，Luma的資料分散於多個來源。 因此，他們面臨重大挑戰：

* 行銷組織必須與各自擁有資料來源的各種團隊合作，包括網站、行動應用程式、忠誠度系統、CRM等。
* 當行銷團隊存取資料時，資料通常會過時，且不再與時效性強的行銷活動相關。
* 他們需統一資料，將目標定位為使用者，而非管道。

因此，Luma具備下列業務目標：

* 從消費者的不同資料來源建立其消費者的即時單一檢視。
* 使用跨不同頻道和裝置的相關訊息，個人化行銷活動。

為了滿足這些目標，行銷團隊需要能夠大規模管理客戶資料。

有了Adobe Experience Platform提供的Real-Time CDP，Luma的行銷組織可以：

1. 從不同的平台收集資料，並確保其可用於下游的其他行銷活動。
1. 建立其消費者的單一即時檢視，不受資料來源地影響。
1. 在每個接觸點推動一致、相關和個人化的體驗。

## 步驟

本教學課程包含下列步驟：

1. 建置 [客戶設定檔](#customer-profile).
1. [個人化](#personalizing-the-user-experience) 使用者體驗。
1. 使用 [多個資料來源](#using-multiple-data-sources).
1. [設定資料來源](#configuring-a-data-source).
1. [收集資料](#bringing-the-data-together-for-a-specific-customer) 適用於特定客戶。
1. 設定 [對象](#audiences).
1. 設定 [目的地](#destinations).
1. [跨裝置拼接設定檔](#cross-device-identity-stitching).
1. [分析設定檔](#analyzing-the-profile).

## 客戶設定檔

客戶首次造訪您的網站時，您對他們一無所知。

![影像](assets/luma-site.png)

當資料導覽時，系統會即時擷取資料，不僅會傳送至Adobe Analytics中的報表套裝，還會直接傳送至Adobe Experience Platform。 收集資料時，您會根據中的行為資料，開始形成消費者的單一檢視 [!DNL Experience Platform's real-time customer profile].

網站的許多訪客可能是先前從Luma購買的回頭客戶。  Luma個人化訊息和服務以處理新訪客和重複訪客以及已知客戶很重要。

### 新客戶的首次造訪

例如，一位身份不明的訪客導覽至Luma網站上的男性區段，並檢視幾件跑步運動衫。

![影像](assets/luma-sweatshirts.png)

當客戶導覽以深入瞭解這些產品時，這些產品檢視會在Adobe Analytics中收集並傳送至 [!DNL Experience Platform].

<!--![image](assets/luma-shirt-detail.png)-->

Luma可將訪客的行為對應至Adobe Experience Platform上的使用者設定檔，並開始收集該消費者行為的更豐富檢視。

### 取得更詳細的客戶檢視

隨著客戶繼續與網站互動，畫面會更清晰。 例如，假設訪客新增產品至購物車並登入。

客戶登入時，她自稱是Sarah Rose。

![影像](assets/luma-login.png)

兩個身分已合併：

* 匿名瀏覽資料
* 與Sarah Rose的帳戶相關聯的現有資料

兩個身分都會合併為中的單一設定檔 [!DNL Experience Platform]. Luma現在擁有此消費者的統一檢視。

根據匿名訪客在網站男性區段的瀏覽行為，我們可能會假設客戶是男性。 Luma現在已登入，可辨識出Sarah Rose。 Luma運用 [!DNL Real-Time Customer Profile] 以調整跨頻道傳送給她的訊息。

## 個人化使用者體驗

我們以忠誠訊息歡迎Sarah，並感謝Sarah成為銅級會員，並提供更多有關福利以及如何提升其地位和積分的資訊。

她導覽至首頁以瀏覽更多內容。

![影像](assets/luma-personal.png)

Sarah會獲得個人化首頁體驗，並依據她以動態方式傳送 [!DNL Real-Time Customer Profile] 在Adobe Experience Platform中。

透過Adobe Target中的Adobe Sensei支援個人化，她可以看到相關內容，其中會考慮她過去的購買情形，以及她對執行服裝和用具的相似性。 Luma也根據她最近的瀏覽，為男士量身打造跑步用具的男士目錄內容。

在本頁的下方，Sarah會看到精選產品，以及根據最近檢視的專案顯示的新建議匣。

此個人化內容可協助Sarah快速找到相關專案。 這會提高轉換率，並提供更令人愉快的客戶體驗。

### 讓客戶回來

Sarah分心並離開網站，結束工作階段。 Luma可在Adobe Experience Platform中使用她的資料，協助帶她返回網站。

Real-time Customer Data Platform採用Adobe Experience Platform技術，專為客戶體驗管理而打造。 它可讓組織：

* 簡化資料整合與啟用
* 控管已知和未知的資料使用情況
* 大規模加速行銷使用案例

## 使用多項資料來源

Luma的團隊將其所有行為和客戶資料放在一個地方。

![影像](assets/luma-dash.png)

他們可以內嵌下列所有來源的資料：

* 現有的Adobe Experience Cloud解決方案資料
* 非Adobe來源，例如Luma的忠誠度計畫、客服中心和銷售點系統資料
* 來自Luma資料來源的即時串流資料
* 來自Adobe解決方案的即時資料（不需要新標籤）

來自不同來源的所有資料都會合併至單一統一客戶設定檔。

## 設定資料來源

使用 [!DNL Real-Time Customer Data Platform] 將新的資料來源帶入Platform。 Real-Time CDP包括資料來源目錄，可快速輕鬆新增至設定檔。

![影像](assets/luma-source-cat.png)

例如，若要內嵌Luma的CRM資料，請篩選目錄依據 *CRM*，以及包含下列專案的所有現成可用聯結器 *CRM* 都會列出。 新增 [!DNL Microsoft Dynamics CRM] 資料：

1. 授權連線。

   ![影像](assets/luma-source-auth.png)

1. 從建議的XDM預先對應表格清單中，選擇您要匯入的內容。

   <!--    ![image](assets/luma-source-import.png) -->

   例如，選取 **[!UICONTROL 連絡人]**. 連絡人資料的預覽會自動載入，因此您可以確定一切都如預期般顯示。

   Real-Time CDP會將標準欄位自動對應至「 」，以省去此流程中的許多手動工作。 [!DNL Experience Data Model] (XDM)設定檔結構描述。

1. 檢閱欄位對應。

   <!--    ![image](assets/luma-source-mapping.png) -->

   例如，仔細檢查連絡人的電子郵件欄位是否已正確對應。\
   您可以選擇預覽資料並執行進階對應。

1. 設定排程。

   ![影像](assets/luma-source-sched.png)

已完成。 您剛才已新增 [!DNL Microsoft CRM] 做為資料來源至 [!DNL Experience Platform].

### 標示使用原則的內嵌資料

Luma有許多內部政策，會限制使用某些種類的已收集資訊，且必須符合資料使用方面的法律和隱私權相關考量。 使用Adobe Experience Platform資料控管，預先定義的資料使用標籤可套用至資料集（以及這些資料集內的特定欄位），讓Luma根據特定使用限制來分類其資料。

![](assets/governance-labels.png)

套用資料使用標籤後，Luma就可以使用資料控管來建立資料使用原則。 資料使用原則是描述您可在包含特定標籤的資料上執行的動作型別的規則。 當嘗試在Real-Time CDP中執行構成原則違規的動作時，會阻止該動作，並發出警示，以顯示違反哪個原則及原因。

此外，Real-Time CDP

## 將特定客戶的資料彙集在一起

在此案例中，搜尋Sarah Rose的設定檔。 她的設定檔隨即出現，並顯示她用來登入的電子郵件。

<!-- ![image](assets/luma-find-profile.png) -->

Luma擁有有關Sarah顯示的所有設定檔資訊。 這包括她的個人資訊，例如地址和電話號碼、通訊偏好設定，以及她符合資格的對象。

| 類別 | 說明 |
|---|---|
| 身分 | 顯示連結在一起的身分 [!DNL Platform] 來自Sarah與Luma跨頻道和裝置的互動。 隨即顯示她來自網站的ECID。 她的身分也包含行動應用程式的ECID、電子郵件ID，以及最近新增的CRM ID [!DNL Microsoft Dynamics] 和從Luma忠誠度系統傳入Adobe Experience Platform的忠誠度ID。 |
| 活動 | 顯示Sarah與Luma品牌的所有互動資料。 這包括她剛才檢視的專案、過去檢視的任何專案、收到的電子郵件、她與客服中心的互動，以及這些互動中每個環節發生的頻道和裝置。 |

Real-Time CDP設定檔將Luma行銷團隊的工作流程從幾週縮短至幾分鐘，並根據此360度客戶檢視開啟個人化的可能性。 設定檔會合併她在登入前瀏覽網站時的行為資料，以及現有的客戶設定檔，以建立Sarah的全面檢視。

行銷團隊可以使用此增強功能， [!DNL Real-Time Customer Profile] 以便更個人化Sarah的體驗，並提高她對Luma的品牌忠誠度。

## 對象

強大的Adobe Experience Platform細分功能可讓行銷人員根據在中擷取的資料，結合屬性、事件和現有對象。 [!DNL Real-Time Customer Profile].

<!-- ![image](assets/luma-segments.png) -->

在這個案例中，Sarah最近在網站上的互動表現出與她過去動作不同的行為。 她通常買女裝。 不過，她購物車中的商品是男士大運動衫。

Luma資料科學團隊已針對購買傾向建立模型。 一種模式會識別服裝類別（例如女士/女士）或現有消費者人數的突然變化。 Sarah的購買行為有所改變，這表示她不是在為自己購物。

<!-- ![image](assets/luma-gift.png) -->

### 定義對象

使用對象工作區中的各種視覺化構成或程式碼型運算式編輯器選項，來修改或建立代表似乎正在購買禮物的購物車放棄者的對象：

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

因為Sarah在購物車中新增了看似禮品的專案並捨棄了，Luma可以免費贈送禮品套裝優惠來鎖定她。

## 目的地

當您新增「放棄贈送禮品購物車」對象時，您可以看到大致有多少人屬於此對象。 您可以對其採取動作，使其可用於跨頻道個人化。

選取 **[!UICONTROL 傳送至目的地]**.

在Real-Time CDP中，Luma可順暢地對其對象進行個人化操作。\
我們在這裡看到Luma可將此目的地傳送至的所有目的地，包括Adobe和非Adobe解決方案：

![影像](assets/luma-dest.png)

### 選取目的地

在此案例中，Luma想要跨下列目的地透過個人化重新鎖定此對象：

* Google，用於顯示
  <!--* Facebook -->
* Adobe Campaign，用於電子郵件

<!-- ![image](assets/luma-sched-dest.png) -->

### 正在排程目的地

您也可以將對象匯出排程在特定時間開始或結束。 對象將會在排程日期在設定的平台上張貼和自動更新。

>[!NOTE]
>
>（選擇性）如果您選取日期欄位，則會自動排程90天。

選取 **[!UICONTROL 儲存]** 前往下一頁。

當此對象中的客戶進行購買時，其對此對象的成員資格會即時被抑制。 他們不再符合資格，因為其狀態已變更。

這樣就不會對不合格的受眾使用清查資源，讓Luma媒體團隊的主管節省數十萬美元。

### 強制目的地的資料使用原則

Adobe Experience Platform包含隱私權與安全性控制項，用以判斷對象是否可供在特定目的地啟用。 啟用是根據建立目的地時指派的行銷目的啟用或限制，以及您的組織定義的資料使用原則。

如果您的活動違反原則，便會出現警告。 此警告包含資料歷程資訊，可協助您識別違反原則的原因，以及您可以如何解決違規。

有了這些控制項， [!DNL Experience Platform] 協助Luma以負責任的方式遵守法規與市場。 這些控制具有彈性，可以修改以符合Luma安全性和治理團隊的需求，讓他們能夠自信地處理區域和組織對於管理已知和未知客戶資料的需求。

<!--

### Data flow canvas

When you save, a visual data flow canvas shows the segment mapped from the unified profile to the three destinations you selected.

![image](assets/luma-flow.png)

-->

## 跨裝置身分識別拼接

Sarah在行動裝置上瀏覽社群媒體網站，且看到Luma廣告。 它提醒她她購物車中留下的物品。

稍後，她開啟電子郵件，看到重新定位的電子郵件。 她從電子郵件中選取Luma連結。

此連結會將Sarah帶往Luma行動首頁，她將在這裡看到Adobe Target提供的高度個人化體驗。

* 我們歡迎她成為銅級會員。
* 她看到「禮物」訊息。
* 她也會看到「免費贈品包裝」訊息，這是她銅級會員權益的一部分。
* 根據她執行時的相似性，主圖影像中仍會鎖定她。

她購買毛衣、加入禮物包裝，並寫禮品單。 她也可以選擇記住這個活動，並收到明年的提醒，以便在這個時候收到禮物。 她說是的，並排程在第二年進行電子郵件促銷活動，以提醒她購買其他禮物。

由於受眾抑制功能，Sarah的男士毛衣將不會成為目標。

## 分析設定檔

Luma行銷人員使用Adobe Experience Platform在Real-Time CDP控制面板上檢視贈送禮物的對象。 他們檢視此行動方案隨時間推移的結果，並看到其成長。 客戶對優惠方案做出回應並花費更多金錢。

這些見解讓行銷人員能夠針對此訊號採取行動，此訊號在CDP中提供此資料，並將客戶（例如Sarah）附加至受眾，進一步推動此訊號。

Luma使用此CDP資料來提高忠誠度和客戶滿意度。
