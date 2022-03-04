<h1 align="center"> Weather </h1>

<p align="center"> 基于 <a href="https://lbs.amap.com/">高德开放平台</a> 的 PHP 天气信息组件。</p>


## 安装

```shell
$ composer require drizzle/weather -vvv
```

## 配置
在使用本扩展之前，你需要去 <a href="https://lbs.amap.com/">高德开放平台</a> 注册账号，然后创建应用，获取应用的 API Key。

## 使用

```php
use Drizzle\Weather\Weather;

$key = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx';

$weather = new Weather($key);
```
### 获取实时天气
```php
$response = $weather->getLiveWeather('深圳');
```
### 示例
```
{
    "status": "1",
    "count": "1",
    "info": "OK",
    "infocode": "10000",
    "lives": [
        {
            "province": "广东",
            "city": "深圳市",
            "adcode": "440300",
            "weather": "中雨",
            "temperature": "27",
            "winddirection": "西南",
            "windpower": "5",
            "humidity": "94",
            "reporttime": "2018-08-21 16:00:00"
        }
    ]
}
```
### 获取近期天气预报
```php
$response = $weather->getForecastsWeather('深圳', 'all');
```
### 实例
```
{
    "status": "1", 
    "count": "1", 
    "info": "OK", 
    "infocode": "10000", 
    "forecasts": [
        {
            "city": "深圳市", 
            "adcode": "440300", 
            "province": "广东", 
            "reporttime": "2018-08-21 11:00:00", 
            "casts": [
                {
                    "date": "2018-08-21", 
                    "week": "2", 
                    "dayweather": "雷阵雨", 
                    "nightweather": "雷阵雨", 
                    "daytemp": "31", 
                    "nighttemp": "26", 
                    "daywind": "无风向", 
                    "nightwind": "无风向", 
                    "daypower": "≤3", 
                    "nightpower": "≤3"
                }, 
                {
                    "date": "2018-08-22", 
                    "week": "3", 
                    "dayweather": "雷阵雨", 
                    "nightweather": "雷阵雨", 
                    "daytemp": "32", 
                    "nighttemp": "27", 
                    "daywind": "无风向", 
                    "nightwind": "无风向", 
                    "daypower": "≤3", 
                    "nightpower": "≤3"
                }, 
                {
                    "date": "2018-08-23", 
                    "week": "4", 
                    "dayweather": "雷阵雨", 
                    "nightweather": "雷阵雨", 
                    "daytemp": "32", 
                    "nighttemp": "26", 
                    "daywind": "无风向", 
                    "nightwind": "无风向", 
                    "daypower": "≤3", 
                    "nightpower": "≤3"
                }, 
                {
                    "date": "2018-08-24", 
                    "week": "5", 
                    "dayweather": "雷阵雨", 
                    "nightweather": "雷阵雨", 
                    "daytemp": "31", 
                    "nighttemp": "26", 
                    "daywind": "无风向", 
                    "nightwind": "无风向", 
                    "daypower": "≤3", 
                    "nightpower": "≤3"
                }
            ]
        }
    ]
}
```
### 获取 XML 格式返回值
> 第三个参数为返回值类型，可选 json 与 xml，默认 json：
```php
$response = $weather->getLiveWeather('深圳', 'all', 'xml');
```
### 实例
```
<response>
    <status>1</status>
    <count>1</count>
    <info>OK</info>
    <infocode>10000</infocode>
    <lives type="list">
        <live>
            <province>广东</province>
            <city>深圳市</city>
            <adcode>440300</adcode>
            <weather>中雨</weather>
            <temperature>27</temperature>
            <winddirection>西南</winddirection>
            <windpower>5</windpower>
            <humidity>94</humidity>
            <reporttime>2018-08-21 16:00:00</reporttime>
        </live>
    </lives>
</response>
```
### 参数说明
```
array|string getLiveWeather|getForecastsWeather(string $city, string $format = 'json')
```
## 在 Laravel 中使用
>在 `Laravel` 中使用也是同样的安装方式，配置写在 `config/services.php` 中：
```php
     'weather' => [
        'key' => env('WEATHER_API_KEY'),
    ]
```
>然后在 `.env` 中配置 `WEATHER_API_KEY` ：
```
WEATHER_API_KEY=xxxxxxxxxxxxxxxxxxxxx
```
>可以用两种方式来获取 `Lsoex\Weather\Weather` 实例：
>方法参数注入
```php
public function edit(Weather $weather) 
{
    $response = $weather->getLiveWeather('深圳');
}
```
>服务名访问
```php
public function edit() 
{
    $response = app('weather')->getLiveWeather('深圳');
}
```

## 如果对你有帮助请star哦！✨

## 参考
<a href="https://lbs.amap.com/api/webservice/guide/api/weatherinfo/">高德开放平台天气接口</a>
## License
MIT
