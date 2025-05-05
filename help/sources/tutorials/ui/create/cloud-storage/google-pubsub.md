---
title: 在使用者介面中建立Google PubSub Source連線
description: 瞭解如何使用Google使用者介面建立Experience Platform PubSub來源聯結器。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 1%

---

# 在使用者介面中建立[!DNL Google PubSub]來源連線

>[!IMPORTANT]
>
>[!DNL Google PubSub]來源可在來源目錄中提供給已購買Real-Time Customer Data Platform Ultimate的使用者。

本教學課程提供使用Experience Platform使用者介面建立[!DNL Google PubSub] （以下稱為「[!DNL PubSub]」）的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

如果您已經有有效的[!DNL PubSub]連線，您可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/batch/cloud-storage.md)的教學課程。

### 收集必要的認證

您必須提供下列連線屬性的值，才能將您的[!DNL PubSub]帳戶連線至Experience Platform。 如需有關驗證和先決條件設定的詳細資訊，請閱讀[[!DNL PubSub source] 總覽](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites)。


>[!BEGINTABS]

>[!TAB 以專案為基礎的驗證]

| 認證 | 說明 |
| --- | --- |
| 專案ID | 驗證[!DNL PubSub]所需的專案識別碼。 |
| 認證 | 驗證[!DNL PubSub]所需的認證。 您必須確保在移除認證的空格後，放入完整的JSON檔案。 |

>[!TAB 主題和訂閱式驗證]

| 認證 | 說明 |
| --- | --- |
| 認證 | 驗證[!DNL PubSub]所需的認證。 您必須確保在移除認證的空格後，放入完整的JSON檔案。 |
| 主題名稱 | 您的[!DNL PubSub]訂閱名稱。 在[!DNL PubSub]中，訂閱可讓您訂閱訊息發佈至的主題，以接收訊息。 **注意**：單一[!DNL PubSub]訂閱只能用於一個資料流。 若要建立多個資料流，您必須有多個訂閱。 |
| 訂閱名稱 | 您的[!DNL PubSub]訂閱名稱。 在[!DNL PubSub]中，訂閱可讓您訂閱訊息發佈至的主題，以接收訊息。 |

>[!ENDTABS]

如需這些值的詳細資訊，請參閱下列[PubSub驗證](https://cloud.google.com/pubsub/docs/authentication)檔案。 如果您使用以服務帳戶為基礎的驗證，請參閱下列[PubSub指南](https://cloud.google.com/docs/authentication/production#create_service_account)以瞭解如何產生認證的步驟。

>[!TIP]
>
>如果您使用以服務帳戶為基礎的驗證，在複製和貼上認證時，請確保您已授予足夠的使用者存取權給您的服務帳戶，並且JSON中沒有額外的空格。

收集必要的認證後，您可以依照下列步驟將[!DNL PubSub]帳戶連結至Experience Platform。

## 連線您的[!DNL PubSub]帳戶

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以用來建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在[!UICONTROL 雲端儲存空間]類別下，選取&#x200B;**[!UICONTROL Google PubSub]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![Experience Platform UI上的來源目錄。](../../../../images/tutorials/create/google-pubsub/catalog.png)

**[!UICONTROL 連線至Google PubSub]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取您要用來建立新資料流的[!DNL PubSub]帳戶，然後選取[下一步] **以繼續。**

![來源工作流程中的現有帳戶選擇。](../../../../images/tutorials/create/google-pubsub/existing.png)

### 新帳戶

>[!TIP]
>
>* 建立存取受限的帳戶時，您必須至少提供一個主題名稱或訂閱名稱。 如果缺少這兩個值，驗證將會失敗。
>* 建立後，您無法變更[!DNL Google PubSub]基本連線的驗證型別。 若要變更驗證型別，您必須建立新的基礎連線。

如果您正在建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後為您新的[!DNL PubSub]帳戶提供名稱和選擇性說明。

![來源工作流程中Google PubSub來源的新帳戶介面](../../../../images/tutorials/create/google-pubsub/new.png)

[!DNL PubSub]來源可讓您指定在驗證期間允許使用的存取型別。 您可以將帳戶設定為使用專案型驗證、主題與訂閱型驗證。 以專案為基礎的驗證可讓您授與帳戶中根層級專案的存取權，而以主題和訂閱為基礎的驗證則可讓您限制對特定[!DNL PubSub]主題和訂閱的存取權。

>[!BEGINTABS]

>[!TAB 以專案為基礎的驗證]

若要建立可存取您的根[!DNL PubSub]專案資料夾的帳戶。 選取&#x200B;**[!UICONTROL Google PubSub驗證認證]**&#x200B;作為您的驗證型別，並提供您的專案ID和認證。 完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後等待一段時間以建立新連線。

![已選取根存取權的Google PubSub來源的新帳戶介面。](../../../../images/tutorials/create/google-pubsub/root.png)

>[!TAB 主題和訂閱式驗證]

若要建立僅對特定[!DNL PubSub]主題和訂閱具有受限存取權的帳戶，請選取&#x200B;**[!UICONTROL Google PubSub Scoped驗證認證]**，然後提供您的認證、主題名稱和/或訂閱名稱。 完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後等待一段時間以建立新連線。

![已選取範圍存取的Google PubSub來源的新帳戶介面。](../../../../images/tutorials/create/google-pubsub/scoped.png)

>[!ENDTABS]

>[!NOTE]
>
>指派給[!DNL PubSub]專案的主體（角色）會繼承[!DNL PubSub]專案內建立的所有主題和訂閱。 如果您希望主參與者（角色）能夠存取特定主題，則也必須將該主參與者（角色）新增到主題的對應訂閱中。 如需詳細資訊，請閱讀有關存取控制[&#128279;](<https://cloud.google.com/pubsub/docs/access-control>)的[!DNL PubSub] 檔案。

## 選取資料

成功的驗證會將您帶往[!UICONTROL 選取資料]步驟，您可在此導覽您的[!DNL PubSub]資料階層，並選取您要帶入Experience Platform的資料。

>[!BEGINTABS]

>[!TAB 以專案為基礎的驗證]

如果您已通過專案型存取驗證，[!UICONTROL 選取資料]介面將會顯示專案中所有附加了主題的訂閱。

![具有專案型驗證之來源工作流程的選取資料步驟。](../../../../images/tutorials/create/google-pubsub/root-folders.png)

>[!TAB 主題和訂閱式驗證]

如果您已透過主題和訂閱型存取驗證過，[!UICONTROL 選取資料]介面的顯示可能會依您提供的資訊而有所不同。

* 如果您只提供主題名稱，介面會顯示與所提供之主題對應的所有主題訂閱配對。
* 如果您只提供訂閱名稱，介面會顯示與提供的訂閱名稱對應的所有主題 — 訂閱配對。
* 如果同時提供主題和訂閱名稱，介面會顯示與兩個提供值對應的主題 — 訂閱配對。

![來源工作流程的選取資料步驟具有主題和訂閱式驗證。](../../../../images/tutorials/create/google-pubsub/scoped-folders.png)

>[!ENDTABS]

## 後續步驟

依照此教學課程，您已建立[!DNL PubSub]帳戶與Experience Platform之間的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流，以將雲端儲存空間的串流資料匯入Experience Platform](../../dataflow/streaming/cloud-storage-streaming.md)。
