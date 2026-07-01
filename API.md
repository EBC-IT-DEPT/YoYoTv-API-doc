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

`result != "success"` 視為失敗（拋 `APIError26.apiFailure`）。

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

---

## 2. dfp（首頁廣告 / Google AD）

**Request**
```json
{
    "request": "dfp",
    "platform": "ios",
    "ip_address": "",
    "param": {
        "type": "string"
    }
}
```

**Response data**：`HomeADData`
```json
{
    "response": "dfp",
    "platform": "ios",
    "result": "success",
    "message": "",
    "data": {
        "code": "/xxxx/yoyotv_app_banner",
        "size": ["320", "50"],
        "show": "1"
    }
}
```

---

## 3. flash_list（快訊）

**Request**
```json
{
    "request": "flash_list",
    "platform": "ios",
    "ip_address": ""
}
```

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
> `app_event_type` / `ask_id` / `point_id` / `ask_title` / `app_event_id` 為選填。

---

## 4. home_video_list（首頁影片區塊）

**Request**
```json
{
    "request": "home_video_list",
    "platform": "ios",
    "ip_address": ""
}
```

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

---

## 5. video_tab_list（首頁分類 Tab）

**Request**
```json
{
    "request": "video_tab_list",
    "platform": "ios",
    "ip_address": ""
}
```

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
> `code` 對應 `Video_Tab.Video_TAB_ID`。

---

## 6. top_banner_list（首頁推薦）

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
> App 端僅取 `type == "banner"` 的項目。

---

## 7. video_recommend_list（影音頁 YOYO推薦）

**Request**
```json
{
    "request": "video_recommend_list",
    "platform": "ios",
    "ip_address": ""
}
```

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
> `is_new` 為 `"Y"` 時顯示「最新上線」標籤。

---

## 8. featured_video_list（影音頁主打輪播）

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

---

## 9. tab_show_video_list（影音頁分類影片區塊）

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
                    "image": "http://<TEST_HOST>/upload/yoyotv/img/banner.gif",
                    "is_new": "Y"
                }
            ]
        }
    ]
}
```
> `type` 支援 `yt_channel` / `yt_list` / `single_video`。`single_video` 的 `code` 為主機影片路徑或 VIDEO_CODE；YT 類型的 `code` 為 YOUTUBE_ID。
> `video_topic_main_code` / `video_topic_sub_code` 用於帶入 `video_detail_list`（主分類/子分類 ID）。
> `is_new`：`Y` 為最新上線、`N` 為否。

---

## 10. video_detail_list（影音頁播放清單內容）

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
        "video_ad": [
            {
                "video_ad_url": "https://yoyotv.ebc.net.tw/video"
            }
        ],
        "video_banner": {
            "banner_portrait_video_image": "",
            "banner_landscape_image": "",
            "banner_url": ""
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
> `type` 支援 `ytvideo` / `dfp`（`banner` 已從 type 移除，改由 `video_banner` 物件承載）。
> `video_banner` 為單一物件（非陣列），提供 banner 直式/橫式圖片與單一 `banner_url` 連結（直式/橫式共用同一個連結，不再分開）。
> 目前 2026 影音詳細頁主要處理 `ytvideo`；`dfp` 及 `video_banner` 欄位保留供後續使用。
