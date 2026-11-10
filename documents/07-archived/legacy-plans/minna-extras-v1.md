# Plan: Minna no Nihongo — Extras (Alphabet + Counters)
**Version:** v1
**Created:** 2026-02-21
**Status:** 🔴 Not Started (blocked by minna-refactor-v1 Phase 1+2)
**Scope:** Bổ sung 2 section mới theo giáo trình Minna no Nihongo: bảng chữ cái và đếm số/trợ số từ

---

## Changelog
| Version | Date | Changes |
|---------|------|---------|
| v1 | 2026-02-21 | Initial plan |

---

## 🎯 Mục tiêu

Bổ sung 2 section học ngoài 25 bài từ vựng chính:

1. **Bảng chữ cái** — Hiragana & Katakana reference + luyện tập
2. **Đếm số & Trợ số từ** — Số đếm, cách đọc theo ngữ cảnh (tuổi, tầng, số lượng, thời gian...)

Cả hai section đều là **nội dung tham khảo + quiz**, không thay đổi cấu trúc app hiện tại.

---

## 📊 Nội dung chi tiết

### Section 1: Bảng chữ cái

**Hiragana (平仮名):**
- 46 chữ cơ bản (あ→ん)
- 20 chữ dakuten/handakuten (が、ざ、だ、ば、ぱ...)
- 33 chữ kết hợp youon (きゃ、しゅ、ちょ...)

**Katakana (片仮名):**
- 46 chữ cơ bản (ア→ン)
- 20 chữ dakuten/handakuten (ガ、ザ、ダ、バ、パ...)
- 33 chữ kết hợp youon (キャ、シュ、チョ...)

**Tính năng:**
- Bảng grid (5 cột a/i/u/e/o × N hàng)
- Click cell → phát âm (Web Speech API)
- Tab Hiragana | Katakana | So sánh (2 cột)
- Flashcard mode: hiện romaji → nhập kana (hoặc ngược lại)

---

### Section 2: Đếm số & Trợ số từ

**Số cơ bản:**
| Số | Kanji | Hiragana | Romaji |
|----|-------|----------|--------|
| 0 | 零 | ぜろ/れい | zero/rei |
| 1-10 | 一〜十 | いち〜じゅう | ichi〜juu |
| 11-99 | 十一〜 | じゅういち〜 | juuichi〜 |
| 100 | 百 | ひゃく | hyaku |
| 1,000 | 千 | せん | sen |
| 10,000 | 万 | まん | man |

**Trợ số từ (Counters) theo Minna no Nihongo:**

| Counter | Kanji | Dùng cho | Irregular readings | Bài |
|---------|-------|----------|--------------------|-----|
| 〜個 | 個 | Vật nhỏ (táo, kẹo) | 1:いっこ, 6:ろっこ, 8:はっこ, 10:じゅっこ | L11 |
| 〜枚 | 枚 | Vật phẳng (giấy, quần áo, tem) | Đều | L11 |
| 〜本 | 本 | Vật dài (bút, chai, cà vạt) | 1:いっぽん, 3:さんぼん, 6:ろっぽん, 8:はっぽん | L11 |
| 〜冊 | 冊 | Sách, vở | 1:いっさつ, 8:はっさつ, 10:じゅっさつ | L11 |
| 〜台 | 台 | Máy móc, xe | Đều | L11 |
| 〜杯 | 杯 | Cốc, bát, ly | 1:いっぱい, 3:さんばい, 6:ろっぱい | L11 |
| 〜匹 | 匹 | Thú nhỏ (cá, mèo, chó) | 1:いっぴき, 3:さんびき, 6:ろっぴき | L11 |
| 〜頭 | 頭 | Thú lớn (bò, ngựa, voi) | Đều | — |
| 〜羽 | 羽 | Chim, thỏ | 1:いちわ, 3:さんば, 6:ろくわ | — |
| 〜人 | 人 | Người | 1:ひとり, 2:ふたり, 3〜:〜にん | L3 |
| 〜歳/才 | 歳 | Tuổi | 1:いっさい, 8:はっさい, 20:はたち | L4 |
| 〜階 | 階 | Tầng | 3:さんがい, 6:ろっかい, 8:はっかい | L10 |
| 〜番 | 番 | Số thứ tự | Đều | L3 |
| 〜時 | 時 | Giờ (o'clock) | 4:よじ, 7:しちじ, 9:くじ | L3 |
| 〜分 | 分 | Phút | 1:いっぷん, 3:さんぷん, 4:よんぷん | L3 |
| 〜月 | 月 | Tháng | 4:しがつ, 7:しちがつ, 9:くがつ | L4 |
| 〜日 | 日 | Ngày | 1〜10: đặc biệt (ついたち, ふつか...) | L4 |

**Tính năng:**
- Bảng tham khảo số + cách đọc biến đổi (irregular)
- Bảng counter: counter + cách dùng + ví dụ câu
- Flashcard/MC mode: nghe số/counter → chọn cách đọc đúng
- Quiz đặc biệt: nghe ngữ cảnh → chọn counter phù hợp

---

## 🗺️ Kiến trúc

### Data files mới

```
js/data/minna/
├── alphabet.js        # Hiragana + Katakana data
├── counters.js        # Numbers + Counter data
└── index.js          # (update) thêm ALPHABET_DATA, COUNTERS_DATA vào export
```

**Schema alphabet.js:**
```javascript
const ALPHABET_DATA = {
  hiragana: {
    basic:    [{ kana, romaji, row, col }],  // 46
    dakuten:  [{ kana, romaji, row, col }],  // 20
    combo:    [{ kana, romaji, base, small }], // 33
  },
  katakana: {
    basic:    [...],
    dakuten:  [...],
    combo:    [...],
  }
};
```

**Schema counters.js:**
```javascript
const COUNTERS_DATA = {
  numbers: {
    title: "Số đếm cơ bản",
    items: [
      { number: 1, kanji: "一", kana: "いち", romaji: "ichi" },
      // ...
    ]
  },
  counters: [
    {
      counter: "枚",
      kana: "まい",
      romaji: "mai",
      vietnamese: "vật phẳng (giấy, quần áo)",
      lesson: 11,
      readings: [
        { number: 1, form: "一枚", kana: "いちまい", romaji: "ichimai" },
        // ...  lên đến 10
      ],
      example: { japanese: "切手を三枚ください", vietnamese: "Cho tôi 3 con tem" }
    },
    // ...
  ]
};
```

### Screens mới

```
js/screens/
├── alphabet.js        # renderAlphabetGrid, openAlphabetScreen, tab switching
└── counters.js        # renderCountersTable, renderNumbersTable, openCountersScreen
```

### UI: Entry point từ màn hình chính

Thêm 2 card đặc biệt ở đầu lesson grid (trước bài 1):

```
[ 🔤 Bảng chữ cái ]  [ 🔢 Đếm số & Trợ số từ ]
[ Bài 1 ] [ Bài 2 ] ... [ Bài 25 ]
```

Hoặc thêm 2 button vào header/nav nếu muốn truy cập nhanh hơn.

---

## 📋 Phases

### Phase A: Bảng chữ cái
- [ ] Tạo `js/data/minna/alphabet.js` (46+20+33 × 2 bộ = ~198 entries)
- [ ] Tạo `js/screens/alphabet.js` (grid render, tab switch, speak on click)
- [ ] Thêm screen `#screen-alphabet` vào `index.html`
- [ ] Thêm CSS grid cho bảng chữ cái
- [ ] Thêm entry card trên lesson grid
- [ ] Test: hiragana grid đầy đủ, katakana đầy đủ, phát âm OK

### Phase B: Đếm số & Trợ số từ
- [ ] Tạo `js/data/minna/counters.js` (số 1-10000 + ~17 counters)
- [ ] Tạo `js/screens/counters.js` (bảng số + bảng counter + irregular readings)
- [ ] Thêm screen `#screen-counters` vào `index.html`
- [ ] Thêm CSS cho bảng counter (highlight irregular cells)
- [ ] Thêm entry card trên lesson grid
- [ ] Test: bảng số đúng, irregular readings highlight OK

### Phase C: Quiz mode
**Alphabet quiz modes** (kana ↔ romaji):
| Mode | Hiển thị | Trả lời |
|------|----------|---------|
| `alpha-fc` | Flashcard — mặt trước: kana, sau: romaji | biết/chưa biết |
| `alpha-mc-kr` | MC — hỏi kana, chọn romaji đúng từ 4 đáp án | click đáp án |
| `alpha-mc-rk` | MC — hỏi romaji, chọn kana đúng từ 4 đáp án | click đáp án |
| `alpha-typing` | Typing — nhìn kana, gõ romaji | gõ phím |

Config: **Bộ chữ** (hiragana/katakana/cả hai) × **Loại** (cơ bản 46/tất cả +youon)

**Counter quiz modes**:
| Mode | Hiển thị | Trả lời |
|------|----------|---------|
| `counter-fc` | Flashcard — mặt trước: form (三本), sau: cách đọc (さんぼん/sanbon) | biết/chưa biết |
| `counter-mc` | MC — hỏi form (三本), chọn cách đọc đúng từ 4 đáp án | click đáp án |

Config: **Lọc** (tất cả / chỉ irregular)

**Item format chuẩn** (tương thích với quiz infrastructure hiện tại):
```js
// Alpha item
{ japanese: 'し', kana: 'し', romaji: 'shi', vietnamese: 'shi', english: '', example: '' }
// Counter item
{ japanese: '三本', kana: 'さんぼん', romaji: 'sanbon',
  vietnamese: 'さんぼん (sanbon)', english: '3 (本)', example: '…' }
```

**Files thêm/sửa:**
- `js/quiz/alpha-quiz.js` (new) — render functions cho alpha modes
- `js/quiz/counter-quiz.js` (new) — render functions cho counter modes
- `js/quiz/session.js` — route `alpha-*` và `counter-*` modes
- `js/core/state.js` — thêm `currentItems: []` (dùng cho retry-all không cần currentLesson)
- `js/screens/results.js` — guard `currentLesson` null, dùng `currentItems` cho retry-all
- `js/screens/alphabet.js` — thêm quiz panel + `buildAlphaItems()`
- `js/screens/counters.js` — thêm quiz panel + `buildCounterItems()`
- `index.html` — quiz panel HTML trong #screen-alphabet, #screen-counters
- `css/style.css` — `.quiz-panel` styles

**Checklist Phase C:**
- [ ] state.js: currentItems field
- [ ] results.js: guard currentLesson + dùng currentItems cho retry
- [ ] alpha-quiz.js: 4 render functions (fc, mc-kr, mc-rk, typing)
- [ ] counter-quiz.js: 2 render functions (fc, mc)
- [ ] session.js: route alpha-* và counter-*
- [ ] alphabet.js: buildAlphaItems() + quiz panel wiring
- [ ] counters.js: buildCounterItems() + quiz panel wiring
- [ ] index.html: quiz panel HTML
- [ ] CSS: quiz-panel styles
- [ ] Test: 6 quiz modes hoạt động, retry OK

---

## ⚠️ Lưu ý kỹ thuật

- **Content filtering:** `alphabet.js` chứa 198 ký tự Japanese — phải dùng Bash extraction hoặc write từng bộ nhỏ (basic/dakuten/combo riêng lẻ)
- **Không phá vỡ** cấu trúc 25 bài hiện tại — chỉ thêm mới
- `VOCABULARY_DATA` giữ nguyên — thêm `ALPHABET_DATA`, `COUNTERS_DATA` là global riêng
- Entry cards trên lesson grid: dùng CSS class riêng (`lesson-card--special`) để phân biệt

---

## 🔗 Dependencies
- Blocked by: `minna-refactor-v1` Phase 1 ✅ + Phase 2 ✅
- Independent với: `hsk-vocab-v1`
