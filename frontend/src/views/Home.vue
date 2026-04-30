<template>
  <div class="home-wrap">
    <nav class="navbar">
      <div class="nav-inner">
        <div class="nav-logo">BOTOPOLIS</div>
        <div class="nav-center-links">
          <span class="nav-link">{{ $t('home.step01Title') }}</span>
          <span class="nav-link">{{ $t('home.step02Title') }}</span>
          <span class="nav-link">{{ $t('home.step03Title') }}</span>
          <span class="nav-link">{{ $t('home.step04Title') }}</span>
        </div>
        <div class="nav-right">
          <LanguageSwitcher />
          <a href="https://github.com/secgmbh/mirofish" target="_blank" class="nav-cta">GitHub &#8599;</a>
        </div>
      </div>
    </nav>

    <section class="hero">
      <div class="hero-bg-grid"></div>
      <div class="hero-glow hero-glow-1"></div>
      <div class="hero-glow hero-glow-2"></div>
      <div class="hero-inner">
        <div class="hero-badge">
          <span class="badge-dot"></span>
          {{ $t('home.tagline') }} {{ $t('home.version') }}
        </div>
        <h1 class="hero-title">
          {{ $t('home.heroTitle1') }}<br>
          <span class="hero-title-gradient">{{ $t('home.heroTitle2') }}</span>
        </h1>
        <p class="hero-sub">
          <i18n-t keypath="home.heroDesc" tag="span">
            <template #brand><strong>{{ $t('home.heroDescBrand') }}</strong></template>
            <template #agentScale><span class="text-accent">{{ $t('home.heroDescAgentScale') }}</span></template>
            <template #optimalSolution><code>{{ $t('home.heroDescOptimalSolution') }}</code></template>
          </i18n-t>
        </p>
        <div class="hero-actions">
          <button class="btn-primary" @click="scrollToStart">{{ $t('home.startEngine') }} &#8594;</button>
          <button class="btn-ghost" @click="scrollToSteps">{{ $t('home.workflowSequence') }} &#8595;</button>
        </div>
        <div class="hero-stats">
          <div class="stat-item">
            <span class="stat-num">5</span>
            <span class="stat-label">Steps</span>
          </div>
          <div class="stat-divider"></div>
          <div class="stat-item">
            <span class="stat-num">&#8734;</span>
            <span class="stat-label">{{ $t('home.metricHighAvailDesc') }}</span>
          </div>
          <div class="stat-divider"></div>
          <div class="stat-item">
            <span class="stat-num">{{ $t('home.metricLowCostDesc') }}</span>
            <span class="stat-label">{{ $t('home.metricLowCost') }}</span>
          </div>
        </div>
      </div>
    </section>

    <section class="section-steps" ref="stepsRef">
      <div class="section-inner">
        <div class="section-label">{{ $t('home.workflowSequence') }}</div>
        <h2 class="section-title">{{ $t('home.systemReady') }}</h2>
        <p class="section-sub">{{ $t('home.systemReadyDesc') }}</p>
        <div class="steps-grid">
          <div class="step-card" v-for="(step, i) in steps" :key="i">
            <div class="step-num-badge">{{ String(i+1).padStart(2,'0') }}</div>
            <h3 class="step-card-title">{{ step.title }}</h3>
            <p class="step-card-desc">{{ step.desc }}</p>
          </div>
        </div>
      </div>
    </section>

    <section class="section-features">
      <div class="section-inner">
        <div class="section-label">Features</div>
        <h2 class="section-title">{{ $t('home.systemStatus') }}</h2>
        <div class="features-grid">
          <div class="feature-card" v-for="(feat, i) in steps.slice(0,4)" :key="i">
            <div class="feature-icon">{{ ['&#11041;','&#10696;','&#9726;','&#9711;'][i] }}</div>
            <h4>{{ feat.title }}</h4>
            <p>{{ feat.desc }}</p>
          </div>
        </div>
      </div>
    </section>

    <section class="section-start" ref="startRef">
      <div class="section-inner">
        <div class="section-label">&gt;_ Engine</div>
        <h2 class="section-title">{{ $t('home.startEngine') }}</h2>
        <p class="section-sub">{{ $t('home.systemReadyDesc') }}</p>
        <div class="engine-grid">
          <div class="engine-panel">
            <div class="panel-head">
              <span class="panel-num">01</span>
              <span>{{ $t('home.realitySeed') }}</span>
              <span class="panel-meta">{{ $t('home.supportedFormats') }}</span>
            </div>
            <div
              class="drop-zone"
              :class="{ 'drag-active': isDragOver, 'has-files': files.length > 0 }"
              @dragover.prevent="handleDragOver"
              @dragleave.prevent="handleDragLeave"
              @drop.prevent="handleDrop"
              @click="triggerFileInput"
            >
              <input ref="fileInput" type="file" multiple accept=".pdf,.md,.txt"
                @change="handleFileSelect" style="display:none" :disabled="loading" />
              <div v-if="files.length === 0" class="drop-placeholder">
                <div class="drop-icon">&#8593;</div>
                <div>{{ $t('home.dragToUpload') }}</div>
                <div class="drop-hint">{{ $t('home.orBrowse') }}</div>
              </div>
              <div v-else class="file-list">
                <div v-for="(f, i) in files" :key="i" class="file-row">
                  <span>&#128196; {{ f.name }}</span>
                  <button @click.stop="removeFile(i)" class="rm-btn">&#215;</button>
                </div>
              </div>
            </div>
          </div>
          <div class="engine-panel">
            <div class="panel-head">
              <span class="panel-num">02</span>
              <span>{{ $t('home.inputParams') }}</span>
            </div>
            <div class="prompt-wrap">
              <textarea v-model="formData.simulationRequirement" class="prompt-input"
                :placeholder="$t('home.promptPlaceholder')" rows="9" :disabled="loading"></textarea>
              <div class="engine-badge">{{ $t('home.engineBadge') }}</div>
            </div>
            <button class="launch-btn" @click="startSimulation" :disabled="!canSubmit || loading">
              <span v-if="!loading">{{ $t('home.startEngine') }}</span>
              <span v-else>{{ $t('home.initializing') }}</span>
              <span>&#8594;</span>
            </button>
          </div>
        </div>
      </div>
    </section>

    <section class="section-history">
      <div class="section-inner">
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
.home-wrap { min-height: 100vh; background: #070B14; color: #F8FAFC; font-family: 'Space Grotesk', system-ui, sans-serif; }

.navbar { position: sticky; top: 0; z-index: 100; background: rgba(7,11,20,0.85); backdrop-filter: blur(16px); border-bottom: 1px solid rgba(37,99,235,0.2); }
.nav-inner { max-width: 1280px; margin: 0 auto; padding: 0 40px; height: 64px; display: flex; align-items: center; justify-content: space-between; }
.nav-logo { font-family: 'JetBrains Mono', monospace; font-weight: 800; font-size: 1.1rem; letter-spacing: 3px; background: linear-gradient(90deg, #60A5FA, #2563EB); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
.nav-center-links { display: flex; gap: 32px; }
.nav-link { font-size: 0.85rem; color: #94A3B8; cursor: pointer; transition: color 0.2s; }
.nav-link:hover { color: #F8FAFC; }
.nav-right { display: flex; align-items: center; gap: 16px; }
.nav-cta { font-family: 'JetBrains Mono', monospace; font-size: 0.8rem; color: #60A5FA; text-decoration: none; border: 1px solid rgba(37,99,235,0.2); padding: 6px 16px; transition: all 0.2s; }
.nav-cta:hover { background: rgba(37,99,235,0.15); border-color: #2563EB; }

.hero { position: relative; min-height: 100vh; display: flex; align-items: center; justify-content: center; overflow: hidden; padding: 120px 40px 80px; }
.hero-bg-grid { position: absolute; inset: 0; background-image: linear-gradient(rgba(37,99,235,0.07) 1px, transparent 1px), linear-gradient(90deg, rgba(37,99,235,0.07) 1px, transparent 1px); background-size: 60px 60px; }
.hero-glow { position: absolute; border-radius: 50%; filter: blur(120px); pointer-events: none; }
.hero-glow-1 { width: 600px; height: 600px; background: rgba(37,99,235,0.18); top: -100px; right: -100px; }
.hero-glow-2 { width: 400px; height: 400px; background: rgba(96,165,250,0.1); bottom: 0; left: -50px; }
.hero-inner { position: relative; z-index: 1; max-width: 860px; text-align: center; }
.hero-badge { display: inline-flex; align-items: center; gap: 8px; font-family: 'JetBrains Mono', monospace; font-size: 0.75rem; color: #60A5FA; border: 1px solid rgba(96,165,250,0.3); padding: 6px 16px; border-radius: 100px; margin-bottom: 32px; background: rgba(37,99,235,0.08); letter-spacing: 1px; }
.badge-dot { width: 6px; height: 6px; background: #22C55E; border-radius: 50%; animation: pulse-dot 2s ease-in-out infinite; }
@keyframes pulse-dot { 0%,100% { opacity: 1; transform: scale(1); } 50% { opacity: 0.6; transform: scale(0.8); } }
.hero-title { font-size: 5rem; font-weight: 700; line-height: 1.1; letter-spacing: -2px; margin: 0 0 28px; color: #F8FAFC; }
.hero-title-gradient { background: linear-gradient(135deg, #60A5FA 0%, #2563EB 50%, #818CF8 100%); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
.hero-sub { font-size: 1.05rem; color: #94A3B8; line-height: 1.8; max-width: 680px; margin: 0 auto 40px; }
.hero-sub strong { color: #F8FAFC; }
.text-accent { color: #60A5FA; font-weight: 600; }
.hero-sub code { font-family: 'JetBrains Mono', monospace; background: rgba(37,99,235,0.15); padding: 2px 8px; border-radius: 4px; color: #60A5FA; font-size: 0.9em; }
.hero-actions { display: flex; gap: 16px; justify-content: center; margin-bottom: 56px; }
.btn-primary { background: linear-gradient(135deg, #1D4ED8, #2563EB); color: #fff; border: none; padding: 14px 36px; font-family: 'JetBrains Mono', monospace; font-weight: 700; font-size: 0.95rem; cursor: pointer; border-radius: 2px; transition: all 0.3s; letter-spacing: 1px; box-shadow: 0 0 24px rgba(37,99,235,0.35); }
.btn-primary:hover { transform: translateY(-2px); box-shadow: 0 0 40px rgba(37,99,235,0.55); }
.btn-ghost { background: transparent; color: #94A3B8; border: 1px solid rgba(37,99,235,0.2); padding: 14px 36px; font-family: 'JetBrains Mono', monospace; font-size: 0.95rem; cursor: pointer; border-radius: 2px; transition: all 0.2s; }
.btn-ghost:hover { color: #F8FAFC; border-color: #3B82F6; background: rgba(37,99,235,0.08); }
.hero-stats { display: inline-flex; align-items: center; gap: 32px; background: rgba(255,255,255,0.03); border: 1px solid rgba(37,99,235,0.2); border-radius: 4px; padding: 16px 36px; }
.stat-item { display: flex; flex-direction: column; align-items: center; gap: 4px; }
.stat-num { font-family: 'JetBrains Mono', monospace; font-size: 1.4rem; font-weight: 700; color: #60A5FA; }
.stat-label { font-size: 0.72rem; color: #94A3B8; letter-spacing: 0.5px; }
.stat-divider { width: 1px; height: 32px; background: rgba(37,99,235,0.2); }

.section-steps, .section-features, .section-start, .section-history { padding: 100px 40px; }
.section-steps { background: #0A0F1E; }
.section-features { background: #070B14; border-top: 1px solid rgba(37,99,235,0.15); }
.section-start { background: #0A0F1E; border-top: 1px solid rgba(37,99,235,0.15); }
.section-history { background: #070B14; border-top: 1px solid rgba(37,99,235,0.15); }
.section-inner { max-width: 1280px; margin: 0 auto; }
.section-label { font-family: 'JetBrains Mono', monospace; font-size: 0.72rem; color: #3B82F6; letter-spacing: 3px; text-transform: uppercase; margin-bottom: 16px; }
.section-title { font-size: 2.8rem; font-weight: 700; letter-spacing: -1px; margin: 0 0 16px; color: #F8FAFC; }
.section-sub { font-size: 1rem; color: #94A3B8; max-width: 560px; line-height: 1.7; margin-bottom: 60px; }

.steps-grid { display: grid; grid-template-columns: repeat(5, 1fr); gap: 1px; background: rgba(37,99,235,0.15); border: 1px solid rgba(37,99,235,0.15); }
.step-card { background: #0A0F1E; padding: 36px 28px; transition: background 0.2s; }
.step-card:hover { background: rgba(37,99,235,0.06); }
.step-num-badge { font-family: 'JetBrains Mono', monospace; font-size: 2.5rem; font-weight: 800; color: rgba(37,99,235,0.25); margin-bottom: 20px; line-height: 1; }
.step-card-title { font-size: 0.95rem; font-weight: 600; color: #F8FAFC; margin: 0 0 10px; }
.step-card-desc { font-size: 0.8rem; color: #94A3B8; line-height: 1.6; }

.features-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 20px; }
.feature-card { background: #0D1526; border: 1px solid rgba(37,99,235,0.2); padding: 36px 28px; transition: all 0.3s; }
.feature-card:hover { border-color: #2563EB; transform: translateY(-4px); box-shadow: 0 8px 32px rgba(37,99,235,0.15); }
.feature-icon { font-size: 2rem; margin-bottom: 20px; color: #3B82F6; }
.feature-card h4 { font-size: 1rem; font-weight: 600; margin: 0 0 12px; color: #F8FAFC; }
.feature-card p { font-size: 0.82rem; color: #94A3B8; line-height: 1.6; }

.engine-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 24px; }
.engine-panel { background: #0D1526; border: 1px solid rgba(37,99,235,0.2); padding: 32px; display: flex; flex-direction: column; gap: 20px; }
.panel-head { display: flex; align-items: center; gap: 12px; font-family: 'JetBrains Mono', monospace; font-size: 0.78rem; color: #94A3B8; border-bottom: 1px solid rgba(37,99,235,0.15); padding-bottom: 16px; }
.panel-num { font-size: 1.4rem; font-weight: 800; color: rgba(37,99,235,0.4); }
.panel-meta { margin-left: auto; }
.drop-zone { flex: 1; min-height: 220px; border: 1px dashed rgba(37,99,235,0.3); background: rgba(37,99,235,0.03); display: flex; align-items: center; justify-content: center; cursor: pointer; transition: all 0.2s; overflow-y: auto; }
.drop-zone.drag-active, .drop-zone:hover { border-color: #2563EB; background: rgba(37,99,235,0.08); }
.drop-zone.has-files { align-items: flex-start; }
.drop-placeholder { text-align: center; color: #94A3B8; }
.drop-icon { font-size: 2rem; margin-bottom: 12px; color: rgba(37,99,235,0.4); }
.drop-hint { font-family: 'JetBrains Mono', monospace; font-size: 0.72rem; color: rgba(148,163,184,0.6); margin-top: 6px; }
.file-list { width: 100%; padding: 16px; display: flex; flex-direction: column; gap: 8px; }
.file-row { display: flex; align-items: center; justify-content: space-between; background: rgba(37,99,235,0.08); border: 1px solid rgba(37,99,235,0.2); padding: 8px 14px; font-family: 'JetBrains Mono', monospace; font-size: 0.8rem; color: #F8FAFC; }
.rm-btn { background: none; border: none; color: #94A3B8; cursor: pointer; font-size: 1.1rem; }
.rm-btn:hover { color: #F87171; }
.prompt-wrap { position: relative; flex: 1; }
.prompt-input { width: 100%; min-height: 200px; background: rgba(37,99,235,0.04); border: 1px solid rgba(37,99,235,0.2); color: #F8FAFC; font-family: 'JetBrains Mono', monospace; font-size: 0.88rem; line-height: 1.7; padding: 20px; resize: vertical; outline: none; transition: border-color 0.2s; }
.prompt-input:focus { border-color: #2563EB; }
.prompt-input::placeholder { color: rgba(148,163,184,0.5); }
.engine-badge { position: absolute; bottom: 12px; right: 14px; font-family: 'JetBrains Mono', monospace; font-size: 0.68rem; color: rgba(96,165,250,0.4); }
.launch-btn { width: 100%; background: linear-gradient(135deg, #1D4ED8, #2563EB); color: #fff; border: none; padding: 18px 24px; font-family: 'JetBrains Mono', monospace; font-weight: 700; font-size: 1rem; letter-spacing: 2px; cursor: pointer; display: flex; justify-content: space-between; align-items: center; transition: all 0.3s; box-shadow: 0 0 20px rgba(37,99,235,0.3); }
.launch-btn:hover:not(:disabled) { box-shadow: 0 0 40px rgba(37,99,235,0.5); transform: translateY(-1px); }
.launch-btn:disabled { background: #1E293B; color: #475569; cursor: not-allowed; box-shadow: none; transform: none; }

@media (max-width: 1024px) {
  .hero-title { font-size: 3.2rem; }
  .steps-grid { grid-template-columns: repeat(3, 1fr); }
  .features-grid { grid-template-columns: repeat(2, 1fr); }
  .engine-grid { grid-template-columns: 1fr; }
  .nav-center-links { display: none; }
}
@media (max-width: 640px) {
  .hero-title { font-size: 2.4rem; }
  .hero-actions { flex-direction: column; }
  .steps-grid { grid-template-columns: 1fr; }
  .features-grid { grid-template-columns: 1fr; }
  .hero-stats { flex-direction: column; gap: 16px; }
  .stat-divider { display: none; }
}
</style>
