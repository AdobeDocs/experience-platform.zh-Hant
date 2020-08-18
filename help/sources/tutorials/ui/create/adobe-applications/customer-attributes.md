---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立客戶屬性來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 999ff0e9525d7d9f67298862c68bb59ddc35e558
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 8%

---


# 在UI中建立客戶屬性來源連接器

本教學課程提供在UI中建立來源連接器的步驟，以便將客戶屬性描述檔資料收集到Adobe Experience Platform。 有關客戶屬性的詳細資訊，請參閱 [概述檔案](https://docs.adobe.com/content/help/zh-Hant/core-services/interface/customer-attributes/attributes.html)。

## 建立源連接

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選 **[!UICONTROL 取Sources]** ，以存取來源工作區。 「目 **[!UICONTROL 錄]** 」螢幕顯示可用的源以建立入站連接，每個源顯示與其關聯的現有連接數。 選擇「客戶屬性」 **[!UICONTROL 的選項]** ，然後選擇「 **[!UICONTROL 添加資料」]**。 如果連線成功建立，將會重新導向您。

>[!NOTE]
>
>如果您已建立客戶屬性描述檔資料的來源連接器，則與來源連線的選項將會停用。

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

「源 *活動* 」螢幕列出客戶屬性配置檔案資料的所有先前建立的連接，您可以通過按一下「選擇資料」來建立 **新連接**。

>[!NOTE]
>
>可以建立多個來源的入站連接，以導入不同的資料。

![](../../../../images/tutorials/create/customer-attributes/source_activity.png)

從可用客戶屬性配置檔案資料集清單中，選擇要導入的資料集，然後按一下「下 [!DNL Platform] 一步」 ****。

>[!NOTE]
>
>每個客戶屬性來源連線只能選取一個資料集。

![](../../../../images/tutorials/create/customer-attributes/select_data.png)

此時 *會出現* 「查看」步驟，允許您在建立新入站連接之前查看該連接。 連接的詳細資訊按類別分組，包括：

* *來源詳細資訊*:顯示源連接的類型和選定的源資料。
* *目標詳細資訊*:建立其他來源連接器時，此容器會顯示來源資料所吸收的資料集，包括資料集所遵守的架構。 客戶屬性描述檔資料會自動對應並收錄至即時客戶描述檔。

![](../../../../images/tutorials/create/customer-attributes/review.png)

## 後續步驟

建立連線後，系統會自動建立目標結構和資料集以包含傳入的資料。當初始擷取完成時，下游服務（例如和）可使用客戶屬 [!DNL Platform] 性描述檔 [!DNL Real-time Customer Profile] 資料 [!DNL Segmentation Service]。 如需詳細資訊，請參閱下列檔案：

* [[!DNL Real-time Customer Profile] 概述](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 概述](../../../../../segmentation/home.md)
