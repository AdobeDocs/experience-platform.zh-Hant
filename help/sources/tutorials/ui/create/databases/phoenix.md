---
title: 使用Experience Platform使用者介面連線您的Phoenix帳戶
description: 瞭解如何使用使用者介面連線您的Phoenix帳戶，並將Phoenix資料庫中的資料帶入Experience Platform。
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: 0e3fee4d78646b1d1d6730495358b3ced4127f4e
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 1%

---

# 使用UI連線您的[!DNL Phoenix]帳戶以Experience Platform

>[!IMPORTANT]
>
>[!DNL Phoenix]來源將於2025年5月底淘汰。 作為替代方法，您可以使用[[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md)來源。

本教學課程提供如何連線您的[!DNL Phoenix]帳戶以及將[!DNL Phoenix]資料庫中的資料帶入Experience Platform的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經擁有已驗證的[!DNL Phoenix]帳戶，則可以略過本檔案的其餘部分，並繼續進行有關[為資料庫設定資料流](../../dataflow/databases.md)的教學課程。

### 收集必要的認證

若要在Experience Platform上存取您的[!DNL Phoenix]帳戶，您必須提供下列值：

| 認證 | 說明 |
| --- | --- |
| Host | [!DNL Phoenix]伺服器的IP位址或主機名稱。 |
| 連接埠 | [!DNL Phoenix]伺服器用來監聽使用者端連線的TCP連線埠。 如果您要連線到[!DNL Azure HDInsights]，則指定連線埠為443。 如果未提供此引數，則值預設為8765。 |
| HTTP路徑 | 對應至[!DNL Phoenix]伺服器的部分URL。 如果您使用[!DNL Azure HDInsights]叢集，請指定/hbasephoenix0。 |
| 使用者名稱 | 您用來存取[!DNL Phoenix]伺服器的使用者名稱。 |
| 密碼 | 與使用者對應的密碼。 |
| Enable SSL | 指定是否使用SSL加密伺服器連線的切換按鈕。 |

如需開始使用的詳細資訊，請參閱[此 [!DNL Phoenix] 檔案](https://python-phoenixdb.readthedocs.io/en/latest/api.html)。

收集必要的認證後，您可以依照下列步驟連線您的[!DNL Phoenix]帳戶以Experience Platform。

## 連線您的[!DNL Phoenix]帳戶

在Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取來源工作區。 *[!UICONTROL 目錄]*&#x200B;畫面會顯示Experience Platform來源目錄中的各種可用來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找特定來源。

從來源類別清單選取&#x200B;**[!UICONTROL 資料庫]**，然後從[!DNL Phoenix]卡片選取&#x200B;**[!UICONTROL 新增資料]**。

>[!TIP]
>
>來源目錄中的來源可能會根據來源的狀態顯示不同的提示。
> 
>* **[!UICONTROL 新增資料]**&#x200B;表示存在與您所選來源關聯的現有已驗證帳戶。
>
>* **[!UICONTROL 設定]**&#x200B;表示您必須提供認證並驗證新帳戶，才能使用您選取的來源。

![已選取Phoenix來源卡的Experience PlatformUI上的來源目錄。](../../../../images/tutorials/create/phoenix/catalog.png)

**[!UICONTROL 連線至Phoenix]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

>[!BEGINTABS]

>[!TAB 使用現有的Phoenix帳戶]

若要使用現有帳戶，請選取[!UICONTROL 現有帳戶]，然後從顯示的清單中選取您要使用的帳戶。 完成後，選取[!UICONTROL 下一步]以繼續。

![貴組織中已經存在的已驗證Phoenix資料庫帳戶清單。](../../../../images/tutorials/create/phoenix/existing.png)

>[!TAB 建立新的Phoenix帳戶]

若要使用新帳戶，請選取[!UICONTROL 新帳戶]，並提供名稱、說明和您的[!DNL Phoenix]驗證認證。 完成時，請選取[!UICONTROL 連線到來源]，並等待幾秒鐘以建立新連線。

![新的帳戶介面，您可以在其中提供驗證認證並建立Phoenix帳戶。](../../../../images/tutorials/create/phoenix/new.png)

>[!ENDTABS]

## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL Phoenix]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流以將資料帶入Experience Platform](../../dataflow/databases.md)。
