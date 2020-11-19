---
keywords: email;Email;e-mail;email destinations
title: 電子郵件行銷目標
seo-title: 電子郵件行銷目標
type: Tutorial
description: 電子郵件服務供應商(ESP)可讓您管理電子郵件行銷活動，例如傳送促銷電子郵件促銷活動。
seo-description: 電子郵件服務供應商(ESP)可讓您管理電子郵件行銷活動，例如傳送促銷電子郵件促銷活動。
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 1%

---


# 電子郵件行銷目標 {#email-marketing-destinations}

電子郵件服務供應商(ESP)可讓您管理電子郵件行銷活動，例如傳送促銷電子郵件宣傳。 即時客戶資料平台可讓您將區段啟用至電子郵件行銷目的地，與ESP整合。

若要將區段傳送至行銷活動的電子郵件目的地，Adobe即時CDP必須先連線至目的地。

連線至電子郵件行銷目的地是三步驟。 本頁將進一步說明每個步驟。

在連接目標流中（如下節所述），連接到Amazon S3或SFTP。 即時CDP將您的細分導出為 `.csv` 或文 `.txt` 件，並將其發送到您的首選位置。 從即時CDP中啟用的儲存位置，排程您在電子郵件行銷平台中的資料匯入。 匯入資料的程式會因每個合作夥伴而異。 如需詳細資訊，請參閱個別的目標文章。

## 配置目標 {#connect-destination}

在「 **[!UICONTROL 連線]** >目 **[!UICONTROL 的地]**」中，選取您要連線的電子郵件行銷目的地，然後選取「設 **[!UICONTROL 定」]**。

![連接到目標](./assets/connect-email-marketing.png)

在「驗 **[!UICONTROL 證]** 」步驟中，如果您先前已設定電子郵件行銷目的地的連線，請選取「現有帳戶 **** 」並選取您現有的連線。 或者，您可以選 **[!UICONTROL 取「新帳戶]** 」來設定與電子郵件行銷目的地的新連線。 在「連 **[!UICONTROL 接類型]** 」選擇器中，您可以選擇Amazon S3、SFTP含密碼或SSH金鑰的SFTP。 根據您的連線類型，填入下列資訊，然後選取「連 **[!UICONTROL 線」]**。

- 對於 **S3連接**，您必須提供您的Amazon存取金鑰ID和密碼存取金鑰。
- 對於 **具有密碼連接的SFTP** ，您必須為SFTP伺服器提供域、埠、用戶名和密碼。
- 對於 **具有SSH密鑰連接的SFTP** ，必須為SFTP伺服器提供域、埠、用戶名和SSH密鑰。

或者，您可以附加RSA格式的公開密鑰，以便在「密鑰」部分下為導出的檔案添加 **[!UICONTROL 加密]** 。 請注意，此公開金 **鑰必** 須寫入為Base64編碼字串。

在「設 **[!UICONTROL 置]** 」步驟中，輸入新目標的名稱和說明，以及導出檔案的檔案格式。

如果您在上一步驟中選擇了Amazon S3作為儲存選項，請將儲存段名稱和資料夾路徑插入雲儲存目標中將檔案發送到的位置。 對於SFTP儲存選項，插入要傳送檔案的資料夾路徑。

此外，您也可以在此步驟中選取任何應套用至此目的地的行銷使用案例。 行銷使用案例會指出將資料匯出至目的地的方式。 您可以從Adobe定義的行銷使用案例中選擇，也可以建立自己的行銷使用案例。 有關行銷使用案例的詳細資訊，請參 [閱即時CDP中的資料治理頁](/help/rtcdp/privacy/data-governance-overview.md#destinations) 。 如需個別Adobe定義之行銷使用案例的詳細資訊，請參閱「資 [料使用政策」概觀](/help/data-governance/policies/overview.md#core-actions)。

![電子郵件設定步驟](./assets/email-setup-step.png)

## 選擇要包含在目標導出中的段成員 {#select-segments}

在「選 **[!UICONTROL 擇區段]** 」頁面上，選取要傳送至目的地的區段。 尋找以下各節中欄位的詳細資訊。

![選取區段](/help/rtcdp/destinations/assets/email-select-segments.png)

## 配置檔案名

如需區段排程和檔案名稱編輯選項的詳細資訊，請參閱啟 [動目標教學課程的](/help/rtcdp/destinations/activate-destinations.md#configure) 「設定」步驟。

## 選擇屬性——選擇要在導出的檔案中用作目標屬性的架構欄位 {#destination-attributes}

在此步驟中，您會選取要匯出至電子郵件行銷目的地的欄位，以及標示哪些欄位是必填欄位。

![目標屬性](/help/rtcdp/destinations/assets/recommended-attributes.png)

有關此步驟的詳細資訊，請參閱激活目 [標教程中的](/help/rtcdp/destinations/activate-destinations.md#select-attributes) 「選擇屬性」步驟。

### 身份 {#identity}

建議您從聯合架構中選擇唯一 [識別碼](../../profile/home.md#profile-fragments-and-union-schemas)。 這是您使用者身分識別的欄位。 最常見的欄位是電子郵件地址，但也可以是忠誠度方案ID或電話號碼。 請參見下表，瞭解模式中最常見的唯一標識符及其XDM欄位。

| 唯一識別碼 | 統一模式中的XDM欄位 |
---------|----------
| Email Address | `personalEmail.address` |
| 電話 | `mobilePhone.number` |
| 忠誠度方案ID | `Customer-defined XDM field` |

### 其他目標屬性

在「結構」欄位選擇器中，選擇要匯出至電子郵件目的地的其他欄位。 建議的選項包括：

| 結構 | XDM欄位 |
---------|----------
| 「名字」 | `person.name.firstName` |
| 「姓氏」 | `person.name.lastName` |
| 電話 | `mobilePhone.number` |
| 地址城市 | `homeAddress.city` |
| 地址狀態 | `homeAddress.stateProvince` |
| 地址郵遞區號 | `homeAddress.postalCode` |
| 生日 | `person.birthDayAndMonth` |
| 區段會籍 | `segmentMembership.status` |

## 將資料從儲存位置匯入目標

請參閱個別電子郵件行銷目標文章，瞭解如何將資料從儲存位置匯入目標：

- [Adobe Campaign](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
- [Salesforce Marketing Cloud](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
- [Oracle Exovila](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
- [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## 啟用區段至電子郵件行銷目標

如需如何啟用區段至電子郵件行銷目的地的指示，請參閱啟 [用資料至目的地](/help/rtcdp/destinations/activate-destinations.md)。

## 其他資源

- [將資料啟動至目標](/help/rtcdp/destinations/activate-destinations.md)
- [使用Flow Service API建立電子郵件行銷目標並啟用資料](https://docs.adobe.com/content/help/en/experience-platform/tutorials/destinations/email-marketing-api.html)