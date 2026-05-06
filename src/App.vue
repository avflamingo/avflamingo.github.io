<script setup lang="ts">
import { showcaseExamples } from './showcaseExamples'

const navLinks = [
  { label: 'Benchmarks', href: '#benchmarks', external: false, primary: true },
  { label: 'Examples', href: '#examples', external: false, primary: false },
  { label: 'Architecture', href: '#architecture', external: false, primary: false },
  { label: 'Data', href: '#data', external: false, primary: false },
]

const heroStats = [
  { value: 'Audio + video', label: 'joint understanding' },
  { value: '15 min', label: 'long-video training' },
  { value: 'approx. 7M', label: 'caption and QA instances' },
  { value: '15+', label: 'benchmark families' },
]

const featureCards = [
  {
    title: 'Joint audio-visual reasoning',
    detail:
      'AVF reasons across speech, sounds, music, images, and video frames instead of treating audio and visuals as separate late-fused evidence.',
  },
  {
    title: 'Temporal interleaving',
    detail:
      'Synchronized visual and audio chunks are interleaved along time and enriched with Constrained Rotary Time Embeddings before the language model.',
  },
  {
    title: 'Long and complex videos',
    detail:
      'Training moves from short-context skills into long-form captioning, event alignment, temporal QA, and long-context video reasoning up to 15 minutes.',
  },
  {
    title: 'Timestamp-grounded reasoning',
    detail:
      'Temporal Audio-Visual Interleaved Chain-of-Thought grounds intermediate reasoning to timestamps across audio and visual evidence.',
  },
]

const architectureBlocks = [
  {
    title: 'SigLIP vision tower',
    detail:
      'Images and video frames are encoded with SigLIP and Dynamic-S2 preprocessing to retain high-resolution visual detail with compact tokens.',
  },
  {
    title: 'AF-Whisper audio tower',
    detail:
      'Audio is resampled to 16 kHz, converted to 128-bin log-mel features, and processed in 30-second windows for long-form inputs.',
  },
  {
    title: 'Cross-modal alignment',
    detail:
      'Projected visual and audio embeddings are grouped by timestamp, interleaved, and passed through rotary time embedding for temporal structure.',
  },
  {
    title: 'Qwen2.5-7B backbone',
    detail:
      'A decoder-only language model receives the fused multimodal prefix plus the user prompt and generates text responses, with optional voice output.',
  },
]

const benchmarks = [
  {
    area: 'Omni',
    benchmark: 'WorldSense',
    baseline: 'OmniVinci 48.2',
    metric: 'ACC up',
    result: '50.3 / 51.6',
    variant: 'Instruct / Think',
  },
  {
    area: 'Omni',
    benchmark: 'DailyOmni',
    baseline: 'OmniVinci 66.5',
    metric: 'ACC up',
    result: '72.4 / 73.9',
    variant: 'Instruct / Think',
  },
  {
    area: 'Omni',
    benchmark: 'OmniBench',
    baseline: 'Gemini 1.5 Pro 47.6',
    metric: 'ACC up',
    result: '48.5 / 50.6',
    variant: 'Instruct / Think',
  },
  {
    area: 'Omni',
    benchmark: 'MMOU',
    baseline: 'Gemini 2.5 Pro 64.2',
    metric: 'ACC up',
    result: '56.9 / 60.2',
    variant: 'Instruct / Think',
  },
  {
    area: 'Omni',
    benchmark: 'AVHBench',
    baseline: 'Gemini 2.0 Flash 83.3 | 63.3',
    metric: 'ACC up',
    result: '77.0 | 81.1 / 79.0 | 85.9',
    variant: 'A->V | V->A, Instruct / Think',
  },
  {
    area: 'Audio',
    benchmark: 'MMAR',
    baseline: 'OmniVinci 58.4',
    metric: 'ACC up',
    result: '60.1',
    variant: 'AVF-Instruct',
  },
  {
    area: 'Audio',
    benchmark: 'MMSU',
    baseline: 'Gemini 1.5 Pro 60.7',
    metric: 'ACC up',
    result: '61.5',
    variant: 'AVF-Instruct',
  },
  {
    area: 'Audio',
    benchmark: 'MMAU-v05.15.25',
    baseline: 'Audio Flamingo 3 72.42',
    metric: 'ACC up',
    result: '77.97 | 73.17 | 69.33 | 73.49',
    variant: 'sound | music | speech | avg',
  },
  {
    area: 'Audio',
    benchmark: 'CMM Hallucination',
    baseline: 'Gemini 2.5 Pro 82.0',
    metric: 'ACC up',
    result: '86.7',
    variant: 'AVF-Instruct',
  },
  {
    area: 'Video',
    benchmark: 'Video-MME',
    baseline: 'OmniVinci 67.3 | 68.6',
    metric: 'ACC up',
    result: '70.7 | 71.2',
    variant: 'without | with subtitles',
  },
  {
    area: 'Video',
    benchmark: 'LongVideoBench',
    baseline: 'OmniVinci 62.0',
    metric: 'ACC up',
    result: '60.1',
    variant: 'AVF-Instruct',
  },
  {
    area: 'Video',
    benchmark: 'MVHBench',
    baseline: 'OmniVinci 70.6',
    metric: 'ACC up',
    result: '71.7',
    variant: 'AVF-Instruct',
  },
  {
    area: 'Speech',
    benchmark: 'LibriSpeech',
    baseline: 'Phi-4-mm | Qwen2.5-O: 1.67 | 3.4',
    metric: 'WER down',
    result: '1.64 | 3.5',
    variant: 'test-clean | test-other',
  },
  {
    area: 'Speech',
    benchmark: 'SPGISpeech',
    baseline: 'Qwen2-Audio Inst. 3.0',
    metric: 'WER down',
    result: '2.8',
    variant: 'AVF-Instruct',
  },
  {
    area: 'Speech',
    benchmark: 'TEDLIUM',
    baseline: 'Phi-4-mm 2.9',
    metric: 'WER down',
    result: '3.0',
    variant: 'AVF-Instruct',
  },
  {
    area: 'Speech',
    benchmark: 'GigaSpeech',
    baseline: 'Phi-4-mm 9.78',
    metric: 'WER down',
    result: '10.2',
    variant: 'AVF-Instruct',
  },
  {
    area: 'Speech',
    benchmark: 'VoxPopuli',
    baseline: 'Phi-4-mm 5.9',
    metric: 'WER down',
    result: '5.8',
    variant: 'AVF-Instruct',
  },
]

const dataStats = [
  { value: '100K hrs', label: 'AV-Skills-Short video' },
  { value: '3.8M', label: 'short-context training instances' },
  { value: '2.8M', label: 'short-context QA pairs' },
  { value: 'approx. 140K hrs', label: 'long-video data' },
  { value: '3.2M', label: 'long-video training instances' },
  { value: '2.0M', label: 'long-video QA pairs' },
  { value: '24K', label: 'AV-Think reasoning samples' },
  { value: '16K -> 32K', label: 'training context scaling' },
]

const shortSkills = [
  'relation reasoning',
  'emotion change',
  'temporal reasoning',
  'spatial perception',
  'causal reasoning',
  'hallucination detection',
  'audio counting',
  'video counting',
]

const longSkills = [
  'needle-in-the-haystack',
  'temporal referring',
  'temporal order',
  'temporal attribute',
  'sub-scene understanding',
  'holistic reasoning',
  'counting',
  'audio-visual referring',
  'topic-level reasoning',
  'detailed captioning',
  'event sequence',
  'event alignment',
  'inference',
  'comparative reasoning',
  'context understanding',
]

const trainingStages = [
  {
    title: 'Initialization + short-context SFT',
    detail:
      'Initialize from OmniVinci, then fine-tune on AV-Skills-Short plus audio-only, vision-only, ASR, captioning, and QA data with 5-minute inputs and 16K context.',
  },
  {
    title: 'Long-context SFT',
    detail:
      'Expand to AV-Skills-Long, long-form captions, temporal QA, and downsampled short-context data with 15-minute inputs and 32K context, producing AVF-Instruct.',
  },
  {
    title: 'CoT post-training',
    detail:
      'Start from AVF-Instruct, run SFT on AV-Think timestamp-grounded reasoning triplets, then apply GRPO-based RL to produce AVF-Think.',
  },
]
</script>

<template>
  <main class="page-shell">
    <section class="hero-section">
      <div class="hero-overlay"></div>
      <div class="content hero-content">
        <nav class="top-nav" aria-label="Primary navigation">
          <a
            v-for="link in navLinks"
            :key="link.href"
            :href="link.href"
            :target="link.external ? '_blank' : undefined"
            :rel="link.external ? 'noopener' : undefined"
            :class="link.primary ? 'nav-link nav-link--primary' : 'nav-link'"
          >
            {{ link.label }}
          </a>
        </nav>

        <img src="/logo.png?v=20260506" alt="Audio-Visual Flamingo logo" width="148" height="148" class="hero-logo">
        <p class="eyebrow">Open audio-visual intelligence for long and complex videos</p>
        <h1>Audio-Visual Flamingo</h1>
        <p class="hero-copy">
          A fully open AV-LLM for joint understanding and reasoning across audio, images, and long-form videos, with
          temporal interleaving, rotary time alignment, and timestamp-grounded reasoning for complex real-world media.
        </p>

        <div class="hero-stats" aria-label="Audio-Visual Flamingo summary statistics">
          <div v-for="stat in heroStats" :key="stat.label" class="stat-card stat-card--hero">
            <strong>{{ stat.value }}</strong>
            <span>{{ stat.label }}</span>
          </div>
        </div>
      </div>
    </section>

    <section class="section-band section-band--light">
      <div class="content intro-grid">
        <div>
          <p class="section-kicker">Why It Matters</p>
          <h2>Joint perception over the full timeline</h2>
          <p class="lead-text">
            AVF is designed for media where the answer depends on what is seen, what is heard, and when those events
            occur. It targets long-form video settings such as interviews, sports, lectures, trailers, city tours, and
            documentary-style content where speech, sound, music, and visuals all carry evidence.
          </p>
        </div>
        <div class="feature-grid">
          <article v-for="feature in featureCards" :key="feature.title" class="info-card">
            <h3>{{ feature.title }}</h3>
            <p>{{ feature.detail }}</p>
          </article>
        </div>
      </div>
    </section>

    <section id="benchmarks" class="section-band">
      <div class="content benchmark-layout">
        <div>
          <p class="section-kicker">Benchmark Snapshot</p>
          <h2>Strong transfer across audio, video, omni, and speech tasks</h2>
          <p class="body-text">
            The current paper reports AVF across omni, audio, video, and speech evaluations. AVF-Instruct improves on
            several similarly sized open baselines, while AVF-Think adds gains on timestamp-heavy omni reasoning.
          </p>
          <figure class="figure-panel figure-panel--tall">
            <img src="/figures/radar.webp" alt="Radar comparison of AVF and previous state of the art" loading="lazy">
            <figcaption>Normalized comparison across audio, video, omni, and speech benchmarks.</figcaption>
          </figure>
          <div class="table-wrap">
            <table class="benchmark-table">
              <thead>
                <tr>
                  <th>Area</th>
                  <th>Benchmark</th>
                  <th>Baseline</th>
                  <th>Metric</th>
                  <th>AVF</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="row in benchmarks" :key="row.area + row.benchmark">
                  <td>{{ row.area }}</td>
                  <td>
                    <strong>{{ row.benchmark }}</strong>
                  </td>
                  <td>{{ row.baseline }}</td>
                  <td>{{ row.metric }}</td>
                  <td>
                    <strong class="result-value">{{ row.result }}</strong>
                    <span>{{ row.variant }}</span>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </section>

    <section id="examples" class="section-band section-band--light">
      <div class="content">
        <div class="section-heading examples-heading">
          <p class="section-kicker">Model Examples</p>
          <h2>Long-form audio-visual understanding in the wild</h2>
          <p>
            These examples show AVF producing dense descriptions that combine visible events, background sounds, speech,
            and temporal grounding over real videos.
          </p>
        </div>

        <div class="showcase-list">
          <article v-for="example in showcaseExamples" :key="example.youtubeUrl" class="showcase-card">
            <div class="example-context">
              <div class="example-topline">
                <span>{{ example.task }}</span>
                <a :href="example.youtubeUrl" target="_blank" rel="noopener">Open video</a>
              </div>
              <h3>{{ example.title }}</h3>
              <div class="example-block">
                <strong>Prompt</strong>
                <p>{{ example.prompt }}</p>
              </div>
              <div class="video-shell">
                <iframe
                  :src="example.embedUrl"
                  :title="example.title"
                  loading="lazy"
                  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
                  referrerpolicy="strict-origin-when-cross-origin"
                  allowfullscreen
                ></iframe>
              </div>
            </div>

            <div class="example-response">
              <strong>AVF response</strong>
              <pre class="response-scroll" v-text="example.response"></pre>
            </div>
          </article>
        </div>
      </div>
    </section>

    <section id="architecture" class="section-band section-band--dark">
      <div class="content">
        <div class="section-heading">
          <p class="section-kicker">Architecture</p>
          <h2>Temporal fusion before language reasoning</h2>
          <p>
            AVF accepts images, videos, audio, and text prompts. Visual and auditory streams are encoded separately,
            compressed into audio-visual embeddings, temporally grouped, then aligned with prompt tokens before the
            Qwen2.5-7B backbone performs language reasoning.
          </p>
        </div>
        <figure class="wide-figure">
          <img src="/figures/architecture.webp" alt="Audio-Visual Flamingo architecture and training diagram" loading="lazy">
        </figure>
        <div class="architecture-grid">
          <article v-for="block in architectureBlocks" :key="block.title" class="dark-card">
            <h3>{{ block.title }}</h3>
            <p>{{ block.detail }}</p>
          </article>
        </div>
      </div>
    </section>

    <section id="data" class="section-band section-band--light">
      <div class="content data-layout">
        <div>
          <p class="section-kicker">AVF-Skills</p>
          <h2>Data built for cross-modal reasoning</h2>
          <p class="lead-text">
            AVF-Skills combines short and long videos with approximately 7M caption and QA training instances,
            including approximately 4.8M QA pairs. The curation emphasizes situations where audio and vision must be
            used together: event order, sound-source alignment, visual references, counting, temporal attributes, and
            broader scene context.
          </p>

          <div class="data-stats">
            <div v-for="stat in dataStats" :key="stat.label" class="stat-card">
              <strong>{{ stat.value }}</strong>
              <span>{{ stat.label }}</span>
            </div>
          </div>
        </div>
        <figure class="figure-panel">
          <img src="/figures/data-pie.webp" alt="Distribution of AVF video categories" loading="lazy">
          <figcaption>Training videos cover vlogs, trailers, music, sports, education, travel, news, cooking, and more.</figcaption>
        </figure>
      </div>

      <div class="content skills-layout">
        <div class="skill-panel">
          <h3>Short-context skills</h3>
          <div class="chip-list">
            <span v-for="skill in shortSkills" :key="skill">{{ skill }}</span>
          </div>
        </div>
        <div class="skill-panel">
          <h3>Long-context skills</h3>
          <div class="chip-list">
            <span v-for="skill in longSkills" :key="skill">{{ skill }}</span>
          </div>
        </div>
      </div>

      <div class="content">
        <figure class="wide-figure wide-figure--light">
          <img src="/figures/examples.webp" alt="Examples of AVF-Skills prompts and responses" loading="lazy">
        </figure>
        <figure class="wide-figure wide-figure--light">
          <img
            src="/figures/examples-appendix.webp"
            alt="Additional AVF-Skills long-form prompt examples"
            loading="lazy"
          >
        </figure>
      </div>
    </section>

    <section class="section-band">
      <div class="content training-layout">
        <div>
          <p class="section-kicker">Training Curriculum</p>
          <h2>From short-range perception to long-horizon reasoning</h2>
          <p class="body-text">
            The curriculum gradually increases input duration and task complexity. Short-context SFT caps inputs at 5
            minutes and 16K context; long-context SFT expands to 15-minute audio-visual inputs and 32K context; CoT
            post-training teaches temporally grounded reasoning with AV-Think.
          </p>
        </div>
        <div class="timeline">
          <article v-for="(stage, index) in trainingStages" :key="stage.title" class="timeline-item">
            <span>{{ index + 1 }}</span>
            <div>
              <h3>{{ stage.title }}</h3>
              <p>{{ stage.detail }}</p>
            </div>
          </article>
        </div>
      </div>
    </section>
  </main>
</template>

<style scoped>
:global(html) {
  scroll-behavior: smooth;
}

:global(body) {
  margin: 0;
  color: #2a160f;
  background: #fff8ed;
  font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
}

:global(a) {
  color: inherit;
  text-decoration: none;
}

.page-shell {
  min-height: 100vh;
  overflow-x: hidden;
  background:
    linear-gradient(180deg, rgba(255, 248, 237, 0.98) 0%, rgba(255, 252, 245, 1) 34%, rgba(255, 248, 237, 1) 100%);
}

.content {
  width: min(1180px, calc(100% - 32px));
  margin: 0 auto;
}

.hero-section {
  position: relative;
  min-height: 92vh;
  display: flex;
  align-items: center;
  color: #fffaf0;
  background:
    linear-gradient(135deg, rgba(92, 14, 12, 0.96), rgba(190, 45, 15, 0.92) 52%, rgba(237, 139, 28, 0.86)),
    url('/figures/architecture.webp') center / cover no-repeat;
}

.hero-overlay {
  position: absolute;
  inset: 0;
  background:
    radial-gradient(circle at 72% 22%, rgba(255, 205, 80, 0.22), transparent 28%),
    linear-gradient(90deg, rgba(42, 12, 7, 0.72), rgba(42, 12, 7, 0.24));
  pointer-events: none;
}

.hero-content {
  position: relative;
  z-index: 1;
  padding: 32px 0 56px;
}

.top-nav {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  justify-content: flex-end;
  margin-bottom: 56px;
}

.nav-link {
  display: inline-flex;
  align-items: center;
  min-height: 38px;
  padding: 0 14px;
  border: 1px solid rgba(255, 237, 213, 0.4);
  border-radius: 8px;
  color: #fff7ed;
  font-size: 0.92rem;
  font-weight: 700;
  background: rgba(255, 247, 237, 0.08);
  backdrop-filter: blur(8px);
}

.nav-link:hover {
  border-color: rgba(255, 214, 121, 0.86);
  background: rgba(255, 247, 237, 0.16);
}

.nav-link--primary {
  color: #5c1608;
  background: #ffd36a;
  border-color: #ffd36a;
}

.hero-logo {
  width: 148px;
  height: auto;
  margin-bottom: 22px;
  filter: drop-shadow(0 20px 28px rgba(44, 12, 8, 0.32));
}

.eyebrow,
.section-kicker {
  margin: 0 0 14px;
  color: #b91c1c;
  font-size: 0.78rem;
  font-weight: 900;
  letter-spacing: 0.14em;
  text-transform: uppercase;
}

.hero-section .eyebrow {
  color: #ffe7a3;
}

h1,
h2,
h3,
p {
  margin-top: 0;
}

h1 {
  max-width: 920px;
  margin-bottom: 20px;
  font-size: clamp(3.4rem, 7vw, 6.9rem);
  line-height: 0.96;
  font-weight: 900;
  letter-spacing: 0;
}

h2 {
  color: #2a160f;
  font-size: clamp(2rem, 3.4vw, 3.8rem);
  line-height: 1;
  font-weight: 900;
  letter-spacing: 0;
}

h3 {
  color: #35170e;
  font-size: 1.08rem;
  font-weight: 850;
  letter-spacing: 0;
}

.hero-copy {
  max-width: 780px;
  color: #fff4dd;
  font-size: 1.26rem;
  line-height: 1.7;
}

.hero-stats {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 12px;
  max-width: 980px;
  margin-top: 32px;
}

.stat-card {
  border: 1px solid rgba(194, 65, 12, 0.18);
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.82);
  padding: 18px;
  box-shadow: 0 18px 38px -28px rgba(79, 25, 10, 0.48);
}

.stat-card strong,
.stat-card span {
  display: block;
}

.stat-card strong {
  color: #b91c1c;
  font-size: 1.34rem;
  line-height: 1.1;
}

.stat-card span {
  margin-top: 8px;
  color: #6b3218;
  font-size: 0.93rem;
  line-height: 1.35;
}

.stat-card--hero {
  border-color: rgba(255, 237, 213, 0.34);
  background: rgba(255, 248, 237, 0.12);
  box-shadow: none;
  backdrop-filter: blur(8px);
}

.stat-card--hero strong {
  color: #ffd36a;
}

.stat-card--hero span {
  color: rgba(255, 250, 240, 0.86);
}

.section-band {
  padding: 86px 0;
  background: #fffdf8;
}

.section-band--light {
  background: #fff3df;
}

.section-band--dark {
  background:
    linear-gradient(180deg, #301007 0%, #561808 100%);
  color: #fff2df;
}

.intro-grid,
.data-layout,
.training-layout {
  display: grid;
  grid-template-columns: minmax(0, 0.92fr) minmax(0, 1.08fr);
  gap: 42px;
  align-items: start;
}

.benchmark-layout {
  display: grid;
  grid-template-columns: 1fr;
  gap: 28px;
}

.feature-grid,
.architecture-grid,
.data-stats {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 14px;
}

.info-card,
.dark-card,
.skill-panel,
.timeline-item {
  border-radius: 8px;
  padding: 20px;
}

.info-card {
  border: 1px solid rgba(194, 65, 12, 0.18);
  background: rgba(255, 255, 255, 0.82);
}

.info-card p,
.dark-card p,
.timeline-item p {
  margin-bottom: 0;
  color: #6b3218;
  line-height: 1.7;
}

.lead-text,
.body-text,
.section-heading p {
  color: #5c2a16;
  font-size: 1.05rem;
  line-height: 1.8;
}

.table-wrap {
  margin-top: 28px;
  overflow-x: auto;
  border: 1px solid rgba(194, 65, 12, 0.18);
  border-radius: 8px;
  background: white;
}

.benchmark-table {
  width: 100%;
  min-width: 1120px;
  border-collapse: collapse;
  font-size: 0.95rem;
}

.benchmark-table th {
  color: #7c2d12;
  background: #fff1d6;
  text-align: left;
  font-size: 0.76rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}

.benchmark-table th,
.benchmark-table td {
  padding: 14px 16px;
  border-bottom: 1px solid rgba(194, 65, 12, 0.12);
  vertical-align: top;
}

.benchmark-table tbody tr:hover {
  background: #fff7ed;
}

.benchmark-table td:last-child span {
  display: block;
  margin-top: 4px;
  color: #7c2d12;
  font-size: 0.82rem;
}

.result-value {
  color: #dc2626;
}

.examples-heading {
  max-width: 820px;
}

.showcase-list {
  display: grid;
  gap: 24px;
}

.showcase-card {
  display: grid;
  grid-template-columns: minmax(320px, 0.86fr) minmax(0, 1.14fr);
  gap: 24px;
  align-items: start;
  border: 1px solid rgba(194, 65, 12, 0.18);
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.78);
  padding: 18px;
  box-shadow: 0 24px 45px -34px rgba(69, 26, 3, 0.35);
}

.video-shell {
  aspect-ratio: 16 / 9;
  overflow: hidden;
  border-radius: 8px;
  background: #2a160f;
  margin-top: 18px;
}

.video-shell iframe {
  display: block;
  width: 100%;
  height: 100%;
  border: 0;
}

.example-context h3 {
  margin-bottom: 16px;
  font-size: 1.45rem;
  line-height: 1.15;
}

.example-topline {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 12px;
}

.example-topline span,
.example-topline a {
  display: inline-flex;
  align-items: center;
  min-height: 32px;
  border-radius: 8px;
  padding: 0 10px;
  font-size: 0.82rem;
  font-weight: 850;
}

.example-topline span {
  color: #7c2d12;
  background: #fff1d6;
}

.example-topline a {
  color: #5c1608;
  background: #ffd36a;
}

.example-block {
  margin-top: 16px;
}

.example-block strong,
.example-response strong {
  display: block;
  margin-bottom: 8px;
  color: #7c2d12;
  font-size: 0.78rem;
  font-weight: 900;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}

.example-block p {
  margin-bottom: 0;
  color: #5c2a16;
  line-height: 1.65;
}

.example-response {
  min-width: 0;
}

.response-scroll {
  max-height: 560px;
  margin: 0;
  overflow: auto;
  border-radius: 8px;
  background: #2a160f;
  color: #fff7ed;
  padding: 16px;
  font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, "Liberation Mono", monospace;
  font-size: 0.82rem;
  line-height: 1.65;
  white-space: pre-wrap;
  word-break: break-word;
}

.figure-panel,
.wide-figure {
  margin: 0;
  border: 1px solid rgba(194, 65, 12, 0.18);
  border-radius: 8px;
  background: white;
  padding: 12px;
  box-shadow: 0 24px 45px -32px rgba(69, 26, 3, 0.35);
}

.figure-panel img,
.wide-figure img {
  display: block;
  width: 100%;
  height: auto;
  border-radius: 6px;
}

.figure-panel--tall img {
  max-height: 680px;
  object-fit: contain;
}

.benchmark-layout .figure-panel--tall {
  width: min(100%, 760px);
  margin: 0 auto;
}

figcaption {
  margin-top: 12px;
  color: #7c3d1c;
  font-size: 0.92rem;
  line-height: 1.55;
}

.section-band--dark .section-kicker {
  color: #ffc65a;
}

.section-band--dark h2,
.section-band--dark h3 {
  color: #fff8ed;
}

.section-band--dark .section-heading p {
  color: #f9d8b6;
}

.section-heading {
  max-width: 900px;
  margin-bottom: 32px;
}

.wide-figure {
  background: #fffaf3;
}

.wide-figure--light {
  margin-top: 34px;
}

.architecture-grid {
  grid-template-columns: repeat(4, minmax(0, 1fr));
  margin-top: 22px;
}

.dark-card {
  border: 1px solid rgba(255, 211, 106, 0.22);
  background: rgba(255, 244, 223, 0.08);
}

.dark-card p {
  color: #f6d7b4;
}

.data-layout {
  grid-template-columns: minmax(0, 1fr) minmax(320px, 0.86fr);
}

.data-stats {
  margin-top: 28px;
}

.skills-layout {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 18px;
  margin-top: 34px;
}

.skill-panel {
  border: 1px solid rgba(194, 65, 12, 0.18);
  background: rgba(255, 255, 255, 0.72);
}

.chip-list {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-top: 16px;
}

.chip-list span {
  display: inline-flex;
  align-items: center;
  min-height: 32px;
  border: 1px solid rgba(234, 88, 12, 0.24);
  border-radius: 8px;
  background: #fff7ed;
  color: #7c2d12;
  padding: 0 10px;
  font-size: 0.9rem;
  font-weight: 700;
}

.timeline {
  display: grid;
  gap: 16px;
}

.timeline-item {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 16px;
  border: 1px solid rgba(194, 65, 12, 0.18);
  background: #fff8ed;
}

.timeline-item > span {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 34px;
  height: 34px;
  border-radius: 8px;
  color: #5a180b;
  background: #ffc65a;
  font-weight: 900;
}

@media (max-width: 980px) {
  .hero-section {
    min-height: auto;
  }

  .hero-content {
    padding-bottom: 46px;
  }

  .top-nav {
    justify-content: flex-start;
    margin-bottom: 42px;
  }

  .hero-stats,
  .intro-grid,
  .data-layout,
  .training-layout,
  .skills-layout,
  .showcase-card {
    grid-template-columns: 1fr;
  }

  .architecture-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}

@media (max-width: 640px) {
  .content {
    width: min(100% - 24px, 1180px);
  }

  .hero-content {
    padding-top: 20px;
  }

  .top-nav {
    gap: 8px;
  }

  .nav-link {
    min-height: 34px;
    padding: 0 10px;
    font-size: 0.84rem;
  }

  .hero-logo {
    width: 118px;
  }

  h1 {
    font-size: 3.35rem;
  }

  .hero-copy {
    font-size: 1.06rem;
  }

  .response-scroll {
    max-height: 320px;
  }

  .section-band {
    padding: 58px 0;
  }

  .hero-stats,
  .feature-grid,
  .architecture-grid,
  .data-stats {
    grid-template-columns: 1fr;
  }

  .stat-card,
  .info-card,
  .dark-card,
  .skill-panel,
  .timeline-item {
    padding: 16px;
  }

}
</style>
