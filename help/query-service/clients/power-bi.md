---
keywords: Experience Platform; home；熱門主題；查詢服務；查詢服務；Power BI;power bi；連接到查詢服務；
solution: Experience Platform
title: 將Power BI連接到查詢服務
topic-legacy: connect
description: 本檔案將逐步介紹如何連接Power BI與Adobe Experience Platform查詢服務。
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---

# 將[!DNL Power BI]連接到查詢服務(PC)

本檔案涵蓋連接Adobe Experience Platform查詢服務的Power BI步驟。

>[!NOTE]
>
> 本指南假定您已經擁有[!DNL Power BI]的訪問權限，並熟悉如何導航其介面。 有關[!DNL Power BI]的更多資訊，請參閱[official [!DNL Power BI] 文檔](https://docs.looker.com/)。
>
> 此外，Power BI在Windows裝置上僅&#x200B;**可用。**

安裝Power BI後，您需要安裝`Npgsql`，這是用於PostgreSQL的。NET驅動程式包。 有關Npgsql的詳細資訊，請參閱[Npgsql文檔](https://www.npgsql.org/doc/index.html)。

>[!IMPORTANT]
>
>您必須下載v4.0.10或更低版本，因為較新版本會導致錯誤。

在自訂設定畫面的「[!DNL Npgsql GAC Installation]」下，選取&#x200B;**[!DNL Will be installed on local hard drive]**。

要確保npgsql已正確安裝，請在繼續下一步之前重新啟動電腦。

## 將[!DNL Power BI]連接到[!DNL Query Service]

要將[!DNL Power BI]連接到[!DNL Query Service]，請開啟[!DNL Power BI]並在頂部菜單帶中選擇&#x200B;**[!DNL Get Data]**。

![](../images/clients/power-bi/open-power-bi.png)

選擇&#x200B;**[!DNL PostgreSQL database]**，後面跟&#x200B;**[!DNL Connect]**。

![](../images/clients/power-bi/get-data.png)

您現在可以輸入伺服器和資料庫的值。 有關查找資料庫名稱、主機、埠和登錄憑據的詳細資訊，請訪問Platform](https://platform.adobe.com/query/configuration)上的[ credentials頁。 若要尋找您的認證，請登入[!DNL Platform]，然後選取&#x200B;**[!UICONTROL Queries]**，後面接著&#x200B;**[!UICONTROL Credentials]**。

**[!DNL Server]** 是在連接詳細資訊下找到的主機。對於生產環境，請將埠`:80`添加到主機字串的末尾。 **[!DNL Database]** 可以是「all」或資料集表格名稱。

此外，您也可以選取&#x200B;**[!DNL Data Connectivity mode]**。 選擇&#x200B;**[!DNL Import]**&#x200B;以顯示所有可用表的清單，或選擇&#x200B;**[!DNL DirectQuery]**&#x200B;直接建立查詢。

若要進一步瞭解&#x200B;**[!DNL Import]**&#x200B;模式，請閱讀有關預覽和匯入表](#preview)的章節。 [要瞭解有關&#x200B;**[!DNL DirectQuery]**&#x200B;模式的更多資訊，請閱讀有關建立SQL陳述式](#create)的章節。 [確認資料庫詳細資訊後，選擇&#x200B;**[!DNL OK]**。

![](../images/clients/power-bi/connectivity-mode.png)

出現提示，詢問您的使用者名稱、密碼和應用程式設定。 填寫這些詳細資訊，然後選取&#x200B;**[!DNL Connect]**&#x200B;以繼續下一步驟。

![](../images/clients/power-bi/import-mode.png)

## 預覽並導入表{#preview}

如果已選擇&#x200B;**[!DNL Import]**&#x200B;模式，則會出現對話框，顯示所有可用表的清單。 選擇要預覽的表，然後選擇&#x200B;**[!DNL Load]**&#x200B;以將資料集導入[!DNL Power BI]。

![](../images/clients/power-bi/preview-table.png)

表格現在會匯入到Power BI。

![](../images/clients/power-bi/import-table.png)

## 建立SQL陳述式{#create}

如果已選擇&#x200B;**[!DNL DirectQuery]**&#x200B;模式，則需要用要建立的SQL查詢填寫「高級選項」部分。

在&#x200B;**[!DNL SQL statement]**&#x200B;下，插入要建立的SQL查詢。 確保選中標有&#x200B;**[!DNL Include relationship columns]**&#x200B;的複選框。 在寫入查詢後，選擇&#x200B;**[!DNL OK]**&#x200B;繼續。

![](../images/clients/power-bi/direct-query-mode.png)

此時會顯示查詢的預覽。 選擇&#x200B;**[!DNL Load]**&#x200B;以查看查詢結果。

![](../images/clients/power-bi/preview-direct-query.png)

## 後續步驟

現在您已連接[!DNL Query Service]，您可以使用[!DNL Power BI]來編寫查詢。 有關如何寫入和運行查詢的詳細資訊，請閱讀[運行查詢](../best-practices/writing-queries.md)的指南。
