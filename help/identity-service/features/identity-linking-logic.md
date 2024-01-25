---
title: Identity Service連結邏輯
description: 瞭解Identity Service如何連結不同的身分，以建立客戶的完整檢視。
exl-id: 1c958c0e-0777-48db-862c-eb12b2e7a03c
source-git-commit: 2b6700b2c19b591cf4e60006e64ebd63b87bdb2a
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 0%

---

# Identity Service連結邏輯

當身分名稱空間和身分值相符時，就會建立兩個身分之間的連結。

有兩種型別的身分會連結：

* **設定檔記錄**：這些身分通常來自CRM系統。
* **體驗事件**：這些身分識別通常來自WebSDK實作或Adobe Analytics來源。

## 建立連結的語意意義

身分代表真實世界的實體。 如果在兩個身分之間建立了連結，則表示兩個身分會彼此相關聯。 以下範例說明此概念：

| 動作 | 已建立的連結 | 含義 |
| --- | --- | --- |
| 一般使用者使用電腦登入。 | CRM ID與ECID會連結在一起。 | 使用者(CRM ID)所擁有的裝置具有瀏覽器(ECID)。 |
| 一般使用者使用iPhone匿名瀏覽。 | IDFA與ECID連結。 | Apple硬體裝置(IDFA) (例如iPhone)會與瀏覽器(ECID)建立關聯。 |
| 一般使用者先使用Google Chrome，再使用Firefox登入。 | CRM ID已與兩個不同的ECID連結。 | 人員(CRM ID)與2個網頁瀏覽器相關聯(**注意**：每個瀏覽器都有自己的ECID)。 |
| 資料工程師會擷取CRM記錄，該記錄包含兩個標示為身分的欄位： CRM ID和電子郵件。 | CRM ID與電子郵件已連結。 | 人員(CRM ID)已與此電子郵件地址相關聯。 |

## 瞭解Identity Service連結邏輯

身分由身分名稱空間和身分值組成。

* 身分名稱空間是指定的身分值目標的前後關聯。 常見的身分識別名稱空間範例包括CRM ID、電子郵件和電話。
* 身分值是代表真實世界實體的字串。 例如：「julien」<span>@acme.com」可以是電子郵件名稱空間的身分值，555-555-1234可以是電話名稱空間的對應身分值。

>[!TIP]
>
>身分名稱空間很重要，因為如果沒有它，身分值就會遺失其上下文，而且沒有足夠的資訊來成功比對身分。

如需有關Identity Service連結邏輯運作方式的視覺化表示法，請參閱下列圖表：

>[!BEGINTABS]

>[!TAB 現有圖表]

假設您有一個具有三個連結身分的現有身分圖表：

* 電話：(555)-555-1234
* 電子郵件：julien<span>@acme.com
* CRM ID：60013ABC

![現有圖表](../images/identity-settings/existing-graph.png)

>[!TAB 傳入資料]

一對身分識別已擷取到您的圖表中，而且此對包含：

* CRM ID：60013ABC
* ECID：100066526

![傳入資料](../images/identity-settings/incoming-data.png)

>[!TAB 已更新圖表]

Identity Service可辨識您的圖形中已存在CRM ID：60013ABC，因此僅連結新的ECID

![更新的圖表](../images/identity-settings/updated-graph.png)

>[!ENDTABS]

## 客戶案例

您是資料工程師，且將下列CRM資料集（設定檔記錄）擷取至Experience Platform。

| CRM ID** | 電話* | 電子郵件* | 名字 | 姓氏 |
| --- | --- | --- | --- | --- |
| 60013ABC | 555-555-1234 | 朱利安<span>@acme.com | 朱利安 | Smith |
| 31260XYZ | 777-777-6890 | evan<span>@acme.com | Evan | Smith |

>[!NOTE]
>
>* `**`  — 代表標示為主要身分的欄位。
>* `*`  — 代表標示為次要身分的欄位。
>
>身分服務無法區分主要身分和次要身分。 只要欄位標示為身分，就會將其擷取至Identity Service。

您也已實施WebSDK並內嵌包含以下資料表格的WebSDK資料集（體驗事件）：

| 時間戳記 | 事件中的身分* | 活動 |
| --- | --- | --- |
| `t=1` | ECID：38652 | 檢視首頁 |
| `t=2` | ECID：38652， CRM ID：31260XYZ | 搜尋鞋子 |
| `t=3` | ECID：44675 | 檢視首頁 |
| `t=4` | ECID：44675， CRM ID： 31260XYZ | 檢視購買記錄 |

每個事件的主要身分將會根據 [如何設定資料元素型別](../../tags/extensions/client/web-sdk/data-element-types.md).

>[!NOTE]
>
>* 如果您選取CRM ID作為主要身分，則已驗證的事件（具有包含CRM ID和ECID之身分對應的事件）將具有CRM ID的主要身分。 對於未驗證的事件（具有僅包含ECID之身分對應的事件），將具有ECID的主要身分識別。 Adobe建議使用此選項。
>
>* 如果您選取ECID作為主要身分，則無論驗證狀態為何，ECID都會成為主要身分。

在此範例中：

* `t=1`，使用桌上型電腦(ECID：38652)並匿名檢視首頁。
* `t=2`，使用相同的桌上型電腦，登入(CRM ID：31260XYZ)然後搜尋鞋子。
   * 使用者登入後，事件會將ECID和CRM ID傳送至Identity Service。
* `t=3`，使用筆記型電腦(ECID：44675)且以匿名方式瀏覽。
* `t=4`，使用相同的筆記型電腦，登入(CRM ID： 31260XYZ)然後檢視購買記錄。


>[!BEGINTABS]

>[!TAB timestamp=0]

在 `timestamp=0`，您有兩個適用於不同客戶的身分圖表。 兩者分別由三個連結的身分表示。

| | CRM ID | 電子郵件 | 電話 |
| --- | --- | --- | --- |
| Customer one | 60013ABC | 朱利安<span>@acme.com | 555-555-1234 |
| 客戶二 | 31260XYZ | evan<span>@acme.com | 777-777-6890 |

![timestamp-0](../images/identity-settings/timestamp-zero.png)

>[!TAB timestamp=1]

在 `timestamp=1`，客戶使用筆記型電腦造訪您的電子商務網站、檢視您的首頁並匿名瀏覽。 此匿名瀏覽事件可識別為ECID：38652。 由於Identity Service只會儲存至少有兩個身分的事件，因此不會儲存此資訊。

![timestamp-one](../images/identity-settings/timestamp-one.png)

>[!TAB timestamp=2]

在 `timestamp=2`，客戶使用相同的筆記型電腦造訪您的電子商務網站。 使用者會使用自己的使用者名稱和密碼組合登入，並瀏覽尋找鞋子。 身分識別服務會在客戶登入時識別其帳戶，因為它對應至其CRM ID： 31260XYZ。 此外，Identity Service會將ECID：38562與CRM ID：31260XYZ建立關聯，因為兩者在相同裝置上使用相同的瀏覽器。

![timestamp-2](../images/identity-settings/timestamp-two.png)

>[!TAB timestamp=3]

在 `timestamp=3` 客戶使用平板電腦造訪您的電子商務網站，並以匿名方式瀏覽。 此匿名瀏覽事件可識別為ECID：44675。 由於Identity Service只會儲存至少有兩個身分的事件，因此不會儲存此資訊。

![timestamp-3](../images/identity-settings/timestamp-three.png)

>[!TAB timestamp=4]

在 `timestamp=4`，客戶使用相同的平板電腦，登入其帳戶(CRM ID：31260XYZ)並檢視其購買記錄。 此事件會將其CRM ID：31260XYZ連結至指派給匿名瀏覽活動、ECID：44675的Cookie識別碼，並將ECID：44675連結至客戶2的身分圖表。

![timestamp-4](../images/identity-settings/timestamp-four.png)

>[!ENDTABS]
