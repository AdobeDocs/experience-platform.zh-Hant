---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目的地
title: 電子郵件行銷目的地概觀
type: Tutorial
description: 電子郵件服務提供者(ESP)可讓您管理電子郵件行銷活動，例如傳送促銷電子郵件行銷活動。
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: d3e1bc9bc075117dcc96c85b8b9c81d6ee617d29
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 1%

---

# 電子郵件行銷目的地概觀{#email-marketing-destinations}

電子郵件服務提供者(ESP)可讓您管理電子郵件行銷活動，例如傳送促銷電子郵件行銷活動。 Adobe Experience Platform可讓您啟用區段至電子郵件行銷目的地，與ESP整合。

若要傳送區段至您促銷活動的電子郵件行銷目的地，Platform必須先連線至目的地。

連線至電子郵件行銷目的地是三步驟程式（[設定目標](#connect-destination)、[啟用區段](#select-segments)、[從儲存位置匯入資料至目標](#import-data-into-destination)）。 本頁面下文將詳細說明每個步驟。

在連接目標流中（如下節所述），連接到[!DNL Amazon S3]或[!DNL SFTP]。 Platform會將您的區段匯出為`.csv`檔案，並將其傳送至您偏好的位置。 從[!DNL Platform]中啟用的儲存位置，排程電子郵件行銷平台中的資料匯入。 匯入資料的程式因各合作夥伴而異。 如需詳細資訊，請參閱個別目的地文章。

## 配置目標{#connect-destination}

在&#x200B;**[!UICONTROL 連線]** > **[!UICONTROL 目的地]**&#x200B;中，選取您要連線的電子郵件行銷目的地，然後選取&#x200B;**[!UICONTROL 設定]**。

![連接到目標](../../assets/catalog/email-marketing/overview/connect-email-marketing.png)

在&#x200B;**[!UICONTROL 帳戶]**&#x200B;步驟中，如果您先前已設定與電子郵件行銷目的地的連線，請選取&#x200B;**[!UICONTROL 現有帳戶]**&#x200B;並選取您現有的連線。 或者，您可以選取&#x200B;**[!UICONTROL 新帳戶]**&#x200B;來設定與電子郵件行銷目的地的新連線。 在&#x200B;**[!UICONTROL 連線類型]**&#x200B;選擇器中，可以在[!UICONTROL Amazon S3]、[!UICONTROL Azure Blob]、[!UICONTROL 具有密碼的SFTP]或[!UICONTROL 具有SSH密鑰的SFTP]之間進行選擇。 根據您的連接類型，填寫以下資訊，然後選擇&#x200B;**[!UICONTROL Connect]**。

- 對於&#x200B;**S3連線**，您必須提供您的Amazon存取金鑰ID和機密存取金鑰。
- 對於&#x200B;**使用密碼**&#x200B;連接的SFTP，必須為SFTP伺服器提供域、埠、用戶名和密碼。
- 對於&#x200B;**具有SSH金鑰**&#x200B;連線的SFTP，您必須為SFTP伺服器提供網域、連接埠、使用者名稱和SSH金鑰。

或者，您可以附加RSA格式的公鑰，以在&#x200B;**[!UICONTROL Key]**&#x200B;部分下嚮導出的檔案添加加密。 您的公開金鑰必須寫入為[!DNL Base64]編碼字串。

在&#x200B;**[!UICONTROL Authentication]**&#x200B;步驟中，輸入新目標的名稱和說明，以及導出檔案的檔案格式。

如果您在上一個步驟中選取Amazon S3作為儲存選項，請在要傳送檔案的雲端儲存目的地中插入貯體名稱和資料夾路徑。 對於SFTP儲存選項，插入要傳送檔案的資料夾路徑。

在此步驟中，您也可以選取應套用至此目的地的任何行銷動作。 行銷動作會指出要將資料匯出至目的地的目的。 您可以從Adobe定義的行銷動作中選取，或者您可以建立自己的行銷動作。 如需行銷動作的詳細資訊，請參閱[資料使用原則概述](../../../data-governance/policies/overview.md)。

![電子郵件設定步驟](../../assets/catalog/email-marketing/overview/email-setup-step.png)

## 選擇要在目標導出項中包含的段成員{#select-segments}

在&#x200B;**[!UICONTROL 選取區段]**&#x200B;頁面上，選取要傳送至目的地的區段。 尋找下節中欄位的詳細資訊。

![選取區段](../../assets/common/email-select-segments.png)

## 配置檔案名

如需區段排程和檔案名稱編輯選項的相關資訊，請參閱啟用目標教學課程中的[設定](../../ui/activate-destinations.md#configure)步驟。

## 選擇屬性 — 選擇要在導出的檔案{#destination-attributes}中用作目標屬性的架構欄位

在此步驟中，您要選取要匯出至電子郵件行銷目的地的欄位，並標示哪些欄位是必填欄位。
如需此步驟的相關資訊，請參閱啟動目的地教學課程中的[選取屬性](../../ui/activate-destinations.md#select-attributes)步驟。

## 身分 {#identity}

Adobe建議您從[union結構](../../../profile/home.md#profile-fragments-and-union-schemas)中選取唯一識別碼。 這是您的使用者身分識別所擷取的欄位。 最常見的欄位是電子郵件地址，但也可以是忠誠計畫ID或電話號碼。 如需架構中最常見的唯一識別碼及其XDM欄位，請參閱下表。

| 唯一識別碼 | 統一架構中的XDM欄位 |
|----------------- | ---------------------------|
| Email Address | `personalEmail.address` |
| 電話 | `mobilePhone.number` |
| 忠誠計畫ID | `Customer-defined XDM field` |

## 其他目標屬性

在「結構」欄位選取器中，選擇要匯出至電子郵件目的地的其他欄位。 建議的選項有：

| 結構 | XDM欄位 |
|------ | ---------|
| 「名字」 | `person.name.firstName` |
| 「姓氏」 | `person.name.lastName` |
| 電話 | `mobilePhone.number` |
| 地址城市 | `homeAddress.city` |
| 地址狀態 | `homeAddress.stateProvince` |
| 地址郵遞區號 | `homeAddress.postalCode` |
| 生日 | `person.birthDayAndMonth` |
| 區段成員資格 | `segmentMembership.status` |

## 將資料從儲存位置導入目標{#import-data-into-destination}

請參閱個別電子郵件行銷目的地文章，了解如何將資料從您的儲存位置匯入目的地：

- [Adobe Campaign](./adobe-campaign.md#import-data-into-campaign)
- [Oracle雄辯](./oracle-eloqua.md#import-data-into-eloqua)
- [OracleResponsys](./oracle-responsys.md#import-data-into-responsys)
- [SalesforceMarketing Cloud](./salesforce-marketing-cloud.md#import-data-into-salesforce)

## 啟用區段至電子郵件行銷目的地

如需如何啟用區段至電子郵件行銷目的地的指示，請參閱[啟用設定檔和區段至目的地](../../ui/activate-destinations.md)。

## 其他資源

- [對目的地啟用資料](../../ui/activate-destinations.md)
- [使用流量服務API建立電子郵件行銷目的地和啟用資料](../../api/email-marketing.md)
