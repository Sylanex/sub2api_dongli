<template>
  <!-- Custom Home Content: Full Page Mode (admin override) -->
  <div v-if="homeContent" class="min-h-screen">
    <iframe
      v-if="isHomeContentUrl"
      :src="homeContent.trim()"
      class="h-screen w-full border-0"
      allowfullscreen
    ></iframe>
    <!-- HTML mode - SECURITY: homeContent is admin-only setting, XSS risk is acceptable -->
    <div v-else v-html="homeContent"></div>
  </div>

  <!-- Default Landing Page (DongliAI) -->
  <div v-else class="landing-root relative min-h-screen overflow-x-hidden bg-[#0a1421] text-slate-100">
    <!-- Background decorations -->
    <div class="pointer-events-none absolute inset-0 overflow-hidden">
      <div
        class="absolute -top-40 right-0 h-[32rem] w-[32rem] rounded-full bg-primary-500/10 blur-3xl"
      ></div>
      <div
        class="absolute top-[40rem] -left-40 h-[28rem] w-[28rem] rounded-full bg-cyan-500/10 blur-3xl"
      ></div>
      <div
        class="absolute inset-0 bg-[linear-gradient(rgba(20,184,166,0.025)_1px,transparent_1px),linear-gradient(90deg,rgba(20,184,166,0.025)_1px,transparent_1px)] bg-[size:64px_64px] [mask-image:radial-gradient(ellipse_at_center,black_30%,transparent_75%)]"
      ></div>
    </div>

    <!-- Header -->
    <header class="sticky top-0 z-30 border-b border-white/5 bg-[#0a1421]/80 backdrop-blur-md">
      <nav class="mx-auto flex max-w-7xl items-center justify-between px-6 py-4">
        <!-- Brand -->
        <a href="#top" class="flex items-center gap-2.5">
          <div
            class="flex h-9 w-9 items-center justify-center rounded-xl bg-gradient-to-br from-primary-400 to-primary-600 shadow-lg shadow-primary-500/30"
          >
            <svg
              class="h-5 w-5 text-white"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2.5"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z" />
            </svg>
          </div>
          <span class="text-base font-semibold text-white">{{ siteName }}</span>
        </a>

        <!-- Nav links (desktop) -->
        <div class="hidden items-center gap-8 md:flex">
          <a
            href="#top"
            class="text-sm text-slate-300 transition-colors hover:text-white"
            >首页</a
          >
          <a
            href="#features"
            class="text-sm text-slate-300 transition-colors hover:text-white"
            >功能</a
          >
          <a
            href="#channels"
            class="text-sm text-slate-300 transition-colors hover:text-white"
            >模型渠道</a
          >
          <a
            href="#faq"
            class="text-sm text-slate-300 transition-colors hover:text-white"
            >常见问题</a
          >
        </div>

        <!-- Actions -->
        <div class="flex items-center gap-3">
          <router-link
            v-if="isAuthenticated"
            :to="dashboardPath"
            class="inline-flex items-center gap-1.5 rounded-full bg-primary-500 px-4 py-1.5 text-sm font-medium text-white shadow-lg shadow-primary-500/20 transition-all hover:bg-primary-400 hover:shadow-primary-500/40"
          >
            <span
              class="flex h-5 w-5 items-center justify-center rounded-full bg-white/20 text-[10px] font-semibold text-white"
            >
              {{ userInitial }}
            </span>
            <span>控制台</span>
          </router-link>
          <template v-else>
            <router-link
              to="/login"
              class="hidden rounded-full px-4 py-1.5 text-sm font-medium text-slate-300 transition-colors hover:text-white sm:inline-flex"
            >
              登录
            </router-link>
            <router-link
              to="/register"
              class="inline-flex items-center rounded-full bg-primary-500 px-4 py-1.5 text-sm font-medium text-white shadow-lg shadow-primary-500/20 transition-all hover:bg-primary-400 hover:shadow-primary-500/40"
            >
              立即注册
            </router-link>
          </template>
        </div>
      </nav>
    </header>

    <!-- ============== Hero ============== -->
    <section id="top" class="relative z-10 px-6 pb-16 pt-20 md:pt-28">
      <div class="mx-auto max-w-7xl">
        <div
          class="flex flex-col items-center gap-12 lg:flex-row lg:items-center lg:gap-16"
        >
          <!-- Left: Text content -->
          <div class="flex-1 text-center lg:text-left">
            <!-- Badge -->
            <div
              class="mb-6 inline-flex items-center gap-2 rounded-full border border-primary-500/30 bg-primary-500/10 px-4 py-1.5"
            >
              <svg
                class="h-3.5 w-3.5 text-primary-400"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <path d="M9 12l2 2 4-4M7.835 4.697a3.42 3.42 0 001.946-.806 3.42 3.42 0 014.438 0 3.42 3.42 0 001.946.806 3.42 3.42 0 013.138 3.138 3.42 3.42 0 00.806 1.946 3.42 3.42 0 010 4.438 3.42 3.42 0 00-.806 1.946 3.42 3.42 0 01-3.138 3.138 3.42 3.42 0 00-1.946.806 3.42 3.42 0 01-4.438 0 3.42 3.42 0 00-1.946-.806 3.42 3.42 0 01-3.138-3.138 3.42 3.42 0 00-.806-1.946 3.42 3.42 0 010-4.438 3.42 3.42 0 00.806-1.946 3.42 3.42 0 013.138-3.138z" />
              </svg>
              <span class="text-xs font-medium text-primary-300">专为开发者打造</span>
            </div>

            <!-- Headline -->
            <h1
              class="mb-6 text-4xl font-bold leading-tight tracking-tight text-white md:text-5xl lg:text-5xl xl:text-6xl"
            >
              稳定高速的
              <span
                class="bg-gradient-to-r from-primary-400 via-primary-300 to-cyan-300 bg-clip-text text-transparent"
              >
                AI 模型网关
              </span>
            </h1>

            <!-- Subtitle -->
            <p
              class="mx-auto mb-10 max-w-2xl text-base leading-relaxed text-slate-400 md:text-lg lg:mx-0"
            >
              统一接入 Claude、GPT、Gemini 等主流模型，多账号智能调度，按 Token 精确计费，
              为开发者打造稳定可靠的 AI API 服务。
            </p>

            <!-- CTAs -->
            <div
              class="flex flex-wrap items-center justify-center gap-4 lg:justify-start"
            >
              <router-link
                :to="isAuthenticated ? dashboardPath : '/register'"
                class="group inline-flex items-center gap-2 rounded-lg bg-primary-500 px-6 py-3 text-sm font-semibold text-white shadow-lg shadow-primary-500/30 transition-all hover:bg-primary-400 hover:shadow-primary-500/50"
              >
                {{ isAuthenticated ? '进入控制台' : '立即开始' }}
                <svg
                  class="h-4 w-4 transition-transform group-hover:translate-x-0.5"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                >
                  <path d="M5 12h14M13 5l7 7-7 7" />
                </svg>
              </router-link>
              <a
                href="#features"
                class="inline-flex items-center gap-2 rounded-lg border border-slate-700/80 bg-slate-800/40 px-6 py-3 text-sm font-medium text-slate-200 backdrop-blur-sm transition-all hover:border-slate-600 hover:bg-slate-800/80"
              >
                <svg
                  class="h-4 w-4"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                >
                  <path d="M12 6.253v13M2.25 12h19.5" />
                </svg>
                了解更多
              </a>
            </div>
          </div>

          <!-- Right: Terminal -->
          <div class="w-full flex-1">
            <div class="terminal-window">
              <div class="terminal-header">
                <div class="terminal-buttons">
                  <span class="btn-close"></span>
                  <span class="btn-minimize"></span>
                  <span class="btn-maximize"></span>
                </div>
                <span class="terminal-title">terminal</span>
              </div>
              <div class="terminal-body">
                <div class="code-line line-1">
                  <span class="code-prompt">$</span>
                  <span class="code-cmd">curl</span>
                  <span class="code-flag">-X POST</span>
                  <span class="code-url">/v1/messages</span>
                </div>
                <div class="code-line line-2">
                  <span class="code-comment"># Routing to upstream...</span>
                </div>
                <div class="code-line line-3">
                  <span class="code-success">200 OK</span>
                  <span class="code-response">{ "content": "Hello!" }</span>
                </div>
                <div class="code-line line-4">
                  <span class="code-prompt">$</span>
                  <span class="cursor"></span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ============== Features ============== -->
    <section id="features" class="relative z-10 px-6 py-24">
      <div class="mx-auto max-w-7xl">
        <div class="mb-14 text-center">
          <h2 class="mb-4 text-3xl font-bold tracking-tight text-white md:text-4xl">
            为什么选择 <span class="text-primary-400">{{ siteName }}</span>
          </h2>
          <p class="text-base text-slate-400">不只是简单的 API 代理，而是为开发者打磨的完整网关体验</p>
        </div>

        <div class="grid gap-6 md:grid-cols-2 lg:grid-cols-3">
          <div
            v-for="(feature, idx) in features"
            :key="idx"
            class="feature-card group rounded-2xl border border-slate-800 bg-slate-900/40 p-6 backdrop-blur-sm transition-all hover:border-slate-700 hover:bg-slate-900/70"
          >
            <div
              class="mb-4 flex h-11 w-11 items-center justify-center rounded-lg shadow-lg transition-transform group-hover:scale-110"
              :class="feature.iconBg"
            >
              <svg
                class="h-5 w-5 text-white"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
                v-html="feature.iconPath"
              ></svg>
            </div>
            <h3 class="mb-2 text-base font-semibold text-white">{{ feature.title }}</h3>
            <p class="text-sm leading-relaxed text-slate-400">{{ feature.desc }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- ============== Channels (placeholder) ============== -->
    <section id="channels" class="relative z-10 px-6 py-24">
      <div class="mx-auto max-w-7xl">
        <div class="mb-14 text-center">
          <h2 class="mb-4 text-3xl font-bold tracking-tight text-white md:text-4xl">
            多样化的 <span class="text-primary-400">模型渠道</span>
          </h2>
          <p class="text-base text-slate-400">提供多种 AI 模型渠道，满足不同场景的开发需求</p>
        </div>

        <div class="grid gap-6 md:grid-cols-3">
          <div
            v-for="(_, idx) in 3"
            :key="idx"
            class="rounded-2xl border border-dashed border-slate-700/70 bg-slate-900/30 p-6 backdrop-blur-sm"
          >
            <div class="mb-4 flex items-center gap-2">
              <span
                class="rounded-md bg-slate-800 px-2 py-0.5 text-xs font-medium text-slate-500"
                >即将上线</span
              >
              <span class="text-base font-semibold text-slate-400">渠道占位 {{ idx + 1 }}</span>
            </div>
            <div class="space-y-3 text-sm text-slate-500">
              <div class="flex items-center justify-between">
                <span>当前倍率</span>
                <span class="font-mono text-slate-400">— : —</span>
              </div>
              <div class="flex items-center justify-between">
                <span>额度说明</span>
                <span class="text-slate-400">敬请期待</span>
              </div>
              <div class="border-t border-slate-800 pt-3">
                <p class="mb-2 text-xs uppercase tracking-wider text-slate-600">支持模型</p>
                <div class="flex flex-wrap gap-1.5">
                  <span
                    v-for="n in 3"
                    :key="n"
                    class="h-5 w-16 rounded-md bg-slate-800/60"
                  ></span>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="mt-10 text-center">
          <span class="text-sm text-slate-500">渠道列表筹备中，敬请期待</span>
        </div>
      </div>
    </section>

    <!-- ============== FAQ (placeholder) ============== -->
    <section id="faq" class="relative z-10 px-6 py-24">
      <div class="mx-auto max-w-3xl">
        <div class="mb-14 text-center">
          <h2 class="mb-4 text-3xl font-bold tracking-tight text-white md:text-4xl">常见问题</h2>
          <p class="text-base text-slate-400">关于 {{ siteName }} 服务的常见疑问解答</p>
        </div>

        <div class="space-y-3">
          <details
            v-for="(_, idx) in 4"
            :key="idx"
            class="group rounded-xl border border-slate-800 bg-slate-900/40 backdrop-blur-sm transition-colors hover:border-slate-700"
          >
            <summary
              class="flex cursor-pointer items-center justify-between px-5 py-4 text-sm font-medium text-slate-300"
            >
              <span>问题占位 {{ idx + 1 }}（即将补充）</span>
              <svg
                class="h-4 w-4 text-slate-500 transition-transform group-open:rotate-180"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <path d="M6 9l6 6 6-6" />
              </svg>
            </summary>
            <div class="border-t border-slate-800 px-5 py-4 text-sm leading-relaxed text-slate-500">
              答案内容筹备中，将在正式上线前补全。
            </div>
          </details>
        </div>
      </div>
    </section>

    <!-- ============== Footer ============== -->
    <footer class="relative z-10 mt-12 border-t border-white/5 px-6 py-12">
      <div class="mx-auto max-w-7xl">
        <div class="grid grid-cols-2 gap-10 md:grid-cols-4">
          <!-- Brand col -->
          <div class="col-span-2 md:col-span-1">
            <div class="mb-3 flex items-center gap-2.5">
              <div
                class="flex h-8 w-8 items-center justify-center rounded-lg bg-gradient-to-br from-primary-400 to-primary-600"
              >
                <svg
                  class="h-4 w-4 text-white"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                >
                  <path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z" />
                </svg>
              </div>
              <span class="text-sm font-semibold text-white">{{ siteName }}</span>
            </div>
            <p class="text-sm leading-relaxed text-slate-500">
              专业的 AI 模型聚合网关，为开发者提供稳定、高速的 API 访问服务。
            </p>
          </div>

          <!-- Product col -->
          <div>
            <h4 class="mb-3 text-sm font-semibold text-white">产品</h4>
            <ul class="space-y-2 text-sm text-slate-500">
              <li><a href="#features" class="hover:text-slate-300">功能特性</a></li>
              <li><a href="#channels" class="hover:text-slate-300">模型渠道</a></li>
              <li>
                <router-link :to="isAuthenticated ? dashboardPath : '/login'" class="hover:text-slate-300"
                  >控制台</router-link
                >
              </li>
            </ul>
          </div>

          <!-- Support col -->
          <div>
            <h4 class="mb-3 text-sm font-semibold text-white">支持</h4>
            <ul class="space-y-2 text-sm text-slate-500">
              <li><a href="#faq" class="hover:text-slate-300">常见问题</a></li>
              <li>
                <a v-if="docUrl" :href="docUrl" target="_blank" rel="noopener noreferrer" class="hover:text-slate-300"
                  >使用文档</a
                >
                <span v-else class="opacity-50">使用文档</span>
              </li>
              <li>
                <router-link to="/register" class="hover:text-slate-300">快速开始</router-link>
              </li>
            </ul>
          </div>

          <!-- Community col -->
          <div>
            <h4 class="mb-3 text-sm font-semibold text-white">社区</h4>
            <ul class="space-y-2 text-sm text-slate-500">
              <li class="opacity-60">敬请期待</li>
            </ul>
          </div>
        </div>

        <div
          class="mt-12 flex flex-col items-center justify-between gap-3 border-t border-white/5 pt-8 sm:flex-row"
        >
          <p class="text-xs text-slate-600">
            &copy; {{ currentYear }} {{ siteName }}. 保留所有权利。
          </p>
          <div class="flex items-center gap-5 text-xs text-slate-600">
            <router-link to="/legal/terms" class="hover:text-slate-400">服务条款</router-link>
            <router-link to="/legal/privacy" class="hover:text-slate-400">隐私政策</router-link>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { computed, onMounted } from 'vue'
import { useAuthStore, useAppStore } from '@/stores'

const authStore = useAuthStore()
const appStore = useAppStore()

// Brand: 硬编码为 DongliAI（不受后台 site_name 影响，避免被 Sub2API 覆盖）
const siteName = 'DongliAI'
const docUrl = computed(() => appStore.cachedPublicSettings?.doc_url || appStore.docUrl || '')
const homeContent = computed(() => appStore.cachedPublicSettings?.home_content || '')

const isHomeContentUrl = computed(() => {
  const content = homeContent.value.trim()
  return content.startsWith('http://') || content.startsWith('https://')
})

// Auth
const isAuthenticated = computed(() => authStore.isAuthenticated)
const isAdmin = computed(() => authStore.isAdmin)
const dashboardPath = computed(() => (isAdmin.value ? '/admin/dashboard' : '/dashboard'))
const userInitial = computed(() => {
  const user = authStore.user
  if (!user || !user.email) return ''
  return user.email.charAt(0).toUpperCase()
})

const currentYear = computed(() => new Date().getFullYear())

// Features grid (6 cards, matches pincc layout)
const features = [
  {
    title: '实惠价格',
    desc: '相比市场同类服务更有优势的价格，让每一个开发者都能享受 AI 编程的便利。',
    iconBg: 'bg-gradient-to-br from-emerald-500 to-emerald-600 shadow-emerald-500/30',
    iconPath:
      '<path d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8V6m0 12v2m9-7a9 9 0 11-18 0 9 9 0 0118 0z" />',
  },
  {
    title: '稳定可靠',
    desc: '多节点冗余部署，企业级后端架构，确保服务长时间稳定运行。',
    iconBg: 'bg-gradient-to-br from-sky-500 to-sky-600 shadow-sky-500/30',
    iconPath:
      '<path d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />',
  },
  {
    title: '即时激活',
    desc: '购买后立即获取激活码，开通即可使用，无需等待。',
    iconBg: 'bg-gradient-to-br from-amber-500 to-amber-600 shadow-amber-500/30',
    iconPath: '<path d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />',
  },
  {
    title: '多模型支持',
    desc: '支持 Claude、GPT、Gemini 等多家主流 AI 模型，满足不同场景需求。',
    iconBg: 'bg-gradient-to-br from-violet-500 to-violet-600 shadow-violet-500/30',
    iconPath:
      '<path d="M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10" />',
  },
  {
    title: '低延迟响应',
    desc: '优化线路，智能路由，为你提供稳定快速的 API 响应体验。',
    iconBg: 'bg-gradient-to-br from-cyan-500 to-cyan-600 shadow-cyan-500/30',
    iconPath: '<path d="M13 10V3L4 14h7v7l9-11h-7z" />',
  },
  {
    title: '技术支持',
    desc: '专业团队提供技术支持，遇到问题随时获取帮助。',
    iconBg: 'bg-gradient-to-br from-rose-500 to-rose-600 shadow-rose-500/30',
    iconPath:
      '<path d="M18.364 5.636a9 9 0 010 12.728m0 0l-2.829-2.829m2.829 2.829L21 21M15.536 8.464a5 5 0 010 7.072m0 0l-2.829-2.829m-4.243 2.829a4.978 4.978 0 01-1.414-2.83m-1.414 5.658a9 9 0 01-2.167-9.238m7.824 2.167a1 1 0 111.414 1.414m-1.414-1.414L3 3m8.293 8.293l1.414 1.414" />',
  },
]

onMounted(() => {
  authStore.checkAuth()
  if (!appStore.publicSettingsLoaded) {
    appStore.fetchPublicSettings()
  }
})
</script>

<style scoped>
.landing-root {
  /* Force dark visual regardless of html.dark class */
  color-scheme: dark;
}

/* ============== Terminal ============== */
.terminal-window {
  background: linear-gradient(145deg, #1e293b 0%, #0f172a 100%);
  border-radius: 12px;
  box-shadow:
    0 25px 50px -12px rgba(0, 0, 0, 0.6),
    0 0 0 1px rgba(20, 184, 166, 0.15),
    0 0 60px rgba(20, 184, 166, 0.08),
    inset 0 1px 0 rgba(255, 255, 255, 0.08);
  overflow: hidden;
  text-align: left;
}

.terminal-header {
  display: flex;
  align-items: center;
  padding: 14px 20px;
  background: rgba(15, 23, 42, 0.6);
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}

.terminal-buttons {
  display: flex;
  gap: 8px;
}

.terminal-buttons span {
  width: 13px;
  height: 13px;
  border-radius: 50%;
}

.btn-close {
  background: #ef4444;
}
.btn-minimize {
  background: #eab308;
}
.btn-maximize {
  background: #22c55e;
}

.terminal-title {
  flex: 1;
  text-align: center;
  font-size: 13px;
  font-family: ui-monospace, monospace;
  color: #64748b;
  margin-right: 56px;
}

.terminal-body {
  padding: 28px 32px;
  font-family: ui-monospace, 'Fira Code', monospace;
  font-size: 15px;
  line-height: 2.1;
  min-height: 220px;
}

@media (min-width: 1024px) {
  .terminal-body {
    font-size: 16px;
    padding: 32px 36px;
    min-height: 260px;
  }
}

.code-line {
  display: flex;
  align-items: center;
  gap: 8px;
  flex-wrap: wrap;
  opacity: 0;
  animation: line-appear 0.5s ease forwards;
}

.line-1 {
  animation-delay: 0.3s;
}
.line-2 {
  animation-delay: 1s;
}
.line-3 {
  animation-delay: 1.8s;
}
.line-4 {
  animation-delay: 2.5s;
}

@keyframes line-appear {
  from {
    opacity: 0;
    transform: translateY(5px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.code-prompt {
  color: #22c55e;
  font-weight: bold;
}
.code-cmd {
  color: #38bdf8;
}
.code-flag {
  color: #a78bfa;
}
.code-url {
  color: #14b8a6;
}
.code-comment {
  color: #64748b;
  font-style: italic;
}
.code-success {
  color: #22c55e;
  background: rgba(34, 197, 94, 0.15);
  padding: 2px 8px;
  border-radius: 4px;
  font-weight: 600;
}
.code-response {
  color: #fbbf24;
}

.cursor {
  display: inline-block;
  width: 9px;
  height: 18px;
  background: #22c55e;
  animation: blink 1s step-end infinite;
}

@keyframes blink {
  0%,
  50% {
    opacity: 1;
  }
  51%,
  100% {
    opacity: 0;
  }
}

/* Feature card subtle hover lift */
.feature-card {
  transition:
    transform 0.2s ease,
    border-color 0.2s ease,
    background-color 0.2s ease;
}
.feature-card:hover {
  transform: translateY(-2px);
}
</style>
