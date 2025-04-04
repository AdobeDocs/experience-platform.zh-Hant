---
keywords: Experience Platform；首頁；熱門主題；tableau；Tableau；查詢服務；查詢服務；連線到查詢服務；
solution: Experience Platform
title: 將Tableau連線至查詢服務
description: 本檔案將逐步說明連線Tableau與Adobe Experience Platform查詢服務的步驟。
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# 將[!DNL Tableau]連線至查詢服務

本檔案提供連線[!DNL Tableau]與Adobe Experience Platform [!DNL Query Service]的資訊。

>[!NOTE]
>
> 本指南假設您已擁有[!DNL Tableau]的存取權，且熟悉如何導覽其介面。 有關[!DNL Tableau]的更多資訊可在[正式 [!DNL Tableau] 檔案](https://help.tableau.com/current/pro/desktop/en-us/default.htm)中找到。

有關如何[使用Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm)連線至PostgreSQL伺服器的說明，請參閱官方Tableau網站。 連線設定對話方塊顯示後，請在引數欄位中輸入您的Experience Platform認證，以與Adobe Experience Platform連線。 以下列出必要的連線引數清單。

| 連線引數 | 說明 |
|---|---|
| **[!DNL Server]** | SFTP儲存位置的位址。 使用您的Experience Platform **[!UICONTROL 主機]**&#x200B;認證的值。 |
| **[!DNL Port]:** | [!DNL Query Service]的連線埠。 您必須使用連線埠&#x200B;**80**&#x200B;或&#x200B;**5432**&#x200B;來與[!DNL Query Service]連線。 |
| **[!DNL Database]** | 您要存取的資料庫。 使用您的Experience Platform **[!UICONTROL 資料庫]**&#x200B;認證的值： `prod:all`。 |
| **[!DNL Authentication]:** | 您選擇的證明使用者身分的方法。 建議您從下拉式功能表的可用選項中選取[!DNL Username and Password]。 |
| **[!DNL Username]** | 這是您的Experience Platform組織ID。 使用您的Experience Platform **[!UICONTROL 使用者名稱]**&#x200B;認證的值。 ID將採用`ORG_ID@AdobeOrg`格式。 |
| **[!DNL Password]** | 此英數字串是您的Experience Platform **[!UICONTROL 密碼]**&#x200B;認證。 如果您想要使用不會到期的認證，此值是從`technicalAccountID`和在組態JSON檔案中下載的`credential`串連的引數。 密碼值的格式為： {technicalAccountId}：{credential}。 不會到期的認證的設定JSON檔案是在其初始化期間的一次性下載，Adobe不會保留其副本。 |

如需尋找您的使用者名稱、密碼和登入認證的詳細資訊，請參閱[認證指南](../ui/credentials.md)。 若要尋找您的認證，請登入[!DNL Experience Platform]，然後選取&#x200B;**[!UICONTROL 查詢]**，接著選取&#x200B;**[!UICONTROL 認證]**。

>[!IMPORTANT]
>
>身為Tableau或Power BI使用者，您可以從查詢服務憑證標籤將Customer Journey Analytics連線至您的BI工具。 請參閱認證檔案，瞭解如何[將您的BI工具連線至Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics)的說明。

在嘗試連線之前，請確定您已核取&#x200B;**[!UICONTROL 需要SSL]**&#x200B;方塊。 請參閱[SSL模式檔案](./ssl-modes.md)，瞭解關於協力廠商連線至Adobe Experience Platform查詢服務的SSL支援。

>[!IMPORTANT]
>
>第三方BI工具中的巢狀資料結構可以平面化，以提高其可用性，並減少擷取、分析、轉換和報表資料所需的工作量。 請參閱[`FLATTEN`功能](../key-concepts/flatten-nested-data.md)的相關檔案，瞭解連線至資料庫時如何啟用此設定的說明。

填寫完您的所有認證後，請確認您的設定以繼續。 您現在已連線Adobe Experience Platform。

## 後續步驟

現在您已連線到[!DNL Query Service]，您可以使用[!DNL Tableau]來撰寫查詢。 如需如何撰寫和執行查詢的詳細資訊，請閱讀[執行查詢](../best-practices/writing-queries.md)的指南。
