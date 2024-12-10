---
title: 醫療保健資料模型V2
description: 瞭解一些常見的醫療保健使用案例和要使用的最佳類別、相關欄位群組和資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a796b58b-b36f-4277-870b-0d3939af8061
source-git-commit: 36f1a443eda47917d5b6bd84d4765ff044b5093a
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 12%

---

# [!UICONTROL 醫療保健]資料模型V2

## 欄位群組和類別 {#field-groups}

下表概述幾種常見醫療保健使用案例的建議類別和結構描述欄位群組。

<table>
  <thead>
    <tr>
      <th>使用案例</th>
      <th>欄位群組</th>
      <th>相容類別</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>建立/更新病人</strong>：當病人到達醫院服務檯時，會建立病人記錄，包括人口統計細節，例如識別碼（選擇性）、病人姓名、出生日期、性別和地址。 這是醫療保健IT的重要元件。</td>
      <td><a href="./field-groups/patient.md">患者</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM 個人輪廓</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="6"><strong>疫苗接種</strong>：加速疫苗接種程式、管理病人免疫記錄，以及將EMR與疫苗管理系統整合。</td>
      <td><a href="./field-groups/immunization.md">免疫</a></td>
      <td>
        <li><a href="../../classes/experienceevent.md">XDM體驗事件</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/patient.md">患者</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM 個人輪廓</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/location.md">位置</a></td>
      <td>
        <li><a href="./classes/location.md">位置</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication.md">藥物</a></td>
      <td>
        <li><a href="../../classes/medication.md">藥物</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication-dispense.md">藥物配發</a></td>
      <td>
        <li><a href="../../classes/medication.md">藥物</a></li>
        <li><a href="../../classes/individual-profile.md">XDM 個人輪廓</a></li>
        <li><a href="../../classes/provider.md">提供者</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication-request.md">藥物請求</a></td>
      <td>
        <li><a href="../../classes/medication.md">藥物</a></li>
        <li><a href="../../classes/individual-profile.md">XDM 個人輪廓</a></li>
        <li><a href="../../classes/provider.md">提供者</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="4"><strong>照護後守約</strong>：激勵病人和照護者完成他們的治療計畫，並降低匯款率。</td>
      <td><a href="./field-groups/patient.md">患者</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM 個人輪廓</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/location.md">位置</a></td>
      <td>
        <li><a href="./classes/location.md">位置</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/care-plan.md">服務計畫</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM 個人輪廓</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/goal.md">目標</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM 個人輪廓</a></li>
        <li><a href="../../classes/provider.md">提供者</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="7"><strong>保險的消費者體驗</strong>：改善購買保險的消費者的數位贏取和體驗。 例如： 
        <li> 了解消費者行為，向存取包含一般資訊（例如計畫、計畫名稱/層級、Medicaid或健康計畫）之頁面的使用者傳送促銷電子郵件或目標第三方廣告
        </li> 
        <li> 傳送心臟健康的疫苗相關資訊，以建立品牌獎勵或請求排程疫苗給搜尋心臟健康和疫苗資訊的人。
        </li>
      </td>
      <td><a href="./field-groups/patient.md">患者</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM 個人輪廓</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/coverage.md">涵蓋範圍</a></td>
      <td>
        <li><a href="../../classes/plan.md">計畫</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/account.md">帳戶</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM 個人輪廓</a></li>
        <li><a href="../../classes/provider.md">提供者</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/location.md">位置</a></td>
      <td>
        <li><a href="./classes/location.md">位置</a></li>
      </td>
    </tr>
      <tr>
      <td><a href="./field-groups/medication.md">藥物</a></td>
      <td>
        <li><a href="../../classes/medication.md">藥物</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication-dispense.md">藥物配發</a></td>
      <td>
        <li><a href="../../classes/medication.md">藥物</a></li>
        <li><a href="../../classes/individual-profile.md">XDM 個人輪廓</a></li>
        <li><a href="../../classes/provider.md">提供者</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication-request.md">藥物請求</a></td>
      <td>
        <li><a href="../../classes/medication.md">藥物</a></li>
        <li><a href="../../classes/individual-profile.md">XDM 個人輪廓</a></li>
        <li><a href="../../classes/provider.md">提供者</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="5"><strong>增強型提供者經驗</strong>：使用EMR系統的提供者資料，根據預約可用性、地點和專業來建議替代提供者。 <br> <br>改善提供者搜尋，以顯示具有所需可用性的結果，驗證選取的提供者是否為付款者網路的一部分，並提供成本預估。
      </td>
      <td><a href="./field-groups/patient.md">患者</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM 個人輪廓</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/location.md">位置</a></td>
      <td>
        <li><a href="./classes/location.md">位置</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/organization.md">組織</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM 個人輪廓</a></li>
        <li><a href="../../classes/provider.md">提供者</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/practioner.md">實踐者</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM 個人輪廓</a></li>
        <li><a href="../../classes/provider.md">提供者</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/schedule.md">排程</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM 個人輪廓</a></li>
        <li><a href="../../classes/provider.md">提供者</a></li>
      </td>
    </tr>
  </tbody>
</table>

## 資料類型 {#data-types}

下表概述根據[!DNL HL7 FHIR Release 5]規格建立的資料型別。

| 名稱 | 說明 |
| --- | --- |
| [[!UICONTROL 位址]](./data-types/address.md) | 說明使用郵遞區號慣例（而非GPS或其他位置定義格式）表示的地址。 |
| [[!UICONTROL 註解]](./data-types/annotation.md) | 歸因於作者的文位元組點。 |
| [[!UICONTROL 可用性]](./data-types/availability.md) | 專案的可用性資料。 |
| [[!UICONTROL 可程式碼概念]](./data-types/codeable-concept.md) | 從一種資源到另一種資源的參考。 |
| [[!UICONTROL 可程式碼參考]](./data-types/codeable-reference.md) | 對資源或概念的參照。 |
| [[!UICONTROL 編碼]](./data-types/coding.md) | 術語系統定義的程式碼參考。 |
| [[!UICONTROL 聯絡視窗]](./data-types/contact-point.md) | 個人的聯絡詳細資訊。 |
| [[!UICONTROL 劑量]](./data-types/dosage.md) | 用藥方式或應如何服用。 |
| [[!UICONTROL 持續時間]](./data-types/duration.md) | 時間長度。 |
| [[!UICONTROL 延伸連絡人詳細資料]](./data-types/extended-contact-detail.md) | 延伸連絡人的資訊。 |
| [[!UICONTROL 人名]](./data-types/human-name.md) | 有關人類或其他生命實體名稱的資訊。 |
| [[!UICONTROL 識別碼]](./data-types/identifier.md) | 用於計算的識別碼。 |
| [[!UICONTROL 金額]](./data-types/money.md) | 以某些公認的貨幣表示的經濟公用程式金額。 |
| [[!UICONTROL 週期]](./data-types/period.md) | 由開始和結束日期/時間定義的時間期間。 |
| [[!UICONTROL 人員]](./data-types/person.md) | 有關一般人員記錄的資訊。 |
| [[!UICONTROL 數量]](./data-types/quantity.md) | 測量或可測量的金額。 |
| [[!UICONTROL Range]](./data-types/range.md) | 由低值和高值繫結的一組值。 |
| [[!UICONTROL 比例]](./data-types/ratio.md) | 透過分子和分母的兩個[[!UICONTROL 數量]](./data-types/quantity.md)值的比例。 |
| [[!UICONTROL 參考]](./data-types/reference.md) | 從一種資源到另一種資源的參考。 |
| [[!UICONTROL 重複]](./data-types/repeat.md) | 說明事件排程時間的一組規則。 |
| [[!UICONTROL 簡單數量]](./data-types/simple-quantity.md) | 測量或可測量的金額。 |
| [[!UICONTROL 計時]](./data-types/timing.md) | 關於可能發生多次之事件的資訊。 |
| [[!UICONTROL 虛擬服務詳細資料]](./data-types/virtual-service-detail.md) | 虛擬服務連絡人詳細資料。 |
