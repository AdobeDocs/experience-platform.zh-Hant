---
audience: user
user-guide-title: Experience Data Model (XDM) 系統說明
breadcrumb-title: Experience Data Model (XDM) 指南
user-guide-description: 使用 Experience Data Model (XDM) 類別和 mixin 將體驗資料標準化。
feature: 結構描述
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 21%

---


# 體驗資料模型(XDM)系統{#xdm}

* [XDM系統概述](home.md)
* 結構描述 {#schema}
   * [架構構成基礎](schema/composition.md)
   * [資料建模的最佳實務](schema/best-practices.md)
   * [XDM欄位類型約束](schema/field-constraints.md)
   * [XDM欄位字典](schema/field-dictionary.md)
   * 行業資料模型{#industries}
      * [概覽](./schema/industries/overview.md)
      * [零售資料模型ERD](./schema/industries/retail.md)
      * [金融服務資料模型](./schema/industries/financial.md)
      * [旅行和接待服務資料模型](./schema/industries/travel-hospitality.md)
* 類別 {#classes}
   * [XDM個人資料](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
   * [區段定義](./classes/segment-definition.md)
* Mixins {#mixins}
   * 描述檔混音{#profile}
      * [IdentityMap](./mixins/profile/identitymap.md)
      * [人口統計詳細資訊](./mixins/profile/person-details.md)
      * [個人聯絡資訊](./mixins/profile/personal-details.md)
      * [隱私權／個人化／行銷偏好設定（同意）](./mixins/profile/consents.md)
      * [區段會籍詳細資訊](./mixins/profile/segmentation.md)
      * [工作聯繫人詳細資訊](./mixins/profile/work-details.md)
   * 事件混音{#event}
      * [用戶ID詳細資訊](./mixins/event/enduserids.md)
      * [環境詳細資訊](./mixins/event/environment-details.md)
   * [Mixin名稱更新](./mixins/name-updates.md)
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
   * [訂單](./data-types/order.md)
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
* [!UICONTROL Schemas] UI {#ui}
   * [概覽](./ui/overview.md)
   * [探索XDM資源](./ui/explore.md)
   * 建立和編輯資源{#resources}
      * [結構描述](./ui/resources/schemas.md)
      * [類別](./ui/resources/classes.md)
      * [Mixins](./ui/resources/mixins.md)
      * [資料類型](./ui/resources/data-types.md)
   * 定義欄位{#fields}
      * [概覽](./ui/fields/overview.md)
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
   * [Mixins](api/mixins.md)
   * [資料類型](api/data-types.md)
   * [描述符](api/descriptors.md)
   * [工會](api/unions.md)
   * [匯出／匯入](api/export-import.md)
   * [範例資料](api/sample-data.md)
   * [審計日誌](api/audit-log.md)
   * [臨機結構](api/ad-hoc.md)
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