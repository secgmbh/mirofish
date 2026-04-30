<template>
  <div class="page-wrap">

    <!-- NAVBAR: transparent over hero, sticky on scroll -->
    <header class="site-header" :class="{ 'is-sticky': isSticky }">
      <div class="header-inner">
        <div class="header-logo">BOTOPOLIS</div>
        <nav class="header-nav">
          <a class="nav-item active" href="#">Home</a>
          <a class="nav-item" @click="scrollToSteps">{{ $t('home.workflowSequence') }}</a>
          <a class="nav-item" @click="scrollToStart">{{ $t('home.startEngine') }}</a>
        </nav>
        <div class="header-actions">
          <LanguageSwitcher />
          <a href="https://github.com/secgmbh/mirofish" target="_blank" class="btn-outline">
            <span>GitHub</span>
            <i>&#8599;</i>
          </a>
        </div>
      </div>
    </header>

    <!-- HERO: full-bleed with side margin, rounded, image-style background -->
    <section class="hero-section">
      <div class="hero-wrap">
        <!-- Animated background layers -->
        <div class="hero-bg">
          <div class="hero-blob hero-blob-1"></div>
          <div class="hero-blob hero-blob-2"></div>
          <div class="hero-blob hero-blob-3"></div>
          <div class="hero-grid-overlay"></div>
          <div class="hero-gradient-bottom"></div>
        </div>
        <!-- Content -->
        <div class="hero-content">
          <div class="hero-left">
            <div class="hero-eyebrow">
              <span class="eyebrow-dot"></span>
              {{ $t('home.tagline') }}
            </div>
            <h1 class="hero-title">
              {{ $t('home.heroTitle1') }}<br>
              <span class="hero-title-color">{{ $t('home.heroTitle2') }}</span>
            </h1>
            <div class="hero-btns">
              <button class="btn-primary" @click="scrollToStart">
                <span>{{ $t('home.startEngine') }}</span>
                <i class="btn-arrow">&#8599;</i>
              </button>
              <button class="btn-secondary" @click="scrollToSteps">
                <span>{{ $t('home.workflowSequence') }}</span>
              </button>
            </div>
          </div>
          <div class="hero-right">
            <div class="hero-card">
              <div class="hero-card-label">{{ $t('home.systemStatus') }}</div>
              <div class="hero-card-status">
                <span class="status-pulse"></span>
                {{ $t('home.systemReady') }}
              </div>
              <p class="hero-card-desc">{{ $t('home.systemReadyDesc') }}</p>
              <div class="hero-card-stats">
                <div class="hstat">
                  <span class="hstat-n">5</span>
                  <span class="hstat-l">Steps</span>
                </div>
                <div class="hstat">
                  <span class="hstat-n">&#8734;</span>
                  <span class="hstat-l">{{ $t('home.metricHighAvailDesc') }}</span>
                </div>
                <div class="hstat">
                  <span class="hstat-n">{{ $t('home.metricLowCostDesc') }}</span>
                  <span class="hstat-l">{{ $t('home.metricLowCost') }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- SERVICE CARDS: 3 large image-style cards like Aiero -->
    <section class="cards-section">
      <div class="cards-container">
        <div class="srv-card srv-card-1" ref="stepsRef">
          <div class="srv-card-bg srv-bg-1"></div>
          <div class="srv-card-content">
            <div class="srv-tags">
              <span class="srv-tag">{{ $t('home.step01Title') }}</span>
              <span class="srv-tag">{{ $t('home.step02Title') }}</span>
            </div>
            <h3 class="srv-title">{{ $t('home.heroTitle1') }}<br>{{ $t('home.heroTitle2') }}</h3>
            <a class="srv-link" @click="scrollToStart">{{ $t('home.startEngine') }} &#8594;</a>
          </div>
          <div class="srv-arrow" @click="scrollToStart">&#8599;</div>
        </div>
        <div class="srv-card srv-card-2">
          <div class="srv-card-bg srv-bg-2"></div>
          <div class="srv-card-content srv-card-content-v2">
            <h3 class="srv-title">{{ $t('home.step03Title') }}</h3>
            <p class="srv-desc">{{ $t('home.step03Desc') }}</p>
            <div class="srv-agents">
              <div class="agent-bubble" v-for="n in 5" :key="n">{{ n }}</div>
              <span class="agent-count">{{ $t('home.metricHighAvailDesc') }}</span>
            </div>
          </div>
          <div class="srv-arrow">&#8599;</div>
        </div>
        <div class="srv-card srv-card-3">
          <div class="srv-card-bg srv-bg-3"></div>
          <div class="srv-card-content srv-card-content-v3">
            <h3 class="srv-title">{{ $t('home.step04Title') }} +<br>{{ $t('home.step05Title') }}</h3>
            <p class="srv-desc">{{ $t('home.step04Desc') }}</p>
            <div class="srv-icon">&#9711;</div>
          </div>
        </div>
      </div>
    </section>

    <!-- HOW IT WORKS: numbered steps row -->
    <section class="process-section">
      <div class="process-inner">
        <div class="section-head">
          <p class="section-eyebrow">{{ $t('home.workflowSequence') }}</p>
          <h2 class="section-title">{{ $t('home.systemReady') }}</h2>
        </div>
        <div class="process-steps">
          <div class="process-step" v-for="(step, i) in steps" :key="i">
            <div class="ps-num">{{ String(i+1).padStart(2,'0') }}</div>
            <div class="ps-line"></div>
            <h4 class="ps-title">{{ step.title }}</h4>
            <p class="ps-desc">{{ step.desc }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- ENGINE: upload + prompt, full-width prominent -->
    <section class="engine-section" ref="startRef">
      <div class="engine-inner">
        <div class="engine-head">
          <p class="section-eyebrow">&gt;_ Engine</p>
          <h2 class="section-title">{{ $t('home.startEngine') }}</h2>
          <p class="engine-sub">{{ $t('home.systemReadyDesc') }}</p>
        </div>
        <div class="engine-body">
          <div class="engine-box">
            <!-- Upload -->
            <div class="ebox-panel">
              <div class="ebox-label">
                <span class="ebox-num">01</span>
                <span>{{ $t('home.realitySeed') }}</span>
                <span class="ebox-meta">{{ $t('home.supportedFormats') }}</span>
              </div>
              <div
                class="drop-area"
                :class="{ active: isDragOver, filled: files.length > 0 }"
                @dragover.prevent="handleDragOver"
                @dragleave.prevent="handleDragLeave"
                @drop.prevent="handleDrop"
                @click="triggerFileInput"
              >
                <input ref="fileInput" type="file" multiple accept=".pdf,.md,.txt"
                  @change="handleFileSelect" style="display:none" :disabled="loading" />
                <div v-if="files.length === 0" class="drop-empty">
                  <div class="drop-up-icon">&#8593;</div>
                  <p>{{ $t('home.dragToUpload') }}</p>
                  <small>{{ $t('home.orBrowse') }}</small>
                </div>
                <div v-else class="drop-files">
                  <div v-for="(f, i) in files" :key="i" class="drop-file-row">
                    <span>&#128196; {{ f.name }}</span>
                    <button @click.stop="removeFile(i)" class="drop-rm">&#215;</button>
                  </div>
                </div>
              </div>
            </div>

            <!-- Prompt -->
            <div class="ebox-panel">
              <div class="ebox-label">
                <span class="ebox-num">02</span>
                <span>{{ $t('home.inputParams') }}</span>
              </div>
              <div class="prompt-area">
                <textarea
                  v-model="formData.simulationRequirement"
                  class="prompt-ta"
                  :placeholder="$t('home.promptPlaceholder')"
                  rows="8"
                  :disabled="loading"
                ></textarea>
                <span class="prompt-badge">{{ $t('home.engineBadge') }}</span>
              </div>
              <button
                class="launch-btn"
                @click="startSimulation"
                :disabled="!canSubmit || loading"
              >
                <span>{{ loading ? $t('home.initializing') : $t('home.startEngine') }}</span>
                <i>&#8599;</i>
              </button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- HISTORY -->
    <section class="history-section">
      <div class="engine-inner">
        <HistoryDatabase />
      </div>
    </section>

  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { useI18n } from 'vue-i18n'
import { useRouter } from 'vue-router'
import HistoryDatabase from '../components/HistoryDatabase.vue'
import LanguageSwitcher from '../components/LanguageSwitcher.vue'

const router = useRouter()
const { t } = useI18n()

// 表单数据
const formData = ref({
  simulationRequirement: ''
})

// 文件列表
const files = ref([])

// 状态
const loading = ref(false)
const error = ref('')
const isDragOver = ref(false)

// 文件输入引用
const fileInput = ref(null)
const isSticky = ref(false)
if (typeof window !== 'undefined') {
  window.addEventListener('scroll', () => { isSticky.value = window.scrollY > 60 })
}
const stepsRef = ref(null)
const startRef = ref(null)

// 计算属性:是否可以提交
const canSubmit = computed(() => {
  return formData.value.simulationRequirement.trim() !== '' && files.value.length > 0
})

// 触发文件选择
const triggerFileInput = () => {
  if (!loading.value) {
    fileInput.value?.click()
  }
}

// 处理文件选择
const handleFileSelect = (event) => {
  const selectedFiles = Array.from(event.target.files)
  addFiles(selectedFiles)
}

// 处理拖拽相关
const handleDragOver = (e) => {
  if (!loading.value) {
    isDragOver.value = true
  }
}

const handleDragLeave = (e) => {
  isDragOver.value = false
}

const handleDrop = (e) => {
  isDragOver.value = false
  if (loading.value) return
  
  const droppedFiles = Array.from(e.dataTransfer.files)
  addFiles(droppedFiles)
}

// 添加文件
const addFiles = (newFiles) => {
  const validFiles = newFiles.filter(file => {
    const ext = file.name.split('.').pop().toLowerCase()
    return ['pdf', 'md', 'txt'].includes(ext)
  })
  files.value.push(...validFiles)
}

// 移除文件
const removeFile = (index) => {
  files.value.splice(index, 1)
}

// 滚动到底部
const scrollToBottom = () => {
  window.scrollTo({
    top: document.body.scrollHeight,
    behavior: 'smooth'
  })
}

const scrollToSteps = () => stepsRef.value?.scrollIntoView({ behavior: 'smooth' })
const scrollToStart = () => startRef.value?.scrollIntoView({ behavior: 'smooth' })

const steps = computed(() => [
  { title: t('home.step01Title'), desc: t('home.step01Desc') },
  { title: t('home.step02Title'), desc: t('home.step02Desc') },
  { title: t('home.step03Title'), desc: t('home.step03Desc') },
  { title: t('home.step04Title'), desc: t('home.step04Desc') },
  { title: t('home.step05Title'), desc: t('home.step05Desc') },
])

// 开始模拟 - 立即跳转，API调用在Process页面进行
const startSimulation = () => {
  if (!canSubmit.value || loading.value) return
  
  // 存储待上传的数据
  import('../store/pendingUpload.js').then(({ setPendingUpload }) => {
    setPendingUpload(files.value, formData.value.simulationRequirement)
    
    // 立即跳转到Process页面（使用特殊标识表示新建项目）
    router.push({
      name: 'Process',
      params: { projectId: 'new' }
    })
  })
}
</script>

<style scoped>
/* ── Fonts loaded in index.html: Sora, Manrope, JetBrains Mono ── */

/* ── CSS Variables ── */
:root {
  --clr-bg:        #111111;
  --clr-surface:   #1a1a1a;
  --clr-card:      #1f1f1f;
  --clr-border:    rgba(255,255,255,0.08);
  --clr-primary:   #2563EB;
  --clr-accent:    #45d0bd;
  --clr-red:       #ef6464;
  --clr-white:     #ffffff;
  --clr-gray:      #888888;
  --clr-text:      #cccccc;
  --grad-teal:     linear-gradient(113deg, #45d0bd 2.7%, #44b6e9 98.55%);
  --grad-btn:      linear-gradient(102deg, #2563EB 0%, #1D4ED8 100%);
  --grad-hero:     linear-gradient(135deg, #0a1628 0%, #0f2350 50%, #1a3a7a 100%);
  --radius-card:   25px;
  --radius-btn:    15px;
  --font-head:     'Sora', Arial, sans-serif;
  --font-body:     'Manrope', Arial, sans-serif;
  --font-mono:     'JetBrains Mono', monospace;
  --transition:    all 0.3s ease;
}

/* ── Reset ── */
.page-wrap {
  min-height: 100vh;
  background: var(--clr-bg);
  color: var(--clr-white);
  font-family: var(--font-body);
}

/* ═══════════════════════════════
   NAVBAR
═══════════════════════════════ */
.site-header {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 200;
  padding: 0 40px;
  transition: var(--transition);
}

.site-header.is-sticky {
  background: rgba(17,17,17,0.92);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--clr-border);
}

.header-inner {
  max-width: 1320px;
  margin: 0 auto;
  height: 80px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.header-logo {
  font-family: var(--font-head);
  font-weight: 800;
  font-size: 1.3rem;
  letter-spacing: 2px;
  background: var(--grad-teal);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.header-nav {
  display: flex;
  gap: 40px;
}

.nav-item {
  font-family: var(--font-body);
  font-size: 15px;
  font-weight: 500;
  color: rgba(255,255,255,0.75);
  cursor: pointer;
  text-decoration: none;
  transition: var(--transition);
  position: relative;
}

.nav-item::after {
  content: '';
  position: absolute;
  bottom: -4px; left: 0;
  width: 0; height: 2px;
  background: var(--grad-teal);
  transition: width 0.3s;
}

.nav-item:hover, .nav-item.active { color: var(--clr-white); }
.nav-item:hover::after, .nav-item.active::after { width: 100%; }

.header-actions {
  display: flex;
  align-items: center;
  gap: 20px;
}

.btn-outline {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  height: 48px;
  padding: 0 24px;
  border: 1.5px solid rgba(255,255,255,0.2);
  border-radius: var(--radius-btn);
  font-family: var(--font-body);
  font-size: 14px;
  font-weight: 600;
  color: var(--clr-white);
  text-decoration: none;
  transition: var(--transition);
}

.btn-outline:hover {
  border-color: var(--clr-accent);
  color: var(--clr-accent);
}

/* ═══════════════════════════════
   HERO
═══════════════════════════════ */
.hero-section {
  padding: 100px 20px 0;
  position: relative;
}

.hero-wrap {
  position: relative;
  border-radius: 30px;
  overflow: hidden;
  min-height: 85vh;
  background: var(--grad-hero);
  display: flex;
  align-items: center;
}

.hero-bg {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.hero-blob {
  position: absolute;
  border-radius: 50%;
  filter: blur(100px);
  opacity: 0.5;
}

.hero-blob-1 {
  width: 700px; height: 700px;
  background: rgba(37,99,235,0.35);
  top: -200px; right: -100px;
  animation: float1 12s ease-in-out infinite;
}

.hero-blob-2 {
  width: 500px; height: 500px;
  background: rgba(69,208,189,0.2);
  bottom: -150px; left: -100px;
  animation: float2 15s ease-in-out infinite;
}

.hero-blob-3 {
  width: 350px; height: 350px;
  background: rgba(239,100,100,0.15);
  top: 50%; left: 40%;
  transform: translate(-50%,-50%);
  animation: float3 10s ease-in-out infinite;
}

@keyframes float1 { 0%,100%{transform:translate(0,0)} 50%{transform:translate(-40px,30px)} }
@keyframes float2 { 0%,100%{transform:translate(0,0)} 50%{transform:translate(30px,-40px)} }
@keyframes float3 { 0%,100%{transform:translate(-50%,-50%)} 50%{transform:translate(-50%,-60%)} }

.hero-grid-overlay {
  position: absolute; inset: 0;
  background-image:
    linear-gradient(rgba(255,255,255,0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.03) 1px, transparent 1px);
  background-size: 60px 60px;
}

.hero-gradient-bottom {
  position: absolute;
  bottom: 0; left: 0; right: 0;
  height: 200px;
  background: linear-gradient(to bottom, transparent, var(--clr-bg));
}

.hero-content {
  position: relative;
  z-index: 1;
  max-width: 1320px;
  width: 100%;
  margin: 0 auto;
  padding: 80px 60px;
  display: flex;
  align-items: center;
  gap: 60px;
  justify-content: space-between;
}

.hero-left { flex: 1; max-width: 620px; }

.hero-eyebrow {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  font-family: var(--font-mono);
  font-size: 13px;
  color: var(--clr-accent);
  letter-spacing: 2px;
  text-transform: uppercase;
  margin-bottom: 28px;
  background: rgba(69,208,189,0.1);
  padding: 8px 18px;
  border-radius: 100px;
  border: 1px solid rgba(69,208,189,0.3);
}

.eyebrow-dot {
  width: 7px; height: 7px;
  background: #22C55E;
  border-radius: 50%;
  animation: pulse-dot 2s ease-in-out infinite;
}

@keyframes pulse-dot { 0%,100%{opacity:1;transform:scale(1)} 50%{opacity:0.5;transform:scale(0.7)} }

.hero-title {
  font-family: var(--font-head);
  font-size: 68px;
  font-weight: 700;
  line-height: 1.1;
  letter-spacing: -2px;
  color: var(--clr-white);
  margin: 0 0 36px;
}

.hero-title-color {
  background: var(--grad-teal);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.hero-btns {
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
}

.btn-primary {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  height: 65px;
  padding: 0 32px;
  background: var(--clr-red);
  color: var(--clr-white);
  border: none;
  border-radius: var(--radius-btn);
  font-family: var(--font-body);
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: var(--transition);
}

.btn-primary:hover {
  background: #f57e7e;
  transform: translateY(-2px);
  box-shadow: 0 10px 30px rgba(239,100,100,0.35);
}

.btn-arrow { font-style: normal; font-size: 1.2em; }

.btn-secondary {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  height: 65px;
  padding: 0 32px;
  background: rgba(255,255,255,0.08);
  color: var(--clr-white);
  border: 1.5px solid rgba(255,255,255,0.15);
  border-radius: var(--radius-btn);
  font-family: var(--font-body);
  font-size: 16px;
  font-weight: 500;
  cursor: pointer;
  transition: var(--transition);
  position: relative;
  overflow: hidden;
}

.btn-secondary::before {
  content: '';
  position: absolute;
  inset: -2px;
  border-radius: var(--radius-btn);
  padding: 2px;
  background: var(--grad-teal);
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  opacity: 0;
  transition: opacity 0.3s;
}

.btn-secondary:hover::before { opacity: 1; }
.btn-secondary:hover { border-color: transparent; color: var(--clr-white); }

/* Hero right card */
.hero-right { flex: 0 0 360px; }

.hero-card {
  background: rgba(255,255,255,0.06);
  border: 1px solid rgba(255,255,255,0.12);
  border-radius: 24px;
  padding: 36px;
  backdrop-filter: blur(20px);
}

.hero-card-label {
  font-family: var(--font-mono);
  font-size: 11px;
  color: var(--clr-accent);
  letter-spacing: 3px;
  text-transform: uppercase;
  margin-bottom: 16px;
}

.hero-card-status {
  display: flex;
  align-items: center;
  gap: 10px;
  font-family: var(--font-head);
  font-size: 20px;
  font-weight: 600;
  color: var(--clr-white);
  margin-bottom: 12px;
}

.status-pulse {
  width: 10px; height: 10px;
  background: #22C55E;
  border-radius: 50%;
  box-shadow: 0 0 0 4px rgba(34,197,94,0.2);
  animation: pulse-ring 2s ease-in-out infinite;
}

@keyframes pulse-ring { 0%,100%{box-shadow:0 0 0 4px rgba(34,197,94,0.2)} 50%{box-shadow:0 0 0 8px rgba(34,197,94,0)} }

.hero-card-desc {
  font-size: 14px;
  color: rgba(255,255,255,0.55);
  line-height: 1.6;
  margin-bottom: 28px;
}

.hero-card-stats {
  display: flex;
  gap: 20px;
  border-top: 1px solid rgba(255,255,255,0.08);
  padding-top: 24px;
}

.hstat { display: flex; flex-direction: column; gap: 4px; flex: 1; }
.hstat-n { font-family: var(--font-head); font-size: 22px; font-weight: 700; color: var(--clr-accent); }
.hstat-l { font-size: 11px; color: rgba(255,255,255,0.45); }

/* ═══════════════════════════════
   SERVICE CARDS (Aiero style)
═══════════════════════════════ */
.cards-section {
  padding: 0 20px 40px;
}

.cards-container {
  max-width: 1320px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 2fr 1.5fr 1fr;
  gap: 20px;
  align-items: stretch;
}

.srv-card {
  position: relative;
  border-radius: var(--radius-card);
  overflow: hidden;
  min-height: 520px;
  cursor: pointer;
}

.srv-card-bg {
  position: absolute;
  inset: 0;
  transition: transform 0.6s cubic-bezier(0.23,1,0.32,1);
}

.srv-card:hover .srv-card-bg { transform: scale(1.04); }

.srv-bg-1 {
  background: linear-gradient(135deg, #0f2044 0%, #1a3a7a 40%, #45d0bd20 100%),
              linear-gradient(to bottom right, #1D4ED8, #0a1628);
}

.srv-bg-2 {
  background: linear-gradient(135deg, #1a0a2e 0%, #2d1b69 50%, #4c1d95 100%);
}

.srv-bg-3 {
  background: linear-gradient(135deg, #0a2020 0%, #0d3d3d 50%, #45d0bd30 100%);
}

/* Decorative inner glow */
.srv-card::after {
  content: '';
  position: absolute;
  bottom: 0; right: 0;
  width: 120px; height: 120px;
  border-radius: 25px 0 25px 0;
  background: rgba(255,255,255,0.03);
}

.srv-card-content {
  position: absolute;
  inset: 0;
  padding: 48px;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
}

.srv-card-content-v2 {
  justify-content: center;
}

.srv-card-content-v3 {
  justify-content: space-between;
  align-items: flex-start;
}

.srv-tags {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
  flex-wrap: wrap;
}

.srv-tag {
  font-size: 12px;
  font-weight: 500;
  color: rgba(255,255,255,0.7);
  border: 1px solid rgba(255,255,255,0.2);
  padding: 5px 14px;
  border-radius: 100px;
  background: rgba(255,255,255,0.06);
}

.srv-title {
  font-family: var(--font-head);
  font-size: 36px;
  font-weight: 500;
  color: var(--clr-white);
  line-height: 1.2;
  margin: 0 0 24px;
}

.srv-link {
  font-size: 14px;
  font-weight: 500;
  color: var(--clr-white);
  cursor: pointer;
  padding-bottom: 4px;
  border-bottom: 1px solid rgba(255,255,255,0.5);
  width: fit-content;
  transition: var(--transition);
}

.srv-link:hover { color: var(--clr-accent); border-color: var(--clr-accent); }

.srv-desc {
  font-size: 14px;
  color: rgba(255,255,255,0.6);
  line-height: 1.6;
  margin-bottom: 20px;
}

.srv-agents {
  display: flex;
  align-items: center;
  gap: 8px;
}

.agent-bubble {
  width: 34px; height: 34px;
  border-radius: 50%;
  background: linear-gradient(135deg, #45d0bd, #2563EB);
  display: flex; align-items: center; justify-content: center;
  font-size: 12px; font-weight: 700;
  border: 2px solid rgba(255,255,255,0.15);
  margin-left: -8px;
}

.agent-bubble:first-child { margin-left: 0; }

.agent-count {
  font-size: 13px;
  color: rgba(255,255,255,0.6);
  margin-left: 8px;
}

.srv-icon {
  font-size: 80px;
  color: rgba(69,208,189,0.4);
  position: absolute;
  bottom: 30px; right: 40px;
}

.srv-arrow {
  position: absolute;
  top: 24px; right: 24px;
  width: 44px; height: 44px;
  background: rgba(255,255,255,0.1);
  border-radius: 12px;
  display: flex; align-items: center; justify-content: center;
  font-size: 18px;
  color: var(--clr-white);
  cursor: pointer;
  transition: var(--transition);
  border: 1px solid rgba(255,255,255,0.15);
}

.srv-arrow:hover { background: var(--clr-accent); border-color: var(--clr-accent); color: #000; }

/* ═══════════════════════════════
   PROCESS STEPS
═══════════════════════════════ */
.process-section {
  padding: 100px 20px;
  background: var(--clr-surface);
}

.process-inner {
  max-width: 1320px;
  margin: 0 auto;
}

.section-head {
  margin-bottom: 60px;
}

.section-eyebrow {
  font-family: var(--font-mono);
  font-size: 12px;
  color: var(--clr-accent);
  letter-spacing: 3px;
  text-transform: uppercase;
  margin-bottom: 12px;
}

.section-title {
  font-family: var(--font-head);
  font-size: 52px;
  font-weight: 700;
  letter-spacing: -2px;
  color: var(--clr-white);
  margin: 0;
}

.process-steps {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 0;
  border: 1px solid var(--clr-border);
  border-radius: 20px;
  overflow: hidden;
}

.process-step {
  padding: 48px 36px;
  border-right: 1px solid var(--clr-border);
  transition: var(--transition);
  position: relative;
}

.process-step:last-child { border-right: none; }

.process-step:hover {
  background: rgba(69,208,189,0.04);
}

.ps-num {
  font-family: var(--font-head);
  font-size: 52px;
  font-weight: 800;
  color: rgba(255,255,255,0.06);
  line-height: 1;
  margin-bottom: 24px;
}

.ps-line {
  width: 32px; height: 2px;
  background: var(--grad-teal);
  margin-bottom: 20px;
  transition: width 0.3s;
}

.process-step:hover .ps-line { width: 56px; }

.ps-title {
  font-family: var(--font-head);
  font-size: 16px;
  font-weight: 600;
  color: var(--clr-white);
  margin: 0 0 10px;
}

.ps-desc {
  font-size: 13px;
  color: rgba(255,255,255,0.45);
  line-height: 1.6;
}

/* ═══════════════════════════════
   ENGINE SECTION
═══════════════════════════════ */
.engine-section {
  padding: 100px 20px;
  background: var(--clr-bg);
}

.engine-inner {
  max-width: 1320px;
  margin: 0 auto;
}

.engine-head {
  max-width: 600px;
  margin-bottom: 60px;
}

.engine-sub {
  font-size: 16px;
  color: rgba(255,255,255,0.5);
  line-height: 1.7;
  margin-top: 16px;
}

.engine-box {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 24px;
  background: var(--clr-surface);
  border: 1px solid var(--clr-border);
  border-radius: 24px;
  padding: 40px;
}

.ebox-panel {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.ebox-label {
  display: flex;
  align-items: center;
  gap: 12px;
  font-family: var(--font-mono);
  font-size: 12px;
  color: rgba(255,255,255,0.4);
  padding-bottom: 16px;
  border-bottom: 1px solid var(--clr-border);
}

.ebox-num {
  font-size: 28px;
  font-weight: 800;
  color: rgba(255,255,255,0.06);
  font-family: var(--font-head);
  line-height: 1;
}

.ebox-meta { margin-left: auto; color: rgba(255,255,255,0.3); }

.drop-area {
  flex: 1;
  min-height: 200px;
  border: 1.5px dashed rgba(255,255,255,0.1);
  border-radius: 16px;
  background: rgba(255,255,255,0.02);
  display: flex; align-items: center; justify-content: center;
  cursor: pointer;
  transition: var(--transition);
  overflow-y: auto;
}

.drop-area.active, .drop-area:hover {
  border-color: var(--clr-accent);
  background: rgba(69,208,189,0.04);
}

.drop-area.filled { align-items: flex-start; }

.drop-empty { text-align: center; color: rgba(255,255,255,0.3); padding: 20px; }
.drop-up-icon { font-size: 2rem; margin-bottom: 10px; }
.drop-empty p { font-size: 14px; margin-bottom: 4px; }
.drop-empty small { font-size: 12px; }

.drop-files { width: 100%; padding: 16px; display: flex; flex-direction: column; gap: 10px; }
.drop-file-row {
  display: flex; justify-content: space-between; align-items: center;
  background: rgba(255,255,255,0.04); border: 1px solid var(--clr-border);
  padding: 10px 16px; border-radius: 10px;
  font-family: var(--font-mono); font-size: 13px; color: var(--clr-white);
}
.drop-rm { background: none; border: none; color: rgba(255,255,255,0.4); cursor: pointer; font-size: 1.1rem; }
.drop-rm:hover { color: #ef6464; }

.prompt-area { position: relative; flex: 1; }

.prompt-ta {
  width: 100%;
  min-height: 200px;
  background: rgba(255,255,255,0.02);
  border: 1.5px solid rgba(255,255,255,0.08);
  border-radius: 16px;
  color: var(--clr-white);
  font-family: var(--font-mono);
  font-size: 14px;
  line-height: 1.7;
  padding: 20px;
  resize: vertical;
  outline: none;
  transition: border-color 0.2s;
}

.prompt-ta:focus { border-color: var(--clr-accent); }
.prompt-ta::placeholder { color: rgba(255,255,255,0.2); }

.prompt-badge {
  position: absolute; bottom: 14px; right: 16px;
  font-family: var(--font-mono); font-size: 11px;
  color: rgba(255,255,255,0.2);
}

.launch-btn {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 65px;
  padding: 0 28px;
  background: var(--clr-red);
  color: var(--clr-white);
  border: none;
  border-radius: var(--radius-btn);
  font-family: var(--font-body);
  font-size: 16px;
  font-weight: 700;
  cursor: pointer;
  transition: var(--transition);
  letter-spacing: 0.5px;
}

.launch-btn i { font-style: normal; font-size: 1.3em; }
.launch-btn:hover:not(:disabled) { background: #f57e7e; transform: translateY(-2px); box-shadow: 0 10px 30px rgba(239,100,100,0.3); }
.launch-btn:disabled { background: rgba(255,255,255,0.06); color: rgba(255,255,255,0.2); cursor: not-allowed; }

/* ═══════════════════════════════
   HISTORY
═══════════════════════════════ */
.history-section {
  padding: 60px 20px 100px;
  background: var(--clr-surface);
}

/* ═══════════════════════════════
   RESPONSIVE
═══════════════════════════════ */
@media (max-width: 1100px) {
  .cards-container { grid-template-columns: 1fr 1fr; }
  .srv-card-3 { display: none; }
  .process-steps { grid-template-columns: repeat(3, 1fr); }
  .engine-box { grid-template-columns: 1fr; }
  .hero-content { flex-direction: column; }
  .hero-right { width: 100%; }
  .hero-card-stats { flex-wrap: wrap; }
}

@media (max-width: 768px) {
  .hero-title { font-size: 44px; }
  .section-title { font-size: 36px; }
  .cards-container { grid-template-columns: 1fr; }
  .srv-card-3 { display: block; }
  .process-steps { grid-template-columns: 1fr 1fr; }
  .header-nav { display: none; }
  .hero-wrap { border-radius: 20px; }
}
</style>
