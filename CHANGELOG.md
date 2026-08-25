# Japanese Practice — Changelog

All notable changes are listed here. Versions follow **semver**: `MAJOR.MINOR.PATCH`.

- **MAJOR**: breaking changes (new data shape, removed mode, etc.)
- **MINOR**: new features (new mode, new sub-category, new lesson)
- **PATCH**: bug fixes, polish, content additions inside existing structure

The version number is shown in the app footer and stamped into `data/manifest.json`.

---

## v1.10.0 - 2026-08-25

### Added — Lesson 18
- Imported **Dai_Ka 18.pdf** (Ikoma Language School). **+30 items** (21 vocab + 6 kaiwa + 3 related) and **+10 example sentences**.
- Grammar milestone: introduces **できます (potential/ability)** and the **辞書形 + ことができます** structure — the first way of expressing "can do X" without a dedicated potential form.
- Hobby verbs: 弾きます (play instrument), 歌います (sing), 集めます (collect), 捨てます (throw away), 換えます (exchange), 運転します (drive), 予約します (reserve/book), 洗います (wash).
- Nouns: ピアノ, ～メートル, 現金, 趣味, 日記, お祈り, 動物, 馬, インターネット.
- Workplace titles: 課長 (section head), 部長 (department head), 社長 (company president) — builds on L1–3 job/title vocab.
- Reaction 会話: 特に / へえ / それはおもしろいですね / なかなか (with negatives) / ほんとうですか / ぜひ.
- 関連単語: 故郷 (Furusato — song title), ビートルズ, 秋葉原.
- Cumulative: **827 vocab / 180 sentences / L1–L18 covered**.

---

## v1.9.0 - 2026-08-24

### Added — Lesson 17
- Imported **Dai_Ka 17.pdf** (Ikoma Language School). **+35 items** (29 vocab + 6 kaiwa) and **+10 example sentences**.
- Grammar setup for **~ないでください / ~なければなりません / ~までに** (obligation and deadlines).
- Verbs: 覚えます (memorise), 忘れます (forget), なくします (lose), 払います (pay), 返します (return), 出かけます (go out), 脱ぎます (take off), 持って行きます / 持って来ます (take/bring), 心配します (worry), 残業します (work overtime), 出張します (business trip), 飲みます [薬を~] (take medicine), 入ります [お風呂に~] (take a bath).
- na-adj: 大切／大丈夫. i-adj: 危ない (dangerous). 禁煙 (no smoking).
- Health vocab: 熱, 病気, 薬, 風邪, [健康]保険証, のど, 上着, 下着, [お]風呂.
- Time: ～までに (by ~), 2、3日, 2、3～, ですから.
- Doctor 会話: どうしましたか / [~が]痛いです / それから / お大事に.

---

## v1.8.0 - 2026-08-24

### Added — Lesson 16
- Imported **Dai_Ka 16.pdf** (Ikoma Language School). **+58 items** (41 vocab + 8 kaiwa + 2 renshuu C + 7 related) and **+10 example sentences**.
- Movement verbs: 乗ります [電車に~], 降ります [電車を~], 乗り換えます — introduces the に / を particle distinction for boarding/alighting.
- Transitive/intransitive setup: 入れます (put in), 出します (take out), 押します (push), 下ろします [お金を~] (withdraw).
- University lifecycle: 入ります [大学に~] (enter university), 出ます [大学を~] (graduate from). IDs disambiguated from earlier lesson homographs.
- Daily-life verbs: 浴びます [シャワーを~] (take a shower), 飲みます (drink alcohol — disambiguated from L6 のみます), 始めます (begin), 見学します (tour/visit), 電話します (phone).
- **i-adjectives**: 若い, 長い, 短い, 明るい, 暗い — sets up ~くない negative form.
- **Body parts (12)**: 体, 頭, 髪, 顔, 目, 耳, 鼻, 口, 歯, おなか, 足, 背 — feeds L17 illness kaiwa (~が痛いです).
- ATM kaiwa: お引き出しですか / まず / 次に / キャッシュカード / 暗証番号 / 金額 / 確認 / ボタン.
- 練習C: すごいですね / [いいえ、]まだまだです.
- 関連単語: JR, 雪祭り, バンドン, フランケン, ベラクルス, 梅田, 大学前.
- Direction pattern: どうやって + どの ～ / どれ (choosing from three or more).
- Cumulative: **797 vocab / 170 sentences / L1–L17 covered**.

---

## v1.7.0 - 2026-07-04

### Added — Lesson 15
- Imported **Dai_Ka 15.pdf** (Ikoma Language School). **+24 vocabulary items** and **+10 example sentences**. Totals: 704 vocab / 150 sentences / L1–L15 covered.
- Vocabulary focus: **Group I verbs** (置きます / 作ります / 売ります / 知ります / 住みます) + Group III (研究します) → sets up the transition to plain-form conjugation in later lessons.
- Nouns: 資料, カタログ, 時刻表, 服, 製品, ソフト, 電子辞書, 経済, 市役所, 高校, 歯医者, 独身, plus すみません as apology.
- 会話: 思い出します (remember, recollect), いらっしゃいます (honorific of います).
- 練習C: 皆さん (everybody).
- 関連単語: 日本橋 (Osaka shopping district), みんなのインタビュー (fictitious TV programme).
- Included 10 example sentences drilling the new verbs against L1–L14 grammar (は…に住みます / を作ります / に置きます / を知っています / いいえ、しりません / を研究しています / がほしい / どくしんですか).

---

## v1.6.5 - 2026-06-16

### Fixed — Audio no longer stops when screen locks
- Master audio now **requests a screen wake lock** (`navigator.wakeLock`) while a lesson is playing. The screen stays on for the duration → iOS no longer suspends JS → playback continues uninterrupted. Wake lock is released automatically when you tap stop or switch modes.
- Added **MediaSession** metadata so iOS lock-screen / Android notification panel now shows "Lesson N · Reading vocab + sentences" with a working stop button. You can stop the queue from the lock screen without unlocking your phone.
- Both APIs are feature-gated — older browsers that don't support them (e.g. Firefox Android < 121) gracefully fall back to the previous behaviour (audio still stops on lock).
- Trade-off: screen stays on while playing. Brightness can still be dimmed. Stops as soon as you tap the Stop button, switch mode, or close the app.

---

## v1.6.4 - 2026-06-16

### Changed
- Master audio further slowed for commute use:
  - **English** rate **0.70** (was 0.75)
  - **Japanese** rate **0.60** (was 0.65)
  - **Gaps** **400 ms** after every utterance (was 350 ms)

---

## v1.6.3 - 2026-06-16

### Changed
- Master audio further slowed for easier listening / commute use:
  - **English** rate **0.75** (was 0.85)
  - **Japanese** rate **0.65** (was 0.75)
  - **Gaps** **350 ms** after every utterance (was 250 ms)

---

## v1.6.2 - 2026-06-16

### Changed
- Master audio gaps simplified to a uniform **250 ms** after every utterance (English and Japanese alike). Was 200 ms after English / 500 ms after Japanese.

---

## v1.6.1 - 2026-06-16

### Changed
- Per-lesson master audio (and "Read all") now reads at a slower, more deliberate pace:
  - **English** rate **0.85** (was 0.95)
  - **Japanese** rate **0.75** (was 0.85)
- Gaps unchanged: 200 ms after English, 500 ms after Japanese.

---

## v1.6.0 - 2026-06-16

### Added — Per-lesson master audio button (Review tab)
- **🔊 Read lesson** pill button at the top of every lesson section in Review. Tap once → the app reads, at a measured pace, the **English** then the **Japanese** for every vocab item + sentence in that lesson, hands-free. Designed for commute / passive listening.
- Pace is deliberate: English at rate 0.95, Japanese at rate 0.85 with a 500 ms gap between pairs (not rushed).
- Button visually pulses orange while reading. Tap again → stop. Tap a different lesson → stops the first and starts the new one. Switching mode (e.g. into Flashcards) auto-stops playback.
- Per-row 🔊 buttons (single word) are **unchanged** — still work.
- The existing bottom "Read all (selected lessons)" button has been upgraded to the same EN→JP pacing for consistency.
- Cross-device safe: uses `onend` chaining when available, with a safety timeout fallback so iOS PWA / Samsung Internet quirks don't stall the queue. Calls `unlockAudio()` from the click gesture so iOS allows the first utterance.

---

## v1.5.0 - 2026-06-16

### Added — Te Form sub-category in Shukudai
- **New "Te Form" Shukudai sub-category** sourced from `Te Form Exercise.pdf`.
- **Learn view** (3 cards: Group I / II / III):
  - Group I (五段) shows all 9 ending-rules side-by-side (き→いて, ぎ→いで, し→して, ち→って, り→って, い→って, び→んで, み→んで, plus the irregular いきます → いって highlighted yellow).
  - Group II (一段) — drop ます, add て.
  - Group III — します → して, きます → きて, plus all ~します compound verbs.
- Each card shows the conjugation **rules first**, then a list of **verbs** (drawn from your existing L1-L14 vocab so they are familiar). 41 verbs total. Tap any row to hear the te-form.
- **Practice view** — random masu-form verb → tap reveal → see the te-form, romaji, and the rule used ("Group I · ち → って"). Use the existing 🔊 / Next flow.
- Uses the same `.review-row` markup as the Review tab and every other Learn view — visually consistent across iOS / Android / desktop.

---

## v1.4.0 - 2026-06-16

### Added — Lesson 14 (Dai_Ka 14.pdf)
- **40 main vocab items**: 21 verbs commonly used with the ~てください request form (つけます/けします/あけます/しめます/いそぎます/まちます/もちます/とります/てつだいます/よびます/はなします/つかいます/とめます/みせます/おしえます/すわります/たちます/はいります/でます/ふります/コピーします), 10 nouns (でんき/エアコン/パスポート/なまえ/じゅうしょ/ちず/しお/さとう/もんだい/こたえ + reading-related よみかた / ~かた), and 7 adverbs (まっすぐ/ゆっくり/すぐ/また/あとで/もうすこし/もう~).
- **3 会話 phrases**: 信号を 右へ 曲がってください (turn right at the traffic lights), これで おねがいします (I'll pay with this), お釣り (change).
- **2 練習C interjections**: さあ (right, let's go), あれ？ (Oh! Eh?).
- **1 関連単語**: みどり町 (fictitious town).
- **10 example sentences** practising the L14 ~てください pattern: "Please turn on the air conditioner", "Please wait a moment", "Please show me your passport", etc.
- Lesson 14 pill now appears in the lesson filter.

---

## v1.3.0 - 2026-06-15

### Added — Lesson 13 (Dai_Ka 13.pdf)
- **22 main vocab items**: leisure verbs (あそびます, およぎます, むかえます, つかれます, けっこんします, かいものします, しょくじします, さんぽします), adjectives (たいへん, ほしい, ひろい, せまい), nouns (プール, かわ, びじゅつ, つり, スキー, しゅうまつ, [お]しょうがつ), and time/place indefinites (~ごろ, なにか, どこか).
- **6 会話 phrases for ordering food**: ご注文は？ / 定食 / 牛丼 / ~を おねがいします / ~で ございます / 別に.
- **3 練習C idioms**: のどが かわきます (get thirsty), おなかが すきます (get hungry), そう しましょう (Let's do that).
- **2 関連単語**: チェニックス (fictitious company), おはようテレビ (fictitious TV programme).
- **10 example sentences** using L13 grammar (~たいです, ~がほしいです, verb-stem + に + 行きます, ~ましょう), e.g., "I want to go fishing at the river this weekend", "I'll have the gyūdon please", "I'm hungry. Let's eat something."
- Lesson 13 pill now appears in the lesson filter.

---

## v1.2.0 - 2026-05-19

### Added — Lesson 12 (Dai_Ka 12.pdf)
- **44 vocab items**: i-adjectives + na-adjective (かんたん, ちかい, とおい, はやい, おそい, おおい, すくない, あたたかい, すずしい, あまい, からい, おもい, かるい), seasons (はる/なつ/あき/ふゆ + きせつ), weather (てんき, あめ, ゆき, くもり), places (ホテル, くうこう, うみ, せかい, パーティー, [お]まつり), food (すきやき, さしみ, [お]すし, てんぷら, ぶたにく, とりにく, ぎゅうにく, レモン), culture (いけばな, もみじ), and comparison words (どちら, どちらも, いちばん, ずっと, はじめて).
- **4 会話 phrases**: ただいま (I'm home), お帰りなさい (Welcome home), わあ、すごい人ですね (Wow, look at all those people!), 疲れました (I'm tired).
- **5 関連単語**: 祇園祭 (Gion Festival), ホンコン (Hong Kong), シンガポール (Singapore), and two fictitious supermarket names.
- **10 example sentences** using L12 grammar (AとBとどちらが~ですか, ~のなかで~がいちばん~, weather/seasons, food preferences, comparing transport).
- Lesson 12 pill now appears in the lesson filter.


## v1.1.4 - 2026-05-18

### Fixed
- **All Shukudai Learn views now use the exact same row layout as the Review tab** — Counters, Numbers, Money, Time, Dates included. Prompt (number/symbol/label) on the left in sans-serif left-aligned. Japanese with romaji italic underneath in the centre. Speaker button on the right. Tap any row to hear it spoken.
- **Romaji shown for every reading** (auto-generated from kana for tables that didn't have it).
- **Voice over on every Learn row** (matches Review behaviour).
- **Fixed "いちまんえん" wrapping over 2 lines** — Japanese reading is now ellipsis-truncated within its cell when needed; cells are sized for typical readings.
- **Fixed "1,000,000" breaking out of the Numbers table** — prompt column uses tabular numerals and allows word-break.
- Irregular / rendaku readings still highlighted yellow but now via row-level class override (cleaner CSS, no inline gradient conflicts).
- Removed orphan `.ltable` CSS (replaced by review-row rules).

---

## v1.1.3 - 2026-05-18

### Fixed
- **Quiz of the day** button is now visible in every mode (was hidden in Review / Dictation / Hiragana / Katakana / Shukudai because it lived inside the direction-row). Moved to its own slot on the right of the Lessons row, smaller and labelled "🎯 Quiz (10)".
- Manifest `shukudai_banks_total` now auto-synced from the actual data on every build (was stale at 180 vs actual 75).
- Removed dead Type/MCQ toggle row from DOM + handlers + `state.shuInput`. Was permanently hidden but still in code.
- Trimmed `SHU_BANK_KEYS` constant to actual categories (`family`, `professions`, `places`).
- Removed duplicate `display: none` lines for the deleted row.
- Ikoma footer credit is now plain bold text (link removed — URL was unverified, removing avoids broken links). Restore the link later when the right URL is known.
- Stats line in header stays compact on very narrow viewports (≤360px) — slightly smaller font + tighter gap.

---

## v1.1.2 - 2026-05-18

### Fixed
- **Bank Learn views (Family / Professions / Places)** now use the exact same row markup as the Review tab: sans-serif English on left, large purple gradient Japanese with romaji italic underneath, optional speaker button on right. Looks identical to Review.
- **iOS status bar overlap fixed** — header now respects `env(safe-area-inset-top)` so the iPhone clock and signal icons no longer collide with the page header in PWA / Safari modes. Left/right safe-area insets respected too (landscape).
- Tapping a row in any Bank Learn view now speaks the Japanese word aloud (matches Review behaviour).

---

## v1.1.1 - 2026-05-18

### Changed
- Shukudai Learn tables now use Review-style typography: large purple gradient Japanese readings (19 px / weight 700), muted number labels, subtle row separators, more breathing room.
- "Drill" toggle label renamed to **Mode** (clearer).
- Irregular readings still highlighted yellow but rendered solid (no gradient) so they stand out against the gradient readings.

---

## v1.1.0 - 2026-05-18

### Added
- **Learn / Practice toggle inside every Shukudai sub-category**. Default is Learn so users study patterns BEFORE being drilled.
  - **Counters**: 13 reference tables (1-20). Irregular readings highlighted yellow. Each card has a "Practice ~X only" button to drill that single counter.
  - **Numbers**: rendaku rules table (300=さんびゃく, 600=ろっぴゃく, 800=はっぴゃく, 3000=さんぜん, 8000=はっせん).
  - **Money**: ¥/$/¢ tables with cent rendaku readings (1=いっセント, 8=はっセント, 10/20=じゅっ/にじゅっセント).
  - **Time**: hours 1-12 (irregular: 4, 7, 9) + minutes special readings + AM/PM rules.
  - **Dates**: months 1-12 + days of month 1-31 (1-10 + 14, 20, 24 all irregular).
  - **Family / Professions / Places**: scrollable reference list grouped by category.
- Per-category Learn/Practice preference persists per browser.
- Switching category always resets to Learn (so each new category invites study first).

### Changed
- Counters generator can be filtered to a single counter type via the "Practice ~X only" button in the Learn cards.

---

## v1.0.0 — 2026-05-18

First versioned release. Baseline for everything below.

**Content**
- 548 vocab items across Lessons 1–11 (Dai_Ka.pdf + Dai_Ka 11.pdf, including 会話 and 練習C phrases)
- 110 example sentences across Lessons 1–11
- 142 kana (hiragana + katakana, basic + dakuten/handakuten)
- 75 curated drill items in Shukudai (Family, Professions, Places)

**Modes / Categories**
- 📖 Review — scan vocab + sentences for selected lessons
- Flashcards — EN → JP recall with reveal + self-grade
- Multiple Choice — pick the right JP from 4 options
- Sentences — translate full sentences
- Dictation — listen (TTS) + type romaji/kana, or draw on canvas
- Hiragana — write the kana with finger on canvas
- Katakana — same for katakana
- 📚 Shukudai — drill generators (Numbers, Money, Time, Dates, Counters with 13 counter types incl. duration counters from L11) + curated banks (Family, Professions, Places)

**Smart features**
- Leitner spaced repetition with no-repeat deck cycling
- Per-lesson mastery % shown on lesson pills
- 🔥 Daily streak counter
- Quiz of the day (10 mixed-mode cards from selected lessons)
- Search across all vocab + sentences
- EN↔JP direction toggle for Flashcards/Sentences

**UI**
- Dark + light theme, auto-detects OS preference on first visit, manual toggle persists
- Sticky header, glass-blur panels, gradient text (with solid-colour fallback for non-WebKit browsers)
- Mobile: 2-column mode tabs, compact rows, safe-area insets, 44pt touch targets
- Desktop: wider container (1200/1320px on ≥1100/1400px), 3–4 column review grid, keyboard shortcuts modal (?), custom focus ring, stronger hover affordances

**Cross-browser**
- iOS Safari (primary): tested
- Android Chrome / Samsung Internet: voice loading with retries, hint banner if no Japanese voice installed, Pointer Events for canvas, gradient-text + backdrop-filter fallbacks

**Infrastructure**
- Single-file HTML deploys to GitHub Pages
- Data lives in `/data/*.json` (vocab, sentences, kana, shukudai, manifest)
- Build script (`build.py`) composes HTML from data + template
- Refresh playbook: drop a PDF → say "refresh" → I scan, extract, append, rebuild
- Stable per-card IDs so Leitner box history survives content updates

**Attribution**
- Content derived from Ikoma Language School Singapore curriculum
- Personal study aid, not affiliated with or endorsed by Ikoma

---

## Versioning conventions going forward

When you ask for new work, I'll bump the version per these rules:

- **PATCH** (e.g., 1.0.0 → 1.0.1): a tweak, fix, or copy-edit. Examples: "fix the Check button bug", "bump font size", "remove a category", "fix a typo in 3 sentences".
- **MINOR** (e.g., 1.0.0 → 1.1.0): new content or new feature. Examples: "add Lesson 12", "add a new drill type", "add a new mode".
- **MAJOR** (e.g., 1.0.0 → 2.0.0): something that changes how the app works. Examples: "switch to a different data shape", "rebuild the UI from scratch", "merge with another tool".

The app footer always shows the current version. Hover (or tap on mobile) to see the build date.
