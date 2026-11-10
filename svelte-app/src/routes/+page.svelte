<script lang="ts">
  import { base } from '$app/paths';
  import { getAllHSKLevels } from '$lib/data/hsk';
  const levels = getAllHSKLevels();
</script>

<svelte:head>
  <title>Học tiếng Trung HSK 1–5 | Smart Quiz</title>
  <meta name="description" content="Học từ vựng tiếng Trung HSK 1 đến HSK 5 với chữ Hán, pinyin, nghĩa tiếng Việt và bài luyện tập." />
</svelte:head>

<div class="hsk-home">
  <p class="eyebrow">SMART QUIZ · TIẾNG TRUNG</p>
  <h1>Học tiếng Trung theo cấp độ HSK</h1>
  <p class="intro">Chọn HSK 1, 2, 3, 4 hoặc 5 để học chữ Hán, pinyin và nghĩa tiếng Việt. Mỗi cấp độ đều có bài luyện tập.</p>
  <div class="level-grid">
    {#each levels as level}
      <a class="level-card" href="{base}/hsk?level={level.level}">
        <span class="level-name">HSK {level.level}</span>
        <span>{level.wordCount} từ vựng · {level.groupCount} nhóm</span>
        <span class="arrow">Bắt đầu học →</span>
      </a>
    {/each}
  </div>
  <a class="all-levels" href="{base}/hsk">Xem tất cả cấp độ HSK →</a>
</div>
<style>
  .hsk-home { max-width: 980px; margin: 0 auto; padding: clamp(28px,6vw,72px) 22px; }
  .eyebrow { font-size: .82rem; font-weight: 750; color: var(--color-primary); letter-spacing: .08em; }
  h1 { font-size: clamp(2rem,5vw,3.2rem); font-weight: 800; line-height: 1.15; margin: 12px 0; }
  .intro { max-width: 650px; color: var(--color-muted-foreground); line-height: 1.65; margin-bottom: 28px; }
  .level-grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(210px,1fr)); gap:16px; }
  .level-card { display:flex; flex-direction:column; gap:12px; border:1px solid var(--color-border); border-radius:16px; padding:22px; text-decoration:none; color:inherit; background:var(--color-card); transition:transform .15s,border-color .15s; }
  .level-card:hover { transform:translateY(-2px); border-color:var(--color-primary); }
  .level-name { font-size:1.65rem; font-weight:800; color:var(--color-primary); }
  .arrow { margin-top:auto; font-weight:700; }
  .all-levels { display:inline-block; margin-top:24px; color:var(--color-primary); font-weight:700; }
</style>
