---
title: 使用Experience Platform UI建立Oracle Eloqua來源連線
description: 瞭解如何使用Adobe Experience Platform UI將Experience Platform連結至Oracle Eloqua。
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: 7ff0709b62590bb80c1ed664368f28cdc4a950ea
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 2%

---

# 使用Experience Platform UI建立[!DNL Oracle Eloqua]來源連線

>[!WARNING]
>
>[!DNL Oracle Eloqua]來源將於2026年1月汰除。 新的來源將作為替代方案於今年晚些時候發行。 釋放新來源後，您必須在2026年1月底之前建立新的帳戶連線和資料流，以計畫移轉至新來源。

本教學課程提供使用Adobe Experience Platform使用者介面建立[!DNL Oracle Eloqua]來源連線的步驟。

## 快速入門

本指南需要您深入瞭解下列Experience Platform元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

如果您已在Experience Platform上擁有已驗證的[!DNL Oracle Eloqua]帳戶，則您可以略過本檔案的其餘部分，並繼續進行有關[建立資料流以將行銷自動化資料帶入Experience Platform](../../dataflow/marketing-automation.md)的教學課程。

### 收集必要的認證

若要將[!DNL Oracle Eloqua]連線至Experience Platform，您必須提供下列驗證屬性的值：

| 認證 | 說明 |
| --- | --- |
| 端點 | [!DNL Oracle Eloqua]伺服器的端點。 [!DNL Oracle Eloqua]支援多個資料中心。 若要尋找您的端點，請使用您的認證登入[[!DNL Oracle Eloqua] 介面](https://login.eloqua.com)，然後從重新導向URL複製基底URL部分。 您的URL模式格式為`xxx.xx.eloqua.com`，輸入時應不含`http`或`https`。 |
| 使用者名稱 | [!DNL Oracle Eloqua]伺服器的使用者名稱。 使用者名稱必須格式化為`siteName + \\ + username`，其中`siteName`是您用來登入[!DNL Oracle Eloqua]的公司名稱，`username`是您的使用者名稱。 例如，您的登入使用者名稱可以是： `Eloqua\Andy`。 **注意**：您必須在使用UI時使用單一反斜線(`\`)，因為Experience Platform UI會在輸入使用者名稱時自動新增額外的反斜線(`\`)。 |
| 密碼 | 與您的[!DNL Oracle Eloqua]使用者名稱對應的密碼。 |

如需[!DNL Oracle Eloqua]的驗證認證詳細資訊，請參閱驗證[&#128279;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html)的[!DNL Oracle Eloqua] 指南。

收集必要的認證後，您可以依照下列步驟將[!DNL Oracle Eloqua]帳戶連結至Experience Platform。

## 連線您的[!DNL Oracle Eloqua]帳戶

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在[!UICONTROL 行銷自動化]類別下，選取&#x200B;**[!UICONTROL Oracle Eloqua]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![目錄](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

**[!UICONTROL 連線Oracle Eloqua帳戶]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取您要用來建立新資料流的[!DNL Oracle Eloqua]帳戶，然後選取[下一步] **以繼續。**

![現有](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### 新帳戶

如果您正在建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後提供名稱、選擇性說明以及您的[!DNL Oracle Eloqua]認證的適當值。 完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後等待一段時間以建立新連線。

![新](../../../../images/tutorials/create/oracle-eloqua/new.png)

## 後續步驟

依照本教學課程，您已驗證並建立[!DNL Oracle Eloqua]帳戶與Experience Platform之間的來源連線。 您現在可以繼續進行下一個教學課程，並[建立資料流以將行銷自動化資料帶入Experience Platform](../../dataflow/marketing-automation.md)。
