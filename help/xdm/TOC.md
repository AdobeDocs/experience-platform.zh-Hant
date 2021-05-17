---
audience: user
user-guide-title: Experience Data Model (XDM) 系統說明
breadcrumb-title: Experience Data Model (XDM) 指南
user-guide-description: 使用體驗資料模型(XDM)類別和架構欄位群組來標準化體驗資料。
feature: 結構描述
source-git-commit: dcfdc9c479e8a77296f7cb0bf9f5bb36e9261b75
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 17%

---


# 體驗資料模型(XDM)系統 {#xdm}

* [XDM系統概述](home.md)
* 結構描述 {#schema}
   * [架構構成基礎](schema/composition.md)
   * [資料建模的最佳實務](schema/best-practices.md)
   * [XDM欄位類型約束](schema/field-constraints.md)
   * [XDM中的命名空間](./schema/namespaces.md)
   * [XDM欄位字典](schema/field-dictionary.md)
   * 行業資料模型{#industries}
      * [概述](./schema/industries/overview.md)
      * [零售資料模型ERD](./schema/industries/retail.md)
      * [金融服務資料模型](./schema/industries/financial.md)
      * [旅行和接待服務資料模型](./schema/industries/travel-hospitality.md)
* 類別 {#classes}
   * [XDM個人資料](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
   * [區段定義](./classes/segment-definition.md)
* 方案欄位組{#field-groups}
   * 配置檔案欄位組{#profile}
      * [IdentityMap](./field-groups/profile/identitymap.md)
      * [人口統計詳細資訊](./field-groups/profile/demographic-details.md)
      * [個人聯絡資訊](./field-groups/profile/personal-contact-details.md)
      * [區段會籍詳細資訊](./field-groups/profile/segmentation.md)
      * [工作聯繫人詳細資訊](./field-groups/profile/work-contact-details.md)
      * [隱私權／個人化／行銷偏好設定（同意）](./field-groups/profile/consents.md)
   * 事件欄位組{#event}
      * [用戶ID詳細資訊](./field-groups/event/enduserids.md)
      * [環境詳細資訊](./field-groups/event/environment-details.md)
   * [欄位群組名稱更新](./field-groups/name-updates.md)
* 資料類型 {#data-types}
   * [應用程式](./data-types/application.md)
   * [信標](./data-types/beacon.md)
   * [瀏覽器詳細資訊](./data-types/browser-details.md)
   * [商務](./data-types/commerce.md)
   * [同意與偏好](./data-types/consents.md)
   * [裝置](./data-types/device.md)
   * [電子郵件地址](./data-types/email-address.md)
   * [環境](./data-types/environment.md)
   * [通用許可欄位](./data-types/consent-field.md)
   * [一般行銷偏好設定欄位](./data-types/marketing-field.md)
   * [具有訂閱的一般行銷偏好設定欄位](./data-types/marketing-field-subscriptions.md)
   * [一般個人化偏好設定欄位](./data-types/personalization-field.md)
   * [地理](./data-types/geo.md)
   * [地域社交圈](./data-types/geo-circle.md)
   * [地理坐標](./data-types/geo-coordinates.md)
   * [地理互動詳細資訊](./data-types/geo-interaction-details.md)
   * [地理形狀](./data-types/geo-shape.md)
   * [身份](./data-types/identity.md)
   * [測量](./data-types/measure.md)
   * [訂購](./data-types/order.md)
   * [付款項](./data-types/payment-item.md)
   * [「人」](./data-types/person.md)
   * [人員姓名](./data-types/person-name.md)
   * [電話號碼](./data-types/phone-number.md)
   * [置入內容](./data-types/place-context.md)
   * [POI詳細資訊](./data-types/poi-details.md)
   * [POI互動](./data-types/poi-interaction.md)
   * [郵遞區號](./data-types/postal-address.md)
   * [搜尋](./data-types/search.md)
   * [訂閱](./data-types/subscription.md)
   * [網路互動](./data-types/web-interactions.md)
   * [網頁詳細資訊](./data-types/webpage-details.md)
* [!UICONTROL 架構] UI  {#ui}
   * [概述](./ui/overview.md)
   * [探索 XDM 資源](./ui/explore.md)
   * 建立和編輯資源{#resources}
      * [結構描述](./ui/resources/schemas.md)
      * [類別](./ui/resources/classes.md)
      * [欄位群組](./ui/resources/field-groups.md)
      * [資料類型](./ui/resources/data-types.md)
   * 定義欄位{#fields}
      * [概述](./ui/fields/overview.md)
      * [必填欄位](./ui/fields/required.md)
      * [物件欄位](./ui/fields/object.md)
      * [陣列欄位](./ui/fields/array.md)
      * [列舉欄位](./ui/fields/enum.md)
      * [身分欄位](./ui/fields/identity.md)
      * [關係欄位](./ui/fields/relationship.md)
   * [產生範例XDM資料](./ui/sample.md)
   * [匯出XDM結構](./ui/export.md)
* 方案註冊表API {#api}
   * [概述](api/overview.md)
   * [快速入門](api/getting-started.md)
   * [結構描述](api/schemas.md)
   * [行為](api/behaviors.md)
   * [類別](api/classes.md)
   * [架構欄位組](api/field-groups.md)
   * [資料類型](api/data-types.md)
   * [描述符](api/descriptors.md)
   * [工會](api/unions.md)
   * [匯出／匯入](api/export-import.md)
   * [範例資料](api/sample-data.md)
   * [審計日誌](api/audit-log.md)
   * [臨機結構](api/ad-hoc.md)
   * [Mixins（已過時）](api/mixins.md)
   * [附錄](api/appendix.md)
* 教學課程 {#tutorials}
   * [建立結構(UI)](tutorials/create-schema-ui.md)
   * [建立結構(API)](tutorials/create-schema-api.md)
   * [定義兩個結構描述(UI)之間的關係](tutorials/relationship-ui.md)
   * [定義兩個結構描述(API)之間的關係](tutorials/relationship-api.md)
   * [建立臨機結構(API)](tutorials/ad-hoc.md)
* [疑難排解指南](troubleshooting-guide.md)
* [API 參考資料](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [平台版本注意事項](https://www.adobe.com/go/platform-release-notes-en)