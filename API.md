# YoYoTv2026 API 文件

依現有 `Network26` + `HomeAPIService` 呼叫方式整理。

## 共通規格

- **Method**：`POST`
- **Base URL**：`ApiIP`（全域變數）
- **Path**：`api/mobileapi/{request}`
- **Header**：`Content-Type: application/json; charset=utf-8`
- **欄位命名**：Request 與 Response 線上 JSON 皆為 `snake_case`（Swift 端用 `.convertFromSnakeCase` 自動對應）。

### 共通 Response 外層

```json
{
    "response": "string",
    "platform": "ios",
    "result": "success",
    "message": "",
    "data": {}
}
```

> `response`：回應的 API 名稱。
> `platform`：呼叫平台，目前 App 使用 `ios`。
> `result`：執行結果；不為 `success` 時視為失敗，並拋出 `APIError26.apiFailure`。
> `message`：API 回應訊息。
> `data`：各 API 的實際回應資料。

---

## 1. home_slider_list（首頁 Banner）

**Request**
```json
{
    "request": "home_slider_list",
    "platform": "ios",
    "channel": "yoyotv",
    "ip_address": ""
}
```
> `request`：API 名稱，固定為 `home_slider_list`。
> `platform`：呼叫平台，目前 App 使用 `ios`。
> `channel`：頻道名稱，固定為 `yoyotv`。
> `ip_address`：裝置目前的 IP 位址，無法取得時傳空字串。

**Response data**：`[HomeBannerData]`
```json
{
    "response": "home_slider_list",
    "platform": "ios",
    "result": "success",
    "message": "",
    "data": [
        {
            "id": "19",
            "title": "首頁 Banner 測試",
            "image": "http://.../banner.jpg",
            "url": ""
        }
    ]
}
```
> `data[].id`：Banner ID。
> `data[].title`：Banner 標題。
> `data[].image`：Banner 圖片網址。
> `data[].url`：點擊 Banner 後開啟的網址，未設定時為空字串。

---

## 2. flash_list（快訊）

**Request**
```json
{
    "request": "flash_list",
    "platform": "ios",
    "ip_address": ""
}
```
> `request`：API 名稱，固定為 `flash_list`。
> `platform`：呼叫平台，目前 App 使用 `ios`。
> `ip_address`：裝置目前的 IP 位址，無法取得時傳空字串。

**Response data**：`[HomeFlashData]`
```json
{
    "response": "flash_list",
    "platform": "ios",
    "result": "success",
    "message": "",
    "data": [
        {
            "type": "string",
            "code": "string",
            "title": "string",
            "url": "",
            "app_event_type": 0,
            "ask_id": 0,
            "point_id": 0,
            "ask_title": "",
            "app_event_id": 0
        }
    ]
}
```
> `data[].type`：快訊類型。
> `data[].code`：快訊代碼。
> `data[].title`：快訊標題。
> `data[].url`：快訊連結，未設定時為空字串。
> `data[].app_event_type`：APP 專屬活動類型，選填。
> `data[].ask_id`：問答活動 ID，選填。
> `data[].point_id`：集點活動 ID，選填。
> `data[].ask_title`：問答活動標題，選填。
> `data[].app_event_id`：APP 專屬活動 ID，選填。

---

## 3. home_video_list（首頁影片區塊）

**Request**
```json
{
    "request": "home_video_list",
    "platform": "ios",
    "ip_address": ""
}
```
> `request`：API 名稱，固定為 `home_video_list`。
> `platform`：呼叫平台，目前 App 使用 `ios`。
> `ip_address`：裝置目前的 IP 位址，無法取得時傳空字串。

**Response data**：`[HomeVideoSectionData]`
```json
{
    "response": "home_video_list",
    "platform": "ios",
    "result": "success",
    "message": "",
    "data": [
        {
            "code": "46",
            "name": "YOYO強打卡通",
            "total_count": 3,
            "list": [
                {
                    "type": "yt_list",
                    "code": "test-list-1",
                    "title": "影片標題",
                    "image": "http://.../cover.jpg"
                }
            ]
        }
    ]
}
```
> `data[].code`：影片主分類 ID。
> `data[].name`：影片區塊名稱。
> `data[].total_count`：區塊內的影片總數。
> `data[].list[].type`：影片類型。
> `data[].list[].code`：影片或播放清單代碼。
> `data[].list[].title`：影片標題。
> `data[].list[].image`：影片封面圖片網址。

---

## 4. video_tab_list（首頁分類 Tab）

**Request**
```json
{
    "request": "video_tab_list",
    "platform": "ios",
    "ip_address": ""
}
```
> `request`：API 名稱，固定為 `video_tab_list`。
> `platform`：呼叫平台，目前 App 使用 `ios`。
> `ip_address`：裝置目前的 IP 位址，無法取得時傳空字串。

**Response data**：`[HomeCategoryData]`
```json
{
    "response": "video_tab_list",
    "platform": "ios",
    "result": "success",
    "message": "",
    "data": [
        {
            "code": "1",
            "name": "熱門"
        }
    ]
}
```
> `data[].code`：影音分類 ID，對應 `Video_Tab.Video_TAB_ID`。
> `data[].name`：影音分類名稱。

---

## 5. top_banner_list（首頁推薦）

**Request**
```json
{
    "request": "top_banner_list",
    "platform": "ios",
    "ip_address": "",
    "param": {
        "request_count": "100",
        "page": "1"
    }
}
```
> `request`：API 名稱，固定為 `top_banner_list`。
> `platform`：呼叫平台，目前 App 使用 `ios`。
> `ip_address`：裝置目前的 IP 位址，無法取得時傳空字串。
> `param.request_count`：每頁要求的資料筆數。
> `param.page`：頁碼，從 `1` 開始。

**Response data**：`HomeRecommendationListData`
```json
{
    "response": "top_banner_list",
    "platform": "ios",
    "result": "success",
    "message": "",
    "data": {
        "total_count": 10,
        "list": [
            {
                "type": "banner",
                "title": "推薦標題",
                "image": "http://.../cover.jpg",
                "url": "",
                "event_code": "",
                "banner_id": ""
            }
        ]
    }
}
```
> `data.total_count`：推薦資料總數。
> `data.list[].type`：推薦項目類型；App 端僅顯示 `banner`。
> `data.list[].title`：推薦項目標題。
> `data.list[].image`：推薦項目圖片網址。
> `data.list[].url`：點擊後開啟的網址，未設定時為空字串。
> `data.list[].event_code`：關聯活動代碼，未設定時為空字串。
> `data.list[].banner_id`：Banner ID，未設定時為空字串。

---

## 6. video_recommend_list（影音頁 YOYO推薦）

**Request**
```json
{
    "request": "video_recommend_list",
    "platform": "ios",
    "ip_address": ""
}
```
> `request`：API 名稱，固定為 `video_recommend_list`。
> `platform`：呼叫平台，目前 App 使用 `ios`。
> `ip_address`：裝置目前的 IP 位址，無法取得時傳空字串。

**Response data**：`VideoRecommendListData`
```json
{
    "response": "video_recommend_list",
    "platform": "ios",
    "result": "success",
    "message": "",
    "data": {
        "list": [
            {
                "video_tab_code": "1",
                "type": "yt_channel",
                "video_topic_main_code": "194",
                "video_topic_sub_code": "",
                "image": "https://i.ytimg.com/vi/-8hHVZ5jI9c/maxresdefault.jpg",
                "title": "美妙寵物光之美少女",
                "is_new": "Y"
            }
        ]
    }
}
```
> `data.list[].video_tab_code`：影音分類 ID。
> `data.list[].type`：影片類型。
> `data.list[].video_topic_main_code`：影片主分類 ID。
> `data.list[].video_topic_sub_code`：影片子分類 ID，未設定時為空字串。
> `data.list[].image`：影片封面圖片網址。
> `data.list[].title`：影片標題。
> `data.list[].is_new`：是否最新上線；`Y` 顯示「最新上線」標籤，`N` 不顯示。

---

## 7. featured_video_list（影音頁主打輪播）

**Request**
```json
{
    "request": "featured_video_list",
    "platform": "ios",
    "ip_address": "",
    "param": {
        "video_tab_code": "1"
    }
}
```
> `request`：API 名稱，固定為 `featured_video_list`。
> `platform`：呼叫平台，目前 App 使用 `ios`。
> `ip_address`：裝置目前的 IP 位址，無法取得時傳空字串。
> `param.video_tab_code`：影音分類 ID。

**Response data**：`VideoFeaturedListData`
```json
{
    "response": "featured_video_list",
    "platform": "ios",
    "result": "success",
    "message": "",
    "data": {
        "list": [
            {
                "video_tab_code": "1",
                "type": "yt_list",
                "video_topic_main_code": "194",
                "video_topic_sub_code": "",
                "image": "https://i.ytimg.com/vi/-8hHVZ5jI9c/maxresdefault.jpg",
                "title": "美妙寵物光之美少女"
            }
        ]
    }
}
```
> `data.list[].video_tab_code`：影音分類 ID。
> `data.list[].type`：影片類型。
> `data.list[].video_topic_main_code`：影片主分類 ID。
> `data.list[].video_topic_sub_code`：影片子分類 ID，未設定時為空字串。
> `data.list[].image`：主打影片封面圖片網址。
> `data.list[].title`：主打影片標題。

---

## 8. tab_show_video_list（影音頁分類影片區塊）

**Request**
```json
{
    "request": "tab_show_video_list",
    "platform": "ios",
    "ip_address": "",
    "param": {
        "video_tab_code": "1"
    }
}
```
> `request`：API 名稱，固定為 `tab_show_video_list`。
> `platform`：呼叫平台，目前 App 使用 `ios`。
> `ip_address`：裝置目前的 IP 位址，無法取得時傳空字串。
> `param.video_tab_code`：影音分類 ID。

**Response data**：`[VideoSectionData]`
```json
{
    "response": "tab_show_video_list",
    "platform": "ios",
    "result": "success",
    "message": "",
    "data": [
        {
            "video_tab_code": "1",
            "name": "test-影片對應 創意大發現",
            "total_count": 5,
            "list": [
                {
                    "video_topic_main_code": "46",
                    "video_topic_sub_code": "1",
                    "type": "yt_channel",
                    "code": "__SEFSclF58",
                    "title": "影片標題",
                    "video_desc": "影片說明",
                    "image": "http://.../banner.gif",
                    "is_new": "Y"
                }
            ]
        }
    ]
}
```
> `data[].video_tab_code`：影音分類 ID。
> `data[].name`：影片區塊名稱。
> `data[].total_count`：區塊內的影片總數。
> `data[].list[].video_topic_main_code`：影片主分類 ID，用於呼叫 `video_detail_list`。
> `data[].list[].video_topic_sub_code`：影片子分類 ID，用於呼叫 `video_detail_list`。
> `data[].list[].type`：支援 `yt_channel` / `yt_list` / `single_video`。
> `data[].list[].code`：`single_video` 為主機影片路徑或 VIDEO_CODE；YT 類型為 YOUTUBE_ID。
> `data[].list[].title`：影片標題。
> `data[].list[].video_desc`：影片說明，未設定時為空字串或 `null`。
> `data[].list[].image`：影片封面圖片網址。
> `data[].list[].is_new`：是否最新上線，值為 `Y` / `N`。

---

## 9. video_detail_list（影音頁播放清單內容）

**Request**
```json
{
    "request": "video_detail_list",
    "platform": "ios",
    "ip_address": "",
    "param": {
        "video_topic_main_code": "194",
        "video_topic_sub_code": ""
    }
}
```
> `request`：API 名稱，固定為 `video_detail_list`。
> `platform`：呼叫平台，目前 App 使用 `ios`。
> `ip_address`：裝置目前的 IP 位址，無法取得時傳空字串。
> `param.video_topic_main_code`：影片主分類 ID。
> `param.video_topic_sub_code`：影片子分類 ID，未設定時為空字串。

**Response data**：`VideoDetailData`
```json
{
    "response": "video_detail_list",
    "platform": "ios",
    "result": "success",
    "message": "",
    "data": {
        "total_count": 28,
        "player_list_name": "播放清單名稱",
        "player_list_desc": "播放清單說明",
        "video_topic_main_code": "194",
        "video_topic_sub_code": "",
        "video_banner": {
            "banner_portrait_video_image": "",
            "banner_landscape_image": "",
            "banner_url": ""
        },
        "video_ad_setting": {
            "Show_After_Count": 1,
            "First_Show_Seq": 1
        },
        "list": [
            {
                "type": "ytvideo",
                "code": "-8hHVZ5jI9c",
                "image": "https://i.ytimg.com/vi/-8hHVZ5jI9c/maxresdefault.jpg",
                "title": "美妙寵物光之美少女"
            }
        ]
    }
}
```
> `data.total_count`：播放清單項目總數。
> `data.player_list_name`：播放清單名稱。
> `data.player_list_desc`：播放清單說明。
> `data.video_topic_main_code`：影片主分類 ID。
> `data.video_topic_sub_code`：影片子分類 ID。
> `data.video_banner`：單一 Banner 物件，非陣列。
> `data.video_banner.banner_portrait_video_image`：直式 Banner 圖片網址。
> `data.video_banner.banner_landscape_image`：橫式 Banner 圖片網址。
> `data.video_banner.banner_url`：直式與橫式 Banner 共用的點擊網址。
> `data.video_ad_setting.Show_After_Count`：每觀看幾支影片後顯示一次 mp4 廣告，範圍為 `0`～`9`。
> `data.video_ad_setting.First_Show_Seq`：廣告首次出現位置；`0` 無、`1` 片頭、`2` 片尾。
> `data.list[].type`：支援 `ytvideo` / `dfp`；Banner 已改由 `video_banner` 物件承載。
> `data.list[].code`：YouTube 影片 ID 或對應項目代碼。
> `data.list[].image`：影片封面圖片網址。
> `data.list[].title`：影片標題。
> `2026 App 支援狀態`：目前影音詳細頁主要處理 `ytvideo`；`dfp`、`video_banner`、`video_ad_setting` 保留供後續使用。

## 10. video_ad（YT 播放前的廣告）

**Request**
```json
{
    "request": "video_ad",
    "platform": "ios",
    "ip_address": ""
}
```
> `request`：API 名稱，固定為 `video_ad`。
> `platform`：呼叫平台，目前 App 使用 `ios`。
> `ip_address`：裝置目前的 IP 位址，無法取得時傳空字串。

**Response data**：`VideoAdData`
```json
{
    "response": "video_ad",
    "platform": "ios",
    "result": "success",
    "message": "",
    "data": {
        "video_ad_url": "https://yoyotv.ebc.net.tw/video"
    }
}
```
> `data.video_ad_url`：YT 播放前的廣告影片網址。

---

## 13. app_event_content（APP 專屬活動內容）

**API Path**：`/api/mobileapi/app_event_content`

**Request**
```json
{
    "request": "app_event_content",
    "platform": "ios",
    "ip_address": "",
    "param": {
        "code": "1"
    }
}
```
> `request`：API 名稱，固定為 `app_event_content`。
> `platform`：呼叫平台，目前 App 使用 `ios`。
> `ip_address`：裝置目前的 IP 位址，無法取得時傳空字串。
> `param.code`：APP 專屬活動 ID。

**Response data**：APP 專屬活動題目陣列
```json
{
    "response": "app_event_content",
    "platform": "ios",
    "result": "success",
    "message": "",
    "data": [
        {
            "type": "text",
            "code": "1",
            "title": "活動題目",
            "options": [
                {
                    "label": "選項文字或圖片網址",
                    "value": "1",
                    "image_desc": "圖片描述"
                }
            ]
        }
    ]
}
```
> `data[].type`：題目類型；`text` 為純文字、`image` 為純圖片、`text_image` 為文字加圖片。
> `data[].code`：活動代碼。
> `data[].title`：活動標題或題目文字。
> `data[].options[].label`：選項文字或圖片網址。
> `data[].options[].value`：選項值。
> `data[].options[].image_desc`：圖片描述，`type == "text_image"` 時會有值。

---

## 14. app_event_list（APP 專屬活動列表）

**API Path**：`/api/mobileapi/app_event_list`

**參考**：同舊 API 的 `app_event_list`。

**Request**
```json
{
    "request": "app_event_list",
    "platform": "ios",
    "ip_address": ""
}
```
> `request`：API 名稱，固定為 `app_event_list`。
> `platform`：呼叫平台，目前 App 使用 `ios`。
> `ip_address`：裝置目前的 IP 位址，無法取得時傳空字串。

**Response data**：APP 專屬活動列表
```json
{
    "response": "app_event_list",
    "platform": "ios",
    "result": "success",
    "message": "",
    "data": {
        "total_count": 5,
        "events": [
            {
                "code": "1",
                "title": "活動標題",
                "event_begin": "07/01 00:00",
                "event_end": "07/31 23:59",
                "is_completed": "N",
                "is_opened": "Y",
                "description": "活動摘要文字",
                "image": "https://example.com/event.jpg"
            }
        ]
    }
}
```
> `total_count`：活動總數。
> `events.code`：活動代碼。
> `events.title`：活動標題。
> `events.event_begin` / `events.event_end`：活動開始及結束時間，格式為 `MM/dd HH:mm`。
> `events.is_completed`：會員是否已完成活動，值為 `Y` / `N`；未登入一律為 `N`。
> `events.is_opened`：活動於當前時間是否已開放，值為 `Y` / `N`。
> `events.description`：對應網頁活動的摘要文字，未設定時為空字串。
> `events.image`：對應網頁活動的封面圖，未設定時為空字串。
