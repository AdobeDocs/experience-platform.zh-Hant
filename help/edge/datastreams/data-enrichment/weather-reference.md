---
title: 天氣資料欄位映射
description: 可用天氣資料欄位的參考頁，這些欄位是與天氣通道整合的一部分。
exl-id: bc0f158b-f9d0-424a-aa21-953e8380473f
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '12238'
ht-degree: 0%

---

# 天氣資料欄位映射

Adobe與 [!DNL [The Weather Company]](https://www.ibm.com/weather) 把美國天氣的附加背景帶到通過資料流收集的資料中。 您可以使用此資料進行分析、定位和在Experience Platform中建立段。

此頁列出了可用於豐富受眾資料的所有可用欄位。

欄位被分成三個不同的組，這些組與欄位組對齊。

* [**[!UICONTROL 當前天氣]**](#current-weather):根據用戶的位置確定用戶的當前天氣狀況。 這包括當前溫度、枕木、雲覆蓋等。
* [**[!UICONTROL 預測天氣]**](#forecast):預測包括用戶地點的1、2、3、5、7和10天預測。
* [**[!UICONTROL 觸發器]**](#triggers):觸發器是映射到不同語義天氣條件的特定組合。 有三種不同類型的天氣觸發器：

   * **[!UICONTROL 相對觸發器]**:在語義上有意義的條件，例如寒冷或雨天。 不同氣候的定義可能不同。
   * **[!UICONTROL 產品觸發器]**:導致購買不同類型產品的條件。 例如：寒冷的天氣預報可能意味著購買雨衣的可能性更大。
   * **[!UICONTROL 惡劣天氣觸發]**:嚴重的天氣警告，比如冬季風暴或颶風警告。

## 當前天氣 {#current-weather}

根據用戶的位置確定用戶的當前天氣狀況。

| 欄位 | 說明 | XDM路徑 |
| --- | ---- | --- |
| [!UICONTROL 溫度露點攝氏度] | 空氣在恆壓下必須冷卻到飽和的溫度。 露點也是空氣濕度的間接測量。 露點永遠不會超過溫度。 當Dewpoint和Temperature相等時，通常會形成雲或霧。 溫度和露點值越接近，相對濕度越大。 範圍 —80到100(°F)或–62到37(°C)。 溫度（攝氏度） | `weather.current.temperatureDewPoint.celsius` |
| [!UICONTROL 溫度露點華氏] | 空氣在恆壓下必須冷卻到飽和的溫度。 露點也是空氣濕度的間接測量。 露點永遠不會超過溫度。 當Dewpoint和Temperature相等時，通常會形成雲或霧。 溫度和露點值越接近，相對濕度越大。 範圍 —80到100(°F)或–62到37(°C)。 溫度（華氏度） | `weather.current.temperatureDewPoint.fahrenheit` |
| [!UICONTROL 降水最後一小時英吋] | 滾時液體沈澱量。 所呈列的金額是經過請求時間（現在）的滾動時間。 以英吋為單位的降水 | `weather.current.precip1Hour.inches` |
| [!UICONTROL 降水最後一小時毫米] | 滾時液體沈澱量。 所呈列的金額是經過請求時間（現在）的滾動時間。 以毫米計的降水 | `weather.current.precip1Hour.millimeters` |
| [!DNL Precipitation Last 24 Hours Inches] | 滾動二十四小時液體沈澱量。 所呈列的金額是經過請求時間（現在）的滾動時間。 以英吋為單位的降水 | `weather.current.precip24Hour.inches` |
| [!UICONTROL 最近24小時降水毫米] | 滾動二十四小時液體沈澱量。 所呈列的金額是經過請求時間（現在）的滾動時間。 以毫米計的降水 | `weather.current.precip24Hour.millimeters` |
| [!UICONTROL 降水持續6小時] | 滾動六小時液體沈澱量。 所呈列的金額是經過請求時間（現在）的滾動時間。 以英吋為單位的降水 | `weather.current.precip6Hour.inches` |
| [!UICONTROL 降水持續6小時毫米] | 滾動六小時液體沈澱量。 所呈列的金額是經過請求時間（現在）的滾動時間。 以毫米計的降水 | `weather.current.precip6Hour.millimeters` |
| [!UICONTROL 壓力變化] | 在密利巴，過去三小時的壓力變化。 | `weather.current.pressureChange` |
| [!UICONTROL 壓力平均海平面] | 平均海平面壓力為毫巴。  換句話說，海平面的平均氣壓。<br>範圍 — 毫巴精確到1/10 th mb。 | `weather.current.pressureMeanSeaLevel` |
| [!UICONTROL 相對濕度] | 空氣的相對濕度，該相對濕度定義為空氣中水蒸氣量與在恆定溫度下使空氣達到飽和所需的蒸氣量之比。 相對濕度始終以百分比表示。<br>範圍 — 0到100。 | `weather.current.relativeHumidity` |
| [!UICONTROL 雪最後一小時公分] | 一小時的降雪量。  所呈列的金額是經過請求時間（現在）的滾動時間。 降雪量公分 | `weather.current.snow1Hour.centimeters` |
| [!UICONTROL 雪最後一小時英吋] | 一小時的降雪量。  所呈列的金額是經過請求時間（現在）的滾動時間。 降雪（英吋） | `weather.current.snow1Hour.inches` |
| [!UICONTROL 雪24小時公分] | 二十四小時的降雪量。  所呈列的金額是經過請求時間（現在）的滾動時間。 降雪量公分 | `weather.current.snow24Hour.centimeters` |
| 雪24小時英吋 | 二十四小時的降雪量。  所呈列的金額是經過請求時間（現在）的滾動時間。 降雪（英吋） | `weather.current.snow24Hour.inches` |
| [!UICONTROL 雪最近6小時公分] | 一小時的降雪量。  所呈列的金額是經過請求時間（現在）的滾動時間。 降雪量公分 | `weather.current.snow6Hour.centimeters` |
| [!UICONTROL 最近6小時的雪] | 一小時的降雪量。  所呈列的金額是經過請求時間（現在）的滾動時間。 降雪（英吋） | `weather.current.snow6Hour.inches` |
| [!UICONTROL 日落時間] | 日落時間(UTC)。 | `weather.current.sunsetTime` |
| [!UICONTROL 溫度攝氏度] | 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（攝氏度） | `weather.current.temperature.celsius` |
| [!UICONTROL 華氏溫度] | 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（華氏度） | `weather.current.temperature.fahrenheit` |
| [!UICONTROL 溫度變化24小時攝氏度] | 與24小時前的報告相比，氣溫的變化。 溫度（攝氏度） | `weather.current.temperatureChange24Hour.celsius` |
| [!UICONTROL 溫度變化24小時華氏] | 與24小時前的報告相比，氣溫的變化。 溫度（華氏度） | `weather.current.temperatureChange24Hour.fahrenheit` |
| [!UICONTROL 溫度感覺像攝氏] | 一個明顯的溫度。 它代表了風寒或熱指數共同作用對暴露在外的人皮膚&quot;感覺&quot;到的空氣溫度。<br>當溫度為65°F或更高時，Feell Like值表示計算的熱指數。  當溫度低於65°F時，Feell Like值表示計算的風寒。<br>範圍–140到140。 溫度（攝氏度） | `weather.current.temperatureFeelsLike.celsius` |
| [!UICONTROL 溫度感覺像華氏] | 一個明顯的溫度。 它代表了風寒或熱指數共同作用對暴露在外的人皮膚&quot;感覺&quot;到的空氣溫度。<br>當溫度為65°F或更高時，Feell Like值表示計算的熱指數。  當溫度低於65°F時，Feell Like值表示計算的風寒。<br>範圍–140到140。 溫度（華氏度） | `weather.current.temperatureFeelsLike.fahrenheit` |
| [!UICONTROL 自7 AM攝氏度以來的最大溫度] | 自上午7點以來的最高溫度。本地時間。 溫度（攝氏度） | `weather.current.temperatureMaxSince7Am.celsius` |
| [!UICONTROL 自華氏7 AM以來的最高溫度] | 自上午7點以來的最高溫度。本地時間。 溫度（華氏度） | `weather.current.temperatureMaxSince7Am.fahrenheit` |
| [!UICONTROL 最後24小時最低溫度] | 過去24小時的最低氣溫。  24小時時段參考請求時間（現在）。  溫度（攝氏度） | `weather.current.temperatureMin24Hour.celsius` |
| [!UICONTROL 最後24小時華氏溫度] | 過去24小時的最低氣溫。  24小時時段參考請求時間（現在）。  溫度（華氏度） | `weather.current.temperatureMin24Hour.fahrenheit` |
| [!UICONTROL 風向] | 風從磁風方向吹出以度表示。 磁方向在0~359°之間變化，0°表示北、東90°、南180°、西270°等。<br>範圍 — 0&lt;=wind_dire_deg&lt;=350，以10度間隔。 | `weather.current.windDirection` |
| [!UICONTROL 每小時陣風公里] | 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 該報告始終顯示觀測期間記錄的最大陣風速度。 如果顯示「Wind Speed（風速）」，則它是必需的顯示欄位。 陣風速度可以以英里/小時或公里/小時表示。 風速（以公里/小時計） | `weather.current.windGust.kilometersPerHour` |
| [!UICONTROL 陣風時速] | 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 該報告始終顯示觀測期間記錄的最大陣風速度。 如果顯示「Wind Speed（風速）」，則它是必需的顯示欄位。 陣風速度可以以英里/小時或公里/小時表示。 風速（以英里/小時計） | `weather.current.windGust.`英里/小時 |
| [!UICONTROL 每小時風速公里] | 風被當作向量；因此，風必須具有方向和大小（速度）。 在當前條件下報告的風資訊相當於一個10分鐘的平均值，叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以公里/小時計） | `weather.current.windSpeed.kilometersPerHour` |
| [!UICONTROL 風速英里/小時] | 風被當作向量；因此，風必須具有方向和大小（速度）。 在當前條件下報告的風資訊相當於一個10分鐘的平均值，叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以英里/小時計） | `weather.current.windSpeed.milesPerHour` |

## 預測天氣 {#forecast}

根據特定時間點的位置為用戶預測的天氣。

| 欄位 | 說明 | XDM路徑 |
| --- | ---- | --- |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Celsius] | 一天的天氣預報。 指定日的午夜到午夜的每日最高溫度。 溫度（攝氏度） | `weather.forecast.day01Forecast.calendarDayTemperatureMax.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Fahrenheit] | 一天的天氣預報。 指定日的午夜到午夜的每日最高溫度。 溫度（華氏度） | `weather.forecast.day01Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Celsius] | 一天的天氣預報。 指定日的午夜至午夜的每日最低溫度。 溫度（攝氏度） | `weather.forecast.day01Forecast.calendarDayTemperatureMin.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Fahrenheit] | 一天的天氣預報。 指定日的午夜至午夜的每日最低溫度。 溫度（華氏度） | `weather.forecast.day01Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!DNL Day 1 Forecast Day Cloud Cover Miles] | 一天的天氣預報。 白天的天氣資訊。 白天平均雲覆蓋率以百分比表示。 以英里為單位。 | `weather.forecast.day01Forecast.day.cloudCover.inches` |
| [!DNL Day 1 Forecast Day Cloud Cover Kilometers] | 一天的天氣預報。 白天的天氣資訊。 白天平均雲覆蓋率以百分比表示。 距離（以公里計）。 | `weather.forecast.day01Forecast.day.cloudCover.kilometers` |
| [!DNL Day 1 Forecast Day Precipitation Chance] | 一天的天氣預報。 白天的天氣資訊。 降水（百分比）的可能性。 | `weather.forecast.day01Forecast.day.precipChance` |
| [!DNL Day 1 Forecast Day Precipitation Type] | 一天的天氣預報。 白天的天氣資訊。 降水的形式（雨，雪，雨夾雪等）。 | `weather.forecast.day01Forecast.day.precipType` |
| [!DNL Day 1 Forecast Day QPF Inches] | 一天的天氣預報。 白天的天氣資訊。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以英吋為單位的降水 | `weather.forecast.day01Forecast.day.qpf.inches` |
| [!DNL Day 1 Forecast Day QPF Millimeters] | 一天的天氣預報。 白天的天氣資訊。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以毫米計的降水 | `weather.forecast.day01Forecast.day.qpf.millimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Centimeters] | 一天的天氣預報。 白天的天氣資訊。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪量公分 | `weather.forecast.day01Forecast.day.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Inches] | 一天的天氣預報。 白天的天氣資訊。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪（英吋） | `weather.forecast.day01Forecast.day.qpfSnow.inches` |
| [!DNL Day 1 Forecast Day Relative Humidity] | 一天的天氣預報。 白天的天氣資訊。 空氣的相對濕度，該相對濕度定義為空氣中水蒸氣量與在恆定溫度下使空氣達到飽和所需的蒸氣量之比。 相對濕度始終以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day01Forecast.day.relativeHumidity` |
| [!DNL Day 1 Forecast Day Snow Range] | 一天的天氣預報。 白天的天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day01Forecast.day.snowRange` |
| [!DNL Day 1 Forecast Day Temperature Celsius] | 一天的天氣預報。 白天的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（攝氏度） | `weather.forecast.day01Forecast.day.temperature.celsius` |
| [!DNL Day 1 Forecast Day Temperature Fahrenheit] | 一天的天氣預報。 白天的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（華氏度） | `weather.forecast.day01Forecast.day.temperature.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Celsius] | 一天的天氣預報。 白天的天氣資訊。 溫度，就是根據溫度和濕度，對暴露的人感覺的溫度。 溫度（攝氏度） | `weather.forecast.day01Forecast.day.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Fahrenheit] | 一天的天氣預報。 白天的天氣資訊。 溫度，就是根據溫度和濕度，對暴露的人感覺的溫度。 溫度（華氏度） | `weather.forecast.day01Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Celsius] | 一天的天氣預報。 白天的天氣資訊。 溫度，因為它會感受到根據溫度和風速暴露的人。 溫度（攝氏度） | `weather.forecast.day01Forecast.day.temperatureWindChill.celsius` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Fahrenheit] | 一天的天氣預報。 白天的天氣資訊。 溫度，因為它會感受到根據溫度和風速暴露的人。 溫度（華氏度） | `weather.forecast.day01Forecast.day.temperatureWindChill.fahrenheit` |
| [!DNL Day 1 Forecast Day Thunder Index] | 一天的天氣預報。 白天的天氣資訊。 雷暴影響區域的概率指數。 0(無雷擊至5（嚴重雷雨的高風險）。 | `weather.forecast.day01Forecast.day.thunderIndex` |
| [!DNL Day 1 Forecast Day UV Index] | 一天的天氣預報。 白天的天氣資訊。 12小時預測時段的最大UV索引。 | `weather.forecast.day01Forecast.day.uvIndex` |
| [!DNL Day 1 Forecast Day Wind Direction] | 一天的天氣預報。 白天的天氣資訊。 風從磁風方向吹出以度表示。 磁方向在0~359°之間變化，0°表示北、東90°、南180°、西270°等。<br>範圍 — 0&lt;=wind_dire_deg&lt;=350，以10度間隔。 | `weather.forecast.day01Forecast.day.windDirection` |
| [!DNL Day 1 Forecast Day Wind Gust Kilometers per Hour] | 一天的天氣預報。 白天的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 該報告始終顯示觀測期間記錄的最大陣風速度。 如果顯示「Wind Speed（風速）」，則它是必需的顯示欄位。 陣風速度可以以英里/小時或公里/小時表示。 風速（以公里/小時計） | `weather.forecast.day01Forecast.day.windGust.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Gust Miles per Hour] | 一天的天氣預報。 白天的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 該報告始終顯示觀測期間記錄的最大陣風速度。 如果顯示「Wind Speed（風速）」，則它是必需的顯示欄位。 陣風速度可以以英里/小時或公里/小時表示。 風速（以英里/小時計） | `weather.forecast.day01Forecast.day.windGust.milesPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Kilometers per Hour] | 一天的天氣預報。 白天的天氣資訊。 風被當作向量；因此，風必須具有方向和大小（速度）。 在當前條件下報告的風資訊相當於一個10分鐘的平均值，叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以公里/小時計） | `weather.forecast.day01Forecast.day.windSpeed.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Miles per Hour] | 一天的天氣預報。 白天的天氣資訊。 風被當作向量；因此，風必須具有方向和大小（速度）。 在當前條件下報告的風資訊相當於一個10分鐘的平均值，叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以英里/小時計） | `weather.forecast.day01Forecast.day.windSpeed.milesPerHour ` |
| [!DNL Day 1 Forecast Night Cloud Cover Miles] | 一天的天氣預報。 夜間天氣資訊。 白天平均雲覆蓋率以百分比表示。 以英里為單位。 | `weather.forecast.day01Forecast.night.cloudCover.inches` |
| [!DNL Day 1 Forecast Night Cloud Cover Kilometers] | 一天的天氣預報。 夜間天氣資訊。 白天平均雲覆蓋率以百分比表示。 距離（以公里計）。 | `weather.forecast.day01Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第1天預報夜間降水機會] | 一天的天氣預報。 夜間天氣資訊。 降水（百分比）的可能性。 | `weather.forecast.day01Forecast.night.precipChance` |
| [!DNL Day 1 Forecast Night Precipitation Type] | 一天的天氣預報。 夜間天氣資訊。 降水的形式（雨，雪，雨夾雪等）。 | `weather.forecast.day01Forecast.night.precipType` |
| [!DNL Day 1 Forecast Night QPF Inches] | 一天的天氣預報。 夜間天氣資訊。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以英吋為單位的降水 | `weather.forecast.day01Forecast.night.qpf.inches` |
| [!DNL Day 1 Forecast Night QPF Millimeters] | 一天的天氣預報。 夜間天氣資訊。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以毫米計的降水 | `weather.forecast.day01Forecast.night.qpf.millimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Centimeters] | 一天的天氣預報。 夜間天氣資訊。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪量公分 | `weather.forecast.day01Forecast.night.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Inches] | 一天的天氣預報。 夜間天氣資訊。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪（英吋） | `weather.forecast.day01Forecast.night.qpfSnow.inches` |
| [!DNL Day 1 Forecast Night Relative Humidity] | 一天的天氣預報。 夜間天氣資訊。 空氣的相對濕度，該相對濕度定義為空氣中水蒸氣量與在恆定溫度下使空氣達到飽和所需的蒸氣量之比。 相對濕度始終以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day01Forecast.night.relativeHumidity` |
| [!DNL Day 1 Forecast Night Snow Range] | 一天的天氣預報。 夜間天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day01Forecast.night.snowRange` |
| [!DNL Day 1 Forecast Night Temperature Celsius] | 一天的天氣預報。 夜間天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（攝氏度） | `weather.forecast.day01Forecast.night.temperature.celsius` |
| [!DNL Day 1 Forecast Night Temperature Fahrenheit] | 一天的天氣預報。 夜間天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（華氏度） | `weather.forecast.day01Forecast.night.temperature.fahrenheit` |
| [!DNL  Day 1 Forecast Night Temperature Heat Index Celsius] | 一天的天氣預報。 夜間天氣資訊。 溫度，就是根據溫度和濕度，對暴露的人感覺的溫度。 溫度（攝氏度） | `weather.forecast.day01Forecast.night.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Night Temperature Heat Index Fahrenheit] | 一天的天氣預報。 夜間天氣資訊。 溫度，就是根據溫度和濕度，對暴露的人感覺的溫度。 溫度（華氏度） | `weather.forecast.day01Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Night Temperature Wind Chill Celsius] | 一天的天氣預報。 夜間天氣資訊。 溫度，因為它會感受到根據溫度和風速暴露的人。 溫度（攝氏度） | `weather.forecast.day01Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第1天預測夜間溫度風寒華氏度] | 一天的天氣預報。 夜間天氣資訊。 溫度，因為它會感受到根據溫度和風速暴露的人。 溫度（華氏度） | `weather.forecast.day01Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第1天預測夜雷指數] | 一天的天氣預報。 夜間天氣資訊。 雷暴影響區域的概率指數。 0(無雷擊至5（嚴重雷雨的高風險）。 | `weather.forecast.day01Forecast.night.thunderIndex` |
| [!UICONTROL 第1天預測夜間UV指數] | 一天的天氣預報。 夜間天氣資訊。 12小時預測時段的最大UV索引。 | `weather.forecast.day01Forecast.night.uvIndex` |
| [!UICONTROL 第1天預測夜間風向] | 一天的天氣預報。 夜間天氣資訊。 風從磁風方向吹出以度表示。 磁方向在0~359°之間變化，0°表示北、東90°、南180°、西270°等。<br>範圍 — 0&lt;=wind_dire_deg&lt;=350，以10度間隔。 | `weather.forecast.day01Forecast.night.windDirection` |
| [!UICONTROL 第1天預報夜間陣風時速] | 一天的天氣預報。 夜間天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 該報告始終顯示觀測期間記錄的最大陣風速度。 如果顯示「Wind Speed（風速）」，則它是必需的顯示欄位。 陣風速度可以以英里/小時或公里/小時表示。 風速（以公里/小時計） | `weather.forecast.day01Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第1天預報夜間陣風時速] | 一天的天氣預報。 夜間天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 該報告始終顯示觀測期間記錄的最大陣風速度。 如果顯示「Wind Speed（風速）」，則它是必需的顯示欄位。 陣風速度可以以英里/小時或公里/小時表示。 風速（以英里/小時計） | `weather.forecast.day01Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第1天預報夜間風速公里/小時] | 一天的天氣預報。 夜間天氣資訊。 風被當作向量；因此，風必須具有方向和大小（速度）。 在當前條件下報告的風資訊相當於一個10分鐘的平均值，叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以公里/小時計） | `weather.forecast.day01Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第1天預測夜間風速英里/小時] | 一天的天氣預報。 夜間天氣資訊。 風被當作向量；因此，風必須具有方向和大小（速度）。 在當前條件下報告的風資訊相當於一個10分鐘的平均值，叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以英里/小時計） | `weather.forecast.day01Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第1天預測QPF英吋] | 一天的天氣預報。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以英吋為單位的降水 | `weather.forecast.day01Forecast.qpf.inches` |
| [!UICONTROL 第1天預測QPF毫米] | 一天的天氣預報。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以毫米計的降水 | `weather.forecast.day01Forecast.qpf.millimeters` |
| [!UICONTROL 第1天預測QPF雪公分] | 一天的天氣預報。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪量公分 | `weather.forecast.day01Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第1天預測QPF雪英吋] | 一天的天氣預報。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪（英吋） | `weather.forecast.day01Forecast.qpfSnow.inches` |
| [!UICONTROL 第2天預測日曆日溫度最大攝氏度] | 兩天的天氣預報。 指定日的午夜到午夜的每日最高溫度。 溫度（攝氏度） | `weather.forecast.day02Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第2天預測日曆日溫度最高華氏] | 兩天的天氣預報。 指定日的午夜到午夜的每日最高溫度。 溫度（華氏度） | `weather.forecast.day02Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第2天預測日曆日溫度最低攝氏度] | 兩天的天氣預報。 指定日的午夜至午夜的每日最低溫度。 溫度（攝氏度） | `weather.forecast.day02Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第2天預測日曆日溫度最小華氏] | 兩天的天氣預報。 指定日的午夜至午夜的每日最低溫度。 溫度（華氏度） | `weather.forecast.day02Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第2天預測日雲覆蓋英里] | 兩天的天氣預報。 白天的天氣資訊。 白天平均雲覆蓋率以百分比表示。 以英里為單位。 | `weather.forecast.day02Forecast.day.cloudCover.inches` |
| [!UICONTROL 第2天預測日雲覆蓋公里] | 兩天的天氣預報。 白天的天氣資訊。 白天平均雲覆蓋率以百分比表示。 距離（以公里計）。 | `weather.forecast.day02Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 第2天預報日降水機會] | 兩天的天氣預報。 白天的天氣資訊。 降水（百分比）的可能性。 | `weather.forecast.day02Forecast.day.precipChance` |
| [!UICONTROL 第2天預測日降水類型] | 兩天的天氣預報。 白天的天氣資訊。 降水的形式（雨，雪，雨夾雪等）。 | `weather.forecast.day02Forecast.day.precipType` |
| [!UICONTROL 第2天預測第QPF英吋] | 兩天的天氣預報。 白天的天氣資訊。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以英吋為單位的降水 | `weather.forecast.day02Forecast.day.qpf.inches` |
| [!UICONTROL 第2天預測第QPF毫米] | 兩天的天氣預報。 白天的天氣資訊。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以毫米計的降水 | `weather.forecast.day02Forecast.day.qpf.millimeters` |
| [!UICONTROL 第2天預測天QPF雪公分] | 兩天的天氣預報。 白天的天氣資訊。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪量公分 | `weather.forecast.day02Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 第2天預測第QPF雪英吋] | 兩天的天氣預報。 白天的天氣資訊。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪（英吋） | `weather.forecast.day02Forecast.day.qpfSnow.inches` |
| [!UICONTROL 第2天預測天相對濕度] | 兩天的天氣預報。 白天的天氣資訊。 空氣的相對濕度，該相對濕度定義為空氣中水蒸氣量與在恆定溫度下使空氣達到飽和所需的蒸氣量之比。 相對濕度始終以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day02Forecast.day.relativeHumidity` |
| [!UICONTROL 第2天預測天雪域] | 兩天的天氣預報。 白天的天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day02Forecast.day.snowRange` |
| [!UICONTROL 第2天預測天溫度攝氏度] | 兩天的天氣預報。 白天的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（攝氏度） | `weather.forecast.day02Forecast.day.temperature.celsius` |
| [!UICONTROL 第2天預測第2天溫度華氏] | 兩天的天氣預報。 白天的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（華氏度） | `weather.forecast.day02Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 第2天預測天溫度熱指數Celsius] | 兩天的天氣預報。 白天的天氣資訊。 溫度，就是根據溫度和濕度，對暴露的人感覺的溫度。 溫度（攝氏度） | `weather.forecast.day02Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 第2天預測第2天溫度熱指數華氏] | 兩天的天氣預報。 白天的天氣資訊。 溫度，就是根據溫度和濕度，對暴露的人感覺的溫度。 溫度（華氏度） | `weather.forecast.day02Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第2天預測天溫度風寒攝氏度] | 兩天的天氣預報。 白天的天氣資訊。 溫度，因為它會感受到根據溫度和風速暴露的人。 溫度（攝氏度） | `weather.forecast.day02Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 第2天預測天溫度風寒華氏度] | 兩天的天氣預報。 白天的天氣資訊。 溫度，因為它會感受到根據溫度和風速暴露的人。 溫度（華氏度） | `weather.forecast.day02Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第2天預測第2天雷電指數] | 兩天的天氣預報。 白天的天氣資訊。 雷暴影響區域的概率指數。 0(無雷擊至5（嚴重雷雨的高風險）。 | `weather.forecast.day02Forecast.day.thunderIndex` |
| [!UICONTROL 第2天預測日UV索引] | 兩天的天氣預報。 白天的天氣資訊。 12小時預測時段的最大UV索引。 | `weather.forecast.day02Forecast.day.uvIndex` |
| [!UICONTROL 第2天預測第2天風向] | 兩天的天氣預報。 白天的天氣資訊。 風從磁風方向吹出以度表示。 磁方向在0~359°之間變化，0°表示北、東90°、南180°、西270°等。<br>範圍 — 0&lt;=wind_dire_deg&lt;=350，以10度間隔。 | `weather.forecast.day02Forecast.day.windDirection` |
| [!UICONTROL 第2天預測第2天陣風公里/小時] | 兩天的天氣預報。 白天的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 該報告始終顯示觀測期間記錄的最大陣風速度。 如果顯示「Wind Speed（風速）」，則它是必需的顯示欄位。 陣風速度可以以英里/小時或公里/小時表示。 風速（以公里/小時計） | `weather.forecast.day02Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 第2天預測第2天陣風時速] | 兩天的天氣預報。 白天的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 該報告始終顯示觀測期間記錄的最大陣風速度。 如果顯示「Wind Speed（風速）」，則它是必需的顯示欄位。 陣風速度可以以英里/小時或公里/小時表示。 風速（以英里/小時計） | `weather.forecast.day02Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 第2天預測第2天每小時風速公里] | 兩天的天氣預報。 白天的天氣資訊。 風被當作向量；因此，風必須具有方向和大小（速度）。 在當前條件下報告的風資訊相當於一個10分鐘的平均值，叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以公里/小時計） | `weather.forecast.day02Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 第2天預測第一天風速英里/小時] | 兩天的天氣預報。 白天的天氣資訊。 風被當作向量；因此，風必須具有方向和大小（速度）。 在當前條件下報告的風資訊相當於一個10分鐘的平均值，叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以英里/小時計） | `weather.forecast.day02Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 第2天預報夜間雲覆蓋英里] | 兩天的天氣預報。 夜間天氣資訊。 白天平均雲覆蓋率以百分比表示。 以英里為單位。 | `weather.forecast.day02Forecast.night.cloudCover.inches` |
| [!UICONTROL 第2天預報夜雲覆蓋公里] | 兩天的天氣預報。 夜間天氣資訊。 白天平均雲覆蓋率以百分比表示。 距離（以公里計）。 | `weather.forecast.day02Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第2天預報夜間降水機會] | 兩天的天氣預報。 夜間天氣資訊。 降水（百分比）的可能性。 | `weather.forecast.day02Forecast.night.precipChance` |
| [!UICONTROL 第2天預報夜間降水類型] | 兩天的天氣預報。 夜間天氣資訊。 降水的形式（雨，雪，雨夾雪等）。 | `weather.forecast.day02Forecast.night.precipType` |
| [!UICONTROL 第2天預測之夜QPF英吋] | 兩天的天氣預報。 夜間天氣資訊。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以英吋為單位的降水 | `weather.forecast.day02Forecast.night.qpf.inches` |
| [!UICONTROL 第2天預測夜間QPF毫米] | 兩天的天氣預報。 夜間天氣資訊。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以毫米計的降水 | `weather.forecast.day02Forecast.night.qpf.millimeters` |
| [!UICONTROL 第2天預報夜QPF雪公分] | 兩天的天氣預報。 夜間天氣資訊。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪量公分 | `weather.forecast.day02Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 第2天預測之夜QPF雪英吋] | 兩天的天氣預報。 夜間天氣資訊。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪（英吋） | `weather.forecast.day02Forecast.night.qpfSnow.inches` |
| [!UICONTROL 第2天預測夜間相對濕度] | 兩天的天氣預報。 夜間天氣資訊。 空氣的相對濕度，該相對濕度定義為空氣中水蒸氣量與在恆定溫度下使空氣達到飽和所需的蒸氣量之比。 相對濕度始終以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day02Forecast.night.relativeHumidity` |
| [!UICONTROL 第2天預測夜間雪域] | 兩天的天氣預報。 夜間天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day02Forecast.night.snowRange` |
| [!UICONTROL 第2天預測夜間溫度攝氏度] | 兩天的天氣預報。 夜間天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（攝氏度） | `weather.forecast.day02Forecast.night.temperature.celsius` |
| [!UICONTROL 第2天預測夜間溫度華氏] | 兩天的天氣預報。 夜間天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（華氏度） | `weather.forecast.day02Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 第2天預測夜間溫度熱指數攝氏度] | 兩天的天氣預報。 夜間天氣資訊。 溫度，就是根據溫度和濕度，對暴露的人感覺的溫度。 溫度（攝氏度） | `weather.forecast.day02Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 第2天預測夜間溫度熱指數華氏] | 兩天的天氣預報。 夜間天氣資訊。 溫度，就是根據溫度和濕度，對暴露的人感覺的溫度。 溫度（華氏度） | `weather.forecast.day02Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第2天預測夜間溫度風寒攝氏度] | 兩天的天氣預報。 夜間天氣資訊。 溫度，因為它會感受到根據溫度和風速暴露的人。 溫度（攝氏度） | `weather.forecast.day02Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第2天預測夜間溫度風寒華氏度] | 兩天的天氣預報。 夜間天氣資訊。 溫度，因為它會感受到根據溫度和風速暴露的人。 溫度（華氏度） | `weather.forecast.day02Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第2天預測夜雷指數] | 兩天的天氣預報。 夜間天氣資訊。 雷暴影響區域的概率指數。 0(無雷擊至5（嚴重雷雨的高風險）。 | `weather.forecast.day02Forecast.night.thunderIndex` |
| [!UICONTROL 第2天預測夜間UV指數] | 兩天的天氣預報。 夜間天氣資訊。 12小時預測時段的最大UV索引。 | `weather.forecast.day02Forecast.night.uvIndex` |
| [!UICONTROL 第2天預測夜間風向] | 兩天的天氣預報。 夜間天氣資訊。 風從磁風方向吹出以度表示。 磁方向在0~359°之間變化，0°表示北、東90°、南180°、西270°等。<br>範圍 — 0&lt;=wind_dire_deg&lt;=350，以10度間隔。 | `weather.forecast.day02Forecast.night.windDirection` |
| [!UICONTROL 第2天預報夜間陣風時速] | 兩天的天氣預報。 夜間天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 該報告始終顯示觀測期間記錄的最大陣風速度。 如果顯示「Wind Speed（風速）」，則它是必需的顯示欄位。 陣風速度可以以英里/小時或公里/小時表示。 風速（以公里/小時計） | `weather.forecast.day02Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第2天預報夜間陣風時速] | 兩天的天氣預報。 夜間天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 該報告始終顯示觀測期間記錄的最大陣風速度。 如果顯示「Wind Speed（風速）」，則它是必需的顯示欄位。 陣風速度可以以英里/小時或公里/小時表示。 風速（以英里/小時計） | `weather.forecast.day02Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第2天預報夜間風速公里/小時] | 兩天的天氣預報。 夜間天氣資訊。 風被當作向量；因此，風必須具有方向和大小（速度）。 在當前條件下報告的風資訊相當於一個10分鐘的平均值，叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以公里/小時計） | `weather.forecast.day02Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第2天預測夜間風速英里/小時] | 兩天的天氣預報。 夜間天氣資訊。 風被當作向量；因此，風必須具有方向和大小（速度）。 在當前條件下報告的風資訊相當於一個10分鐘的平均值，叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以英里/小時計） | `weather.forecast.day02Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第2天預測QPF英吋] | 兩天的天氣預報。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以英吋為單位的降水 | `weather.forecast.day02Forecast.qpf.inches` |
| [!UICONTROL 第2天預測QPF毫米] | 兩天的天氣預報。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以毫米計的降水 | `weather.forecast.day02Forecast.qpf.millimeters` |
| [!UICONTROL 第2天預測QPF雪公分] | 兩天的天氣預報。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪量公分 | `weather.forecast.day02Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第2天預測QPF雪英吋] | 兩天的天氣預報。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪（英吋） | `weather.forecast.day02Forecast.qpfSnow.inches` |
| [!UICONTROL 第3天預測日曆日溫度最大攝氏度] | 天氣預報三天。 指定日的午夜到午夜的每日最高溫度。 溫度（攝氏度） | `weather.forecast.day03Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第3天預測日曆日溫度最高華氏] | 天氣預報三天。 指定日的午夜到午夜的每日最高溫度。 溫度（華氏度） | `weather.forecast.day03Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第3天預測日曆日溫度攝氏度] | 天氣預報三天。 指定日的午夜至午夜的每日最低溫度。 溫度（攝氏度） | `weather.forecast.day03Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第3天預測日曆日溫度最小華氏] | 天氣預報三天。 指定日的午夜至午夜的每日最低溫度。 溫度（華氏度） | `weather.forecast.day03Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第3天預測日雲覆蓋英里] | 天氣預報三天。 白天的天氣資訊。 白天平均雲覆蓋率以百分比表示。 以英里為單位。 | `weather.forecast.day03Forecast.day.cloudCover.inches` |
| [!UICONTROL 第3天預測日雲覆蓋公里] | 天氣預報三天。 白天的天氣資訊。 白天平均雲覆蓋率以百分比表示。 距離（以公里計）。 | `weather.forecast.day03Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 第3天預報日降水機會] | 天氣預報三天。 白天的天氣資訊。 降水（百分比）的可能性。 | `weather.forecast.day03Forecast.day.precipChance` |
| [!UICONTROL 第3天預測日降水類型] | 天氣預報三天。 白天的天氣資訊。 降水的形式（雨，雪，雨夾雪等）。 | `weather.forecast.day03Forecast.day.precipType` |
| [!UICONTROL 第3天預測第QPF英吋] | 天氣預報三天。 白天的天氣資訊。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以英吋為單位的降水 | `weather.forecast.day03Forecast.day.qpf.inches` |
| [!UICONTROL 第3天預測第QPF毫米] | 天氣預報三天。 白天的天氣資訊。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以毫米計的降水 | `weather.forecast.day03Forecast.day.qpf.millimeters` |
| [!UICONTROL 第3天預測天QPF雪公分] | 天氣預報三天。 白天的天氣資訊。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪量公分 | `weather.forecast.day03Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 第3天預測第QPF雪英吋] | 天氣預報三天。 白天的天氣資訊。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪（英吋） | `weather.forecast.day03Forecast.day.qpfSnow.inches` |
| [!UICONTROL 第3天預測天相對濕度] | 天氣預報三天。 白天的天氣資訊。 空氣的相對濕度，該相對濕度定義為空氣中水蒸氣量與在恆定溫度下使空氣達到飽和所需的蒸氣量之比。 相對濕度始終以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day03Forecast.day.relativeHumidity` |
| [!UICONTROL 第3天預測天雪域] | 天氣預報三天。 白天的天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day03Forecast.day.snowRange` |
| [!UICONTROL 第3天預測天溫度攝氏度] | 天氣預報三天。 白天的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（攝氏度） | `weather.forecast.day03Forecast.day.temperature.celsius` |
| [!UICONTROL 第3天預測天溫度華氏] | 天氣預報三天。 白天的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（華氏度） | `weather.forecast.day03Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 第3天預測天溫度熱指數Celsius] | 天氣預報三天。 白天的天氣資訊。 溫度，就是根據溫度和濕度，對暴露的人感覺的溫度。 溫度（攝氏度） | `weather.forecast.day03Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 第3天預測第3天溫度熱指數華氏] | 天氣預報三天。 白天的天氣資訊。 溫度，就是根據溫度和濕度，對暴露的人感覺的溫度。 溫度（華氏度） | `weather.forecast.day03Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第3天預測天溫度風寒攝氏度] | 天氣預報三天。 白天的天氣資訊。 溫度，因為它會感受到根據溫度和風速暴露的人。 溫度（攝氏度） | `weather.forecast.day03Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 第3天預測天溫度風寒華氏] | 天氣預報三天。 白天的天氣資訊。 溫度，因為它會感受到根據溫度和風速暴露的人。 溫度（華氏度） | `weather.forecast.day03Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第3天預測第2天雷電指數] | 天氣預報三天。 白天的天氣資訊。 雷暴影響區域的概率指數。 0(無雷擊至5（嚴重雷雨的高風險）。 | `weather.forecast.day03Forecast.day.thunderIndex` |
| [!UICONTROL 第3天預測第UV索引] | 天氣預報三天。 白天的天氣資訊。 12小時預測時段的最大UV索引。 | `weather.forecast.day03Forecast.day.uvIndex` |
| [!UICONTROL 第3天預測天風向] | 天氣預報三天。 白天的天氣資訊。 風從磁風方向吹出以度表示。 磁方向在0~359°之間變化，0°表示北、東90°、南180°、西270°等。<br>範圍 — 0&lt;=wind_dire_deg&lt;=350，以10度間隔。 | `weather.forecast.day03Forecast.day.windDirection` |
| [!UICONTROL 第3天預報天陣風公里/小時] | 天氣預報三天。 白天的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 該報告始終顯示觀測期間記錄的最大陣風速度。 如果顯示「Wind Speed（風速）」，則它是必需的顯示欄位。 陣風速度可以以英里/小時或公里/小時表示。 風速（以公里/小時計） | `weather.forecast.day03Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 第3天預測第3天陣風時速] | 天氣預報三天。 白天的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 該報告始終顯示觀測期間記錄的最大陣風速度。 如果顯示「Wind Speed（風速）」，則它是必需的顯示欄位。 陣風速度可以以英里/小時或公里/小時表示。 風速（以英里/小時計） | `weather.forecast.day03Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 第3天預測第3天每小時風速公里] | 天氣預報三天。 白天的天氣資訊。 風被當作向量；因此，風必須具有方向和大小（速度）。 在當前條件下報告的風資訊相當於一個10分鐘的平均值，叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以公里/小時計） | `weather.forecast.day03Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 第3天預測第一天風速英里/小時] | 天氣預報三天。 白天的天氣資訊。 風被當作向量；因此，風必須具有方向和大小（速度）。 在當前條件下報告的風資訊相當於一個10分鐘的平均值，叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以英里/小時計） | `weather.forecast.day03Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 第3天預報夜間雲覆蓋英里] | 天氣預報三天。 夜間天氣資訊。 白天平均雲覆蓋率以百分比表示。 以英里為單位。 | `weather.forecast.day03Forecast.night.cloudCover.inches` |
| [!UICONTROL 第3天預報夜雲覆蓋公里] | 天氣預報三天。 夜間天氣資訊。 白天平均雲覆蓋率以百分比表示。 距離（以公里計）。 | `weather.forecast.day03Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第3天預報夜間降水機會] | 天氣預報三天。 夜間天氣資訊。 降水（百分比）的可能性。 | `weather.forecast.day03Forecast.night.precipChance` |
| [!UICONTROL 第3天預報夜間降水類型] | 天氣預報三天。 夜間天氣資訊。 降水的形式（雨，雪，雨夾雪等）。 | `weather.forecast.day03Forecast.night.precipType` |
| [!UICONTROL 第3天預測之夜QPF英吋] | 天氣預報三天。 夜間天氣資訊。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以英吋為單位的降水 | `weather.forecast.day03Forecast.night.qpf.inches` |
| [!UICONTROL 第3天預測夜間QPF毫米] | 天氣預報三天。 夜間天氣資訊。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以毫米計的降水 | `weather.forecast.day03Forecast.night.qpf.millimeters` |
| [!UICONTROL 第3天預報夜QPF雪公分] | 天氣預報三天。 夜間天氣資訊。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪量公分 | `weather.forecast.day03Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 第3天預測之夜QPF雪英吋] | 天氣預報三天。 夜間天氣資訊。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪（英吋） | `weather.forecast.day03Forecast.night.qpfSnow.inches` |
| [!UICONTROL 第3天預測夜間相對濕度] | 天氣預報三天。 夜間天氣資訊。 空氣的相對濕度，該相對濕度定義為空氣中水蒸氣量與在恆定溫度下使空氣達到飽和所需的蒸氣量之比。 相對濕度始終以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day03Forecast.night.relativeHumidity` |
| [!UICONTROL 第3天預報夜間雪域] | 天氣預報三天。 夜間天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day03Forecast.night.snowRange` |
| [!UICONTROL 第3天預測夜間溫度攝氏度] | 天氣預報三天。 夜間天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（攝氏度） | `weather.forecast.day03Forecast.night.temperature.celsius` |
| [!UICONTROL 第3天預測夜間溫度華氏] | 天氣預報三天。 夜間天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（華氏度） | `weather.forecast.day03Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 第3天預測夜間溫度熱指數攝氏度] | 天氣預報三天。 夜間天氣資訊。 溫度，就是根據溫度和濕度，對暴露的人感覺的溫度。 溫度（攝氏度） | `weather.forecast.day03Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 第3天預測夜間溫度熱指數華氏] | 天氣預報三天。 夜間天氣資訊。 溫度，就是根據溫度和濕度，對暴露的人感覺的溫度。 溫度（華氏度） | `weather.forecast.day03Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第3天預測夜間溫度風寒攝氏度] | 天氣預報三天。 夜間天氣資訊。 溫度，因為它會感受到根據溫度和風速暴露的人。 溫度（攝氏度） | `weather.forecast.day03Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第3天預測夜間溫度風寒華氏度] | 天氣預報三天。 夜間天氣資訊。 溫度，因為它會感受到根據溫度和風速暴露的人。 溫度（華氏度） | `weather.forecast.day03Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第3天預測夜雷指數] | 天氣預報三天。 夜間天氣資訊。 雷暴影響區域的概率指數。 0(無雷擊至5（嚴重雷雨的高風險）。 | `weather.forecast.day03Forecast.night.thunderIndex` |
| [!UICONTROL 第3天預測夜間UV指數] | 天氣預報三天。 夜間天氣資訊。 12小時預測時段的最大UV索引。 | `weather.forecast.day03Forecast.night.uvIndex` |
| [!UICONTROL 第3天預測夜間風向] | 天氣預報三天。 夜間天氣資訊。 風從磁風方向吹出以度表示。 磁方向在0~359°之間變化，0°表示北、東90°、南180°、西270°等。<br>範圍 — 0&lt;=wind_dire_deg&lt;=350，以10度間隔。 | `weather.forecast.day03Forecast.night.windDirection` |
| [!UICONTROL 第3天預報夜間陣風時速] | 天氣預報三天。 夜間天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 該報告始終顯示觀測期間記錄的最大陣風速度。 如果顯示「Wind Speed（風速）」，則它是必需的顯示欄位。 陣風速度可以以英里/小時或公里/小時表示。 風速（以公里/小時計） | `weather.forecast.day03Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第3天預報夜間陣風時速] | 天氣預報三天。 夜間天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 該報告始終顯示觀測期間記錄的最大陣風速度。 如果顯示「Wind Speed（風速）」，則它是必需的顯示欄位。 陣風速度可以以英里/小時或公里/小時表示。 風速（以英里/小時計） | `weather.forecast.day03Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第3天預報夜間風速公里/小時] | 天氣預報三天。 夜間天氣資訊。 風被當作向量；因此，風必須具有方向和大小（速度）。 在當前條件下報告的風資訊相當於一個10分鐘的平均值，叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以公里/小時計） | `weather.forecast.day03Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第3天預測夜間風速英里/小時] | 天氣預報三天。 夜間天氣資訊。 風被當作向量；因此，風必須具有方向和大小（速度）。 在當前條件下報告的風資訊相當於一個10分鐘的平均值，叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以英里/小時計） | `weather.forecast.day03Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第3天預測QPF英吋] | 天氣預報三天。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以英吋為單位的降水 | `weather.forecast.day03Forecast.qpf.inches` |
| [!UICONTROL 第3天預測QPF毫米] | 天氣預報三天。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以毫米計的降水 | `weather.forecast.day03Forecast.qpf.millimeters` |
| [!UICONTROL 第3天預測QPF雪公分] | 天氣預報三天。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪量公分 | `weather.forecast.day03Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第3天預測QPF雪英吋] | 天氣預報三天。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪（英吋） | `weather.forecast.day03Forecast.qpfSnow.inches` |
| [!UICONTROL 第5天預測日曆日溫度最大攝氏度] | 五天天氣預報。 指定日的午夜到午夜的每日最高溫度。 溫度（攝氏度） | `weather.forecast.day05Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第5天預測日曆日溫度最高華氏] | 五天天氣預報。 指定日的午夜到午夜的每日最高溫度。 溫度（華氏度） | `weather.forecast.day05Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第5天預測日曆日溫度最低攝氏度] | 五天天氣預報。 指定日的午夜至午夜的每日最低溫度。 溫度（攝氏度） | `weather.forecast.day05Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第5天預測日曆日溫度最小華氏] | 五天天氣預報。 指定日的午夜至午夜的每日最低溫度。 溫度（華氏度） | `weather.forecast.day05Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第5天預測日雲覆蓋英里] | 五天天氣預報。 白天的天氣資訊。 白天平均雲覆蓋率以百分比表示。 以英里為單位。 | `weather.forecast.day05Forecast.day.cloudCover.inches` |
| [!UICONTROL 第5天預測日雲覆蓋公里] | 五天天氣預報。 白天的天氣資訊。 白天平均雲覆蓋率以百分比表示。 距離（以公里計）。 | `weather.forecast.day05Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 第5天預報日降水機會] | 五天天氣預報。 白天的天氣資訊。 降水（百分比）的可能性。 | `weather.forecast.day05Forecast.day.precipChance` |
| [!UICONTROL 第5天預測日降水類型] | 五天天氣預報。 白天的天氣資訊。 降水的形式（雨，雪，雨夾雪等）。 | `weather.forecast.day05Forecast.day.precipType` |
| [!UICONTROL 第5天預測第QPF英吋] | 五天天氣預報。 白天的天氣資訊。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以英吋為單位的降水 | `weather.forecast.day05Forecast.day.qpf.inches` |
| [!UICONTROL 第5天預測天QPF毫米] | 五天天氣預報。 白天的天氣資訊。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以毫米計的降水 | `weather.forecast.day05Forecast.day.qpf.millimeters` |
| [!UICONTROL 第5天預測天QPF雪公分] | 五天天氣預報。 白天的天氣資訊。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪量公分 | `weather.forecast.day05Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 第5天預測第QPF雪英吋] | 五天天氣預報。 白天的天氣資訊。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪（英吋） | `weather.forecast.day05Forecast.day.qpfSnow.inches` |
| [!UICONTROL 第5天預測日相對濕度] | 五天天氣預報。 白天的天氣資訊。 空氣的相對濕度，該相對濕度定義為空氣中水蒸氣量與在恆定溫度下使空氣達到飽和所需的蒸氣量之比。 相對濕度始終以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day05Forecast.day.relativeHumidity` |
| [!UICONTROL 第5天預測天雪域] | 五天天氣預報。 白天的天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day05Forecast.day.snowRange` |
| [!UICONTROL 第5天預測天溫度攝氏度] | 五天天氣預報。 白天的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（攝氏度） | `weather.forecast.day05Forecast.day.temperature.celsius` |
| [!UICONTROL 第5天預測天溫度華氏] | 五天天氣預報。 白天的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（華氏度） | `weather.forecast.day05Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 第5天預測天溫度熱指數Celsius] | 五天天氣預報。 白天的天氣資訊。 溫度，就是根據溫度和濕度，對暴露的人感覺的溫度。 溫度（攝氏度） | `weather.forecast.day05Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 第5天預測第5天溫度熱指數華氏] | 五天天氣預報。 白天的天氣資訊。 溫度，就是根據溫度和濕度，對暴露的人感覺的溫度。 溫度（華氏度） | `weather.forecast.day05Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第5天預測天溫度風寒攝氏度] | 五天天氣預報。 白天的天氣資訊。 溫度，因為它會感受到根據溫度和風速暴露的人。 溫度（攝氏度） | `weather.forecast.day05Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 第5天預測天溫度風寒華氏] | 五天天氣預報。 白天的天氣資訊。 溫度，因為它會感受到根據溫度和風速暴露的人。 溫度（華氏度） | `weather.forecast.day05Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第5天預測第天雷電指數] | 五天天氣預報。 白天的天氣資訊。 雷暴影響區域的概率指數。 0(無雷擊至5（嚴重雷雨的高風險）。 | `weather.forecast.day05Forecast.day.thunderIndex` |
| [!UICONTROL 第5天預測日UV索引] | 五天天氣預報。 白天的天氣資訊。 12小時預測時段的最大UV索引。 | `weather.forecast.day05Forecast.day.uvIndex` |
| [!UICONTROL 第5天預測天風向] | 五天天氣預報。 白天的天氣資訊。 風從磁風方向吹出以度表示。 磁方向在0~359°之間變化，0°表示北、東90°、南180°、西270°等。<br>範圍 — 0&lt;=wind_dire_deg&lt;=350，以10度間隔。 | `weather.forecast.day05Forecast.day.windDirection` |
| [!UICONTROL 第5天預報天陣風公里/小時] | 五天天氣預報。 白天的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 該報告始終顯示觀測期間記錄的最大陣風速度。 如果顯示「Wind Speed（風速）」，則它是必需的顯示欄位。 陣風速度可以以英里/小時或公里/小時表示。 風速（以公里/小時計） | `weather.forecast.day05Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 第5天預報天陣風時速] | 五天天氣預報。 白天的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 該報告始終顯示觀測期間記錄的最大陣風速度。 如果顯示「Wind Speed（風速）」，則它是必需的顯示欄位。 陣風速度可以以英里/小時或公里/小時表示。 風速（以英里/小時計） | `weather.forecast.day05Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 第5天預測天每小時風速公里] | 五天天氣預報。 白天的天氣資訊。 風被當作向量；因此，風必須具有方向和大小（速度）。 在當前條件下報告的風資訊相當於一個10分鐘的平均值，叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以公里/小時計） | `weather.forecast.day05Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 第5天預測天風速英里/小時] | 五天天氣預報。 白天的天氣資訊。 風被當作向量；因此，風必須具有方向和大小（速度）。 在當前條件下報告的風資訊相當於一個10分鐘的平均值，叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以英里/小時計） | `weather.forecast.day05Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 第5天預報夜間雲覆蓋英里] | 五天天氣預報。 夜間天氣資訊。 白天平均雲覆蓋率以百分比表示。 以英里為單位。 | `weather.forecast.day05Forecast.night.cloudCover.inches` |
| [!UICONTROL 第5天預報夜雲覆蓋公里] | 五天天氣預報。 夜間天氣資訊。 白天平均雲覆蓋率以百分比表示。 距離（以公里計）。 | `weather.forecast.day05Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第5天預報夜間降水機會] | 五天天氣預報。 夜間天氣資訊。 降水（百分比）的可能性。 | `weather.forecast.day05Forecast.night.precipChance` |
| [!UICONTROL 第5天預報夜間降水類型] | 五天天氣預報。 夜間天氣資訊。 降水的形式（雨，雪，雨夾雪等）。 | `weather.forecast.day05Forecast.night.precipType` |
| [!UICONTROL 第5天預測之夜QPF英吋] | 五天天氣預報。 夜間天氣資訊。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以英吋為單位的降水 | `weather.forecast.day05Forecast.night.qpf.inches` |
| [!UICONTROL 第5天預測夜QPF毫米] | 五天天氣預報。 夜間天氣資訊。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以毫米計的降水 | `weather.forecast.day05Forecast.night.qpf.millimeters` |
| [!UICONTROL 第5天預報夜QPF雪公分] | 五天天氣預報。 夜間天氣資訊。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪量公分 | `weather.forecast.day05Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 第5天預測之夜QPF雪英吋] | 五天天氣預報。 夜間天氣資訊。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪（英吋） | `weather.forecast.day05Forecast.night.qpfSnow.inches` |
| [!UICONTROL 第5天預測夜間相對濕度] | 五天天氣預報。 夜間天氣資訊。 空氣的相對濕度，該相對濕度定義為空氣中水蒸氣量與在恆定溫度下使空氣達到飽和所需的蒸氣量之比。 相對濕度始終以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day05Forecast.night.relativeHumidity` |
| [!UICONTROL 第5天預報夜間雪域] | 五天天氣預報。 夜間天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day05Forecast.night.snowRange` |
| [!UICONTROL 第5天預測夜間溫度攝氏度] | 五天天氣預報。 夜間天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（攝氏度） | `weather.forecast.day05Forecast.night.temperature.celsius` |
| [!UICONTROL 第5天預測夜間溫度華氏] | 五天天氣預報。 夜間天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（華氏度） | `weather.forecast.day05Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 第5天預測夜間溫度熱指數攝氏度] | 五天天氣預報。 夜間天氣資訊。 溫度，就是根據溫度和濕度，對暴露的人感覺的溫度。 溫度（攝氏度） | `weather.forecast.day05Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 第5天預測夜間溫度熱指數華氏] | 五天天氣預報。 夜間天氣資訊。 溫度，就是根據溫度和濕度，對暴露的人感覺的溫度。 溫度（華氏度） | `weather.forecast.day05Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第5天預測夜間溫度風寒攝氏度] | 五天天氣預報。 夜間天氣資訊。 溫度，因為它會感受到根據溫度和風速暴露的人。 溫度（攝氏度） | `weather.forecast.day05Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第5天預測夜間溫度風寒華氏] | 五天天氣預報。 夜間天氣資訊。 溫度，因為它會感受到根據溫度和風速暴露的人。 溫度（華氏度） | `weather.forecast.day05Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第5天預測夜雷指數] | 五天天氣預報。 夜間天氣資訊。 雷暴影響區域的概率指數。 0(無雷擊至5（嚴重雷雨的高風險）。 | `weather.forecast.day05Forecast.night.thunderIndex` |
| [!UICONTROL 第5天預測夜UV指數] | 五天天氣預報。 夜間天氣資訊。 12小時預測時段的最大UV索引。 | `weather.forecast.day05Forecast.night.uvIndex` |
| [!UICONTROL 第5天預報夜間風向] | 五天天氣預報。 夜間天氣資訊。 風從磁風方向吹出以度表示。 磁方向在0~359°之間變化，0°表示北、東90°、南180°、西270°等。<br>範圍 — 0&lt;=wind_dire_deg&lt;=350，以10度間隔。 | `weather.forecast.day05Forecast.night.windDirection` |
| [!UICONTROL 第5天預報夜間陣風時速] | 五天天氣預報。 夜間天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 該報告始終顯示觀測期間記錄的最大陣風速度。 如果顯示「Wind Speed（風速）」，則它是必需的顯示欄位。 陣風速度可以以英里/小時或公里/小時表示。 風速（以公里/小時計） | `weather.forecast.day05Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第5天預報夜間陣風時速] | 五天天氣預報。 夜間天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 該報告始終顯示觀測期間記錄的最大陣風速度。 如果顯示「Wind Speed（風速）」，則它是必需的顯示欄位。 陣風速度可以以英里/小時或公里/小時表示。 風速（以英里/小時計） | `weather.forecast.day05Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第5天預報夜間風速公里/小時] | 五天天氣預報。 夜間天氣資訊。 風被當作向量；因此，風必須具有方向和大小（速度）。 在當前條件下報告的風資訊相當於一個10分鐘的平均值，叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以公里/小時計） | `weather.forecast.day05Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第5天預測夜間風速英里/小時] | 五天天氣預報。 夜間天氣資訊。 風被當作向量；因此，風必須具有方向和大小（速度）。 在當前條件下報告的風資訊相當於一個10分鐘的平均值，叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以英里/小時計） | `weather.forecast.day05Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第5天預測QPF英吋] | 五天天氣預報。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以英吋為單位的降水 | `weather.forecast.day05Forecast.qpf.inches` |
| [!UICONTROL 第5天預測QPF毫米] | 五天天氣預報。 12或24小時期間的可測降水量（液體或液體當量）。 以毫米計。 以毫米計的降水 | `weather.forecast.day05Forecast.qpf.millimeters` |
| [!UICONTROL 第5天預測QPF雪公分] | 五天天氣預報。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪量公分 | `weather.forecast.day05Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第5天預測QPF雪英吋] | 五天天氣預報。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪（英吋） | `weather.forecast.day05Forecast.qpfSnow.inches` |
| [!UICONTROL 第7天預測日曆日溫度最大攝氏度] | 天氣預報七天。 指定日的午夜到午夜的每日最高溫度。 溫度（攝氏度） | `weather.forecast.day07Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第7天預測日曆日溫度最高華氏] | 天氣預報七天。 指定日的午夜到午夜的每日最高溫度。 溫度（華氏度） | `weather.forecast.day07Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第7天預測日曆日溫度攝氏度] | 天氣預報七天。 指定日的午夜至午夜的每日最低溫度。 溫度（攝氏度） | `weather.forecast.day07Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第7天預測日曆日溫度最小華氏] | 天氣預報七天。 指定日的午夜至午夜的每日最低溫度。 溫度（華氏度） | `weather.forecast.day07Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第7天預測雲覆蓋英里] | 天氣預報七天。 白天平均雲覆蓋率以百分比表示。 以英里為單位。 | `weather.forecast.day07Forecast.cloudCover.inches` |
| [!UICONTROL 第7天預測雲覆蓋公里] | 天氣預報七天。 白天平均雲覆蓋率以百分比表示。 距離（以公里計）。 | `weather.forecast.day07Forecast.cloudCover.kilometers` |
| [!UICONTROL 第7天預測QPF英吋] | 天氣預報七天。 24小時內的可測降水量（液體或液體當量）。 以英吋為單位的降水 | `weather.forecast.day07Forecast.qpf.inches` |
| [!UICONTROL 第7天預測QPF毫米] | 天氣預報七天。 24小時內的可測降水量（液體或液體當量）。 以毫米計的降水 | `weather.forecast.day07Forecast.qpf.millimeters` |
| [!UICONTROL 第7天預測QPF雪公分] | 天氣預報七天。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪量公分 | `weather.forecast.day07Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第7天預測QPF雪英吋] | 天氣預報七天。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪（英吋） | `weather.forecast.day07Forecast.qpfSnow.inches` |
| [!UICONTROL 第7天預測UV索引] | 天氣預報七天。 12小時預測時段的最大UV索引。 | `weather.forecast.day07Forecast.uvIndex` |
| [!UICONTROL 第7天預測風向] | 天氣預報七天。 平均風向磁譜法。 | `weather.forecast.day07Forecast.windDirection` |
| [!UICONTROL 第7天預測風速公里/小時] | 天氣預報七天。 在12小時預測期間最大持續風速的預測。<br>風被當作向量；因此，風必須具有方向和大小（速度）。 預測中報告的風資訊相當於一個10分鐘的平均值叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以公里/小時計） | `weather.forecast.day07Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 第7天預測風速英里/小時] | 天氣預報七天。 在12小時預測期間最大持續風速的預測。<br>風被當作向量；因此，風必須具有方向和大小（速度）。 預測中報告的風資訊相當於一個10分鐘的平均值叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以英里/小時計） | `weather.forecast.day07Forecast.windSpeed.milesPerHour` |
| [!UICONTROL 第10天預測日曆日溫度最大攝氏度] | 十天天氣預報。 指定日的午夜到午夜的每日最高溫度。 溫度（攝氏度） | `weather.forecast.day10Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第10天預測日曆日溫度最大華氏度] | 十天天氣預報。 指定日的午夜到午夜的每日最高溫度。 溫度（華氏度） | `weather.forecast.day10Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第10天預測日曆日溫度攝氏度] | 十天天氣預報。 指定日的午夜至午夜的每日最低溫度。 溫度（攝氏度） | `weather.forecast.day10Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第10天預測日曆日溫度最小華氏] | 十天天氣預報。 指定日的午夜至午夜的每日最低溫度。 溫度（華氏度） | `weather.forecast.day10Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第10天預測雲覆蓋英里] | 十天天氣預報。 白天平均雲覆蓋率以百分比表示。 以英里為單位。 | `weather.forecast.day10Forecast.cloudCover.inches` |
| [!UICONTROL 第10天預測雲覆蓋公里] | 十天天氣預報。 白天平均雲覆蓋率以百分比表示。 距離（以公里計）。 | `weather.forecast.day10Forecast.cloudCover.kilometers` |
| [!UICONTROL 第10天預測QPF英吋] | 十天天氣預報。 24小時內的可測降水量（液體或液體當量）。 以英吋為單位的降水 | `weather.forecast.day10Forecast.qpf.inches` |
| [!UICONTROL 第10天預測QPF毫米] | 十天天氣預報。 24小時內的可測降水量（液體或液體當量）。 以毫米計的降水 | `weather.forecast.day10Forecast.qpf.millimeters` |
| [!UICONTROL 第10天預測QPF雪公分] | 十天天氣預報。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪量公分 | `weather.forecast.day10Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第10天預測QPF雪英吋] | 十天天氣預報。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪（英吋） | `weather.forecast.day10Forecast.qpfSnow.inches` |
| [!UICONTROL 第10天預測UV索引] | 十天天氣預報。 12小時預測時段的最大UV索引。 | `weather.forecast.day10Forecast.uvIndex` |
| [!UICONTROL 第10天預測風向] | 十天天氣預報。 平均風向磁譜法。 | `weather.forecast.day10Forecast.windDirection` |
| [!UICONTROL 第10天預測風速公里/小時] | 十天天氣預報。 在12小時預測期間最大持續風速的預測。<br>風被當作向量；因此，風必須具有方向和大小（速度）。 預測中報告的風資訊相當於一個10分鐘的平均值叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以公里/小時計） | `weather.forecast.day10Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 第10天預測風速英里/小時] | 十天天氣預報。 在12小時預測期間最大持續風速的預測。<br>風被當作向量；因此，風必須具有方向和大小（速度）。 預測中報告的風資訊相當於一個10分鐘的平均值叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以英里/小時計） | `weather.forecast.day10Forecast.windSpeed.milesPerHour` |
| [!UICONTROL 第14天預測日曆日溫度最高攝氏度] | 14天天氣預報。 指定日的午夜到午夜的每日最高溫度。 溫度（攝氏度） | `weather.forecast.day14Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第14天預測日曆日溫度最大華氏度] | 14天天氣預報。 指定日的午夜到午夜的每日最高溫度。 溫度（華氏度） | `weather.forecast.day14Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第14天預測日曆日溫度最低攝氏度] | 14天天氣預報。 指定日的午夜至午夜的每日最低溫度。 溫度（攝氏度） | `weather.forecast.day14Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第14天預測日曆日溫度最小華氏] | 14天天氣預報。 指定日的午夜至午夜的每日最低溫度。 溫度（華氏度） | `weather.forecast.day14Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第14天預測雲覆蓋英里] | 14天天氣預報。 白天平均雲覆蓋率以百分比表示。 以英里為單位。 | `weather.forecast.day14Forecast.cloudCover.inches` |
| [!UICONTROL 第14天預測雲覆蓋公里] | 14天天氣預報。 白天平均雲覆蓋率以百分比表示。 距離（以公里計）。 | `weather.forecast.day14Forecast.cloudCover.kilometers` |
| 第14天預測QPF英吋 | 14天天氣預報。 24小時內的可測降水量（液體或液體當量）。 以英吋為單位的降水 | `weather.forecast.day14Forecast.qpf.inches` |
| [!UICONTROL 第14天預測QPF毫米] | 14天天氣預報。 24小時內的可測降水量（液體或液體當量）。 以毫米計的降水 | `weather.forecast.day14Forecast.qpf.millimeters` |
| [!UICONTROL 第14天預測QPF雪公分] | 14天天氣預報。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪量公分 | `weather.forecast.day14Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第14天預測QPF雪英吋] | 14天天氣預報。 預測的12小時或24小時預報期的可測降水量為雪。 以公分計。 降雪（英吋） | `weather.forecast.day14Forecast.qpfSnow.inches` |
| [!UICONTROL 第14天預測UV索引] | 14天天氣預報。 12小時預測時段的最大UV索引。 | `weather.forecast.day14Forecast.uvIndex` |
| 第14天預測風向 | 14天天氣預報。 平均風向磁譜法。 | `weather.forecast.day14Forecast.windDirection` |
| [!UICONTROL 第14天預測風速公里/小時] | 14天天氣預報。 在12小時預測期間最大持續風速的預測。<br>風被當作向量；因此，風必須具有方向和大小（速度）。 預測中報告的風資訊相當於一個10分鐘的平均值叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以公里/小時計） | `weather.forecast.day14Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 第14天預測風速英里/小時] | 14天天氣預報。 在12小時預測期間最大持續風速的預測。<br>風被當作向量；因此，風必須具有方向和大小（速度）。 預測中報告的風資訊相當於一個10分鐘的平均值叫做持續風速。 風速的突然或短暫變化被稱為「風刮」，並在單獨的資料場中報告。 風向總是表示為&quot;風從何而來&quot;，即北風由北向南吹。 如果你在北風中面對北風，風就會吹向你的臉。 朝南面，北風在你後面。 風速（以英里/小時計） | `weather.forecast.day14Forecast.windSpeed.milesPerHour` |

## 觸發器 {#triggers}

觸發器根據各種輸入定義語義天氣條件。

| 欄位 | 說明 | XDM路徑 |
| --- | ---- | --- |
| [!UICONTROL 產品觸發器] | 指示條件何時適合推動某些類別產品的銷售。  它們被映射到整數度。 可從IBM獲得完整清單。 | `weather.productTriggers` |
| [!UICONTROL 相對觸發器] | 相對條件基於人類感知。 像《熱或冷》 它們被映射到整數度。 可從IBM獲得完整清單。 | `weather.relativeTriggers` |
| [!UICONTROL 惡劣天氣觸發] | 表明颶風或過度降雨等各種惡劣天氣狀況。 | `weather.severeTriggers` |
