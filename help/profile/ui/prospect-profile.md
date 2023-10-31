---
title: 潛在客戶設定檔
description: 瞭解如何建立和使用潛在客戶設定檔，以使用第三方資訊收集有關未知客戶的資訊。
type: Documentation
exl-id: 194d25d6-88ae-4a7a-9b79-39120bced5c7
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 7%

---

# 潛在客戶設定檔

Adobe Experience Platform 讓您能夠為客戶提供一致且相關的協調體驗，無論他們何時何地與您的品牌互動。

潛在客戶設定檔用於表示尚未與您的公司互動，但您想要聯絡的人。 使用潛在客戶設定檔，您可以使用受信任的第三方合作夥伴的屬性來補充您的客戶設定檔。

## 瀏覽 {#browse}

若要存取潛在客戶設定檔，請選取 **[!UICONTROL 設定檔]** 在 **[!UICONTROL 潛在客戶]** 區段。

此 **[!UICONTROL 瀏覽]** 頁面隨即顯示。 此時會顯示貴組織的所有潛在客戶設定檔清單。

![此 [!UICONTROL 設定檔] 按鈕會反白顯示 [!UICONTROL 瀏覽] 潛在客戶設定檔頁面。](../images/prospect-profile/browse-profiles.png)

>[!IMPORTANT]
>
>雖然客戶設定檔和潛在客戶設定檔之間的大多數瀏覽功能相同，但您 **無法** 依合併原則瀏覽潛在客戶設定檔。 這是因為潛在客戶設定檔是由系統設計的以時間為基礎的合併原則自動控管。 有關合併原則的更多資訊可在以下網址找到： [合併原則概觀](../merge-policies/overview.md).

如需有關瀏覽設定檔的詳細資訊，請參閱 [設定檔使用手冊的瀏覽區段](./user-guide.md#browse-identity).

## 潛在客戶設定檔詳細資訊 {#profile-details}

>[!IMPORTANT]
>
>潛在客戶設定檔在Adobe Experience Platform中居住25天後會自動過期。

若要檢視特定潛在客戶設定檔的詳細資訊，請在 [!UICONTROL 瀏覽] 頁面。

![潛在客戶設定檔會醒目顯示在瀏覽頁面上。](../images/prospect-profile/select-specific-profile.png)

系統會顯示潛在客戶設定檔的相關資訊，包括與設定檔和對象成員資格相關聯的屬性。

![將會顯示潛在客戶設定檔詳細資訊頁面。](../images/prospect-profile/profile-details.png)

如需這些標籤的詳細資訊，請參閱 [檢視設定檔使用手冊的設定檔詳細資訊區段](./user-guide.md#profile-detail).

您也可以選取「 」，檢視JSON格式的所有屬性 **[!UICONTROL 檢視JSON]**.

![此 [!UICONTROL 檢視JSON] 「潛在客戶設定檔詳細資訊」頁面上會醒目顯示按鈕。](../images/prospect-profile/profile-select-view-json.png)

此 [!UICONTROL 檢視JSON] 對話方塊隨即顯示。 潛在客戶設定檔的屬性現在會顯示為JSON表單。

![潛在客戶設定檔的屬性會顯示在JSON表單中。](../images/prospect-profile/profile-view-json.png)

## 建議的使用案例 {#use-cases}

若要瞭解如何在Experience Platform中結合其他Platform功能使用潛在客戶設定檔功能，請閱讀以下使用案例檔案：

- [透過潛在客戶功能吸引和贏取新客戶](../../rtcdp/partner-data/prospecting.md)

## 後續步驟

閱讀本指南後，您現在瞭解如何在Adobe Experience Platform中使用潛在客戶設定檔。 若要瞭解這些潛在客戶設定檔如何用於受眾，請閱讀 [潛在客戶受眾指南](../../segmentation/ui/prospect-audience.md).
