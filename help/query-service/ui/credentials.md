---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢；查詢編輯器；查詢編輯器；查詢編輯器；
solution: Experience Platform
title: 查詢服務認證指南
description: Adobe Experience Platform查詢服務提供使用者介面，可用於寫入和執行查詢、檢視以前執行的查詢，以及存取組織內使用者儲存的查詢。
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: 264d3b12d8fd3bd100018513af1576b3de1cbb33
workflow-type: tm+mt
source-wordcount: '1955'
ht-degree: 2%

---

# 認證指南

Adobe Experience Platform查詢服務可讓您與外部使用者端連線。 您可以使用即將到期的認證或不即將到期的認證來連線到這些外部使用者端。

>[!NOTE]
>
>此認證面板不會自動提供給所有使用者使用。如果您需要，請聯絡您的Adobe帳戶團隊以請求將[!UICONTROL 認證]索引標籤包含在查詢服務工作區中。 如有要求，此變更將適用於整個組織，並由Adobe的工程團隊執行。 這不是由使用者控制的設定。

## 到期的認證 {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="用戶端的 SSL 模式"
>abstract="必須在連線至查詢服務的用戶端中啟用 SSL。確保 SSL 模式設定為「要求」。"

您可以使用即將到期的認證來快速設定與外部使用者端的連線。

![已反白顯示[即將到期的認證]區段的[查詢儀表板認證]索引標籤。](../images/ui/credentials/expiring-credentials.png)

**[!UICONTROL 即將到期的認證]**&#x200B;區段提供下列資訊：

- **[!UICONTROL 主機]**：要連線使用者端的主機名稱。 這會合併您的組織名稱，如同在Experience Platform UI的頂端功能區中所示。
- **[!UICONTROL 連線埠]**：要連線之主機的連線埠號碼。
- **[!UICONTROL 資料庫]**：要連線使用者端的資料庫名稱。
- **[!UICONTROL 使用者名稱]**：用來連線到查詢服務的使用者名稱。
- **[!UICONTROL 密碼]**：用來連線到查詢服務的密碼。 UI中的密碼已進行雜湊處理，以提高安全性。 選取復製圖示(![復製圖示。](/help/images/icons/copy.png))，將您完整的未雜湊認證複製到剪貼簿。
- **[!UICONTROL PSQL命令]**：自動插入所有相關資訊的命令，供您在命令列上使用PSQL連線到查詢服務。
- **[!UICONTROL 到期]**：到期認證的到期日期和時間。 權杖的預設有效期間為24小時，但可在Admin Console的進階設定中變更。

>[!TIP]
>
>若要變更您即將到期的認證連線至查詢服務的工作階段期限，請瀏覽至[Admin Console](https://adminconsole.adobe.com/)，並在熒幕選項上選取下列專案： **設定** > **隱私權和安全性** > **驗證設定** > **進階設定** > **工作階段期限上限**。
>
>![反白顯示「隱私權與安全性」、「驗證設定」和「最長工作階段壽命」的Admin Console設定標籤。](../images/ui/credentials/max-session-life.png)
>
>請參閱Adobe說明檔案，以取得有關Admin Console所提供的[進階設定](https://helpx.adobe.com/tw/enterprise/using/authentication-settings.html#advanced-settings)的詳細資訊。

### 連線至查詢工作階段中的Customer Journey Analytics資料 {#connect-to-customer-journey-analytics}

使用Customer Journey Analytics BI擴充功能搭配Power BI或Tableau，使用SQL存取您的Customer Journey Analytics [資料檢視](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/cja-dataviews/data-views)。 藉由整合Query Service與BI擴充功能，您可以直接在Query Service工作階段中存取資料檢視。 此整合簡化了使用查詢服務作為其PostgreSQL介面的BI工具功能。 此功能消除了在BI工具中重複資料檢視的需求，確保跨平台的一致報告，並簡化了Customer Journey Analytics資料與BI平台中其他來源的整合。

請參閱檔案以瞭解如何[將Query Service連線至各種案頭使用者端應用程式](../clients/overview.md)，例如[Power BI](../clients/power-bi.md)或[Tableau](../clients/tableau.md)

>[!IMPORTANT]
>
>需要Customer Journey Analytics工作區專案和資料檢視才能使用此功能。

若要在Power BI或Tableau中存取Customer Journey Analytics資料，請選取[!UICONTROL 資料庫]下拉式功能表，然後從可用選項中選取`prod:cja`。 接著，複製您的[!DNL Postgres]認證引數（主機、連線埠、資料庫、使用者名稱及其他），以用於您的Power BI或Tableau設定。

![資料庫下拉式清單反白顯示的[查詢服務認證]索引標籤。](../images/ui/credentials/database-dropdown.png)

>[!NOTE]
>
>當您將Power BI或Tableau連線至Customer Journey Analytics時，將會使用查詢服務「並行工作階段」權益。 如果需要其他工作階段和查詢，可購買額外的臨時查詢使用者套件附加元件，以取得五個額外的並行工作階段和一個額外的並行查詢。

您也可以直接從Query Editor或Postgres CLI存取您的Customer Journey Analytics資料。 若要這麼做，請在撰寫查詢時參考`cja`資料庫。 請參閱查詢編輯器[查詢撰寫指南](./user-guide.md#query-authoring)，以取得如何撰寫、執行和儲存查詢的詳細資訊。

如需使用SQL存取Customer Journey Analytics資料檢視的完整指示，請參閱[BI擴充功能指南](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/cja-dataviews/bi-extension)。

## 不會到期的認證 {#non-expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_migratenonexpiringcredentials"
>title="移轉到 OAuth 伺服器對伺服器認證"
>abstract="由於JWT憑證將在2025年6月30日之後停止運作，因此需要進行此移轉。 大約需要30到40秒，並且啟動後無法取消。 所有現有工作和整合在移轉後仍可使用OAuth。 您可以離開此畫面並隨時返回以檢查狀態。"

您可以使用不會到期的認證來設定與外部使用者端之間更永久的連線。

>[!NOTE]
>
>不會到期的認證有下列限制：
>
>- 使用者必須以`{technicalAccountId}:{credential}`的格式使用使用者名稱和密碼登入。 在[產生認證](#generate-credentials)區段中可找到更多資訊。
>- 根據預設，不會到期的認證僅被授與執行`SELECT`個查詢的許可權。 若要執行`CTAS`或`ITAS`個查詢，請手動將「管理資料集」和「管理結構描述」許可權新增至與非到期認證相關的角色。 您可以在「資料模型」區段下找到「管理結構描述」許可權，且「管理資料集」許可權位於[Adobe Developer Console](<https://developer.adobe.com/console/>)的「資料管理」區段下。
>- 列出查詢物件時，協力廠商使用者端可能會以與預期不同的方式執行。 例如，某些協力廠商使用者端（例如[!DNL DB Visualizer]）不會在左側面板中顯示檢視名稱。 不過，若在`SELECT`查詢中呼叫，則可存取檢視名稱。 同樣地，[!DNL PowerUI]可能不會列出透過SQL建立的暫時檢視，以供在建立儀表板時選取。

### 先決條件

您必須先在Adobe Admin Console中完成下列步驟，才能產生不會到期的認證：

1. 登入[Adobe Admin Console](https://adminconsole.adobe.com/)，並從上方導覽列中選取相關組織。
2. [選取產品設定檔。](../../access-control/ui/browse.md)
3. [針對產品設定檔設定&#x200B;**沙箱**&#x200B;和&#x200B;**管理查詢服務整合**&#x200B;許可權](../../access-control/ui/permissions.md)。
4. [將新的使用者新增至產品設定檔](../../access-control/ui/users.md)，以便授予他們設定的許可權。
5. [將使用者新增為產品設定檔管理員](https://helpx.adobe.com/tw/enterprise/using/manage-product-profiles.html)，以允許為任何使用中的產品設定檔建立帳戶。
6. [將使用者新增為產品設定檔開發人員](https://helpx.adobe.com/jp/enterprise/using/manage-developers.html)，以建立整合。

若要深入瞭解如何指派許可權，請閱讀有關[存取控制](../../access-control/home.md)的檔案。

現在，所有必要的許可權已在Adobe Developer Console中設定，讓使用者能使用即將到期的認證功能。

### 產生認證 {#generate-credentials}

若要建立一組不會到期的認證，請返回Experience Platform UI並從左側導覽選取&#x200B;**[!UICONTROL 查詢]**&#x200B;以存取[!UICONTROL 查詢]工作區。 接著，選取&#x200B;**[!UICONTROL 認證]**&#x200B;標籤，接著選取&#x200B;**[!UICONTROL 產生認證]**。

![顯示[認證]索引標籤和[產生認證]的查詢儀表板。](../images/ui/credentials/generate-credentials.png)

會出現一個對話方塊，讓您產生認證。 若要建立不會到期的認證，您必須提供下列詳細資料：

- **[!UICONTROL 名稱]**：您正在產生的認證名稱。
- **[!UICONTROL 描述]**： （選擇性）您產生的認證描述。
- **[!UICONTROL 指派給]**：將指派認證的使用者。 此值應為建立認證之使用者的電子郵件地址。
- **[!UICONTROL 密碼]** （選擇性）您認證的選擇性密碼。 如果未設定密碼，Adobe會自動為您產生密碼。

提供所有必要的詳細資料後，請選取&#x200B;**[!UICONTROL 產生認證]**&#x200B;以產生您的認證。

![[產生認證]對話方塊已反白顯示。](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>選取&#x200B;**[!UICONTROL 產生認證]**&#x200B;時，會將組態JSON檔案下載到您的本機電腦。 由於Adobe **不會**&#x200B;記錄產生的認證，因此您必須安全地儲存下載的檔案，並保留認證的記錄。
>
>此外，如果認證在90天內未使用，認證將會被清除。

設定JSON檔案包含技術帳戶名稱、技術帳戶ID和認證等資訊。 提供下列格式。

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

儲存您產生的認證之後，請選取&#x200B;**[!UICONTROL 關閉]**。 您現在可以看到所有不會到期的認證清單。

![反白顯示[未到期認證]區段的[查詢儀表板認證]索引標籤。](../images/ui/credentials/list-credentials.png)

您可以編輯或刪除不會到期的認證。 若要編輯不會到期的認證，請選取鉛筆圖示(![鉛筆圖示。](/help/images/icons/edit.png))。 若要刪除不會到期的認證，請選取刪除圖示（![垃圾桶圖示。](/help/images/icons/delete.png)）。

編輯不會到期的認證時，強制回應視窗會出現。 您可以提供下列詳細資料以進行更新：

- **[!UICONTROL 名稱]**：您正在產生的認證名稱。
- **[!UICONTROL 描述]**： （選擇性）您產生的認證描述。
- **[!UICONTROL 指派給]**：將指派認證的使用者。 此值應為建立認證之使用者的電子郵件地址。

![更新帳戶對話方塊。](../images/ui/credentials/update-credentials.png)

提供所有必要的詳細資料後，請選取&#x200B;**[!UICONTROL 更新帳戶]**&#x200B;以完成認證的更新。

### 將認證移轉至OAuth {#migrate-credentials}

如果您使用不會到期的JWT憑證，您必須在2025年6月30日之前將每個憑證移轉至OAuth伺服器對伺服器，以避免服務中斷。

>[!IMPORTANT]
>
>JWT憑證將在2025年6月30日後停止運作。 您必須手動完成此移轉以維持授權。

若要瞭解如何識別受影響的認證並完成移轉，請參閱[從JWT移轉至OAuth伺服器對伺服器認證指南](./migrate-jwt-to-oauth.md)。

如需瞭解常見問題，請參閱[移轉常見問題集](./migrate-jwt-to-oauth.md#faq)。

## 使用認證來連線到外部使用者端 {#use-credential-to-connect}

您可以使用到期或不到期的認證來連線至外部使用者端，例如Aqua Data Studio、Looker或Power BI。 這些憑證的輸入方法會因外部使用者端而異。 請參閱外部使用者端檔案，取得使用這些憑證的特定指示。

此影像會指出在UI中找到的每個引數的位置，但不包括不會到期的認證的密碼。 雖然不會到期的認證是由其JSON設定檔案所提供，但您可以在UI的&#x200B;**認證**&#x200B;標籤下檢視即將到期的認證。

![已反白顯示[即將到期的認證]區段的[查詢]工作區[認證]索引標籤。](../images/ui/credentials/expiring-credentials.png)

下表概述連線至外部使用者端時通常所需的引數。

>[!NOTE]
>
>使用不會到期的認證連線到主機時，除了密碼和使用者名稱外，仍需使用[!UICONTROL 即將到期的認證]區段中列出的所有引數。
>輸入使用者名稱與密碼的格式使用冒號分隔值，如本範例`username:{your_username}`和`password:{password_string}`所示。

| 參數 | 說明 | 範例 |
|---|---|---|
| **伺服器/主機** | 您連線的伺服器/主機名稱。 <ul><li>此值同時用於即將到期的認證和不即將到期的認證，並且採用`server.adobe.io`的形式。 在[!UICONTROL 即將到期的認證]區段的&#x200B;**[!UICONTROL 主機]**&#x200B;下找到值。</ul></li> | `acme.platform.adobe.io` |
| **連線埠** | 您連線的伺服器/主機連線埠。 <ul><li>此值同時用於即將到期的認證和不即將到期的認證，可以在[!UICONTROL 即將到期的認證]區段的&#x200B;**[!UICONTROL 連線埠]**&#x200B;下找到。</ul></li> | `80` |
| **資料庫** | 您正在連線的資料庫。 <ul><li>此值同時用於到期認證和不到期認證，並且可在[!UICONTROL 到期認證]區段的&#x200B;**[!UICONTROL 資料庫]**&#x200B;下找到。 </ul></li> | `prod:all` |
| **使用者名稱** | 連線到外部使用者端的使用者使用者名稱。 <ul><li>此值會用於即將到期的認證和不即將到期的認證。 它採用`@AdobeOrg`之前的英數字串形式。 此值位於&#x200B;**[!UICONTROL 使用者名稱]**&#x200B;下。</li></ul> | `ECBB80245ECFC73E8A095EC9@AdobeOrg` |
| **密碼** | 連線到外部使用者端的使用者密碼。 <ul><li>如果您正在使用即將到期的認證，可在[!UICONTROL 即將到期的認證]區段的&#x200B;**[!UICONTROL 密碼]**&#x200B;下找到此認證。</li><li>如果您使用不會到期的認證，此值是來自technicalAccountID的串連引數，以及從設定JSON檔案取得的認證。 密碼值的格式為： `{technicalAccountId}:{credential}`。</li></ul> | <ul><li>即將到期的認證密碼超過一千個字元的英數字串。 將不會提供範例。</li><li>不會到期的認證密碼如下： <br>`4F2611B8613DK3670V495N55:3d182fa9e0b54f33a7881305c06203ee`</li></ul> |

{style="table-layout:auto"}

## 後續步驟

現在您已瞭解即將到期和未到期的認證的運作方式，您可以使用這些認證來連線至外部使用者端。 如需有關外部使用者端的詳細資訊，請參閱[將使用者端連線至查詢服務指南](../clients/overview.md)。
