---
title: 套用存取權標籤以管理使用者對UI中來源資料流的存取權
description: 瞭解如何使用Experience Platform UI套用存取標籤並管理使用者對您的來源資料流程的存取。
exl-id: 7aab9706-2f43-43c7-9878-1959d5a8a6b0
source-git-commit: f57fa04e668fa9c61b9b15778e74969edffae0fa
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 2%

---

# 套用存取權標籤以管理使用者對UI中來源資料流的存取權

您可以使用Real-Time CDP中[以屬性為基礎的存取控制](../../../access-control/abac/overview.md)所提供的功能，將標籤套用至您的來源資料流。 透過此功能，您可以確保組織中只有一部分使用者有權存取特定來源資料流。

將存取標籤新增至特定資料流時，只有具備該標籤指派之角色存取權的使用者才能檢視及編輯該資料流。 如果來源資料流未標籤任何標籤，則屬於您組織的所有使用者皆可看到該資料流。 例如，如果您將C12標籤套用至資料流，則指派給沒有C12標籤之角色的使用者，將無法檢視和編輯具有C12標籤的資料流。

請參閱本指南，瞭解如何使用Adobe Experience Platform使用者介面將存取標籤套用至您的來源資料流。

## 快速入門

在使用存取控制標籤之前，請務必先熟悉屬性型存取控制的功能。 如需詳細資訊，請參閱下列檔案：

* [屬性式存取控制概觀](../../../access-control/abac/overview.md)
* [以屬性為基礎的存取控制端對端指南](../../../access-control/abac/end-to-end-guide.md)
* [使用許可權UI管理標籤](../../../access-control/abac/ui/labels.md)
* [資料使用標籤字彙表](../../../data-governance/labels/reference.md)

## 將存取權標籤套用至來源資料流

>[!NOTE]
>
>* 您不能將標籤套用到資料流執行。 不過，資料流執行會繼承您套用至父資料流的任何標籤。
>
>* 如果您沒有資料流的檢視存取權，那麼您將無法檢視其對應的資料流執行。

若要將存取標籤套用至您的來源資料流，請導覽至&#x200B;**[!UICONTROL 來源]** > **[!UICONTROL 資料流]**，然後找到您要更新的資料流並限制使用者存取權。

接著，在[!UICONTROL 名稱]資料行中選取省略符號(`...`)，然後選取&#x200B;**[!UICONTROL 套用存取權標籤]**，以新增和管理所選資料流程的標籤。

![來源中已選取「套用存取標籤」選項的資料流頁面。](../../images/tutorials/labels/apply_access_labels.png)

[!UICONTROL 套用存取權和資料治理標籤]視窗會出現。 您可以在此視窗中選取要套用至資料流的標籤。 您也可以依標籤型別來篩選標籤。 完成後，選取&#x200B;**[!UICONTROL 儲存]**。

![已選取C2標籤的資料治理標籤視窗。](../../images/tutorials/labels/labels_window.png)

當您成功設定資料流的存取標籤後，任何無法存取該標籤的使用者將無法再擷取資料流。 您也可以使用[!UICONTROL 存取標籤]欄來檢視套用至指定資料流程的標籤。

## 後續步驟

您現在知道如何將存取權標籤套用至來源資料流。 您現在可以確保組織內只有特定群組使用者可以存取特定來源資料流。 如需詳細資訊，請參閱下列檔案：

* [將存取標籤套用至API中的來源資料流](../api/labels.md)
* [存取控制概覽](../../../access-control/home.md)
