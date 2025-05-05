---
title: 潛在客戶設定檔
description: 瞭解如何建立和使用潛在客戶設定檔，以使用第三方資訊收集有關未知客戶的資訊。
type: Documentation
exl-id: 194d25d6-88ae-4a7a-9b79-39120bced5c7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 1%

---

# 潛在客戶輪廓

Adobe Experience Platform可讓您為客戶推動協調、一致且相關的體驗，無論客戶在哪裡或何時與您的品牌互動。

潛在客戶設定檔用於表示尚未與您的公司互動，但您想要聯絡的人。 使用潛在客戶設定檔，您可以使用受信任的第三方合作夥伴的屬性來補充您的客戶設定檔。

## 瀏覽 {#browse}

若要存取潛在客戶設定檔，請在&#x200B;**[!UICONTROL 潛在客戶]**&#x200B;區段中選取&#x200B;**[!UICONTROL 設定檔]**。

顯示&#x200B;**[!UICONTROL 瀏覽]**&#x200B;頁面。 此時會顯示貴組織的所有潛在客戶設定檔清單。

![已反白顯示[!UICONTROL 設定檔]按鈕，顯示潛在客戶設定檔的[!UICONTROL 瀏覽]頁面。](../images/prospect-profile/browse-profiles.png)

>[!IMPORTANT]
>
>雖然客戶設定檔和潛在客戶設定檔之間的大部分瀏覽功能相同，但您&#x200B;**無法**&#x200B;依據合併原則瀏覽潛在客戶設定檔。 這是因為潛在客戶設定檔是由系統設計的以時間為基礎的合併原則自動控管。 您可以在[合併原則概觀](../merge-policies/overview.md)中找到有關合併原則的更多資訊。

如需有關瀏覽設定檔的詳細資訊，請參閱設定檔使用手冊[&#128279;](./user-guide.md#browse-identity)的瀏覽區段。

## 潛在客戶設定檔詳細資訊 {#profile-details}

>[!IMPORTANT]
>
>潛在客戶設定檔在Adobe Experience Platform中居住25天後會自動過期。

若要檢視特定潛在客戶設定檔的詳細資訊，請在[!UICONTROL 瀏覽]頁面上選取設定檔。

![在瀏覽頁面上標示潛在客戶設定檔。](../images/prospect-profile/select-specific-profile.png)

系統會顯示潛在客戶設定檔的相關資訊，包括與設定檔和對象成員資格相關聯的屬性。

![潛在客戶設定檔詳細資訊頁面已顯示。](../images/prospect-profile/profile-details.png)

如需這些標籤的詳細資訊，請參閱設定檔使用手冊[&#128279;](./user-guide.md#profile-detail)的檢視設定檔詳細資訊區段。

您也可以選取&#x200B;**[!UICONTROL 檢視JSON]**，檢視JSON格式的所有屬性。

![潛在客戶設定檔詳細資訊頁面上會醒目顯示[!UICONTROL 檢視JSON]按鈕。](../images/prospect-profile/profile-select-view-json.png)

[!UICONTROL 檢視JSON]對話方塊就會顯示。 潛在客戶設定檔的屬性現在會顯示為JSON表單。

![潛在客戶設定檔的屬性會以JSON格式顯示。](../images/prospect-profile/profile-view-json.png)

## 建議的使用案例 {#use-cases}

若要瞭解如何在Experience Platform中將潛在客戶設定檔功能與其他Experience Platform功能搭配使用，請參閱下列使用案例檔案：

- [透過潛在客戶功能吸引和贏取新客戶](../../rtcdp/partner-data/prospecting.md)

## 後續步驟

閱讀本指南後，您現在瞭解如何在Adobe Experience Platform中使用潛在客戶設定檔。 若要瞭解這些潛在客戶設定檔如何在對象中使用，請閱讀[潛在客戶對象指南](../../segmentation/types/prospect-audiences.md)。
