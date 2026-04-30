<template>
  <div class="pw">

    <!-- NAVBAR -->
    <header class="hdr" :class="{ sticky: isSticky }">
      <div class="hdr-inner">
        <div class="hdr-logo">
          <img src="../assets/logo_bot.png" alt="Botopolis" class="hdr-logo-img" />
        </div>
        <nav class="hdr-nav">
          <a class="hdr-link active" href="#">Home</a>
          <a class="hdr-link" @click="scrollToSteps" style="cursor:pointer">{{ $t('home.workflowSequence') }}</a>
          <a class="hdr-link" @click="scrollToStart" style="cursor:pointer">{{ $t('home.startEngine') }}</a>
        </nav>
        <div class="hdr-right">
          <LanguageSwitcher />
        </div>
      </div>
    </header>

    <!-- HERO: full-bleed, no margin, abstract bg -->
    <section class="hero">
      <div class="hero-bg-anim">
        <div class="hba-layer hba-l1"></div>
        <div class="hba-layer hba-l2"></div>
        <div class="hba-layer hba-l3"></div>
        <div class="hba-noise"></div>
        <div class="hba-bottom-fade"></div>
      </div>
      <div class="hero-body">

        <!-- LEFT: Text -->
        <div class="hero-text">
          <div class="hero-eyebrow">
            <span class="hero-eyebrow-dot"></span>
            {{ $t('home.tagline') }}
          </div>
          <h1 class="hero-h1">
            {{ $t('home.heroTitle1') }}<br>
            {{ $t('home.heroTitle2') }}
          </h1>
          <p class="hero-sub">
            <i18n-t keypath="home.heroDesc" tag="span">
              <template #brand><strong>{{ $t('home.heroDescBrand') }}</strong></template>
              <template #agentScale><span class="hero-accent">{{ $t('home.heroDescAgentScale') }}</span></template>
              <template #optimalSolution><em class="hero-em">{{ $t('home.heroDescOptimalSolution') }}</em></template>
            </i18n-t>
          </p>
          <p class="hero-slogan">{{ $t('home.slogan') }}</p>
          <div class="hero-actions">
            <button class="btn-discover" @click="scrollToStart">
              <span>{{ $t('home.startEngine') }}</span>
              <i>&#8599;</i>
            </button>
            <button class="btn-ghost-hero" @click="scrollToSteps">
              {{ $t('home.workflowSequence') }} &#8595;
            </button>
          </div>
          <div class="hero-stats-row">
            <div class="hsr-item">
              <span class="hsr-num">{{ $t('home.metricLowCostDesc') }}</span>
              <span class="hsr-lbl">{{ $t('home.metricLowCost') }}</span>
            </div>
            <div class="hsr-div"></div>
            <div class="hsr-item">
              <span class="hsr-num">&#8734;</span>
              <span class="hsr-lbl">{{ $t('home.metricHighAvailDesc') }}</span>
            </div>
            <div class="hsr-div"></div>
            <div class="hsr-item">
              <span class="hsr-num">5</span>
              <span class="hsr-lbl">Steps</span>
            </div>
          </div>
        </div>

        <!-- RIGHT: Animated Network Visualization -->
        <div class="hero-visual">
          <div class="hv-glow"></div>
          <svg class="hv-svg" viewBox="0 0 460 400" xmlns="http://www.w3.org/2000/svg">
            <circle cx="230" cy="200" r="150" fill="none" stroke="rgba(69,208,189,0.06)" stroke-width="1"/>
            <circle cx="230" cy="200" r="100" fill="none" stroke="rgba(69,208,189,0.08)" stroke-width="1"/>
            <circle cx="230" cy="200" r="50"  fill="none" stroke="rgba(69,208,189,0.12)" stroke-width="1"/>
            <line x1="230" y1="200" x2="90"  y2="80"  stroke="rgba(69,208,189,0.4)"  stroke-width="1.5"/>
            <line x1="230" y1="200" x2="370" y2="80"  stroke="rgba(100,150,255,0.4)" stroke-width="1.5"/>
            <line x1="230" y1="200" x2="60"  y2="230" stroke="rgba(69,208,189,0.3)"  stroke-width="1"/>
            <line x1="230" y1="200" x2="400" y2="230" stroke="rgba(100,150,255,0.3)" stroke-width="1"/>
            <line x1="230" y1="200" x2="140" y2="340" stroke="rgba(130,100,255,0.3)" stroke-width="1"/>
            <line x1="230" y1="200" x2="320" y2="340" stroke="rgba(69,208,189,0.3)"  stroke-width="1"/>
            <line x1="230" y1="200" x2="230" y2="50"  stroke="rgba(255,255,255,0.15)" stroke-width="1"/>
            <line x1="90"  y1="80"  x2="370" y2="80"  stroke="rgba(255,255,255,0.08)" stroke-width="1"/>
            <line x1="60"  y1="230" x2="140" y2="340" stroke="rgba(255,255,255,0.06)" stroke-width="1"/>
            <line x1="400" y1="230" x2="320" y2="340" stroke="rgba(255,255,255,0.06)" stroke-width="1"/>
            <g class="hv-node hv-n1"><circle cx="90"  cy="80"  r="14" fill="#45d0bd" opacity="0.9"/><circle cx="90"  cy="80"  r="22" fill="none" stroke="#45d0bd" stroke-width="1" opacity="0.3"/></g>
            <g class="hv-node hv-n2"><circle cx="370" cy="80"  r="12" fill="#6366f1" opacity="0.9"/><circle cx="370" cy="80"  r="20" fill="none" stroke="#6366f1" stroke-width="1" opacity="0.3"/></g>
            <g class="hv-node hv-n3"><circle cx="60"  cy="230" r="10" fill="#44b6e9" opacity="0.85"/></g>
            <g class="hv-node hv-n4"><circle cx="400" cy="230" r="11" fill="#45d0bd" opacity="0.85"/></g>
            <g class="hv-node hv-n5"><circle cx="140" cy="340" r="9"  fill="#818cf8" opacity="0.8"/></g>
            <g class="hv-node hv-n6"><circle cx="320" cy="340" r="10" fill="#45d0bd" opacity="0.8"/></g>
            <g class="hv-node hv-n7"><circle cx="230" cy="50"  r="8"  fill="#f472b6" opacity="0.75"/></g>
            <circle cx="160" cy="130" r="4" fill="rgba(255,255,255,0.4)" class="hv-dot"/>
            <circle cx="300" cy="130" r="4" fill="rgba(255,255,255,0.4)" class="hv-dot"/>
            <circle cx="150" cy="270" r="3" fill="rgba(255,255,255,0.3)" class="hv-dot"/>
            <circle cx="310" cy="265" r="3" fill="rgba(255,255,255,0.3)" class="hv-dot"/>
            <circle cx="230" cy="200" r="30" fill="rgba(69,208,189,0.12)" stroke="#45d0bd" stroke-width="1.5"/>
            <circle cx="230" cy="200" r="30" fill="none" stroke="#45d0bd" stroke-width="2" class="hv-pulse-ring"/>
            <circle cx="230" cy="200" r="14" fill="#45d0bd"/>
            <text x="230" y="205" text-anchor="middle" font-family="Sora,Arial" font-size="9" font-weight="700" fill="#000">AI</text>
            <circle r="3.5" fill="#ffffff" opacity="0.95" class="hv-pkt hv-pkt1"/>
            <circle r="3"   fill="#45d0bd" opacity="0.9"  class="hv-pkt hv-pkt2"/>
            <circle r="3"   fill="#818cf8" opacity="0.9"  class="hv-pkt hv-pkt3"/>
            <circle r="2.5" fill="#f472b6" opacity="0.85" class="hv-pkt hv-pkt4"/>
          </svg>
          <div class="hv-card hv-card-tl">
            <span class="hvc-dot-green"></span>
            <div>
              <span class="hvc-label">{{ $t('home.systemReady') }}</span>
              <span class="hvc-sub">Engine online</span>
            </div>
          </div>
          <div class="hv-card hv-card-br">
            <span class="hvc-num">&#8734;</span>
            <span class="hvc-label">{{ $t('home.metricHighAvailDesc') }}</span>
          </div>
        </div>

      </div>
    </section>

    <!-- SERVICE CARDS: 3 colored cards like Aiero -->
    <section class="srv-sec">
      <!-- Card 1: Teal -->
      <div class="srv-card sc1" ref="stepsRef">
        <div class="sc-visual sc-vis1"></div>
        <div class="sc-tags">
          <span class="sc-tag">{{ $t('home.step01Title') }}</span>
          <span class="sc-tag">{{ $t('home.step02Title') }}</span>
        </div>
        <h3 class="sc-title">{{ $t('home.heroTitle1') }}<br>{{ $t('home.heroTitle2') }}</h3>
        <a class="sc-link" @click="scrollToStart" style="cursor:pointer">{{ $t('home.startEngine') }} &#8594;</a>
        <div class="sc-arrow" @click="scrollToStart" style="cursor:pointer">&#8599;</div>
      </div>
      <!-- Card 2: Purple -->
      <div class="srv-card sc2">
        <div class="sc-visual sc-vis2"></div>
        <div class="sc-inner">
          <h3 class="sc-title">{{ $t('home.step03Title') }}</h3>
          <p class="sc-desc">{{ $t('home.step03Desc') }}</p>
          <div class="sc-agents">
            <div class="sc-avatar" v-for="n in 5" :key="n">{{ n }}</div>
            <span class="sc-user-count">{{ $t('home.metricHighAvailDesc') }}</span>
          </div>
          <div class="sc-bignum">&#8734;</div>
        </div>
        <div class="sc-arrow">&#8599;</div>
      </div>
      <!-- Card 3: Lavender -->
      <div class="srv-card sc3">
        <div class="sc-visual sc-vis3"></div>
        <div class="sc-inner">
          <h3 class="sc-title">{{ $t('home.step04Title') }} +<br>{{ $t('home.step05Title') }}</h3>
          <p class="sc-desc">{{ $t('home.step04Desc') }}</p>
          <div class="sc-icon-circle">
            <span>&#9711;</span>
          </div>
        </div>
      </div>
    </section>

    <!-- HOW IT WORKS -->
    <section class="proc-sec" >
      <div class="proc-inner">
        <div class="sec-head">
          <p class="sec-eye">{{ $t('home.workflowSequence') }}</p>
          <h2 class="sec-title">{{ $t('home.systemReady') }}</h2>
          <p class="sec-sub">{{ $t('home.systemReadyDesc') }}</p>
        </div>
        <div class="proc-grid">
          <div class="proc-item" v-for="(step, i) in steps" :key="i">
            <span class="proc-num">{{ String(i+1).padStart(2,'0') }}</span>
            <div class="proc-bar"></div>
            <h4 class="proc-title">{{ step.title }}</h4>
            <p class="proc-desc">{{ step.desc }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- ENGINE -->
    <section class="eng-sec" ref="startRef">
      <div class="eng-inner">
        <div class="sec-head">
          <p class="sec-eye">&gt;_ Engine</p>
          <h2 class="sec-title">{{ $t('home.startEngine') }}</h2>
        </div>
        <div class="eng-grid">
          <!-- Upload -->
          <div class="eng-panel">
            <div class="eng-panel-head">
              <span class="eng-pnum">01</span>
              <span class="eng-plabel">{{ $t('home.realitySeed') }}</span>
              <span class="eng-pmeta">{{ $t('home.supportedFormats') }}</span>
            </div>
            <div class="drop-z"
              :class="{ dragging: isDragOver, filled: files.length > 0 }"
              @dragover.prevent="handleDragOver"
              @dragleave.prevent="handleDragLeave"
              @drop.prevent="handleDrop"
              @click="triggerFileInput">
              <input ref="fileInput" type="file" multiple accept=".pdf,.md,.txt"
                @change="handleFileSelect" style="display:none" :disabled="loading"/>
              <div v-if="files.length===0" class="drop-empty">
                <span class="drop-up">&#8593;</span>
                <p>{{ $t('home.dragToUpload') }}</p>
                <small>{{ $t('home.orBrowse') }}</small>
              </div>
              <div v-else class="drop-flist">
                <div v-for="(f,i) in files" :key="i" class="drop-frow">
                  <span>&#128196; {{ f.name }}</span>
                  <button @click.stop="removeFile(i)" class="drop-rm">&#215;</button>
                </div>
              </div>
            </div>
          </div>
          <!-- Prompt -->
          <div class="eng-panel">
            <div class="eng-panel-head">
              <span class="eng-pnum">02</span>
              <span class="eng-plabel">{{ $t('home.inputParams') }}</span>
            </div>
            <div class="prompt-wrap">
              <textarea class="prompt-ta" v-model="formData.simulationRequirement"
                :placeholder="$t('home.promptPlaceholder')" rows="8" :disabled="loading"></textarea>
              <span class="prompt-badge">{{ $t('home.engineBadge') }}</span>
            </div>
            <button class="launch-btn" @click="startSimulation" :disabled="!canSubmit||loading">
              <span>{{ loading ? $t('home.initializing') : $t('home.startEngine') }}</span>
              <i>&#8599;</i>
            </button>
          </div>
        </div>
      </div>
    </section>

    <!-- HISTORY -->
    <section class="hist-sec">
      <div class="eng-inner">
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

<style>
/* Global base — not scoped so it always applies */
body { margin: 0; padding: 0; background: #111111; color: #ffffff; }
.pw { min-height: 100vh; background: #111111; color: #ffffff; font-family: 'Manrope', 'Sora', Arial, sans-serif; }

/* ── NAVBAR ── */
.hdr { position: fixed; top: 0; left: 0; right: 0; z-index: 500; padding: 0 48px; transition: background 0.3s, border 0.3s; }
.hdr.sticky { background: rgba(17,17,17,0.95); backdrop-filter: blur(20px); border-bottom: 1px solid rgba(255,255,255,0.08); }
.hdr-inner { max-width: 1320px; margin: 0 auto; height: 90px; display: flex; align-items: center; justify-content: space-between; }
.hdr-logo { font-family: 'Sora', Arial, sans-serif; font-weight: 800; font-size: 1.25rem; letter-spacing: 2px; color: #ffffff; }
.hdr-nav { display: flex; gap: 40px; }
.hdr-link { font-size: 15px; font-weight: 500; color: rgba(255,255,255,0.8); text-decoration: none; transition: color 0.2s; }
.hdr-link:hover, .hdr-link.active { color: #ffffff; }
.hdr-right { display: flex; align-items: center; gap: 20px; }
.hdr-cta { display: inline-flex; align-items: center; gap: 8px; height: 46px; padding: 0 24px; border: 1.5px solid rgba(255,255,255,0.25); border-radius: 100px; font-size: 14px; font-weight: 600; color: #ffffff; text-decoration: none; transition: all 0.3s; }
.hdr-cta:hover { border-color: #45d0bd; color: #45d0bd; }
.hdr-cta i { font-style: normal; }

/* ── HERO ── */
.hero { position: relative; min-height: 100vh; overflow: hidden; display: flex; flex-direction: column; justify-content: center; padding-top: 80px; }
.hero-bg-anim { position: absolute; inset: 0; }

/* Abstract wave layers mimicking the reference screenshot */
.hba-layer { position: absolute; inset: 0; }
.hba-l1 { background: linear-gradient(135deg, #1a0050 0%, #2d0080 20%, #0044cc 45%, #0088ff 60%, #00ccbb 80%, #45d0bd 100%); }
.hba-l2 { background: repeating-linear-gradient( 25deg, transparent 0px, transparent 40px, rgba(255,255,255,0.04) 40px, rgba(255,255,255,0.04) 41px ); }
.hba-l3 { background: radial-gradient(ellipse 80% 60% at 60% 40%, rgba(0,136,255,0.3) 0%, transparent 70%), radial-gradient(ellipse 50% 80% at 80% 60%, rgba(69,208,189,0.25) 0%, transparent 60%), radial-gradient(ellipse 40% 40% at 30% 30%, rgba(120,0,200,0.3) 0%, transparent 50%); animation: wave-move 20s ease-in-out infinite alternate; }
@keyframes wave-move { 0%{transform:scale(1) rotate(0deg)} 100%{transform:scale(1.1) rotate(3deg)} }
.hba-noise { position: absolute; inset: 0; opacity: 0.04; background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E"); background-size: 200px; }
.hba-bottom-fade { position: absolute; bottom: 0; left: 0; right: 0; height: 260px; background: linear-gradient(to bottom, transparent, #111111); }

.hero-body { position: relative; z-index: 1; max-width: 1320px; margin: 0 auto; padding: 60px 48px; display: flex; align-items: center; justify-content: space-between; gap: 60px; width: 100%; }
.hero-text { max-width: 780px; padding-bottom: 20px; }
.hero-h1 { font-family: 'Sora', Arial, sans-serif; font-size: 72px; font-weight: 600; line-height: 1.1; color: #ffffff; margin: 0 0 24px; letter-spacing: -2px; }
.hero-sub { font-size: 16px; color: rgba(255,255,255,0.7); margin: 0 0 36px; line-height: 1.5; max-width: 480px; }

.btn-discover { display: inline-flex; align-items: center; gap: 16px; height: 65px; padding: 0 36px; background: #ef6464; color: #ffffff; border: none; border-radius: 15px; font-family: 'Manrope', Arial, sans-serif; font-size: 16px; font-weight: 600; cursor: pointer; transition: all 0.3s; }
.btn-discover i { font-style: normal; font-size: 1.1em; }
.btn-discover:hover { background: #f57e7e; transform: translateY(-2px); box-shadow: 0 12px 32px rgba(239,100,100,0.4); }

.hero-badge-box { background: #ffffff; color: #111111; border-radius: 20px; padding: 28px 32px; display: flex; align-items: center; gap: 24px; min-width: 340px; margin-bottom: 20px; }
.hbb-stat { display: flex; flex-direction: column; gap: 4px; }
.hbb-num { font-family: 'Sora', Arial, sans-serif; font-size: 28px; font-weight: 700; color: #45d0bd; }
.hbb-label { font-size: 13px; color: #666666; }
.hbb-divider { width: 1px; height: 40px; background: #e5e5e5; }

/* ── SERVICE CARDS ── */
.srv-sec { display: grid; grid-template-columns: 1.8fr 1.4fr 1fr; gap: 0; }
.srv-card { position: relative; min-height: 420px; overflow: hidden; padding: 40px 44px; display: flex; flex-direction: column; justify-content: flex-end; }
.sc-visual { position: absolute; inset: 0; transition: transform 0.6s cubic-bezier(0.23,1,0.32,1); }
.srv-card:hover .sc-visual { transform: scale(1.05); }
.sc1 { background: #2ecfb5; }
.sc-vis1 { background: linear-gradient(135deg, #1ab8a0 0%, #45d0bd 40%, #2ecfb5 100%); }
.sc2 { background: #7b5ea7; }
.sc-vis2 { background: linear-gradient(135deg, #5b3d87 0%, #7b5ea7 40%, #9b7ec7 100%); }
.sc3 { background: #b8a4d4; }
.sc-vis3 { background: linear-gradient(135deg, #9888c0 0%, #b8a4d4 50%, #cfc0e8 100%); }

/* Large decorative shapes inside cards */
.sc-vis1::after { content: ''; position: absolute; right: -20px; bottom: -40px; width: 280px; height: 280px; border-radius: 50%; background: rgba(255,255,255,0.12); }
.sc-vis2::after { content: ''; position: absolute; right: 20px; bottom: -20px; font-family: 'Sora'; font-size: 160px; font-weight: 900; color: rgba(255,255,255,0.12); }
.sc-vis3::after { content: ''; position: absolute; right: 10px; top: 20px; width: 180px; height: 180px; border: 20px solid rgba(255,255,255,0.15); border-radius: 50%; }

.sc-tags { position: relative; z-index: 1; display: flex; gap: 8px; margin-bottom: 20px; }
.sc-tag { font-size: 12px; font-weight: 500; color: rgba(255,255,255,0.9); border: 1px solid rgba(255,255,255,0.4); padding: 4px 14px; border-radius: 100px; background: rgba(255,255,255,0.1); }
.sc-title { position: relative; z-index: 1; font-family: 'Sora', Arial, sans-serif; font-size: 38px; font-weight: 400; color: #ffffff; line-height: 1.15; margin: 0 0 20px; }
.sc-link { position: relative; z-index: 1; font-size: 14px; font-weight: 500; color: #ffffff; text-decoration: none; border-bottom: 1px solid rgba(255,255,255,0.6); padding-bottom: 2px; width: fit-content; transition: all 0.2s; }
.sc-link:hover { color: #ffffff; border-color: #ffffff; padding-left: 8px; }
.sc-arrow { position: absolute; top: 24px; right: 24px; z-index: 2; width: 44px; height: 44px; background: rgba(0,0,0,0.2); border-radius: 12px; display: flex; align-items: center; justify-content: center; font-size: 18px; color: #ffffff; cursor: pointer; transition: all 0.2s; }
.sc-arrow:hover { background: rgba(0,0,0,0.4); }
.sc-inner { position: relative; z-index: 1; }
.sc-desc { font-size: 14px; color: rgba(255,255,255,0.8); line-height: 1.6; margin: 8px 0 16px; }
.sc-agents { display: flex; align-items: center; gap: 4px; margin-bottom: 8px; }
.sc-avatar { width: 32px; height: 32px; border-radius: 50%; background: rgba(255,255,255,0.3); border: 2px solid rgba(255,255,255,0.5); display: flex; align-items: center; justify-content: center; font-size: 11px; font-weight: 700; color: #fff; margin-left: -6px; }
.sc-avatar:first-child { margin-left: 0; }
.sc-user-count { font-size: 12px; color: rgba(255,255,255,0.8); margin-left: 10px; }
.sc-bignum { font-family: 'Sora', Arial, sans-serif; font-size: 80px; font-weight: 800; color: rgba(255,255,255,0.25); line-height: 1; margin-top: 8px; }
.sc-icon-circle { width: 60px; height: 60px; border-radius: 50%; border: 2px solid rgba(255,255,255,0.4); display: flex; align-items: center; justify-content: center; font-size: 24px; color: rgba(255,255,255,0.7); margin-top: 20px; }

/* ── PROCESS ── */
.proc-sec { padding: 100px 48px; background: #1a1a1a; }
.proc-inner { max-width: 1320px; margin: 0 auto; }
.sec-head { margin-bottom: 56px; }
.sec-eye { font-family: 'JetBrains Mono', monospace; font-size: 12px; color: #45d0bd; letter-spacing: 3px; text-transform: uppercase; margin: 0 0 12px; }
.sec-title { font-family: 'Sora', Arial, sans-serif; font-size: 52px; font-weight: 700; letter-spacing: -2px; color: #ffffff; margin: 0 0 16px; }
.sec-sub { font-size: 16px; color: rgba(255,255,255,0.5); line-height: 1.7; max-width: 520px; margin: 0; }
.proc-grid { display: grid; grid-template-columns: repeat(5, 1fr); border: 1px solid rgba(255,255,255,0.08); border-radius: 20px; overflow: hidden; }
.proc-item { padding: 44px 32px; border-right: 1px solid rgba(255,255,255,0.08); transition: background 0.2s; }
.proc-item:last-child { border-right: none; }
.proc-item:hover { background: rgba(69,208,189,0.04); }
.proc-num { font-family: 'Sora', Arial, sans-serif; font-size: 52px; font-weight: 800; color: rgba(255,255,255,0.05); display: block; margin-bottom: 20px; line-height: 1; }
.proc-bar { width: 32px; height: 2px; background: linear-gradient(90deg, #45d0bd, #44b6e9); margin-bottom: 20px; transition: width 0.3s; }
.proc-item:hover .proc-bar { width: 52px; }
.proc-title { font-family: 'Sora', Arial, sans-serif; font-size: 15px; font-weight: 600; color: #ffffff; margin: 0 0 10px; }
.proc-desc { font-size: 12px; color: rgba(255,255,255,0.4); line-height: 1.6; margin: 0; }

/* ── ENGINE ── */
.eng-sec { padding: 100px 48px; background: #111111; }
.eng-inner { max-width: 1320px; margin: 0 auto; }
.eng-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 24px; background: #1a1a1a; border: 1px solid rgba(255,255,255,0.06); border-radius: 24px; padding: 40px; }
.eng-panel { display: flex; flex-direction: column; gap: 20px; }
.eng-panel-head { display: flex; align-items: center; gap: 12px; font-family: 'JetBrains Mono', monospace; font-size: 12px; color: rgba(255,255,255,0.4); padding-bottom: 16px; border-bottom: 1px solid rgba(255,255,255,0.06); }
.eng-pnum { font-family: 'Sora', Arial, sans-serif; font-size: 28px; font-weight: 800; color: rgba(255,255,255,0.05); line-height: 1; }
.eng-plabel { color: rgba(255,255,255,0.4); }
.eng-pmeta { margin-left: auto; color: rgba(255,255,255,0.25); }

.drop-z { flex: 1; min-height: 200px; border: 1.5px dashed rgba(255,255,255,0.1); border-radius: 16px; background: rgba(255,255,255,0.02); display: flex; align-items: center; justify-content: center; cursor: pointer; transition: all 0.2s; overflow-y: auto; }
.drop-z.dragging, .drop-z:hover { border-color: #45d0bd; background: rgba(69,208,189,0.04); }
.drop-z.filled { align-items: flex-start; }
.drop-empty { text-align: center; color: rgba(255,255,255,0.3); padding: 20px; }
.drop-up { font-size: 2rem; display: block; margin-bottom: 10px; }
.drop-empty p { font-size: 14px; margin: 0 0 4px; color: rgba(255,255,255,0.35); }
.drop-empty small { font-size: 12px; color: rgba(255,255,255,0.2); }
.drop-flist { width: 100%; padding: 16px; display: flex; flex-direction: column; gap: 8px; }
.drop-frow { display: flex; justify-content: space-between; align-items: center; background: rgba(255,255,255,0.04); border: 1px solid rgba(255,255,255,0.06); padding: 10px 14px; border-radius: 10px; font-family: 'JetBrains Mono', monospace; font-size: 13px; color: #ffffff; }
.drop-rm { background: none; border: none; color: rgba(255,255,255,0.3); cursor: pointer; font-size: 1.1rem; }
.drop-rm:hover { color: #ef6464; }

.prompt-wrap { position: relative; flex: 1; }
.prompt-ta { width: 100%; min-height: 200px; background: rgba(255,255,255,0.02); border: 1.5px solid rgba(255,255,255,0.08); border-radius: 16px; color: #ffffff; font-family: 'JetBrains Mono', monospace; font-size: 14px; line-height: 1.7; padding: 20px; resize: vertical; outline: none; transition: border-color 0.2s; box-sizing: border-box; }
.prompt-ta:focus { border-color: #45d0bd; }
.prompt-ta::placeholder { color: rgba(255,255,255,0.2); }
.prompt-badge { position: absolute; bottom: 14px; right: 16px; font-family: 'JetBrains Mono', monospace; font-size: 11px; color: rgba(255,255,255,0.2); }

.launch-btn { display: flex; align-items: center; justify-content: space-between; height: 65px; padding: 0 28px; background: #ef6464; color: #ffffff; border: none; border-radius: 15px; font-family: 'Manrope', Arial, sans-serif; font-size: 16px; font-weight: 700; cursor: pointer; transition: all 0.3s; }
.launch-btn i { font-style: normal; font-size: 1.3em; }
.launch-btn:hover:not(:disabled) { background: #f57e7e; transform: translateY(-2px); box-shadow: 0 12px 32px rgba(239,100,100,0.35); }
.launch-btn:disabled { background: rgba(255,255,255,0.06); color: rgba(255,255,255,0.25); cursor: not-allowed; }

/* ── HISTORY ── */
.hist-sec { padding: 60px 48px 100px; background: #1a1a1a; }

/* ── RESPONSIVE ── */
@media (max-width: 1024px) {
  .hero-h1 { font-size: 52px; }
  .srv-sec { grid-template-columns: 1fr 1fr; }
  .srv-card:last-child { grid-column: 1 / -1; }
  .proc-grid { grid-template-columns: repeat(3, 1fr); }
  .eng-grid { grid-template-columns: 1fr; }
  .hero-body { flex-direction: column; align-items: flex-start; padding-bottom: 60px; }
}
@media (max-width: 768px) {
  .hero-h1 { font-size: 38px; }
  .sec-title { font-size: 36px; }
  .srv-sec { grid-template-columns: 1fr; }
  .proc-grid { grid-template-columns: 1fr 1fr; }
  .hdr-nav { display: none; }
  .hdr { padding: 0 20px; }
  .hero-body { padding: 0 20px 60px; }
  .proc-sec, .eng-sec, .hist-sec { padding-left: 20px; padding-right: 20px; }
}

/* Hero Eyebrow */
.hero-eyebrow { display: inline-flex; align-items: center; gap: 8px; font-family: 'JetBrains Mono', monospace; font-size: 12px; color: #45d0bd; letter-spacing: 2px; text-transform: uppercase; margin-bottom: 20px; background: rgba(69,208,189,0.1); padding: 7px 16px; border-radius: 100px; border: 1px solid rgba(69,208,189,0.3); }
.hero-eyebrow-dot { width: 6px; height: 6px; background: #22C55E; border-radius: 50%; animation: pulse-dot 2s ease-in-out infinite; }
@keyframes pulse-dot { 0%,100%{opacity:1;transform:scale(1)} 50%{opacity:0.5;transform:scale(0.7)} }
.hero-accent { color: #45d0bd; font-weight: 700; }
.hero-sub em { font-style: normal; background: rgba(255,255,255,0.1); padding: 1px 6px; border-radius: 4px; }
.hero-slogan { font-size: 15px; color: rgba(255,255,255,0.5); margin: 0 0 32px; font-style: italic; }
.hero-actions { display: flex; gap: 16px; align-items: center; margin-bottom: 40px; flex-wrap: wrap; }
.btn-learn { background: transparent; border: none; color: rgba(255,255,255,0.6); font-family: 'Manrope', Arial, sans-serif; font-size: 15px; font-weight: 500; cursor: pointer; transition: color 0.2s; padding: 0; }
.btn-learn:hover { color: #ffffff; }
/* Mini stats */
.hero-mini-stats { display: flex; align-items: center; gap: 20px; }
.hms-item { display: flex; flex-direction: column; gap: 3px; }
.hms-num { font-family: 'Sora', Arial, sans-serif; font-size: 22px; font-weight: 700; color: #45d0bd; }
.hms-lbl { font-size: 11px; color: rgba(255,255,255,0.4); }
.hms-divider { width: 1px; height: 32px; background: rgba(255,255,255,0.12); }
/* Hero visual */
.hero-visual { flex: 0 0 440px; position: relative; }
.hero-img-wrap { position: relative; }

.hero-overlay-card { position: absolute; bottom: 20px; left: 20px; right: 20px; background: rgba(255,255,255,0.12); backdrop-filter: blur(20px); border: 1px solid rgba(255,255,255,0.2); border-radius: 16px; padding: 18px 20px; display: flex; align-items: center; gap: 14px; }
.hoc-icon { font-size: 28px; color: #45d0bd; flex-shrink: 0; }
.hoc-info { flex: 1; }
.hoc-title { display: block; font-family: 'Sora', Arial, sans-serif; font-size: 15px; font-weight: 600; color: #ffffff; margin-bottom: 3px; }
.hoc-sub { font-size: 12px; color: rgba(255,255,255,0.6); }
.hoc-pulse { flex-shrink: 0; }
.hoc-dot { display: block; width: 10px; height: 10px; background: #22C55E; border-radius: 50%; box-shadow: 0 0 0 4px rgba(34,197,94,0.2); animation: pulse-ring 2s ease-in-out infinite; }
@keyframes pulse-ring { 0%,100%{box-shadow:0 0 0 4px rgba(34,197,94,0.2)} 50%{box-shadow:0 0 0 8px rgba(34,197,94,0)} }
/* Hero body layout update */
.hero-body { align-items: center !important; }
.hero-text { max-width: 580px !important; }


/* Network Animation */
.hero-anim-wrap { position: relative; width: 440px; height: 380px; flex-shrink: 0; }
.hero-network-svg { width: 100%; height: 100%; }
.net-node { animation: node-pulse 3s ease-in-out infinite; }
.n1 { animation-delay: 0s; }
.n2 { animation-delay: 0.6s; }
.n3 { animation-delay: 1.2s; }
.n4 { animation-delay: 0.9s; }
.n5 { animation-delay: 1.8s; }
.n6 { animation-delay: 0.3s; }
.ns1,.ns2,.ns3,.ns4 { animation: node-pulse 4s ease-in-out infinite; }
@keyframes node-pulse { 0%,100%{opacity:0.85;transform:scale(1)} 50%{opacity:1;transform:scale(1.3)} }
.net-center-pulse { animation: center-ring 2.5s ease-out infinite; transform-origin: 210px 180px; }
@keyframes center-ring { 0%{r:22;opacity:0.8} 100%{r:44;opacity:0} }
/* Packet animations along lines */
.pkt1 { animation: pkt-move-1 3s linear infinite; }
.pkt2 { animation: pkt-move-2 4s linear infinite 1s; }
.pkt3 { animation: pkt-move-3 3.5s linear infinite 0.5s; }
@keyframes pkt-move-1 { 0%{cx:210;cy:180} 100%{cx:80;cy:80} }
@keyframes pkt-move-2 { 0%{cx:80;cy:80} 100%{cx:340;cy:80} }
@keyframes pkt-move-3 { 0%{cx:210;cy:180} 100%{cx:360;cy:220} }
/* Floating badges */
.hav-badge { position: absolute; background: rgba(255,255,255,0.1); backdrop-filter: blur(16px); border: 1px solid rgba(255,255,255,0.15); border-radius: 14px; padding: 12px 18px; display: flex; flex-direction: column; gap: 2px; }
.hav-b1 { top: 20px; right: -10px; }
.hav-b2 { bottom: 30px; left: -10px; }
.hav-bn { font-family: 'Sora', Arial, sans-serif; font-size: 20px; font-weight: 700; color: #45d0bd; }
.hav-bl { font-size: 11px; color: rgba(255,255,255,0.5); }
/* Hero body fix */
.hero-body { align-items: center !important; }
.hero-text { max-width: 580px !important; flex: 1; }


/* ── Hero Visual (SVG Network) ── */
.hero-visual { flex: 0 0 460px; position: relative; height: 400px; }
.hv-glow { position: absolute; width: 300px; height: 300px; background: radial-gradient(circle, rgba(69,208,189,0.15) 0%, transparent 70%); top: 50%; left: 50%; transform: translate(-50%,-50%); border-radius: 50%; pointer-events: none; }
.hv-svg { width: 100%; height: 100%; }
/* Node pulse animations */
.hv-node { animation: hv-node-pulse 3s ease-in-out infinite; }
.hv-n1 { animation-delay: 0s; }
.hv-n2 { animation-delay: 0.5s; }
.hv-n3 { animation-delay: 1s; }
.hv-n4 { animation-delay: 1.5s; }
.hv-n5 { animation-delay: 2s; }
.hv-n6 { animation-delay: 0.8s; }
.hv-n7 { animation-delay: 1.3s; }
.hv-dot { animation: hv-node-pulse 4s ease-in-out infinite; }
@keyframes hv-node-pulse { 0%,100%{opacity:0.85} 50%{opacity:1;filter:brightness(1.3)} }
/* Center ring pulse */
.hv-pulse-ring { animation: hv-ring 2.5s ease-out infinite; transform-origin: 230px 200px; }
@keyframes hv-ring { 0%{opacity:0.7;r:30} 100%{opacity:0;r:60} }
/* Packet movement along lines */
.hv-pkt1 { animation: hv-p1 3s linear infinite; }
.hv-pkt2 { animation: hv-p2 4s linear infinite 0.8s; }
.hv-pkt3 { animation: hv-p3 3.5s linear infinite 1.5s; }
.hv-pkt4 { animation: hv-p4 5s linear infinite 0.3s; }
@keyframes hv-p1 { 0%{cx:230;cy:200} 100%{cx:90;cy:80} }
@keyframes hv-p2 { 0%{cx:230;cy:200} 100%{cx:370;cy:80} }
@keyframes hv-p3 { 0%{cx:230;cy:200} 100%{cx:400;cy:230} }
@keyframes hv-p4 { 0%{cx:230;cy:200} 100%{cx:140;cy:340} }
/* Floating cards on the SVG */
.hv-card { position: absolute; display: flex; align-items: center; gap: 10px; background: rgba(255,255,255,0.1); backdrop-filter: blur(16px); border: 1px solid rgba(255,255,255,0.18); border-radius: 14px; padding: 12px 16px; white-space: nowrap; }
.hv-card-tl { top: 10px; left: 0px; }
.hv-card-br { bottom: 20px; right: 0px; }
.hvc-dot-green { width: 9px; height: 9px; background: #22C55E; border-radius: 50%; flex-shrink: 0; box-shadow: 0 0 0 3px rgba(34,197,94,0.25); animation: hv-ring 2s ease-out infinite; }
.hvc-label { display: block; font-family: 'Sora', Arial, sans-serif; font-size: 13px; font-weight: 600; color: #ffffff; }
.hvc-sub { display: block; font-size: 11px; color: rgba(255,255,255,0.5); margin-top: 2px; }
.hvc-num { font-family: 'Sora', Arial, sans-serif; font-size: 24px; font-weight: 700; color: #45d0bd; }
/* Hero text extras */
.hero-eyebrow { display: inline-flex; align-items: center; gap: 8px; font-family: 'JetBrains Mono', monospace; font-size: 11px; color: #45d0bd; letter-spacing: 2px; text-transform: uppercase; margin-bottom: 20px; background: rgba(69,208,189,0.1); padding: 6px 14px; border-radius: 100px; border: 1px solid rgba(69,208,189,0.3); }
.hero-eyebrow-dot { width: 6px; height: 6px; background: #22C55E; border-radius: 50%; animation: hv-blink 2s ease-in-out infinite; }
@keyframes hv-blink { 0%,100%{opacity:1} 50%{opacity:0.4} }
.hero-accent { color: #45d0bd; font-weight: 700; }
.hero-em { font-style: normal; background: rgba(255,255,255,0.1); padding: 1px 6px; border-radius: 4px; }
.hero-slogan { font-size: 14px; color: rgba(255,255,255,0.45); margin: 0 0 28px; font-style: italic; }
.hero-actions { display: flex; gap: 16px; align-items: center; margin-bottom: 36px; flex-wrap: wrap; }
.btn-ghost-hero { background: transparent; border: none; color: rgba(255,255,255,0.55); font-family: 'Manrope', Arial, sans-serif; font-size: 15px; font-weight: 500; cursor: pointer; transition: color 0.2s; padding: 0; }
.btn-ghost-hero:hover { color: #ffffff; }
.hero-stats-row { display: flex; align-items: center; gap: 20px; }
.hsr-item { display: flex; flex-direction: column; gap: 3px; }
.hsr-num { font-family: 'Sora', Arial, sans-serif; font-size: 20px; font-weight: 700; color: #45d0bd; }
.hsr-lbl { font-size: 11px; color: rgba(255,255,255,0.35); }
.hsr-div { width: 1px; height: 28px; background: rgba(255,255,255,0.1); }
/* Hero body row layout */
.hero-body { flex-direction: row !important; justify-content: space-between !important; align-items: center !important; }

.hdr-logo { display: flex; align-items: center; }
.hdr-logo-img { height: 56px; width: auto; object-fit: contain; }
</style>
