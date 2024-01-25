---
title: 身分最佳化演演算法
description: 瞭解Identity Service中的身分最佳化演演算法。
hide: true
hidefromtoc: true
badge: Alpha
exl-id: 5545bf35-3f23-4206-9658-e1c33e668c98
source-git-commit: 3fe94be9f50d64fc893b16555ab9373604b62e59
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 1%

---

# 身分最佳化演演算法

>[!IMPORTANT]
>
>身分最佳化演演算法Alpha。 功能和檔案可能會有所變更。

身分最佳化演演算法是有助於確保身分圖表能代表單一人員，因此可防止即時客戶個人檔案中不需要的身分合併。

## 輸入引數

單一合併的個人檔案及其對應的身分圖表應代表單一個人（個人實體）。 一般來說，一個人會以CRM ID和/或登入ID表示。 我們預期不會將兩個個人(CRM ID)合併至單一設定檔或圖表。

您必須使用身分最佳化演演算法，指定哪些名稱空間代表Identity Service中的個人實體。 例如，如果CRM資料庫定義使用者帳戶與單一CRM ID和單一電子郵件地址相關聯，則此沙箱的身分設定如下：

* CRM ID名稱空間=唯一
* 電子郵件名稱空間=唯一

您宣告為唯一的名稱空間會自動設定為指定身分圖表中的最大限製為1。 例如，如果您宣告CRM ID名稱空間為唯一，則身分圖表只能有一個包含CRM ID名稱空間的身分。

>[!NOTE]
>
>* 目前，演演算法僅支援使用單一登入識別碼（一個登入名稱空間）。 目前不支援多個登入識別碼（用於登入的多個身分名稱空間）、家用實體圖表和階層式圖表結構。
>
>* 作為人員識別碼以及用在沙箱中以產生身分圖表的所有名稱空間都必須標示為唯一的名稱空間。 否則，您可能會看到不想要的連結結果。

## 程序

擷取新身分時，Identity Service會檢查新身分及其對應的名稱空間是否會導致超過設定的限制。 如果未超過限制，則會繼續擷取新的身分，而且這些身分將會連結到圖表。 但是，如果超過限制，身分最佳化演演算法會更新圖表，以便遵循最新的時間戳記，並移除優先順序較低名稱空間的最舊連結。

## 身分最佳化演演算法的範例案例

下節會概述身分最佳化演演算法在共用裝置或擷取具有相同時間戳記的資料等情境下的行為。

### 共用裝置

共用裝置是指由超過一個使用者使用的裝置。 例如，共用裝置可以是您與合作夥伴或家庭成員共用的筆記型電腦或平板電腦、圖書館電腦或公用資訊站。

>[!BEGINTABS]

>[!TAB 範例一]

| 命名空間 | 限制 |
| --- | --- |
| CRM ID | 1 |
| 電子郵件 | 1 |
| ECID | 不適用 |

在此範例中，CRM ID和電子郵件都被指定為不重複的名稱空間。 在 `timestamp=0`，CRM記錄資料集會擷取並因為限制設定而建立兩個不同的圖形。 每個圖表都包含CRM ID和電子郵件名稱空間。

* `timestamp=1`： Jane使用筆記型電腦登入您的電子商務網站。 Jane以她的CRM ID和電子郵件呈現，而她所使用筆記型電腦上的網頁瀏覽器則以ECID呈現。
* `timestamp=2`： John使用相同的筆記型電腦登入您的電子商務網站。 John由他的CRM ID和電子郵件代表，而他使用的網頁瀏覽器已由ECID代表。 由於相同的ECID連結至兩個不同的圖表，Identity Service可得知此裝置（筆記型電腦）為共用裝置。
* 不過，由於限制設定，每個圖表最多只能設定一個CRM ID名稱空間和一個電子郵件名稱空間，身分最佳化演演算法會將圖表分割為兩個。
   * 最後，由於John是最後驗證的使用者，因此代表筆記型電腦的ECID仍會連結至他的圖表，而非Jane&#39;s。

![共用裝置案例一](../images/identity-settings/shared-device-case-one.png)

>[!TAB 範例二]

| 命名空間 | 限制 |
| --- | --- |
| CRM ID | 1 |
| ECID | 不適用 |

在此範例中，CRM ID名稱空間會指定為唯一的名稱空間。

* `timestamp=1`： Jane使用筆記型電腦登入您的電子商務網站。 她的CRM ID代表自己，而筆記型電腦上的網頁瀏覽器則以ECID代表。
* `timestamp=2`： John使用相同的筆記型電腦登入您的電子商務網站。 他由自己的CRM ID表示，而他使用的網頁瀏覽器由相同的ECID表示。
   * 此事件會將兩個獨立的CRM ID連結至相同的ECID，超過設定的一個CRM ID限制。
   * 因此，身分最佳化演演算法會移除較舊的連結，在此例中是連結在Jane的CRM ID `timestamp=1`.
   * 不過，雖然Jane的CRM ID不再以Identity Service的圖表形式存在，但仍會以即時客戶設定檔的設定檔形式持續存在。 這是因為身分圖表必須至少包含兩個連結的身分，並且在移除連結後，Jane的CRM ID不再擁有可連結的另一個身分。

![shared-device-case-2](../images/identity-settings/shared-device-case-two.png)

>[!ENDTABS]

### 錯誤的電子郵件

在某些情況下，使用者可能會輸入錯誤的電子郵件和/或電話號碼值。

| 命名空間 | 限制 |
| --- | --- |
| CRM ID | 1 |
| 電子郵件 | 1 |
| ECID | 不適用 |

在此範例中，CRM ID和電子郵件名稱空間會指定為唯一。 請考慮Jane和John使用錯誤的電子郵件值（例如，測試）登入您的電子商務網站的案例<span>@test.com)。

* `timestamp=1`： Jane在其iPhone上使用Safari登入您的電子商務網站，建立其CRM ID （登入資訊）和ECID （瀏覽器）。
* `timestamp=2`： John在其iPhone上使用Google Chrome登入您的電子商務網站，建立其CRM ID （登入資訊）和ECID （瀏覽器）。
* `timestamp=3`：您的資料工程師會擷取Jane的CRM記錄，導致其CRM ID連結至不良電子郵件。
* `timestamp=4`：您的資料工程師會擷取John的CRM記錄，因此他的CRM ID會連結至不良電子郵件。
   * 接著會違反設定的限制，因為這會建立具有兩個CRM ID名稱空間的單一圖表。
   * 因此，身分最佳化演演算法會刪除較舊的連結，在此例中，這是Jane具有CRM ID名稱空間的身分與具有測試的身分之間的連結<span>@test。

使用身分最佳化演演算法，不正確的身分值（例如假電子郵件或電話號碼）不會傳播到數個不同的身分圖表中。

![錯誤電子郵件](../images/identity-settings/bad-email.png)

### 匿名事件關聯

ECID會儲存未驗證（匿名）的事件，而CRM ID會儲存已驗證的事件。 若是共用裝置，ECID （未驗證事件的持有者）會與 **上次驗證的使用者**.

請檢視下圖，深入瞭解匿名事件關聯的運作方式：

* Kevin和Nora共用平板電腦。
   * `timestamp=1`： Kevin使用帳戶登入電子商務網站，並建立其CRM ID （登入資訊）和ECID （瀏覽器）。 登入時，Kevin現在被視為最後驗證的使用者。
   * `timestamp=2`： Nora使用她的帳戶登入電子商務網站，因此建立她的CRM ID （登入資訊）和相同的ECID。 登入時，Nora現在被視為最後驗證的使用者。
   * `timestamp=3`：Kevin使用平板電腦瀏覽電子商務網站，但未使用帳戶登入。 Kevin的瀏覽活動會儲存在ECID中，而此ECID又與Nora相關聯，因為她是最後驗證的使用者。 此時，Nora擁有匿名活動。
      * 在Kevin再次登入之前，Nora的合併設定檔將與針對ECID儲存的所有未驗證事件相關聯（其中事件是ECID是主要身分）。
   * `timestamp=4`：Kevin第二次登入。 此時，他再次成為最後驗證的使用者，且現在擁有未驗證的事件：
      * 在他初次登入之前，於 `timestamp=1`；和
      * 他或Nora在匿名瀏覽中間Kevin第一次登入和第二次登入時所做的任何活動。

![anon-event-association](../images/identity-settings/anon-event-association.png)


## 後續步驟

如需身分圖表連結規則的詳細資訊，請參閱下列檔案：

* [身分圖表連結規則概觀](./overview.md)
* [設定身分圖表連結規則的範例案例](./example-scenarios.md)
* [身分連結邏輯](../features/identity-linking-logic.md)
* [Identity Service和即時客戶個人檔案](../identity-and-profile.md)
