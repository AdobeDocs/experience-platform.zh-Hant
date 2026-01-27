---
title: Salesforce Marketing Cloud (V2) Source概觀
description: 瞭解如何使用API或使用者介面將Salesforce Marketing Cloud (V2)連線至Adobe Experience Platform。
source-git-commit: 3c200ff1a29c3462a5d4fef554f6a410cfcbdde8
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud] (V2)來源概觀

>[!IMPORTANT]
>
>自2026年1月起，已棄用原始[[!DNL Salesforce Marketing Cloud] (V1)](salesforce-marketing-cloud.md)來源。 這個已棄用的來源沒有可用的移轉，您必須使用新的[!DNL Salesforce Marketing Cloud] (V2)來源重新實作您的資料。

Adobe [Real-Time CDP](../../../rtcdp/overview.md)與[!DNL Salesforce Marketing Cloud]之間的整合旨在運用資料延伸模組，因為資料延伸模組可提供彈性和控制力。 標準系統表格（資料檢視和內建物件）僅限於預先定義的欄位，且主要提供系統層級的追蹤，不同之處在於，您可以使用資料擴充功能來定義自訂欄位、組織各種企業特定資料，以及量身打造資料結構以符合獨特的需求。

由於這種程度的自訂和可擴充性，Real-Time CDP與[!DNL Salesforce Marketing Cloud]之間的整合依賴資料延伸模組，而非標準系統資料表。 此方法提供更靈活、可擴充及整合的資料管理基礎，確保符合您的業務目標

您可以使用[!DNL Salesforce Marketing Cloud]來源將您的[!DNL Salesforce Marketing Cloud]帳戶連線至Real-Time CDP和Adobe Experience Platform。 請閱讀以下檔案，瞭解如何開始使用。

## 使用案例範例 {#use-case-examples}

### 使用聯絡資料個人化電子郵件行銷活動

零售品牌想要根據客戶生命週期階段（例如，新客戶、回頭客、忠誠客戶）個人化電子郵件行銷活動。 為此，他們會建立聯絡資料擴充功能，以儲存關鍵客戶資訊，包括名稱、電子郵件、生命週期階段和購買行為。 然後這些資料會擷取至Experience Platform，以更深入地進行細分和目標定位。

透過將聯絡資料擴充功能的資料擷取至Experience Platform，品牌可以根據客戶的生命週期階段和購買行為來劃分客戶。 例如，他們可以傳送歡迎優惠給新客戶、向回頭客提供忠誠度獎勵，或甚至透過鎖定優惠重新與不活躍的客戶互動。 此方法可確保個人化溝通，並促成更相關且有效的客戶參與。

### 擷取Campaign資料以進行個人化細分

行銷團隊想要根據客戶與先前行銷活動的參與度來鎖定客戶，以最佳化電子郵件行銷活動。 為此，他們在[!DNL Salesforce Marketing Cloud]中建立Campaign資料擴充功能，以儲存客戶參與資料，例如電子郵件開啟、點按和行銷活動回應。 然後，這些資料會擷取到Experience Platform中，以供進一步細分和個人化。

透過將此資料從Campaign資料擴充功能擷取至Experience Platform，行銷團隊可以根據過去的參與來細分客戶，例如點選產品優惠或正面回應的客戶。 參與的客戶可在未來的電子郵件中收到目標促銷活動，而回應為負面的客戶則可傳送客戶服務後續追蹤。 這項與Experience Platform的整合可確保行銷團隊能根據客戶行為提供更個人化且相關的內容。

### 根據活動資料鎖定客戶

行銷團隊想要根據客戶的活動（例如網站造訪、表單提交或與先前電子郵件行銷活動的互動）來鎖定客戶。 為了達成此目的，他們會建立活動資料擴充功能，以儲存有關每個客戶參與活動的資訊。 然後，這些資料會擷取到Experience Platform中，以便進一步細分和個人化的行銷活動目標定位。

行銷團隊可從活動資料擴充功能擷取資料至Experience Platform，藉此根據客戶的參與歷史記錄進行客戶細分。 例如，如果客戶最近造訪網站但未完成購買，系統會傳送包含特殊優惠的提醒電子郵件。 同樣地，填寫表單的客戶可收到個人化的後續追蹤通訊。 此方法可確保每位客戶都能根據其最近的活動收到相關內容，進而提高參與度和轉換率。

## 先決條件 {#prerequisites}

請閱讀以下章節，瞭解在將來源連線至Experience Platform之前，必須完成的先決條件設定。

### 設定驗證的應用程式 {#set-up-application-for-authentication}

建立與[!DNL Salesforce Marketing Cloud]的整合時，第一步是在&#x200B;**中建立**&#x200B;已安裝的封裝[!DNL Salesforce Marketing Cloud]。 安裝的套件會產生驗證API呼叫所需的使用者端憑證、定義整合型別和關聯的許可權範圍。 此外，安裝的套件為您的租使用者提供正確的API端點。 此外，它還是管理、監視和撤銷存取權的受管容器，確保所有整合功能安全、可稽核，並符合Salesforce建議的驗證模式。

若要建立已安裝的套件，請使用[!DNL Salesforce Marketing Cloud] UI並導覽至&#x200B;**[!DNL Setup]** > **[!DNL Apps]** > **[!DNL Installed Packages]**，然後選取&#x200B;**[!DNL New]**。 使用[!DNL New Package Details]介面提供封裝的名稱和資訊。 完成後，選取&#x200B;**[!DNL Save]**。

![Salesforce Marketing Cloud UI的新套件介面。](../../images/tutorials/create/sfmc/new-package.png)

建立新封裝之後，請選取&#x200B;**[!DNL Add Component]**。

![Salesforce Marketing Cloud UI的新增元件介面。](../../images/tutorials/create/sfmc/add-component.png)

選取&#x200B;**[!DNL API Integration]**&#x200B;作為您的元件型別。

![已選取「API整合」的元件選取視窗。](../../images/tutorials/create/sfmc/api-integration.png)

選取&#x200B;**[!DNL Server-to-Server]**&#x200B;作為您的整合型別。

![整合型別選取視窗](../../images/tutorials/create/sfmc/server-to-server.png)

最後，導覽至&#x200B;**[!DNL Scope]** > **[!DNL Data]**。 在&#x200B;**[!DNL Data Extensions]**&#x200B;下，選取&#x200B;**[!DNL Read]**。

![Salesforce行銷中範圍的資料延伸區段](../../images/tutorials/create/sfmc/data-extensions.png)

選取&#x200B;**[!DNL Save]**，然後複製並儲存您的&#x200B;**使用者端密碼**。 完成後，選取&#x200B;**[!DNL Finish]**。

![產生使用者端密碼的Salesforce Marketing Cloud視窗。](../../images/tutorials/create/sfmc/generate-secret.png)

在離開[!DNL Salesforce Marketing Cloud] UI之前，請複製&#x200B;**使用者端識別碼**&#x200B;和&#x200B;**唯一的基底URI首碼**，因為您將使用這兩個值來建立與Experience Platform的連線。 對於驗證基礎URI，請確保在`.auth.marketingcloudapis.com/`之後移除所有內容

![可擷取使用者端ID和唯一基底URI的Salesforce Marketing Cloud元件介面。](../../images/tutorials/create/sfmc/client-id-and-uri.png)

如需建立已安裝套件的詳細步驟，請參閱[[!DNL Salesforce] 檔案](https://trailhead.salesforce.com/content/learn/modules/marketing-cloud-developer-basics/set-up-your-developer-environment)。

### 收集必要的認證 {#gather-required-credentials}

您必須提供下列認證的值，才能將[!DNL Salesforce Marketing Cloud]連線至Experience Platform。

| 認證 | 說明 |
| --- | --- |
| 用戶端 ID | 授權Experience Platform時，[!DNL Salesforce Marketing Cloud]用來識別您帳戶的公開識別碼。 可從[!DNL Salesforce Marketing Cloud] UI的元件面板擷取使用者端ID。 |
| 用戶端密碼 | 只有使用者端應用程式和授權伺服器才知道的機密金鑰。 您可以依照上述[應用程式設定步驟來產生使用者端密碼](#set-up-application-for-authentication)。 |
| 基底端點 | [!DNL Salesforce Marketing Cloud]的驗證基底URI的前置詞。 |

{style="table-layout:auto"}

## 將[!DNL Salesforce Marketing Cloud]連線至Experience Platform

繼續在Experience Platform中設定您的[!DNL Salesforce Marketing Cloud]來源連線。 如需透過UI設定連線的逐步指南，請參閱這裡的[教學課程](../../tutorials/ui/create/marketing-automation/sfmc.md)。 閱讀本教學課程，瞭解如何連線您的[!DNL Salesforce Marketing Cloud]帳戶、選取資料、對應欄位、排程內嵌及監視資料流程。
