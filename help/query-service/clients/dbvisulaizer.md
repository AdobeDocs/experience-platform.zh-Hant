---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；Db視覺化程式；DbVisualizer；db視覺化程式；連線到查詢服務；
solution: Experience Platform
title: 將DbVisualizer連線到查詢服務
description: 本檔案將逐步說明連線DbVisualizer與Adobe Experience Platform查詢服務的步驟。
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 1%

---

# 將[!DNL DbVisualizer]連線至[!DNL Query Service] {#connect-dbvisualizer}

本檔案說明將[!DNL DbVisualizer]資料庫工具連線至Adobe Experience Platform [!DNL Query Service]的步驟。

## 快速入門

本指南要求您已存取[!DNL DbVisualizer]案頭應用程式，並熟悉如何導覽其介面。 若要下載[!DNL DbVisualizer]案頭應用程式或如需詳細資訊，請參閱[正式 [!DNL DbVisualizer] 檔案](https://www.dbvis.com/download/)。

若要取得連線[!DNL  DbVisualizer]至Experience Platform的必要認證，您必須擁有平台UI中查詢工作區的存取權。 如果您目前無法存取查詢工作區，請聯絡您的組織管理員。

## 建立資料庫連線 {#connect-database}

在本機電腦上安裝案頭應用程式後，請依照官方BDVisualizer指示，[建立新的資料庫連線](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection)。

當您從[!DNL Connections]清單中選取&#x200B;**[!DNL PostgreSQL]**&#x200B;後，新[!DNL PostgreSQL]連線的[!DNL Object View]索引標籤就會顯示。

### 設定連線的驅動程式內容 {#properties}

從[!DNL PostgreSQL]物件檢視標籤，選取&#x200B;**[!DNL Properties]**&#x200B;標籤，接著從導覽側邊欄選取&#x200B;**[!DNL Driver Properties]**。 有關[驅動程式屬性](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties)的詳細資訊，請參閱官方檔案。

接下來，輸入下表所述的驅動程式屬性。

>[!IMPORTANT]
>
>若要將DBVisualizer與Adobe Experience Platform連線，您必須啟用使用SSL。 請參閱[SSL模式檔案](./ssl-modes.md)，瞭解協力廠商連線至Adobe Experience Platform查詢服務的SSL支援，以及如何使用`verify-full` SSL模式連線。

| 屬性 | 說明 |
| ------ | ------ |
| `PGHOST` | [!DNL PostgreSQL]伺服器的主機名稱。 此值是您的Experience Platform **[!UICONTROL 主機]認證**。 |
| `ssl` | 定義SSL值`1`以啟用使用SSL。 |
| `sslmode` | 這會控制SSL保護的等級。 建議您在連線協力廠商使用者端至Adobe Experience Platform時使用`require` SSL模式。 `require`模式可確保所有通訊都需要加密，而且網路被信任可以連線到正確的伺服器。 不需要伺服器SSL憑證驗證。 |
| `user` | 連線至資料庫的使用者名稱是您的組織ID。 它是以`@Adobe.Org`結尾的英數字串。 此值是您的Experience Platform **[!UICONTROL 使用者名稱]認證**。 |

使用搜尋列來尋找每個屬性，然後選取引數值對應的儲存格。 儲存格會以藍色反白顯示。 在值欄位中輸入您的Platform認證，並選取&#x200B;**[!DNL Apply]**&#x200B;以新增驅動程式屬性。

>[!NOTE]
>
>若要新增第二個`user`設定檔，請從引數欄選取`user`，然後選取藍色+ （加號）圖示以新增每個使用者的認證。 選取&#x200B;**[!DNL Apply]**&#x200B;以新增驅動程式屬性。

[!DNL Edited]欄會顯示核取記號，表示引數值已更新。

### 輸入查詢服務認證 {#query-service-credentials}

若要尋找連線BBVisualizer與查詢服務所需的認證，請登入Platform UI並從左側導覽中選取&#x200B;**[!UICONTROL 查詢]**，接著選取&#x200B;**[!UICONTROL 認證]**。 如需尋找您的&#x200B;**主機**、**連線埠**、**資料庫**、**使用者名稱**&#x200B;以及&#x200B;**密碼**&#x200B;認證的相關資訊，請閱讀[認證指南](../ui/credentials.md)。

![包含認證和即將到期認證的Experience Platform查詢工作區的[認證]頁面反白顯示。](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service]還提供不會到期的認證，以允許與協力廠商使用者端進行一次性設定。 請參閱檔案以取得[有關如何產生及使用不會到期的認證](../ui/credentials.md#non-expiring-credentials)的完整指示。 如果您想要以一次性設定方式連線BDVisualizer，則必須完成此程式。 取得的`credential`和`technicalAccountId`值包含DBVisualizer `password`引數的值。

## 驗證 {#authentication}

若要在每次建立連線時都要求使用者識別碼與密碼式驗證，請瀏覽至[!DNL Properties]標籤，然後從[!DNL PostgreSQL]下的瀏覽側邊欄選取&#x200B;**[!DNL Authentication]**。

在[連線驗證]面板中，勾選&#x200B;**[!DNL Require Userid]**&#x200B;和&#x200B;**[!DNL Require Password]**&#x200B;核取方塊，然後選取&#x200B;**[!DNL Apply]**。 有關[設定驗證選項](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options)的詳細資訊，請參閱官方檔案。

## 連線至平台

您可以使用即將到期或未到期的認證建立連線。 若要建立連線，請從「[!DNL PostgreSQL]」物件檢視標籤中選取「**[!DNL Connection]**」標籤，然後針對下列設定輸入您的Experience Platform認證。 官方DBVisualizer網站上提供[設定手動連線](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually)的補充指示。

>[!NOTE]
>
>除非在引數說明中註明，否則下表中BDVisualizer所需的全部認證對於過期和未過期的認證都是相同的。

| 連線引數 | 說明 |
|---|---|
| **[!UICONTROL 名稱]** | 為您的連線建立名稱。 建議您提供好記的名稱，以便辨識連線。 |
| **[!UICONTROL 資料庫伺服器]** | 這是您的Experience Platform **[!UICONTROL 主機]**&#x200B;認證。 |
| **[!UICONTROL 資料庫連線埠]** | [!DNL Query Service]的連線埠。 您必須使用連線埠&#x200B;**80**&#x200B;或&#x200B;**5432**&#x200B;來與[!DNL Query Service]連線。 |
| **[!UICONTROL 資料庫]** | 使用您的Experience Platform **[!UICONTROL 資料庫]**&#x200B;認證值： `prod:all`。 |
| **[!UICONTROL 資料庫使用者ID]** | 這是您的平台組織ID。 使用您的Experience Platform **[!UICONTROL 使用者名稱]**&#x200B;認證值。 ID將採用`ORG_ID@AdobeOrg`格式。 |
| **[!UICONTROL 資料庫密碼]** | 此英數字串是您的Experience Platform **[!UICONTROL 密碼]**&#x200B;認證。 如果您想要使用不會到期的認證，此值是從`technicalAccountID`和在組態JSON檔案中下載的`credential`串連的引數。 密碼值的格式為： {technicalAccountId}：{credential}。 不會到期的認證的設定JSON檔案是在其初始化期間進行一次性下載，且Adobe不會保留的副本。 |

輸入所有相關認證後，請選取&#x200B;**[!DNL Connect]**。

[!DNL Connect]對話方塊會在工作階段的第一次出現。 輸入您的使用者ID和密碼，然後選取&#x200B;**[!DNL Connect]**。 日誌中會顯示一則訊息，確認連線成功。

## 後續步驟

現在您已將[!DNL DbVisualizer]與[!DNL Query Service]連線，您可以使用[!DNL DbVisualizer]來撰寫查詢。 如需如何撰寫和執行查詢的詳細資訊，請參閱查詢執行](../best-practices/writing-queries.md)的[指南。
