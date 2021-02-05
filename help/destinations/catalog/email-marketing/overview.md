---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目標
title: 電子郵件行銷目標概觀
type: Tutorial
description: 電子郵件服務供應商(ESP)可讓您管理電子郵件行銷活動，例如傳送促銷電子郵件促銷活動。
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 1%

---


# 電子郵件行銷目標概觀{#email-marketing-destinations}

電子郵件服務供應商(ESP)可讓您管理電子郵件行銷活動，例如傳送促銷電子郵件宣傳。 Adobe Experience Platform可讓您將區段啟用至電子郵件行銷目的地，與ESP整合。

若要傳送區段至促銷活動的電子郵件行銷目的地，平台必須先連線至目的地。

連線至電子郵件行銷目的地是三步驟。 本頁將進一步說明每個步驟。

在連接目標流中（如下節所述），連接到Amazon S3或SFTP。 平台會將區段匯出為`.csv`或`.txt`檔案，並將它們傳送至您偏好的位置。 從平台中啟用的儲存位置，排程您在電子郵件行銷平台中的資料匯入。 匯入資料的程式會因每個合作夥伴而異。 如需詳細資訊，請參閱個別的目標文章。

## 配置目標{#connect-destination}

在&#x200B;**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**&#x200B;中，選擇您要連接的電子郵件行銷目標，然後選擇&#x200B;**[!UICONTROL Configure]**。

![連接到目標](../../assets/catalog/email-marketing/overview/connect-email-marketing.png)

在&#x200B;**[!UICONTROL 驗證]**&#x200B;步驟中，如果您先前已設定電子郵件行銷目的地的連線，請選取&#x200B;**[!UICONTROL 現有帳戶]**&#x200B;並選取您現有的連線。 或者，您可以選擇&#x200B;**[!UICONTROL 新帳戶]**&#x200B;來設定與電子郵件行銷目的地的新連線。 在&#x200B;**[!UICONTROL 連接類型]**&#x200B;選擇器中，您可以在Amazon S3、SFTP與密碼或SSH密鑰之間選擇。 根據您的連接類型填寫以下資訊，然後選擇&#x200B;**[!UICONTROL Connect]**。

- 對於&#x200B;**S3連接**，您必須提供您的Amazon訪問密鑰ID和秘密訪問密鑰。
- 對於具有Password **連接的** SFTP，必須為SFTP伺服器提供域、埠、用戶名和密碼。
- 對於具有SSH密鑰&#x200B;**連接的** SFTP，必須為SFTP伺服器提供域、埠、用戶名和SSH密鑰。

或者，您可以附加RSA格式的公鑰，以便在&#x200B;**[!UICONTROL 密鑰]**&#x200B;部分下嚮導出的檔案添加加密。 請注意，此公共密鑰&#x200B;**必須**&#x200B;寫入為Base64編碼字串。

在&#x200B;**[!UICONTROL Setup]**&#x200B;步驟中，輸入新目標的名稱和說明，以及導出檔案的檔案格式。

如果您在上一步驟中選擇了Amazon S3作為儲存選項，請將儲存段名稱和資料夾路徑插入雲儲存目標中將檔案發送到的位置。 對於SFTP儲存選項，插入要傳送檔案的資料夾路徑。

此外，您也可以在此步驟中選取任何應套用至此目的地的行銷使用案例。 行銷使用案例會指出將資料匯出至目的地的方式。 您可以從Adobe定義的行銷使用案例中選擇，也可以建立自己的行銷使用案例。 如需行銷使用案例的詳細資訊，請參閱[資料使用政策概述](../../../data-governance/policies/overview.md)。

![電子郵件設定步驟](../../assets/catalog/email-marketing/overview/email-setup-step.png)

## 選擇目標導出中要包含的段成員{#select-segments}

在&#x200B;**[!UICONTROL 選擇區段]**&#x200B;頁面上，選擇要傳送至目的地的區段。 尋找以下各節中欄位的詳細資訊。

![選取區段](../../assets/common/email-select-segments.png)

## 配置檔案名

有關區段排程和檔案名稱編輯選項的資訊，請參閱啟動目標教學課程中的「設定[」步驟。](../../ui/activate-destinations.md#configure)

## 選擇屬性——選擇在導出的檔案{#destination-attributes}中用作目標屬性的架構欄位

在此步驟中，您會選取要匯出至電子郵件行銷目的地的欄位，以及標示哪些欄位是必填欄位。

![目標屬性](../../assets/catalog/email-marketing/overview/recommended-attributes.png)

有關此步驟的詳細資訊，請參閱激活目標教程中的[選擇屬性](../../ui/activate-destinations.md#select-attributes)步驟。

### 身份{#identity}

我們建議您從[union架構](../../../profile/home.md#profile-fragments-and-union-schemas)中選擇唯一標識符。 這是您使用者身分識別的欄位。 最常見的欄位是電子郵件地址，但也可以是忠誠度方案ID或電話號碼。 請參見下表，瞭解模式中最常見的唯一標識符及其XDM欄位。

| 唯一識別碼 | 統一模式中的XDM欄位 |
----------------- | ---------------------------
| Email Address | `personalEmail.address` |
| 電話 | `mobilePhone.number` |
| 忠誠度方案ID | `Customer-defined XDM field` |

### 其他目標屬性

在「結構」欄位選擇器中，選擇要匯出至電子郵件目的地的其他欄位。 建議的選項包括：

| 結構 | XDM欄位 |
------ | ---------
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

- [Adobe Campaign](./adobe-campaign.md#import-data-into-campaign)
- [Oracle Exovila](./oracle-eloqua.md#import-data-into-eloqua)
- [Oracle Responsys](./oracle-responsys.md#import-data-into-responsys)
- [Salesforce Marketing Cloud](./salesforce-marketing-cloud.md#import-data-into-salesforce)

## 啟用區段至電子郵件行銷目標

如需如何啟用區段至電子郵件行銷目的地的指示，請參閱[啟用資料至目的地](../../ui/activate-destinations.md)。

## 其他資源

- [將資料啟動至目標](../../ui/activate-destinations.md)
- [使用Flow Service API建立電子郵件行銷目標並啟用資料](../../api/email-marketing.md)