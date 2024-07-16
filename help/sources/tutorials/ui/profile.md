---
keywords: Experience Platform；首頁；熱門主題；啟用傳入資料；填入設定檔；填入rtcp；填入的統一設定檔
solution: Experience Platform
title: 啟用傳入Source資料以在UI中填入客戶設定檔
type: Tutorial
description: 來源聯結器傳入的資料可用於擴充及填入即時客戶個人檔案資料。
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# 啟用傳入來源資料以填入客戶設定檔

來源聯結器的傳入資料可用於擴充及填入您的[!DNL Real-Time Customer Profile]資料。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM)] 系統](../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   - [結構描述組合的基本概念](../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   - [結構描述編輯器教學課程](../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

此外，本教學課程需要您已建立並設定來源聯結器。  在UI中建立不同聯結器的教學課程清單可在[來源聯結器概觀](../../home.md)中找到。

## 填入您的[!DNL Real-Time Customer Profile]資料

為了擴充客戶設定檔，目標資料集的來源結構描述必須相容以用於[!DNL Real-Time Customer Profile]。 相容的結構描述符合下列需求：

- 結構描述至少指定一個屬性做為身分屬性。
- 結構描述具有定義為主要身分的身分屬性。
- 資料流中存在對應，其中主要身分是目標屬性。

在來源工作區中，按一下&#x200B;**[!UICONTROL 瀏覽]**&#x200B;索引標籤，列出您的基本連線。 在顯示的清單中，尋找包含您要填入設定檔之資料流的連線。 按一下連線的名稱以存取其詳細資料。

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

連線的&#x200B;**[!UICONTROL Source活動]**&#x200B;畫面會出現，顯示連線正在將來源資料擷取的資料集。 按一下您要為[!DNL Profile]啟用的資料集名稱。

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

**[!UICONTROL 資料集活動]**&#x200B;畫面隨即顯示。 畫面右側的&#x200B;**[!UICONTROL 屬性]**&#x200B;欄會顯示資料集的詳細資料，並包含&#x200B;**[!UICONTROL 設定檔]**&#x200B;切換引數以及資料集所遵守之結構描述的連結。 按一下結構描述的名稱，即可檢視其組成。

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

**[!UICONTROL 結構描述編輯器]**&#x200B;出現，顯示中央畫布中的結構描述結構。 在畫布中，選取要設定為主要身分的欄位。 在出現的&#x200B;**[!UICONTROL 欄位屬性]**&#x200B;標籤下，選取&#x200B;**[!UICONTROL 身分]**&#x200B;核取方塊，然後選取&#x200B;**[!UICONTROL 主要身分]**。 最後，選取適當的&#x200B;**[!UICONTROL 身分識別名稱空間]**，然後按一下&#x200B;**[!UICONTROL 套用]**。

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

按一下結構描述結構的頂層物件，就會顯示&#x200B;**[!UICONTROL 結構描述屬性]**&#x200B;欄。 切換&#x200B;**[!UICONTROL 設定檔]**&#x200B;引數，以啟用[!DNL Profile]的結構描述。 按一下&#x200B;**[!UICONTROL 儲存]**&#x200B;以完成變更。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

現在結構描述已啟用[!DNL Profile]，請返回&#x200B;**[!UICONTROL 資料集活動]**&#x200B;畫面，然後按一下&#x200B;**[!UICONTROL 屬性]**&#x200B;欄內的&#x200B;**[!UICONTROL 設定檔]**&#x200B;切換按鈕，以啟用[!DNL Profile]的資料集。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

在結構描述和資料集都為[!DNL Profile]啟用的情況下，擷取到該資料集的資料現在也將填入客戶設定檔。

>[!NOTE]
>
>[!DNL Profile]不會使用最近啟用的資料集中的現有資料。

## 後續步驟

依照此教學課程，您已成功啟用[!DNL Profile]母體的傳入資料。 如需詳細資訊，請參閱[[!DNL Real-Time Customer Profile] 總覽](../../../profile/home.md)。
