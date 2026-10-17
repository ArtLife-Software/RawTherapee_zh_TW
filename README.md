# RawTherapee 正體中文語系檔

[RawTherapee](https://rawtherapee.com/) 的正體中文（台灣用語）介面翻譯，涵蓋全部 4857 個介面字串，沒有遺漏的英文項目。

## 檔案

| 檔案 | 說明 |
|---|---|
| `Chinese Taiwan` | 語系檔本體（UTF-8，無副檔名），選單中顯示為「正體中文」 |

## 安裝

1. 下載 `Chinese Taiwan`。
2. 放進 RawTherapee 安裝目錄下的 `languages` 資料夾，預設位置為：
   ```
   C:\Program Files\RawTherapee\5.13\languages\
   ```
3. 開啟 RawTherapee，進入「Preferences（參數設定）→ General（一般）」。
4. 取消勾選「Use system language（使用系統語言）」，在「Language（語言）」下拉選單選擇「正體中文」。
5. 重新啟動 RawTherapee。

> 更新 RawTherapee 版本後，安裝程式可能會覆蓋 `languages` 資料夾。若選單中找不到「正體中文」，請重新複製本檔案。

## ⚠️ 請勿把檔名改成 `Chinese (Traditional)`

檔名請保持 `Chinese Taiwan`，**不要**改成看起來比較「正式」的 `Chinese (Traditional)`，也不要使用 `Chinese (Simplified)`。

在台灣版 Windows（系統字碼頁 CP950）上，這兩個檔名會讓 RawTherapee 把程式語系設為簡體字碼頁（CP936）。結果是中文檔名比較出錯，造成：

- 檔案瀏覽器只顯示部分縮圖，而且每次重新整理顯示的數量都不同（例如 68 張只出現 4～9 張）。
- 資料夾樹狀圖排序錯亂，無法展開到目前的資料夾。

原因如下：

1. RawTherapee 依語系檔名設定語系：`Chinese (Simplified)` 設為 `zh_CN`，`Chinese (Traditional)` 設為 `zh_SG`（新加坡，使用簡體）。
2. GTK 據此把 C 執行庫的語系設為字碼頁 936。
3. GLib 比較中文字串時，卻是依 Windows 系統字碼頁（950）轉碼。
4. 兩邊字碼頁不一致，`strcoll` 的比較結果就會錯亂。

使用不在對照表內的檔名（例如 `Chinese Taiwan`）時，程式會沿用 Windows 系統語系，兩邊一致，就不會出問題。

已實測的組合（台灣版 Windows，68 張中文檔名的 JPG）：

| 語系檔名 | 結果 |
|---|---|
| `Chinese Taiwan` | ✅ 正常 |
| `Chinese (Traditional)` | ❌ 漏圖、資料夾樹錯亂 |
| `Chinese (Simplified)`（無論內容是簡體或正體） | ❌ 漏圖、資料夾樹錯亂 |
| `English (US)` | ✅ 正常 |

相關討論：[RawTherapee #7304](https://github.com/RawTherapee/RawTherapee/issues/7304)、[RawTherapee #7314](https://github.com/RawTherapee/RawTherapee/issues/7314)、[GLib #3618](https://gitlab.gnome.org/GNOME/glib/-/issues/3618)

## 翻譯來源與方式

| 來源 | 項目數 | 方式 |
|---|---|---|
| 官方簡體中文語系檔已翻譯的部分 | 約 2600 | 以 OpenCC（`s2twp`）轉為台灣正體與用語，再人工修正常見詞彙 |
| 簡體中文檔未翻譯的部分 | 1983 | 參照 English (US)，以 English (UK) 輔助，直接翻譯 |
| 簡體版內容已過時、與英文原文不符的項目 | 38 | 依英文原文重新翻譯（例如快速鍵說明） |
| 人工翻譯段落 | 約 200 | `ABOUT_*`～`EXIFPANEL_*`、`EXPORT_*`、`FILEBROWSER_*` 等 |

所有項目都已檢查格式：`%1`、`<b>`、`<i>`、`\n` 等標記的數量與英文原文一致。

### 主要用語對照

| 英文 | 本翻譯 | 簡體版 |
|---|---|---|
| Mask | 遮罩 | 蒙版 |
| Preferences | 參數設定 | 首选项 |
| Shortcut | 快速鍵 | 快捷键 |
| Pixel | 像素 | 像素 |
| Noise | 雜訊 | 噪点 |
| Slider | 滑桿 | 滑条 |
| Metadata | 中繼資料 | 元数据 |
| Queue | 佇列 | 队列 |
| Cache | 快取 | 缓存 |
| Export | 匯出 | 导出 |
| Local adjustments (Locallab) | 局部－ | 局部- |
| Spot | 調整點 | 调整点 |
| Contrast by Detail Levels | 分頻反差 | 分频反差 |
| Threshold | 閾值 | 阈值 |
| Wavelet | 小波 | 小波 |

## 已知限制

- 從簡體轉換而來的部分保留了原譯者的句型，少數地方可能仍帶有大陸語感。
- 介面中少數來自 GTK 本身的文字（例如開啟檔案對話框）可能顯示為英文，這與本語系檔無關。
- 僅在 Windows 上實際測試；macOS 與 Linux 應可使用，但未經驗證。

## 回報問題與貢獻

發現翻譯錯誤、用語不順或漏譯，歡迎開 Issue 或送 Pull Request。請註明：

- 字串鍵值（例如 `TP_EXPOSURE_LABEL`）或畫面位置
- 目前的翻譯與建議的翻譯

## 致謝

本翻譯以 RawTherapee 官方簡體中文語系檔為基礎。感謝歷任簡體中文譯者：Forrest Sun、Yang Gao (grantyale)、Jiero、Jie Luo、Chongnuo Ji、syyrmb。

## 授權

RawTherapee 以 [GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.html) 釋出，本語系檔衍生自其官方語系檔，同樣採用 GPL-3.0 授權。
