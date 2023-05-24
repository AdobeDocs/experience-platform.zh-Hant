---
keywords: RTCDP;CDP;Real-time Customer Data Platform；即時客戶資料平台；即時cdp;cdp;rtcdp
title: Real-time Customer Data Platform入門
description: 在設定您的 Adobe Real-Time Customer Data Platform 實作時，可使用此範例情境當作範例。
exl-id: 9f775d33-27a1-4a49-a4c5-6300726a531b
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2333'
ht-degree: 2%

---

# Real-time Customer Data Platform入門

本入門指南引導您瞭解Real-time Customer Data Platform(Real-Time CDP)的示例實施。 在設定自己的實現時，可以將其用作示例。 雖然本指南顯示了特定的示例，但它連結到在建立安裝程式時可以使用的其他資訊。

此示例顯示由Adobe Experience Platform提供動力的Real-time Customer Data Platform在以下方面的威力：

* 從多個源接收資料
* 將它們合併到單個 [!DNL real-time customer profile]
* 跨設備提供一致、相關和個性化的體驗。

## 使用案例

運動服裝公司Luma一直在努力改善客戶體驗。 他們有一項新計畫來增加與禮品相關的銷售。 他們還希望減少過度曝光，比如隨顧隨便的煩人廣告。

目前，他們在媒體上花了太多錢，針對訪問者不會購買的商品進行重新定位。 例如，Luma不希望將某個項目重新定為目標，該項目旨在為其他人一次性購買。

目前， Luma的資料分散在多個源中。 因此，他們面臨著重大挑戰：

* 市場營銷組織必須與各自擁有資料源的不同團隊合作，包括網站、移動應用、忠誠系統、CRM等。
* 當營銷團隊訪問資料時，資料往往已過時，不再適合他們對時間敏感的活動。
* 他們需要統一資料，以便瞄準一個人，而不是渠道。

因此，Luma有以下業務目標：

* 從不同的資料源建立其消費者的即時單一視圖。
* 利用不同渠道和設備上的相關資訊個性化營銷活動。

要實現這些目標，營銷團隊需要能夠按規模管理客戶資料。

由於Real-Time CDP由Adobe Experience Platform提供動力，Luma的營銷組織可以：

1. 從不同的平台收集資料並確保資料在下游可用於其他營銷活動。
1. 建立其消費者的單一、即時視圖，而與資料發源地無關。
1. 在每個觸點上提供一致、相關和個性化的體驗。

## 步驟

本教程包括以下步驟：

1. 構建 [客戶配置檔案](#customer-profile)。
1. [個性化](#personalizing-the-user-experience) 用戶體驗。
1. 使用 [多個資料源](#using-multiple-data-sources)。
1. [設定資料來源](#configuring-a-data-source).
1. [收集資料](#bringing-the-data-together-for-a-specific-customer) 為特定客戶。
1. 設定 [段](#segments)。
1. 設定 [目的地](#destinations)。
1. [跨設備縫製配置檔案](#cross-device-identity-stitching)。
1. [分析配置檔案](#analyzing-the-profile)。

## 客戶配置檔案

當客戶首次訪問您的站點時，您對他們一無所知。

![image](assets/luma-site.png)

在導航時，資料被即時捕獲並不僅發送到Adobe Analytics的報告套件，還直接發送到Adobe Experience Platform。 在收集資料時，您開始根據中的行為資料形成消費者的單個視圖 [!DNL Experience Platform's real-time customer profile]。

許多訪問該網站的人可能都是以前從Luma購買過的顧客。  對Luma來說，對消息和產品進行個性化處理對新訪客和重訪客以及已知客戶來說非常重要。

### 新客戶的首次訪問

例如，一位獨具身份的訪客在Luma網站的「男人」區瀏覽，並看到一對穿著運動衫的夫婦。

![image](assets/luma-sweatshirts.png)

當客戶導航以瞭解有關這些產品的詳細資訊時，這些產品視圖將在Adobe Analytics收集併發送到 [!DNL Experience Platform]。

<!--![image](assets/luma-shirt-detail.png)-->

Luma可以將訪問者的行為映射到Adobe Experience Platform的用戶個人資料中，並開始收集更豐富的消費者行為視圖。

### 獲取客戶更詳細的視圖

隨著客戶繼續與網站互動，情況變得更加清晰。 例如，假定訪問者將產品添加到購物車並登錄。

當客戶登錄時，她把自己稱為莎拉·羅絲。

![image](assets/luma-login.png)

將合併兩個標識：

* 匿名瀏覽資料
* 與莎拉·羅斯的帳戶關聯的現有資料

兩個標識將合併到 [!DNL Experience Platform]。 盧瑪現在對這個消費者有了統一的看法。

根據網站「Men&#39;s部分中匿名訪問者的瀏覽行為，可能假定該客戶是男性。 現在她登錄了，Luma認出了Sarah Rose。 Luma使用 [!DNL Real-Time Customer Profile] 來改進通過渠道傳遞給她的資訊。

## 個性化用戶體驗

薩拉受到忠誠的歡迎，並感謝她是銅牌會員，掌握了更多關於福利以及如何提高她的地位和分數的資訊。

她導航到首頁以瀏覽更多內容。

![image](assets/luma-personal.png)

Sarah可以根據自己動態地獲得個性化首頁體驗 [!DNL Real-Time Customer Profile] 在Adobe Experience Platform。

多虧了Adobe Sensei在Adobe Target的個性化設計，她看到了相關內容，這考慮到了她過去的購買和對跑步服裝和裝備的親和力。 盧瑪還根據她最近的瀏覽量，為男性定制跑步服的男性目錄內容。

在頁面的下半部分，Sarah將顯示特色產品，並根據她最近查看的項目顯示一個新的推薦托盤。

此個性化內容可幫助Sarah快速查找相關項。 這增加了轉換，並提供了更令人愉快的客戶體驗。

### 將客戶帶回

莎拉分心了，離開了網站，結束了談話。 Luma可以利用她在Adobe Experience Platform的資料幫助她回到網站。

Real-time Customer Data Platform由Adobe Experience Platform公司提供支援，專為客戶體驗管理而打造。 它使組織能夠：

* 簡化資料整合和激活
* 控制已知和未知的資料使用情況
* 加快規模營銷使用案例

## 使用多項資料來源

Luma的團隊將他們的所有行為和客戶資料放在一個地方。

![image](assets/luma-dash.png)

他們可以從以下所有源中接收資料：

* 現有Adobe Experience Cloud解決方案資料
* 非Adobe來源，如Luma的忠誠計畫、呼叫中心和銷售點系統資料
* 從Luma資料源即時流資料
* 來自Adobe解決方案的即時資料（不需要新標籤）

所有來自不同來源的資料都合併到單個統一的客戶配置檔案中。

## 設定資料來源

使用 [!DNL Real-Time Customer Data Platform] 將新資料源引入平台。 Real-Time CDP公司包括一個資料源目錄，可以快速方便地添加到配置檔案中。

![image](assets/luma-source-cat.png)

例如，要接收Luma的CRM資料，請按 *CRM*，以及包含 *CRM* 清單中。 添加 [!DNL Microsoft Dynamics CRM] 資料：

1. 授權連接。

   ![image](assets/luma-source-auth.png)

1. 從建議的XDM預映射表清單中選擇要導入的內容。

   <!--    ![image](assets/luma-source-import.png) -->

   例如，選擇 **[!UICONTROL 聯繫人]**。 自動載入聯繫人資料的預覽，以確保一切看起來都像預期。

   Adobe Experience平台通過將標準欄位自動映射到 [!DNL Experience Data Model] (XDM)配置式架構。

1. 查看欄位映射。

   <!--    ![image](assets/luma-source-mapping.png) -->

   例如，按兩下聯繫人的電子郵件欄位是否已正確映射。\
   您可以選擇預覽資料並執行高級映射。

1. 設定計畫。

   ![image](assets/luma-source-sched.png)

都結束了。 您剛剛添加 [!DNL Microsoft CRM] 作為資料源 [!DNL Experience Platform]。

### 為使用策略的接收資料添加標籤

Luma有許多內部策略限制某些類型收集的資訊的使用，還必須遵守與資料使用有關的法律和隱私相關的顧慮。 使用Adobe Experience Platform資料治理，預定義的資料使用標籤可以應用於資料集（以及這些資料集中的特定欄位），使Luma能夠根據特定的使用限制對其資料進行分類。

![](assets/governance-labels.png)

一旦應用了資料使用標籤，Luma就可以使用資料管理建立資料使用策略。 資料使用策略是描述允許對包含某些標籤的資料執行的操作類型的規則。 當嘗試在Real-Time CDP執行構成策略違規的操作時，會阻止該操作，並發出警報以顯示違反了哪個策略以及原因。

## 為特定客戶將資料整合在一起

在此方案中，搜索Sarah Rose的配置檔案。 她的個人資料出現，還有她用來登錄的電子郵件。

<!-- ![image](assets/luma-find-profile.png) -->

Luma擁有的關於Sarah的所有配置檔案資訊都顯示出來。 這包括她的個人資訊，如地址和電話號碼、通信首選項以及她有資格獲得的段。

| 類別 | 說明 |
|---|---|
| 身分 | 顯示已連結到的身份 [!DNL Platform] 從莎拉和盧瑪在渠道和設備上的互動中。 顯示她來自網站的ECID。 她的身份還包括她移動應用的ECID、電子郵件ID、最近添加的 [!DNL Microsoft Dynamics] 資料集，以及從Luma忠誠系統傳入Adobe Experience Platform的忠誠ID。 |
| 活動 | 顯示Sarah與Luma品牌的所有交互資料。 這包括她剛剛看過的項目，她過去看過的任何東西，她收到的電子郵件，她與呼叫中心的互動，以及每次互動都發生在什麼渠道和設備上。 |

Real-Time CDP的簡介將Luma營銷團隊的工作流程從數週減少到數分鐘，並基於這個360度的客戶視圖，開啟個性化的可能性。 此配置檔案將她登錄前瀏覽站點時的行為資料與她現有的客戶配置檔案合併在一起，建立了Sarah的全面視圖。

營銷團隊可以使用這種增強功能， [!DNL Real-Time Customer Profile] 更好地個性化莎拉的體驗，並提升她對Luma的品牌忠誠度。

## 區段

強大的Adobe Experience Platform分段功能使營銷人員能夠根據在 [!DNL Real-Time Customer Profile]。

<!-- ![image](assets/luma-segments.png) -->

在這種情形中，莎拉最近在網站上的互動與她過去的行為不同。 她通常買女裝。 不過，她車裡的東西是男人的大運動衫。

Luma資料科學團隊已經建立了關於購買傾向的模型。 一個模型標識了現有消費者服裝類別（例如男女）或大小的突然變化。 莎拉的購物行為改變表明她不是在為自己購物。

<!-- ![image](assets/luma-gift.png) -->

### 定義段

修改或建立一個段，該段表示似乎正在購買禮品的購物車棄用者：

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

因為莎拉在購物車中添加了一個明顯的禮品，並放棄了它，所以Luma可以以免費禮品包為目標。

## 目的地

添加「贈送購物車放棄者」段時，您可以大致看到此段中有多少人。 您可以對其採取操作，並使其可用於跨渠道個性化。

選擇 **[!UICONTROL 發送到目標]**。

在Real-Time CDP,Luma可以無縫地在他們的觀眾群中為個性化而行動。\
在此，我們將看到Luma可以將此目標發送到的所有目標，包括Adobe和非Adobe解決方案：

![image](assets/luma-dest.png)

### 選擇目標

在此場景中，Luma希望通過以下目標將此受眾重新定為個性化目標：

* Google，展示

   <!--* Facebook -->
* Adobe Campaign，用於電子郵件

<!-- ![image](assets/luma-sched-dest.png) -->

### 計畫目標

您還可以安排段在特定時間開始或結束。 該段將在計畫日期在配置的平台上發佈並自動更新。

>[!NOTE]
>
>（可選）如果選擇日期欄位，則它會自動計畫90天外。

選擇 **[!UICONTROL 保存]** 的子菜單。

當此受眾中的客戶進行購買時，他們對此受眾的成員資格將被即時禁止。 他們不再有資格，因為他們的地位已經改變。

這樣，Luma媒體團隊的主管就可以省下數十萬美元，因為他們沒有為不合格的觀眾使用庫存。

### 強制目標的資料使用策略

Adobe Experience Platform包括隱私和安全控制，以確定是否可將段激活到特定目的地。 激活是基於建立時分配給目標的市場營銷目的，以及您的組織定義的資料使用策略來啟用或限制的。

如果活動違反策略，則會顯示警告。 此警告包含資料沿襲資訊，可幫助您確定違反策略的原因以及您可以採取什麼措施來解決違規。

有了這些控制， [!DNL Experience Platform] 幫助Luma負責任地遵守法規和市場。 這些控制是靈活的，可以修改以滿足Luma的安全和治理團隊的要求，使他們能夠自信地滿足管理已知和未知客戶資料的地區和組織要求。

### 資料流畫布

保存時，可視資料流畫布將顯示從統一配置檔案映射到您選擇的三個目標的段。

![image](assets/luma-flow.png)

## 跨設備身份拼接

莎拉在自己的移動設備上瀏覽一個社交媒體網站，她看到了一則Luma廣告。 它讓她想起她在車裡留下的東西。

後來，她開啟郵件，看到那些重新定向的電子郵件。 她從電子郵件中選擇到Luma的連結。

這個連結把莎拉帶到移動的Luma首頁，她在那裡看到了由Adobe Target提供的高度個性化的體驗。

* 她被歡迎為銅人。
* 她看到了「禮物」的訊息。
* 她還看到「免費禮品包裝」，這是她獲得銅牌會員資格的一部分。
* 她依然以她對跑步的親和力為目標。

她買毛衣，加上禮物包裝，還寫了禮物便條。 她還可以選擇記住這次活動，並在明年收到提醒，以便在此時得到禮物。 她說是的，第二年她將參加一個電子郵件活動，提醒她再買一件禮物。

由於觀眾壓制能力，莎拉不會成為那些男人的毛衣的目標。

## 分析配置檔案

Luma的營銷人員使用Adobe Experience Platform查看Real-Time CDP儀表板上的送禮器部分。 他們觀察了這項計畫的成果，並看到它正在增長。 客戶正在響應優惠，並投入更多資金。

這些洞見使營銷人員能夠對此信號採取行動，而這一點的推動因素是，讓CDP中提供此資料，讓像Sarah這樣的客戶連接到該段。

Luma使用此CDP資料來提高忠誠度和客戶滿意度。
