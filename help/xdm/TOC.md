---
product: experience-platform
audience: user
user-guide-title: Experience Data Model (XDM) 系統說明
breadcrumb-title: Data Model (XDM) 指南
user-guide-description: 使用 Experience Data Model (XDM) 類別和 mixin 將體驗資料標準化。
translation-type: tm+mt
source-git-commit: 465582e0d1503426104a048561b1c8c68e7f55ee
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 22%

---


# Experience Data Model (XDM) System {#xdm}

* [XDM系統概述](home.md)
* 結構描述 {#schema}
   * [架構構成基礎](schema/composition.md)
   * [資料建模的最佳實務](schema/best-practices.md)
   * [XDM欄位類型約束](schema/field-constraints.md)
   * [XDM欄位字典](schema/field-dictionary.md)
   * 架構使用案例 {#use-cases}
      * [同意與偏好資料類型](schema/privacy-consent.md)
* 類別 {#classes}
   * [XDM個人資料](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
* Mixins {#mixins}
   * 描述檔混合 {#profile}
      * [IdentityMap](./mixins/profile/identitymap.md)
      * [人口統計詳細資訊](./mixins/profile/person-details.md)
      * [個人聯絡資訊](./mixins/profile/personal-details.md)
      * [區段會籍詳細資訊](./mixins/profile/segmentation.md)
      * [工作聯繫人詳細資訊](./mixins/profile/work-details.md)
   * 事件混合 {#event}
      * [用戶ID詳細資訊](./mixins/event/enduserids.md)
      * [環境詳細資訊](./mixins/event/environment-details.md)
   * [Mixin名稱更新](./mixins/name-updates.md)
* 資料類型 {#data-types}
   * [信標](./data-types/beacon.md)
   * [瀏覽器詳細資訊](./data-types/browser-details.md)
   * [同意與偏好](./data-types/consents.md)
   * [裝置](./data-types/device.md)
   * [電子郵件地址](./data-types/email-address.md)
   * [環境](./data-types/environment.md)
   * [地理](./data-types/geo.md)
   * [地域社交圈](./data-types/geo-circle.md)
   * [地理坐標](./data-types/geo-coordinates.md)
   * [地理互動詳細資訊](./data-types/geo-interaction-details.md)
   * [地理形狀](./data-types/geo-shape.md)
   * [身份](./data-types/identity.md)
   * [人員姓名](./data-types/person-name.md)
   * [電話號碼](./data-types/phone-number.md)
   * [置入內容](./data-types/place-context.md)
   * [POI詳細資訊](./data-types/poi-details.md)
   * [POI互動](./data-types/poi-interaction.md)
   * [郵遞區號](./data-types/postal-address.md)
* 方案註冊表API {#api}
   * [概述](api/overview.md)
   * [快速入門](api/getting-started.md)
   * [結構描述](api/schemas.md)
   * [類別](api/classes.md)
   * [Mixins](api/mixins.md)
   * [資料類型](api/data-types.md)
   * [描述符](api/descriptors.md)
   * [工會](api/unions.md)
   * [臨機結構](api/ad-hoc.md)
   * [附錄](api/appendix.md)
* 教學課程 {#tutorials}
   * [建立結構(API)](tutorials/create-schema-api.md)
   * [建立結構(UI)](tutorials/create-schema-ui.md)
   * [建立和編輯資料類型(UI)](./tutorials/create-data-type.md)
   * [定義兩個結構描述(API)之間的關係](tutorials/relationship-api.md)
   * [定義兩個結構描述(UI)之間的關係](tutorials/relationship-ui.md)
   * [建立臨機結構(API)](tutorials/ad-hoc.md)
* [疑難排解指南](troubleshooting-guide.md)
* [API 參考資料](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [平台版本注意事項](https://www.adobe.com/go/platform-release-notes-en)