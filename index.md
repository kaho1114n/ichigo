<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>いちご日記</title>
<meta name="theme-color" content="#2f5d3f">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Zen+Maru+Gothic:wght@400;500;700&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#f1f5ec;
  --surface:#ffffff;
  --ink:#1f2d24;
  --muted:#5b6a5f;
  --line:#d9e2d3;
  --berry:#d42a4c;
  --on-berry:#ffffff;
  --leaf:#2f5d3f;
  --on-leaf:#ffffff;
  --leaf-soft:#bfd8c4;
  --warm:#d9602f;
  --cold:#3b78b5;
  --seed:#e6b93a;
  color-scheme:light;
}
@media (prefers-color-scheme:dark){
  :root{
    --bg:#131a15;
    --surface:#1d2620;
    --ink:#e8efe6;
    --muted:#9bab9f;
    --line:#2e3b32;
    --berry:#ff6f89;
    --on-berry:#2a0a12;
    --leaf:#82c391;
    --on-leaf:#10200f;
    --leaf-soft:#35553c;
    --warm:#ff9360;
    --cold:#7db3e8;
    --seed:#e6c25a;
    color-scheme:dark;
  }
}
*{box-sizing:border-box}
[hidden]{display:none!important}
html{-webkit-text-size-adjust:100%}
body{
  margin:0;background:var(--bg);color:var(--ink);
  font-family:"Zen Maru Gothic","Hiragino Maru Gothic ProN","Hiragino Sans","Yu Gothic",Meiryo,sans-serif;
  font-size:16px;line-height:1.7;
}
button,input,select,textarea{font:inherit;color:inherit}
button{cursor:pointer}
:focus-visible{outline:3px solid var(--berry);outline-offset:2px;border-radius:6px}
.wrap{max-width:640px;margin:0 auto;padding:0 18px calc(120px + env(safe-area-inset-bottom))}

/* header */
.top{display:flex;align-items:center;justify-content:space-between;padding:18px 0 4px}
.top h1{margin:0;font-size:20px;font-weight:700;letter-spacing:.04em}
.ghost{background:none;border:1px solid var(--line);border-radius:999px;padding:6px 16px;font-size:14px;color:var(--muted)}
.ghost:hover{border-color:var(--muted)}
.banner{margin:10px 0 0;padding:10px 14px;border-radius:12px;background:color-mix(in srgb,var(--seed) 22%,var(--surface));font-size:13px;line-height:1.6}

/* hero */
.hero{padding:22px 0 10px}
.hero-name{margin:0;font-size:15px;color:var(--muted);font-weight:500}
.hero-days{margin:0;display:flex;align-items:baseline;gap:8px;line-height:1.1}
.hero-days .num{font-size:84px;font-weight:700;letter-spacing:-.02em}
.hero-days .unit{font-size:20px;color:var(--muted);font-weight:500}
.hero-sub{margin:2px 0 0;font-size:13px;color:var(--muted)}
.track{display:flex;list-style:none;margin:26px 0 8px;padding:0}
.track li{flex:1;position:relative;text-align:center;font-size:12px;color:var(--muted);padding-top:26px}
.track li::before{content:"";position:absolute;top:8px;left:-50%;width:100%;height:2px;background:var(--line)}
.track li:first-child::before{display:none}
.track li::after{content:"";position:absolute;top:0;left:50%;transform:translateX(-50%);width:18px;height:18px;border-radius:50%;background:var(--bg);border:2px solid var(--line)}
.track li.done::before,.track li.now::before{background:var(--leaf)}
.track li.done::after{background:var(--leaf);border-color:var(--leaf)}
.track li.now{color:var(--ink);font-weight:700}
.track li.now::after{background:var(--berry);border-color:var(--berry);box-shadow:0 0 0 6px color-mix(in srgb,var(--berry) 22%,transparent)}
.wx,.latest{margin:6px 0 0;font-size:14px}
.wx{color:var(--muted)}
.t-hot{color:var(--warm);font-weight:700}
.t-cold{color:var(--cold);font-weight:700}

/* tabs */
.tabs{display:flex;margin-top:18px;border-bottom:1px solid var(--line)}
.tabs button{flex:1;background:none;border:0;border-bottom:3px solid transparent;padding:12px 0 9px;font-size:15px;color:var(--muted);font-weight:500}
.tabs button[aria-selected="true"]{color:var(--ink);font-weight:700;border-bottom-color:var(--berry)}

/* entries */
.entries{list-style:none;margin:0;padding:0}
.entry{display:grid;grid-template-columns:58px 1fr;gap:12px;padding:20px 0;border-bottom:1px solid var(--line)}
.dcol{text-align:center;line-height:1.2}
.dcol b{display:block;font-size:30px;font-weight:700}
.dcol span{font-size:12px;color:var(--muted)}
.e-head{display:flex;flex-wrap:wrap;align-items:center;gap:8px}
.chip{display:inline-block;font-size:12px;line-height:1;padding:6px 10px;border-radius:999px;border:1px solid var(--line);color:var(--muted)}
.chip.stage{background:color-mix(in srgb,var(--berry) 14%,transparent);border-color:transparent;color:var(--ink);font-weight:700}
.chip.alert{border-color:var(--warm);color:var(--warm)}
.edit{margin-left:auto;background:none;border:0;font-size:13px;color:var(--muted);text-decoration:underline;padding:4px}
.e-line{margin:8px 0 0;font-size:14px;display:flex;flex-wrap:wrap;gap:4px 14px}
.e-line b{font-weight:700}
.e-memo{margin:8px 0 0;white-space:pre-wrap;overflow-wrap:anywhere}
.cares{display:flex;flex-wrap:wrap;gap:6px;margin-top:10px}
.photos{display:grid;grid-template-columns:repeat(3,1fr);gap:6px;margin-top:12px}
.ph{padding:0;border:0;background:var(--line);border-radius:10px;overflow:hidden;aspect-ratio:1;display:block}
.ph img{width:100%;height:100%;object-fit:cover;display:block}
.empty{padding:44px 12px;text-align:center;color:var(--muted)}
.empty p{margin:0 0 14px}

/* charts */
.chartbox{position:relative;height:270px;margin:18px 0 6px}
.charttitle{margin:26px 0 0;font-size:15px;font-weight:700}

/* gallery */
.gallery{display:grid;grid-template-columns:repeat(3,1fr);gap:6px;margin-top:18px}
.gallery .ph{position:relative}
.gallery .cap{position:absolute;left:6px;bottom:6px;font-size:11px;color:#fff;background:rgba(0,0,0,.55);padding:1px 7px;border-radius:999px}

/* fab */
.fab{
  position:fixed;left:50%;transform:translateX(-50%);
  bottom:calc(20px + env(safe-area-inset-bottom));
  background:var(--berry);color:var(--on-berry);border:0;border-radius:999px;
  padding:15px 28px;font-size:17px;font-weight:700;letter-spacing:.04em;
  box-shadow:0 8px 22px rgba(0,0,0,.25);
}
.fab:active{transform:translateX(-50%) scale(.97)}

/* dialogs */
dialog{
  border:0;padding:0;background:var(--surface);color:var(--ink);
  width:min(640px,100%);max-width:100%;max-height:92dvh;
  margin:auto auto 0;border-radius:22px 22px 0 0;
}
dialog::backdrop{background:rgba(10,15,12,.5)}
@media (min-width:700px){dialog{margin:auto;border-radius:22px}}
.sheet{display:flex;flex-direction:column;max-height:92dvh}
.sheet-head{display:flex;align-items:center;justify-content:space-between;padding:16px 20px 10px}
.sheet-head h2{margin:0;font-size:18px}
.sheet-body{overflow-y:auto;padding:4px 20px 16px;flex:1}
.sheet-foot{display:flex;gap:10px;padding:12px 20px calc(14px + env(safe-area-inset-bottom));border-top:1px solid var(--line)}
.btn{border:1px solid var(--line);background:none;border-radius:12px;padding:12px 18px;font-weight:700}
.btn.primary{flex:1;background:var(--berry);border-color:var(--berry);color:var(--on-berry)}
.btn.danger{color:var(--warm);border-color:var(--warm)}
.btn.small{padding:8px 14px;font-size:14px;font-weight:500}
.field{display:block;margin:14px 0 0}
.field>span{display:block;font-size:13px;color:var(--muted);margin-bottom:4px}
.field input,.field select,.field textarea{
  width:100%;background:var(--bg);border:1px solid var(--line);border-radius:10px;padding:10px 12px;font-size:16px;
}
.field textarea{min-height:92px;resize:vertical}
.row{display:grid;gap:10px}
.row.c2{grid-template-columns:1fr 1fr}
.row.c3{grid-template-columns:1fr 1fr 1fr}
.group{margin-top:22px;padding-top:6px;border-top:1px solid var(--line)}
.group>h3{margin:10px 0 0;font-size:14px;font-weight:700}
.hint{margin:6px 0 0;font-size:12px;color:var(--muted);line-height:1.6}
.chks{display:flex;flex-wrap:wrap;gap:8px;margin-top:8px}
.chk{position:relative}
.chk input{position:absolute;opacity:0;inset:0}
.chk span{display:inline-block;padding:8px 14px;border:1px solid var(--line);border-radius:999px;font-size:14px;color:var(--muted)}
.chk input:checked+span{background:var(--leaf);border-color:var(--leaf);color:var(--on-leaf);font-weight:700}
.chk input:focus-visible+span{outline:3px solid var(--berry);outline-offset:2px}
.pv{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-top:10px}
.pv div{position:relative;aspect-ratio:1;border-radius:10px;overflow:hidden;background:var(--line)}
.pv img{width:100%;height:100%;object-fit:cover}
.pv button{position:absolute;top:4px;right:4px;width:28px;height:28px;border-radius:50%;border:0;background:rgba(0,0,0,.65);color:#fff;font-size:16px;line-height:1}
.results{display:flex;flex-direction:column;gap:6px;margin-top:8px}
.results button{text-align:left;background:var(--bg);border:1px solid var(--line);border-radius:10px;padding:10px 12px}
.btnrow{display:flex;flex-wrap:wrap;gap:8px;margin-top:10px}
#lightbox{background:#000;color:#fff;border-radius:0;margin:auto;width:100%;height:100%;max-height:100dvh}
#lightbox .lb{display:flex;flex-direction:column;height:100%;padding:12px}
#lightbox img{flex:1;min-height:0;width:100%;object-fit:contain}
#lightbox p{margin:8px 0;text-align:center;font-size:14px}
#lightbox .btn{align-self:center;color:#fff;border-color:#555}
.toast{
  position:fixed;left:50%;bottom:calc(92px + env(safe-area-inset-bottom));transform:translateX(-50%);
  background:var(--ink);color:var(--bg);padding:10px 18px;border-radius:999px;font-size:14px;z-index:99;
  max-width:90vw;text-align:center;
}
@media (prefers-reduced-motion:reduce){*{transition:none!important;animation:none!important}}
</style>
</head>
<body>
<div class="wrap">
  <header class="top">
    <h1>いちご日記</h1>
    <button class="ghost" id="btnSettings" type="button">設定</button>
  </header>
  <div id="banner" class="banner" hidden></div>

  <section class="hero" id="hero" aria-live="polite"></section>

  <nav class="tabs" role="tablist" aria-label="表示の切り替え">
    <button type="button" role="tab" id="tab-log" data-tab="log" aria-selected="true">記録</button>
    <button type="button" role="tab" id="tab-chart" data-tab="chart" aria-selected="false">グラフ</button>
    <button type="button" role="tab" id="tab-photos" data-tab="photos" aria-selected="false">写真</button>
  </nav>

  <main>
    <section id="view-log" role="tabpanel" aria-labelledby="tab-log">
      <ol class="entries" id="list"></ol>
    </section>

    <section id="view-chart" role="tabpanel" aria-labelledby="tab-chart" hidden>
      <div id="chartEmpty" class="empty" hidden><p>グラフは記録が2件以上になると表示されます。</p></div>
      <div id="chartMsg" class="empty" hidden><p>グラフの読み込みに失敗しました。ネットワーク接続を確認してください。</p></div>
      <div id="chartWrap">
        <h2 class="charttitle">気温と草丈</h2>
        <div class="chartbox"><canvas id="chartTemp" aria-label="気温と草丈のグラフ" role="img"></canvas></div>
        <h2 class="charttitle">花・実・収穫の数</h2>
        <div class="chartbox"><canvas id="chartCount" aria-label="花と実と収穫数のグラフ" role="img"></canvas></div>
      </div>
    </section>

    <section id="view-photos" role="tabpanel" aria-labelledby="tab-photos" hidden>
      <div id="gallery" class="gallery"></div>
      <div id="galleryEmpty" class="empty" hidden><p>写真はまだありません。記録に写真を追加すると、ここに日付順で並びます。</p></div>
    </section>
  </main>
</div>

<button class="fab" id="fab" type="button">＋ 記録する</button>

<!-- 記録フォーム -->
<dialog id="entryDlg" aria-labelledby="entryTitle">
  <form id="entryForm" class="sheet">
    <div class="sheet-head">
      <h2 id="entryTitle">今日の記録</h2>
      <button type="button" class="ghost" id="entryClose">閉じる</button>
    </div>
    <div class="sheet-body">
      <div class="row c2">
        <label class="field"><span>日付</span><input type="date" id="f-date" required></label>
        <label class="field"><span>生育ステージ</span>
          <select id="f-stage">
            <option>植え付け</option><option>成長</option><option>開花</option><option>結実</option><option>収穫</option><option>その他</option>
          </select>
        </label>
      </div>

      <div class="group">
        <h3>気温・天気</h3>
        <div class="row c3">
          <label class="field"><span>最高(℃)</span><input type="number" id="f-tmax" step="0.1" inputmode="decimal"></label>
          <label class="field"><span>最低(℃)</span><input type="number" id="f-tmin" step="0.1" inputmode="decimal"></label>
          <label class="field"><span>降水(mm)</span><input type="number" id="f-rain" step="0.1" min="0" inputmode="decimal"></label>
        </div>
        <label class="field"><span>天気</span>
          <select id="f-weather"><option value="">未選択</option><option>晴れ</option><option>くもり</option><option>雨</option><option>雪</option><option>霧</option><option>雷雨</option></select>
        </label>
        <div class="btnrow">
          <button type="button" class="btn small" id="btnWx">天気から自動入力</button>
        </div>
        <p class="hint" id="wxStatus">設定で栽培場所を登録すると、日付に合わせた気温を自動で入れられます。手入力もできます。</p>
      </div>

      <div class="group">
        <h3>生育の様子</h3>
        <div class="row c3">
          <label class="field"><span>草丈(cm)</span><input type="number" id="f-height" step="0.1" min="0" inputmode="decimal"></label>
          <label class="field"><span>葉の数</span><input type="number" id="f-leaves" step="1" min="0" inputmode="numeric"></label>
          <label class="field"><span>花の数</span><input type="number" id="f-flowers" step="1" min="0" inputmode="numeric"></label>
        </div>
        <div class="row c2">
          <label class="field"><span>実の数</span><input type="number" id="f-fruits" step="1" min="0" inputmode="numeric"></label>
          <label class="field"><span>収穫した数</span><input type="number" id="f-harvest" step="1" min="0" inputmode="numeric"></label>
        </div>
      </div>

      <div class="group">
        <h3>お世話</h3>
        <div class="chks" id="f-cares"></div>
      </div>

      <div class="group">
        <label class="field"><span>メモ</span><textarea id="f-memo" placeholder="気づいたことを書いておきましょう"></textarea></label>
      </div>

      <div class="group">
        <h3>写真</h3>
        <div class="btnrow">
          <label class="btn small" for="f-photoinput" style="cursor:pointer">写真を追加</label>
          <input type="file" id="f-photoinput" accept="image/*" multiple hidden>
        </div>
        <div class="pv" id="f-photos"></div>
        <p class="hint" id="photoStatus">端末内に保存するため、長辺1024pxに縮小します。</p>
      </div>
    </div>
    <div class="sheet-foot">
      <button type="button" class="btn danger" id="entryDelete" hidden>削除</button>
      <button type="submit" class="btn primary">保存する</button>
    </div>
  </form>
</dialog>

<!-- 設定 -->
<dialog id="setDlg" aria-labelledby="setTitle">
  <div class="sheet">
    <div class="sheet-head">
      <h2 id="setTitle">設定</h2>
      <button type="button" class="ghost" id="setClose">閉じる</button>
    </div>
    <div class="sheet-body">
      <label class="field"><span>品種・株の名前</span><input type="text" id="s-variety" placeholder="例：章姫、あまおう、プランター1"></label>
      <label class="field"><span>植え付け日</span><input type="date" id="s-planted"></label>

      <div class="group">
        <h3>栽培場所（気温の自動取得に使います）</h3>
        <p class="hint" id="locText">未設定</p>
        <div class="row" style="grid-template-columns:1fr auto;gap:8px;margin-top:8px">
          <input type="text" id="s-place" placeholder="市区町村名で検索（例：札幌市）" style="background:var(--bg);border:1px solid var(--line);border-radius:10px;padding:10px 12px;font-size:16px;width:100%">
          <button type="button" class="btn small" id="btnSearch">検索</button>
        </div>
        <div class="btnrow"><button type="button" class="btn small" id="btnGeo">現在地を使う</button></div>
        <div class="results" id="placeResults"></div>
        <p class="hint">気温データは Open-Meteo（無料・APIキー不要）から取得します。位置情報はこの端末とOpen-Meteoへの問い合わせにのみ使われます。</p>
      </div>

      <div class="group">
        <h3>バックアップ</h3>
        <p class="hint">記録と写真はこのブラウザの中に保存されます。機種変更やブラウザのデータ削除に備えて、ときどき書き出してください。</p>
        <div class="btnrow">
          <button type="button" class="btn small" id="btnExport">書き出す</button>
          <label class="btn small" for="importInput" style="cursor:pointer">読み込む</label>
          <input type="file" id="importInput" accept="application/json,.json" hidden>
          <button type="button" class="btn small danger" id="btnWipe">すべて削除</button>
        </div>
      </div>
    </div>
    <div class="sheet-foot">
      <button type="button" class="btn primary" id="setSave">設定を保存する</button>
    </div>
  </div>
</dialog>

<!-- 写真拡大 -->
<dialog id="lightbox" aria-label="写真の拡大表示">
  <div class="lb">
    <img id="lbImg" alt="">
    <p id="lbCap"></p>
    <button type="button" class="btn" id="lbClose">閉じる</button>
  </div>
</dialog>

<div id="toast" class="toast" role="status" hidden></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
<script>
(() => {
'use strict';

/* ---------- 定数・ユーティリティ ---------- */
const STAGES = ['植え付け','成長','開花','結実','収穫'];
const CARES = ['水やり','肥料','摘花・摘果','ランナー整理','古葉取り','病害虫対策','日当たり調整'];
const $ = (s, r = document) => r.querySelector(s);
const esc = s => String(s ?? '').replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
const pad = n => String(n).padStart(2, '0');
const uid = () => Date.now().toString(36) + Math.random().toString(36).slice(2, 6);
const todayStr = () => { const d = new Date(); return `${d.getFullYear()}-${pad(d.getMonth()+1)}-${pad(d.getDate())}`; };
const parse = s => { const [y,m,d] = s.split('-').map(Number); return new Date(y, m-1, d); };
const daysBetween = (a, b) => Math.round((parse(b) - parse(a)) / 864e5);
const md = s => { const d = parse(s); return `${d.getMonth()+1}/${d.getDate()}`; };
const wd = s => '日月火水木金土'[parse(s).getDay()];
const num = v => (v === '' || v == null || isNaN(Number(v))) ? null : Number(v);
const byDateDesc = (a, b) => b.date.localeCompare(a.date) || b.id.localeCompare(a.id);
const byDateAsc = (a, b) => a.date.localeCompare(b.date) || a.id.localeCompare(b.id);

let toastTimer;
function toast(msg) {
  const t = $('#toast');
  t.textContent = msg; t.hidden = false;
  clearTimeout(toastTimer);
  toastTimer = setTimeout(() => { t.hidden = true; }, 2600);
}

/* ---------- 保存（IndexedDB。使えない環境ではメモリに退避） ---------- */
const Store = (() => {
  let db = null;
  let persistent = false;
  const mem = { profile: {}, entries: new Map() };

  async function init() {
    try {
      db = await new Promise((resolve, reject) => {
        if (!('indexedDB' in window)) return reject(new Error('no indexedDB'));
        const req = indexedDB.open('strawberry-diary', 1);
        req.onupgradeneeded = () => {
          req.result.createObjectStore('entries', { keyPath: 'id' });
          req.result.createObjectStore('meta');
        };
        req.onsuccess = () => resolve(req.result);
        req.onerror = () => reject(req.error);
        req.onblocked = () => reject(new Error('blocked'));
      });
      persistent = true;
      if (navigator.storage && navigator.storage.persist) navigator.storage.persist().catch(() => {});
    } catch (e) {
      db = null; persistent = false;
    }
  }
  const run = (store, mode, fn) => new Promise((resolve, reject) => {
    const t = db.transaction(store, mode);
    const req = fn(t.objectStore(store));
    t.oncomplete = () => resolve(req ? req.result : undefined);
    t.onerror = () => reject(t.error);
    t.onabort = () => reject(t.error);
  });

  return {
    init,
    get persistent() { return persistent; },
    async getProfile() { return persistent ? ((await run('meta','readonly', s => s.get('profile'))) || {}) : mem.profile; },
    async setProfile(p) { if (persistent) await run('meta','readwrite', s => s.put(p, 'profile')); else mem.profile = p; },
    async allEntries() { return persistent ? await run('entries','readonly', s => s.getAll()) : [...mem.entries.values()]; },
    async putEntry(e) { if (persistent) await run('entries','readwrite', s => s.put(e)); else mem.entries.set(e.id, e); },
    async deleteEntry(id) { if (persistent) await run('entries','readwrite', s => s.delete(id)); else mem.entries.delete(id); },
    async clearAll() {
      if (persistent) { await run('entries','readwrite', s => s.clear()); await run('meta','readwrite', s => s.clear()); }
      else { mem.entries.clear(); mem.profile = {}; }
    }
  };
})();

/* ---------- 気温（Open-Meteo） ---------- */
function wxLabel(c) {
  if (c == null) return '';
  if (c <= 1) return '晴れ';
  if (c <= 3) return 'くもり';
  if (c <= 48) return '霧';
  if (c <= 67) return '雨';
  if (c <= 77) return '雪';
  if (c <= 82) return '雨';
  if (c <= 86) return '雪';
  return '雷雨';
}
async function fetchDaily(lat, lon, date) {
  const diff = daysBetween(date, todayStr());
  if (diff < -15) throw new Error('2週間より先の日付は取得できません');
  const bases = diff > 85
    ? ['https://archive-api.open-meteo.com/v1/archive']
    : ['https://api.open-meteo.com/v1/forecast', 'https://archive-api.open-meteo.com/v1/archive'];
  let lastErr = new Error('データがありません');
  for (const base of bases) {
    try {
      const url = `${base}?latitude=${lat}&longitude=${lon}&start_date=${date}&end_date=${date}` +
        `&daily=temperature_2m_max,temperature_2m_min,precipitation_sum,weather_code&timezone=auto`;
      const res = await fetch(url);
      if (!res.ok) throw new Error('取得に失敗しました');
      const j = await res.json();
      const d = j.daily;
      if (d && d.temperature_2m_max && d.temperature_2m_max[0] != null) {
        return {
          tmax: Math.round(d.temperature_2m_max[0] * 10) / 10,
          tmin: Math.round(d.temperature_2m_min[0] * 10) / 10,
          rain: d.precipitation_sum ? d.precipitation_sum[0] : null,
          weather: wxLabel(d.weather_code ? d.weather_code[0] : null)
        };
      }
    } catch (e) { lastErr = e; }
  }
  throw lastErr;
}

/* ---------- 画像の縮小 ---------- */
function fileToDataURL(file, max = 1024, quality = 0.7) {
  return new Promise((resolve, reject) => {
    const url = URL.createObjectURL(file);
    const img = new Image();
    img.onload = () => {
      const s = Math.min(1, max / Math.max(img.width, img.height));
      const c = document.createElement('canvas');
      c.width = Math.round(img.width * s); c.height = Math.round(img.height * s);
      c.getContext('2d').drawImage(img, 0, 0, c.width, c.height);
      URL.revokeObjectURL(url);
      resolve(c.toDataURL('image/jpeg', quality));
    };
    img.onerror = () => { URL.revokeObjectURL(url); reject(new Error('画像を読み込めませんでした')); };
    img.src = url;
  });
}

/* ---------- 状態 ---------- */
const S = { profile: {}, entries: [], tab: 'log', lbList: [] };
let charts = [];
let todayWx = null;

/* ---------- 描画：ヒーロー ---------- */
function renderHero() {
  const p = S.profile, t = todayStr();
  const sorted = [...S.entries].sort(byDateDesc);
  const latest = sorted[0];
  const stageEntry = sorted.find(e => STAGES.includes(e.stage));
  const cur = stageEntry ? STAGES.indexOf(stageEntry.stage) : -1;

  let numTxt, unit, sub;
  if (p.planted) {
    const d = daysBetween(p.planted, t);
    if (d >= 0) { numTxt = d + 1; unit = '日目'; sub = `${p.planted.replace(/-/g,'/')} に植え付け`; }
    else { numTxt = -d; unit = '日後に植え付け'; sub = p.planted.replace(/-/g,'/'); }
  } else {
    numTxt = S.entries.length; unit = '件の記録'; sub = '設定で植え付け日を入れると、育った日数が表示されます';
  }

  let latestTxt = '';
  if (latest) {
    const bits = [];
    if (latest.height != null) bits.push(`草丈 <b>${latest.height}</b>cm`);
    if (latest.flowers != null) bits.push(`花 <b>${latest.flowers}</b>`);
    if (latest.fruits != null) bits.push(`実 <b>${latest.fruits}</b>`);
    latestTxt = `<p class="latest">${md(latest.date)}の記録　${bits.join('　') || 'メモのみ'}</p>`;
  }

  $('#hero').innerHTML = `
    <p class="hero-name">${esc(p.variety || 'いちご')}</p>
    <p class="hero-days"><span class="num">${numTxt}</span><span class="unit">${unit}</span></p>
    <p class="hero-sub">${esc(sub)}</p>
    <ol class="track" aria-label="生育ステージ">
      ${STAGES.map((s, i) => `<li class="${i < cur ? 'done' : i === cur ? 'now' : ''}"${i === cur ? ' aria-current="step"' : ''}>${s}</li>`).join('')}
    </ol>
    <p class="wx" id="todayWx">${todayWxText()}</p>
    ${latestTxt}`;
}
function todayWxText() {
  if (!S.profile.lat) return '設定で栽培場所を入れると、今日の気温がここに出ます';
  if (!todayWx) return '今日の気温を取得中…';
  if (todayWx === 'error') return '';
  const w = todayWx;
  return `今日の天気　${esc(w.weather)}　<span class="t-hot">最高 ${w.tmax}°</span>　<span class="t-cold">最低 ${w.tmin}°</span>`;
}
async function loadTodayWx() {
  if (!S.profile.lat) { todayWx = null; return; }
  todayWx = null;
  try { todayWx = await fetchDaily(S.profile.lat, S.profile.lon, todayStr()); }
  catch (e) { todayWx = 'error'; }
  const el = $('#todayWx'); if (el) el.innerHTML = todayWxText();
}

/* ---------- 描画：記録リスト ---------- */
function entryHTML(e) {
  const d = parse(e.date);
  const temps = [];
  if (e.tmax != null) temps.push(`<span class="t-hot">最高 ${e.tmax}°</span>`);
  if (e.tmin != null) temps.push(`<span class="t-cold">最低 ${e.tmin}°</span>`);
  if (e.weather) temps.push(`<span>${esc(e.weather)}</span>`);
  if (e.rain != null && e.rain > 0) temps.push(`<span>降水 ${e.rain}mm</span>`);
  const metrics = [['草丈', e.height, 'cm'], ['葉', e.leaves, '枚'], ['花', e.flowers, '輪'], ['実', e.fruits, '個'], ['収穫', e.harvest, '個']]
    .filter(m => m[1] != null).map(m => `<span>${m[0]} <b>${m[1]}</b>${m[2]}</span>`);
  const alerts = [];
  if (e.tmin != null && e.tmin <= 0) alerts.push('寒さ注意');
  if (e.tmax != null && e.tmax >= 30) alerts.push('暑さ注意');
  const photos = (e.photos || []).map((p, i) =>
    `<button type="button" class="ph" data-eid="${esc(e.id)}" data-i="${i}" aria-label="写真${i+1}を拡大"><img src="${p}" alt="${md(e.date)}の写真${i+1}" loading="lazy"></button>`).join('');
  return `
  <li class="entry">
    <div class="dcol"><b>${d.getDate()}</b><span>${d.getMonth()+1}月 ${wd(e.date)}</span></div>
    <div>
      <div class="e-head">
        <span class="chip stage">${esc(e.stage || '記録')}</span>
        ${alerts.map(a => `<span class="chip alert">${a}</span>`).join('')}
        <button type="button" class="edit" data-edit="${esc(e.id)}">編集</button>
      </div>
      ${temps.length ? `<p class="e-line">${temps.join('')}</p>` : ''}
      ${metrics.length ? `<p class="e-line">${metrics.join('')}</p>` : ''}
      ${e.memo ? `<p class="e-memo">${esc(e.memo)}</p>` : ''}
      ${(e.cares || []).length ? `<div class="cares">${e.cares.map(c => `<span class="chip">${esc(c)}</span>`).join('')}</div>` : ''}
      ${photos ? `<div class="photos">${photos}</div>` : ''}
    </div>
  </li>`;
}
function renderLog() {
  const list = [...S.entries].sort(byDateDesc);
  $('#list').innerHTML = list.length
    ? list.map(entryHTML).join('')
    : `<li class="empty"><p>まだ記録がありません。<br>今日のいちごの様子を残してみましょう。</p><button class="btn small" type="button" data-act="new">最初の記録を書く</button></li>`;
}

/* ---------- 描画：写真 ---------- */
function renderGallery() {
  const items = [];
  [...S.entries].sort(byDateDesc).forEach(e => (e.photos || []).forEach((p, i) => items.push({ src: p, date: e.date, memo: e.memo, eid: e.id, i })));
  S.lbList = items;
  $('#gallery').innerHTML = items.map((it, k) =>
    `<button type="button" class="ph" data-g="${k}" aria-label="${md(it.date)}の写真を拡大"><img src="${it.src}" alt="${md(it.date)}の写真" loading="lazy"><span class="cap">${md(it.date)}</span></button>`).join('');
  $('#galleryEmpty').hidden = items.length > 0;
}
function openLightbox(src, date, memo) {
  $('#lbImg').src = src;
  $('#lbImg').alt = `${md(date)}の写真`;
  $('#lbCap').textContent = `${date.replace(/-/g,'/')}${memo ? '　' + memo.slice(0, 40) : ''}`;
  $('#lightbox').showModal();
}

/* ---------- 描画：グラフ ---------- */
function drawCharts() {
  charts.forEach(c => c.destroy()); charts = [];
  const list = [...S.entries].sort(byDateAsc);
  const few = list.length < 2;
  $('#chartEmpty').hidden = !few;
  $('#chartWrap').hidden = few;
  $('#chartMsg').hidden = true;
  if (few) return;
  if (!window.Chart) { $('#chartWrap').hidden = true; $('#chartMsg').hidden = false; return; }

  const css = getComputedStyle(document.documentElement);
  const c = n => css.getPropertyValue(n).trim();
  Chart.defaults.font.family = getComputedStyle(document.body).fontFamily;
  Chart.defaults.color = c('--muted');
  const labels = list.map(e => md(e.date));
  const grid = { color: c('--line') };

  charts.push(new Chart($('#chartTemp'), {
    type: 'line',
    data: { labels, datasets: [
      { label: '最高気温(℃)', data: list.map(e => e.tmax), borderColor: c('--warm'), backgroundColor: c('--warm'), tension: .3, spanGaps: true, pointRadius: 3, order: 1 },
      { label: '最低気温(℃)', data: list.map(e => e.tmin), borderColor: c('--cold'), backgroundColor: c('--cold'), tension: .3, spanGaps: true, pointRadius: 3, order: 1 },
      { label: '草丈(cm)', type: 'bar', yAxisID: 'y2', data: list.map(e => e.height), backgroundColor: c('--leaf-soft'), borderRadius: 4, order: 2 }
    ]},
    options: {
      responsive: true, maintainAspectRatio: false,
      interaction: { mode: 'index', intersect: false },
      scales: {
        y: { title: { display: true, text: '℃' }, grid },
        y2: { position: 'right', beginAtZero: true, grid: { display: false }, title: { display: true, text: 'cm' } },
        x: { grid: { display: false } }
      },
      plugins: { legend: { position: 'bottom' } }
    }
  }));

  charts.push(new Chart($('#chartCount'), {
    type: 'line',
    data: { labels, datasets: [
      { label: '花', data: list.map(e => e.flowers), borderColor: c('--seed'), backgroundColor: c('--seed'), tension: .25, spanGaps: true, pointRadius: 3 },
      { label: '実', data: list.map(e => e.fruits), borderColor: c('--berry'), backgroundColor: c('--berry'), tension: .25, spanGaps: true, pointRadius: 3 },
      { label: '収穫', data: list.map(e => e.harvest), borderColor: c('--leaf'), backgroundColor: c('--leaf'), tension: .25, spanGaps: true, pointRadius: 3 }
    ]},
    options: {
      responsive: true, maintainAspectRatio: false,
      interaction: { mode: 'index', intersect: false },
      scales: { y: { beginAtZero: true, ticks: { precision: 0 }, grid }, x: { grid: { display: false } } },
      plugins: { legend: { position: 'bottom' } }
    }
  }));
}

/* ---------- タブ ---------- */
function setTab(name) {
  S.tab = name;
  document.querySelectorAll('.tabs button').forEach(b => b.setAttribute('aria-selected', String(b.dataset.tab === name)));
  ['log','chart','photos'].forEach(n => { $('#view-' + n).hidden = n !== name; });
  if (name === 'chart') drawCharts();
  if (name === 'photos') renderGallery();
}
function renderAll() {
  renderHero(); renderLog();
  if (S.tab === 'chart') drawCharts();
  if (S.tab === 'photos') renderGallery();
}

/* ---------- 記録フォーム ---------- */
let draft = null, isNew = true, tempDirty = false;

function buildCareChips() {
  $('#f-cares').innerHTML = CARES.map((c, i) =>
    `<label class="chk"><input type="checkbox" value="${esc(c)}" id="care-${i}"><span>${esc(c)}</span></label>`).join('');
}
function renderPreviews() {
  $('#f-photos').innerHTML = draft.photos.map((p, i) =>
    `<div><img src="${p}" alt="追加した写真${i+1}"><button type="button" data-rm="${i}" aria-label="写真${i+1}を外す">×</button></div>`).join('');
}
function setWxStatus(msg) { $('#wxStatus').textContent = msg; }

function openEntry(id) {
  const found = id ? S.entries.find(x => x.id === id) : null;
  isNew = !found;
  const last = [...S.entries].sort(byDateDesc)[0];
  draft = found ? JSON.parse(JSON.stringify(found)) : { id: uid(), date: todayStr(), stage: (last && last.stage) || '成長', cares: [], photos: [] };
  draft.photos = draft.photos || [];
  tempDirty = !!found && (found.tmax != null || found.tmin != null);

  $('#entryTitle').textContent = found ? '記録を編集' : '今日の記録';
  $('#f-date').value = draft.date;
  $('#f-stage').value = draft.stage || '成長';
  ['tmax','tmin','rain','height','leaves','flowers','fruits','harvest'].forEach(k => { $('#f-' + k).value = draft[k] ?? ''; });
  $('#f-weather').value = draft.weather || '';
  $('#f-memo').value = draft.memo || '';
  document.querySelectorAll('#f-cares input').forEach(i => { i.checked = (draft.cares || []).includes(i.value); });
  $('#entryDelete').hidden = !found;
  $('#photoStatus').textContent = '端末内に保存するため、長辺1024pxに縮小します。';
  setWxStatus(S.profile.lat ? '日付に合わせて気温を自動入力できます。手入力で直してもOKです。' : '設定で栽培場所を登録すると、日付に合わせた気温を自動で入れられます。手入力もできます。');
  renderPreviews();
  $('#entryDlg').showModal();
  if (isNew && S.profile.lat) autoWeather();
}

async function autoWeather(force) {
  if (!S.profile.lat) { setWxStatus('先に「設定」で栽培場所を登録してください。'); return; }
  const date = $('#f-date').value;
  if (!date) return;
  setWxStatus('気温を取得中…');
  try {
    const w = await fetchDaily(S.profile.lat, S.profile.lon, date);
    if ($('#f-date').value !== date) return;
    $('#f-tmax').value = w.tmax; $('#f-tmin').value = w.tmin;
    $('#f-rain').value = w.rain ?? '';
    $('#f-weather').value = w.weather || '';
    tempDirty = false;
    setWxStatus(`${date.replace(/-/g,'/')} の気温を入力しました（Open-Meteo）。`);
  } catch (e) {
    setWxStatus(`自動取得できませんでした（${e.message}）。手入力してください。`);
  }
}

async function saveEntry(ev) {
  ev.preventDefault();
  const date = $('#f-date').value;
  if (!date) { toast('日付を入れてください'); return; }
  const e = {
    id: draft.id, date,
    stage: $('#f-stage').value,
    tmax: num($('#f-tmax').value), tmin: num($('#f-tmin').value), rain: num($('#f-rain').value),
    weather: $('#f-weather').value,
    height: num($('#f-height').value), leaves: num($('#f-leaves').value),
    flowers: num($('#f-flowers').value), fruits: num($('#f-fruits').value), harvest: num($('#f-harvest').value),
    cares: [...document.querySelectorAll('#f-cares input:checked')].map(i => i.value),
    memo: $('#f-memo').value.trim(),
    photos: draft.photos
  };
  try {
    await Store.putEntry(e);
  } catch (err) {
    toast('保存できませんでした。写真が大きすぎるか、容量が足りない可能性があります。'); return;
  }
  const idx = S.entries.findIndex(x => x.id === e.id);
  if (idx >= 0) S.entries[idx] = e; else S.entries.push(e);
  $('#entryDlg').close();
  renderAll();
  toast('保存しました');
}

async function deleteEntry() {
  if (!confirm('この記録を削除しますか？写真も消えます。')) return;
  await Store.deleteEntry(draft.id);
  S.entries = S.entries.filter(x => x.id !== draft.id);
  $('#entryDlg').close();
  renderAll();
  toast('削除しました');
}

async function addPhotos(files) {
  const list = [...files];
  if (!list.length) return;
  $('#photoStatus').textContent = `写真を処理中… (${list.length}枚)`;
  let ok = 0;
  for (const f of list) {
    try { draft.photos.push(await fileToDataURL(f)); ok++; }
    catch (e) { toast(e.message); }
  }
  renderPreviews();
  $('#photoStatus').textContent = ok ? `${ok}枚を追加しました。保存すると反映されます。` : '写真を追加できませんでした。';
}

/* ---------- 設定 ---------- */
let pendingLoc = null;
function locLabel() {
  return pendingLoc ? `${pendingLoc.name || '指定した場所'}（緯度 ${pendingLoc.lat} / 経度 ${pendingLoc.lon}）` : '未設定';
}
function openSettings() {
  $('#s-variety').value = S.profile.variety || '';
  $('#s-planted').value = S.profile.planted || '';
  pendingLoc = S.profile.lat ? { lat: S.profile.lat, lon: S.profile.lon, name: S.profile.place } : null;
  $('#locText').textContent = locLabel();
  $('#placeResults').innerHTML = '';
  $('#s-place').value = '';
  $('#setDlg').showModal();
}
async function searchPlace() {
  const q = $('#s-place').value.trim();
  if (!q) return;
  const box = $('#placeResults');
  box.innerHTML = '<p class="hint">検索中…</p>';
  try {
    const res = await fetch(`https://geocoding-api.open-meteo.com/v1/search?name=${encodeURIComponent(q)}&count=5&language=ja`);
    const j = await res.json();
    if (!j.results || !j.results.length) { box.innerHTML = '<p class="hint">見つかりませんでした。別の表記で試してください。</p>'; return; }
    box.innerHTML = j.results.map((r, i) =>
      `<button type="button" data-pick="${i}">${esc([r.name, r.admin1, r.country].filter(Boolean).join(' / '))}</button>`).join('');
    box._results = j.results;
  } catch (e) {
    box.innerHTML = '<p class="hint">検索できませんでした。ネットワークを確認してください。</p>';
  }
}
function pickPlace(r) {
  pendingLoc = { lat: Math.round(r.latitude * 100) / 100, lon: Math.round(r.longitude * 100) / 100, name: [r.name, r.admin1].filter(Boolean).join(' ') };
  $('#locText').textContent = locLabel();
  $('#placeResults').innerHTML = '';
}
function useGeo() {
  if (!navigator.geolocation) { toast('この端末では位置情報を使えません'); return; }
  $('#locText').textContent = '現在地を取得中…';
  navigator.geolocation.getCurrentPosition(
    pos => {
      pendingLoc = { lat: Math.round(pos.coords.latitude * 100) / 100, lon: Math.round(pos.coords.longitude * 100) / 100, name: '現在地' };
      $('#locText').textContent = locLabel();
    },
    () => { $('#locText').textContent = locLabel(); toast('現在地を取得できませんでした。市区町村名で検索してください'); },
    { timeout: 10000 }
  );
}
async function saveSettings() {
  const p = {
    variety: $('#s-variety').value.trim(),
    planted: $('#s-planted').value || '',
    lat: pendingLoc ? pendingLoc.lat : null,
    lon: pendingLoc ? pendingLoc.lon : null,
    place: pendingLoc ? pendingLoc.name : ''
  };
  await Store.setProfile(p);
  S.profile = p;
  $('#setDlg').close();
  renderHero();
  loadTodayWx();
  toast('設定を保存しました');
}

/* ---------- バックアップ ---------- */
function exportData() {
  const data = { app: 'strawberry-diary', version: 1, exportedAt: new Date().toISOString(), profile: S.profile, entries: S.entries };
  const blob = new Blob([JSON.stringify(data)], { type: 'application/json' });
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = `strawberry-diary-${todayStr()}.json`;
  document.body.appendChild(a); a.click(); a.remove();
  setTimeout(() => URL.revokeObjectURL(a.href), 1000);
  toast('書き出しました');
}
async function importData(file) {
  try {
    const j = JSON.parse(await file.text());
    if (!j || !Array.isArray(j.entries)) throw new Error('形式が違います');
    for (const e of j.entries) {
      if (!e.id || !e.date) continue;
      await Store.putEntry(e);
      const i = S.entries.findIndex(x => x.id === e.id);
      if (i >= 0) S.entries[i] = e; else S.entries.push(e);
    }
    if (j.profile && typeof j.profile === 'object') { await Store.setProfile(j.profile); S.profile = j.profile; }
    renderAll(); loadTodayWx();
    $('#setDlg').close();
    toast(`${j.entries.length}件を読み込みました`);
  } catch (e) {
    toast('読み込めませんでした：' + e.message);
  }
}
async function wipe() {
  if (!confirm('記録・写真・設定をすべて削除します。元に戻せません。よろしいですか？')) return;
  await Store.clearAll();
  S.entries = []; S.profile = {}; todayWx = null;
  $('#setDlg').close();
  renderAll();
  toast('すべて削除しました');
}

/* ---------- イベント ---------- */
function bind() {
  $('#fab').addEventListener('click', () => openEntry());
  $('#btnSettings').addEventListener('click', openSettings);
  document.querySelectorAll('.tabs button').forEach(b => b.addEventListener('click', () => setTab(b.dataset.tab)));

  $('#list').addEventListener('click', ev => {
    const edit = ev.target.closest('[data-edit]');
    if (edit) return openEntry(edit.dataset.edit);
    if (ev.target.closest('[data-act="new"]')) return openEntry();
    const ph = ev.target.closest('.ph');
    if (ph) {
      const e = S.entries.find(x => x.id === ph.dataset.eid);
      if (e) openLightbox(e.photos[Number(ph.dataset.i)], e.date, e.memo);
    }
  });
  $('#gallery').addEventListener('click', ev => {
    const b = ev.target.closest('[data-g]');
    if (!b) return;
    const it = S.lbList[Number(b.dataset.g)];
    if (it) openLightbox(it.src, it.date, it.memo);
  });
  $('#lbClose').addEventListener('click', () => $('#lightbox').close());
  $('#lightbox').addEventListener('click', ev => { if (ev.target === $('#lightbox')) $('#lightbox').close(); });

  $('#entryForm').addEventListener('submit', saveEntry);
  $('#entryClose').addEventListener('click', () => $('#entryDlg').close());
  $('#entryDelete').addEventListener('click', deleteEntry);
  $('#btnWx').addEventListener('click', () => autoWeather(true));
  $('#f-date').addEventListener('change', () => { if (!tempDirty) autoWeather(); });
  ['f-tmax','f-tmin'].forEach(id => $('#' + id).addEventListener('input', () => { tempDirty = true; }));
  $('#f-photoinput').addEventListener('change', async ev => { await addPhotos(ev.target.files); ev.target.value = ''; });
  $('#f-photos').addEventListener('click', ev => {
    const b = ev.target.closest('[data-rm]');
    if (!b) return;
    draft.photos.splice(Number(b.dataset.rm), 1);
    renderPreviews();
  });

  $('#setClose').addEventListener('click', () => $('#setDlg').close());
  $('#setSave').addEventListener('click', saveSettings);
  $('#btnSearch').addEventListener('click', searchPlace);
  $('#s-place').addEventListener('keydown', ev => { if (ev.key === 'Enter') { ev.preventDefault(); searchPlace(); } });
  $('#btnGeo').addEventListener('click', useGeo);
  $('#placeResults').addEventListener('click', ev => {
    const b = ev.target.closest('[data-pick]');
    if (b) pickPlace($('#placeResults')._results[Number(b.dataset.pick)]);
  });
  $('#btnExport').addEventListener('click', exportData);
  $('#importInput').addEventListener('change', async ev => { const f = ev.target.files[0]; if (f) await importData(f); ev.target.value = ''; });
  $('#btnWipe').addEventListener('click', wipe);

  window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', () => { if (S.tab === 'chart') drawCharts(); });
}

/* ---------- 起動 ---------- */
(async function boot() {
  buildCareChips();
  bind();
  await Store.init();
  try {
    S.profile = await Store.getProfile();
    S.entries = await Store.allEntries();
  } catch (e) { S.profile = {}; S.entries = []; }
  if (!Store.persistent) {
    const b = $('#banner');
    b.hidden = false;
    b.textContent = 'この環境ではブラウザへの保存が使えないため、ページを閉じると記録が消えます。GitHub Pagesなど通常のブラウザで開くと端末に保存されます。';
  }
  renderAll();
  loadTodayWx();
})();
})();
</script>
</body>
</html>
