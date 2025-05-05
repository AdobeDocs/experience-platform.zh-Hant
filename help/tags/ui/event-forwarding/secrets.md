---
title: 在事件轉送中設定秘密
description: 瞭解如何在UI中設定秘密，以驗證用於事件轉送屬性中的端點。
exl-id: eefd87d7-457f-422a-b159-5b428da54189
source-git-commit: 592acdd45b1db5da95430b4e707cd9a2c18c1645
workflow-type: tm+mt
source-wordcount: '2426'
ht-degree: 3%

---

# 在事件轉送中設定秘密

在事件轉送中，密碼是代表其他系統之驗證認證的資源，可允許安全交換資料。 密碼只能在事件轉送屬性中建立。

目前支援的密碼型別如下：

| 密碼型別 | 說明 |
| --- | --- |
| [!UICONTROL Google OAuth 2] | 包含數個屬性以支援[OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749)驗證規格，以便用於[Google Ads API](https://developers.google.com/google-ads/api/docs/oauth/overview)和[Pub/Sub API](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)。 系統會要求您提供必要資訊，然後在指定的間隔內處理這些權杖的續約。 |
| [!UICONTROL HTTP] | 包含使用者名稱和密碼的兩個字串屬性。 |
| [!UICONTROL [!DNL LinkedIn] OAuth 2] | 系統會要求您提供必要資訊，然後在指定的間隔內處理這些權杖的續約。 |
| [!UICONTROL OAuth 2] | 包含數個屬性，可支援[OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749)驗證規格的[使用者端認證授權型別](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.4)。 系統會要求您提供必要資訊，然後在指定的間隔內處理這些權杖的續約。 |
| [!UICONTROL OAuth 2 JWT] | 包含數個屬性，可支援[OAuth 2.0授權](https://datatracker.ietf.org/doc/html/rfc7523#section-2.1)授權的JSON Web權杖(JWT)設定檔。 系統會要求您提供必要資訊，然後在指定的間隔內處理這些權杖的續約。 |
| [!UICONTROL Token] | 代表兩個系統已知且瞭解的驗證Token值的單一字元字串。 |

{style="table-layout:auto"}

本指南提供如何在Experience Platform UI或資料收集UI中設定事件轉送([!UICONTROL Edge])屬性的密碼的高層級概觀。

>[!NOTE]
>
>如需有關如何在Reactor API中管理機密的詳細指引，包括機密結構的JSON範例，請參閱[機密API指南](../../api/guides/secrets.md)。

## 先決條件

本指南假設您已熟悉如何管理UI中標籤和事件轉送的資源，包括如何建立資料元素和事件轉送規則。 如需簡介，請參閱[管理資源](../managing-resources/overview.md)指南。

您也應該實際瞭解標籤和事件轉送的發佈流程，包括如何將資源新增至程式庫，以及將組建安裝至您的網站以進行測試。 如需詳細資訊，請參閱[發佈總覽](../publishing/overview.md)。

## 建立密碼 {#create}

>[!CONTEXTUALHELP]
>id="platform_eventforwarding_secrets_environments"
>title="密碼環境"
>abstract="為了讓密碼可供事件轉送使用，必須將其指派給現有環境。如果您沒有為事件轉送屬性建立任何環境，則必須進行設定才能繼續。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html?lang=zh-Hant" text="環境概觀"

若要建立密碼，請在左側導覽中選取&#x200B;**[!UICONTROL 事件轉送]**，然後開啟您想要新增密碼的事件轉送屬性。 接著，在左側導覽中選取&#x200B;**[!UICONTROL 密碼]**，接著選取&#x200B;**[!UICONTROL 建立新密碼]**。

![建立新密碼](../../images/ui/event-forwarding/secrets/create-new-secret.png)

下一個畫面可讓您設定密碼的詳細資訊。 為了讓密碼可供事件轉送使用，必須將其指派給現有環境。如果您尚未針對事件轉送屬性建立任何環境，請參閱[環境](../publishing/environments.md)上的指南，以瞭解如何設定環境，然後再繼續。

>[!NOTE]
>
>如果您仍要在將密碼新增至環境之前建立並儲存密碼，請先停用&#x200B;**[!UICONTROL 將密碼附加至環境]**&#x200B;切換功能，然後再填寫其餘的資訊。 請注意，如果您想要使用密碼，您之後必須將其指派給環境。
>
>![停用環境](../../images/ui/event-forwarding/secrets/env-disabled.png)

在&#x200B;**[!UICONTROL 目標環境]**&#x200B;下，使用下拉式功能表選取要指派密碼的環境。 在&#x200B;**[!UICONTROL 密碼名稱]**&#x200B;底下，提供環境內容中的密碼名稱。 此名稱在事件轉送屬性下的所有密碼中必須是唯一的。

![環境和名稱](../../images/ui/event-forwarding/secrets/env-and-name.png)

一個密碼一次只能指派給一個環境，但您可以視需要為跨不同環境的多個密碼指派相同的認證。 選取&#x200B;**[!UICONTROL 新增環境]**&#x200B;以新增其他資料列至清單。

![新增環境](../../images/ui/event-forwarding/secrets/add-env.png)

對於您新增的每個環境，您必須為關聯的密碼提供另一個唯一名稱。 如果您耗盡所有可用的環境，**[!UICONTROL 新增環境]**&#x200B;按鈕將不可用。

![無法新增環境](../../images/ui/event-forwarding/secrets/add-env-greyed.png)

在此，建立密碼的步驟因您建立的密碼型別而異。 如需詳細資訊，請參閱以下各小節：

* [[!UICONTROL Token]](#token)
* [[!UICONTROL HTTP]](#http)
* [[!UICONTROL OAuth 2]](#oauth2)
* [[!UICONTROL OAuth 2 JWT]](#oauth2jwt)
* [[!UICONTROL Google OAuth 2]](#google-oauth2)
* [[!UICONTROL [!DNL LinkedIn] OAuth 2]](#linkedin-oauth2)

### [!UICONTROL Token] {#token}

若要建立權杖密碼，請從&#x200B;**[!UICONTROL 型別]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 權杖]**。 在出現的&#x200B;**[!UICONTROL Token]**&#x200B;欄位中，提供您正在驗證的系統可辨識的認證字串。 選取&#x200B;**[!UICONTROL 建立密碼]**&#x200B;以儲存密碼。

![權杖密碼](../../images/ui/event-forwarding/secrets/token-secret.png)

### [!UICONTROL HTTP] {#http}

若要建立HTTP密碼，請從&#x200B;**[!UICONTROL 型別]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 簡單HTTP]**。 在下面顯示的欄位中，請先提供認證的使用者名稱和密碼，再選取&#x200B;**[!UICONTROL 建立密碼]**&#x200B;以儲存密碼。

>[!NOTE]
>
>儲存後，認證會使用[「基本」HTTP驗證配置](https://www.rfc-editor.org/rfc/rfc7617.html)編碼。

![HTTP密碼](../../images/ui/event-forwarding/secrets/http-secret.png)

### [!UICONTROL OAuth 2] {#oauth2}

若要建立OAuth 2密碼，請從&#x200B;**[!UICONTROL 型別]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL OAuth 2]**。 在下面顯示的欄位中，提供您的[[!UICONTROL 使用者端識別碼]和[!UICONTROL 使用者端密碼]](https://www.oauth.com/oauth2-servers/client-registration/client-id-secret/)，以及您的OAuth整合的[[!UICONTROL 權杖URL]](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/)。 UI中的[!UICONTROL 權杖URL]欄位是授權伺服器主機和權杖路徑之間的串連。

![OAuth 2密碼](../../images/ui/event-forwarding/secrets/oauth-secret-1.png)

在&#x200B;**[!UICONTROL 認證選項]**&#x200B;下，您可以提供其他認證選項，例如`scope`和`audience`，其形式為金鑰值組。 若要新增更多索引鍵/值組，請選取&#x200B;**[!UICONTROL 新增其他]**。

![認證選項](../../images/ui/event-forwarding/secrets/oauth-secret-2.png)

最後，您可以設定密碼的&#x200B;**[!UICONTROL 重新整理位移]**&#x200B;值。 這表示系統執行自動重新整理的權杖到期前的秒數。 以小時和分鐘為單位的等效時間會顯示在欄位右側，並會在您輸入時自動更新。

![重新整理位移](../../images/ui/event-forwarding/secrets/oauth-secret-3.png)

例如，如果重新整理位移設定為預設值`14400` （4小時），而存取權杖的`expires_in`值為`86400` （24小時），則系統將在20小時後自動重新整理密碼。

>[!IMPORTANT]
>
>OAuth密碼在重新整理之間至少需要四個小時，並且至少八小時後必須有效。 此限制讓您至少有四個小時可以在產生的Token發生問題時進行干預。
>
>例如，如果位移設為`28800` （8小時），而存取權杖為`expires_in` / `36000` （10小時），則交換會失敗，因為產生的差異少於4小時。

完成後，選取&#x200B;**[!UICONTROL 建立密碼]**&#x200B;以儲存密碼。

![儲存OAuth 2位移](../../images/ui/event-forwarding/secrets/oauth-secret-4.png)

### [!UICONTROL OAuth 2 JWT] {#oauth2jwt}

若要建立OAuth 2 JWT密碼，請從&#x200B;**[!UICONTROL 型別]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL OAuth 2 JWT]**。

![在[!UICONTROL 型別]下拉式清單中反白顯示OAuth 2 JWT密碼的[!UICONTROL 建立密碼]索引標籤。](../../images/ui/event-forwarding/secrets/oauth-jwt-secret.png)

>[!NOTE]
>
>目前唯一支援簽署JWT的[!UICONTROL 演演算法]是RS256。

在下面顯示的欄位中，提供您的[!UICONTROL 簽發者]、[!UICONTROL 主旨]、[!UICONTROL 對象]、[!UICONTROL 自訂宣告]、[!UICONTROL TTL]，然後從下拉式清單中選取[!UICONTROL 演演算法]。 接下來，輸入您的OAuth整合的[!UICONTROL 私密金鑰ID]以及[[!UICONTROL 權杖URL]](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/)。 [!UICONTROL 權杖URL]欄位不是必要欄位。 如果提供值，JWT會與存取權杖交換。 將根據回應中的`expires_in`屬性和[!UICONTROL Refresh Offset]值重新整理密碼。 如果未提供值，則推送至邊緣的秘密為JWT。 將根據[!UICONTROL TTL]和[!UICONTROL 重新整理位移]值來重新整理JWT。

![反白顯示選取的輸入欄位的[!UICONTROL 建立密碼]索引標籤。](../../images/ui/event-forwarding/secrets/oauth-jwt-information.png)

在&#x200B;**[!UICONTROL 認證選項]**&#x200B;底下，您可以提供其他認證選項，例如`jwt_param`的金鑰值組形式。 若要新增更多索引鍵/值組，請選取&#x200B;**[!UICONTROL 新增其他]**。

![反白顯示[!UICONTROL 認證選項]欄位的[!UICONTROL 建立密碼]索引標籤。](../../images/ui/event-forwarding/secrets/oauth-jwt-credential-options.png)

最後，您可以設定密碼的&#x200B;**[!UICONTROL 重新整理位移]**&#x200B;值。 這表示系統執行自動重新整理的權杖到期前的秒數。 以小時和分鐘為單位的等效時間會顯示在欄位右側，並會在您輸入時自動更新。

![醒目提示[!UICONTROL 重新整理位移]欄位的[!UICONTROL 建立密碼]索引標籤。](../../images/ui/event-forwarding/secrets/oauth-jwt-refresh-offset.png)

例如，如果重新整理位移設定為預設值`1800` （30分鐘），而存取權杖具有`expires_in`值`3600` （一小時），則系統將會在一小時內自動重新整理密碼。

>[!IMPORTANT]
>
>OAuth 2 JWT密碼在重新整理之間需要至少30分鐘，並且至少必須在一小時內有效。 此限製為您提供至少30分鐘的時間，以在產生的權杖發生問題時進行干預。
>
>例如，如果位移設為`1800` （30分鐘），而存取權杖有`expires_in` / `2700` （45分鐘），則交換會失敗，因為產生的差異少於30分鐘。

完成後，選取&#x200B;**[!UICONTROL 建立密碼]**&#x200B;以儲存密碼。

![ [!UICONTROL 建立密碼]索引標籤醒目提示[!UICONTROL 建立密碼]](../../images/ui/event-forwarding/secrets/oauth-jwt-create-secret.png)

### [!UICONTROL Google OAuth 2] {#google-oauth2}

若要建立Google OAuth 2密碼，請從&#x200B;**[!UICONTROL 型別]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Google OAuth 2]**。 在&#x200B;**[!UICONTROL 範圍]**&#x200B;下，選取您要使用此密碼授與存取權的Google API。 目前支援下列產品：

* [Google Ads API](https://developers.google.com/google-ads/api/docs/oauth/overview)
* [Pub/Sub API](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)

完成後，選取&#x200B;**[!UICONTROL 建立密碼]**。

![Google OAuth 2密碼](../../images/ui/event-forwarding/secrets/google-oauth.png)

此時會出現彈出視窗，通知您需要透過Google手動授權密碼。 選取&#x200B;**[!UICONTROL 建立並授權]**&#x200B;以繼續。

![Google授權彈出視窗](../../images/ui/event-forwarding/secrets/google-authorization.png)

系統會顯示一個對話方塊，讓您輸入Google帳戶的認證。 依照提示操作，將事件轉送存取權授與選取範圍下的資料。 授權程式完成後，密碼就會建立。

>[!IMPORTANT]
>
>如果您的組織有為Google Cloud應用程式設定的重新驗證原則，則建立的密碼在驗證過期後不會成功重新整理（1到24小時之間，取決於原則設定）。
>
>若要解決此問題，請登入Google Admin Console並導覽至「**[!DNL App access control]**」頁面，以便將事件轉送應用程式(Adobe Real-Time CDP事件轉送)標示為[!DNL Trusted]。 如需詳細資訊，請參閱有關[設定Google雲端服務](https://support.google.com/a/answer/9368756)工作階段長度的相關Google檔案。

### [!UICONTROL [!DNL LinkedIn] OAuth 2] {#linkedin-oauth2}

若要建立[!DNL LinkedIn] OAuth 2密碼，請從&#x200B;**[!UICONTROL 型別]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL [!DNL LinkedIn]OAuth 2]**。 接著，選取&#x200B;**[!UICONTROL 建立密碼]**。

![反白顯示[!UICONTROL 型別]欄位的[!UICONTROL 建立密碼]索引標籤。](../../images/ui/event-forwarding/secrets/linkedin-oauth.png)

此時會出現彈出視窗，通知您需要透過[!DNL LinkedIn]手動授權密碼。 選取&#x200B;**[!UICONTROL 使用[!DNL LinkedIn]]**&#x200B;建立並授權密碼以繼續。

![[!DNL LinkedIn]授權彈出視窗醒目提示[!UICONTROL 使用[!DNL LinkedIn]]建立和授權密碼。](../../images/ui/event-forwarding/secrets/linkedin-authorization.png)

會出現一個對話方塊，提示您輸入您的[!DNL LinkedIn]認證。 依照提示操作，授予資料的事件轉送存取權。

授權程式完成後，您將返回&#x200B;**[!UICONTROL 密碼]**&#x200B;標籤，您可以在其中檢視新建立的密碼。 您可以在此處檢視密碼的狀態和到期日。

![醒目提示新建立密碼的[!UICONTROL 密碼]標籤。](../../images/ui/event-forwarding/secrets/linkedin-new-secret.png)

#### 重新授權[!UICONTROL [!DNL LinkedIn] OAuth 2]密碼

>重要
>
>您必須每365天重新授權使用您的[!DNL LinkedIn]認證。 如果您未適時重新授權，您的密碼將不會重新整理，且[!DNL LinkedIn]轉換要求將會失敗。

在需要重新授權的機密之前三個月，當您導覽屬性的任何頁面時，將會開始顯示快顯視窗。 選取&#x200B;**[!UICONTROL 按一下這裡以移至您的秘密]**。

![ [!UICONTROL 屬性概述]索引標籤醒目提示密碼重新授權快顯視窗。](../../images/ui/event-forwarding/secrets/linkedin-reauthorization-popup.png)

您被重新導向至[!UICONTROL 密碼]標籤。 此頁面上列出的秘密會經過篩選，僅顯示需要重新授權的秘密。 針對您需要重新授權的密碼選取&#x200B;**[!UICONTROL 需要驗證]**。

![ [!DNL LinkedIn]密碼的[!UICONTROL 密碼]索引標籤醒目提示[!UICONTROL 需要驗證]。](../../images/ui/event-forwarding/secrets/linkedin-reauthorization.png)

會出現一個對話方塊，提示您輸入[!DNL LinkedIn]認證。 依照提示重新授權您的密碼。

## 編輯密碼

建立屬性的密碼後，您就可以在&#x200B;**[!UICONTROL 密碼]**&#x200B;工作區中找到這些密碼。 若要編輯現有密碼的詳細資訊，請從清單中選取其名稱。

![選取要編輯的密碼](../../images/ui/event-forwarding/secrets/edit-secret.png)

下一個畫面可讓您變更密碼的名稱和認證。

![編輯密碼](../../images/ui/event-forwarding/secrets/edit-secret-config.png)

>[!NOTE]
>
>如果密碼與現有環境相關聯，則無法將密碼重新指派給其他環境。 如果您要在不同的環境中使用相同的認證，您必須[改為建立新密碼](#create)。 從此畫面重新指派環境的唯一方法是，如果您事先未將密碼指派給環境，或如果您刪除了密碼附加到的環境。

### 重試秘密交換

您可以從編輯畫面重試或重新整理秘密交換。 此過程因所編輯的密碼型別而異：

| 密碼型別 | 重試通訊協定 |
| --- | --- |
| [!UICONTROL Token] | 選取&#x200B;**[!UICONTROL Exchange密碼]**&#x200B;以重試密碼交換。 此控制項僅在有附加至密碼的環境時可用。 |
| [!UICONTROL HTTP] | 如果沒有環境附加至密碼，請選取&#x200B;**[!UICONTROL Exchange Secret]**&#x200B;將認證交換至base64。 如果已附加環境，請選取[選擇&#x200B;**[!UICONTROL Exchange並部署密碼]**]以交換至base64並部署密碼。 |
| [!UICONTROL OAuth 2] | 選取&#x200B;**[!UICONTROL 產生Token]**&#x200B;以交換認證，並從驗證提供者傳回存取權杖。 |

## 刪除密碼

若要刪除&#x200B;**[!UICONTROL 密碼]**&#x200B;工作區中現有的密碼，請先選取密碼名稱旁的核取方塊，再選取&#x200B;**[!UICONTROL 刪除]**。

![刪除密碼](../../images/ui/event-forwarding/secrets/delete.png)

## 在事件轉送中使用秘密

為了在事件轉送中使用密碼，您必須先建立參考密碼本身的[資料元素](../managing-resources/data-elements.md)。 儲存資料元素後，您可以將它包含在事件轉送[規則](../managing-resources/rules.md)中，並將這些規則新增至[資料庫](../publishing/libraries.md)，這些資料庫可部署到Adobe的伺服器做為[組建](../publishing/builds.md)。

建立資料元素時，請選取&#x200B;**[!UICONTROL 核心]**&#x200B;擴充功能，然後為資料元素型別選取&#x200B;**[!UICONTROL 密碼]**。 右側面板會更新並提供下拉式控制項，以將最多三個密碼指派給資料元素：一個分別適用於[!UICONTROL 開發]、[!UICONTROL 測試]和[!UICONTROL 生產]。

![資料元素](../../images/ui/event-forwarding/secrets/data-element.png)

>[!NOTE]
>
>只有附加到開發、測試和生產環境的秘密才會顯示在其各自的下拉清單中。

藉由將多個秘密指派給單一資料元素並將其納入規則，您可以根據[發佈流程](../publishing/publishing-flow.md)中的容納程式庫位置來變更資料元素的值。

![具有多個密碼的資料元素](../../images/ui/event-forwarding/secrets/multi-secret-data-element.png)

>[!NOTE]
>
>建立資料元素時，必須指派開發環境。 預備和生產環境的秘密並非必要，但如果組建的秘密型別資料元素未針對相關環境選取秘密，則嘗試轉移至這些環境的組建將會失敗。

## 後續步驟

本指南說明如何在UI中管理秘密。 有關如何使用Reactor API與密碼互動的資訊，請參閱[密碼端點指南](../../api/endpoints/secrets.md)。
