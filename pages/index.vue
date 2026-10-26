<!-- pages/index.vue -->
<template>
  <div class="min-h-screen bg-[#030712] text-slate-100 pb-20">
    <!-- Navbar Dark -->
    <header class="sticky top-0 z-50 backdrop-blur-xl bg-[#030712]/90 border-b border-blue-950/60">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-18 flex items-center justify-between py-4">
        <!-- Logo Brand & Badge KraaDev -->
        <NuxtLink to="/" class="flex items-center space-x-3 group">
          <div class="w-9 h-9 rounded-lg bg-blue-600/20 border border-blue-500/30 flex items-center justify-center text-blue-400 group-hover:border-blue-400 transition-colors">
            <svg class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4" />
            </svg>
          </div>
          <div class="flex items-center gap-2">
            <span class="text-lg font-black tracking-tight text-white">Mcpe<span class="text-blue-500">Leaks</span></span>
            <span class="text-[11px] font-medium text-blue-400/80 bg-blue-950/50 px-2 py-0.5 rounded border border-blue-800/40">
              by KraaDev
            </span>
          </div>
        </NuxtLink>

        <!-- Status & Tombol Request -->
        <div class="flex items-center space-x-3">
          <div class="hidden sm:flex items-center space-x-2 text-[11px] font-medium text-emerald-400 bg-emerald-950/30 border border-emerald-800/40 px-2.5 py-1 rounded-full">
            <span class="w-1.5 h-1.5 rounded-full bg-emerald-400 animate-ping"></span>
            <span>Online</span>
          </div>

          <!-- Tombol Request (Rp 5k) -->
          <button 
            @click="showRequestModal = true"
            class="inline-flex items-center gap-1.5 px-3.5 py-1.5 rounded-lg text-xs font-bold bg-emerald-600 hover:bg-emerald-500 text-white transition-all shadow-md shadow-emerald-600/20 active:scale-95"
          >
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4" />
            </svg>
            <span>Request (Rp 5k)</span>
          </button>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 pt-12">
      <!-- Hero (Hanya McpeLeaks & Search Bar) -->
      <section class="text-center max-w-2xl mx-auto mb-10">
        <h1 class="text-4xl sm:text-6xl font-black text-white tracking-tight mb-8">
          Mcpe<span class="text-blue-500">Leaks</span>
        </h1>

        <!-- Search Bar -->
        <div class="relative max-w-lg mx-auto">
          <input 
            v-model="searchQuery" 
            type="text" 
            placeholder="Cari server atau keyword..." 
            class="w-full pl-11 pr-4 py-3 rounded-xl bg-[#090f21] border border-blue-950 focus:border-blue-500/50 text-sm text-slate-200 placeholder-slate-500 outline-none transition-all shadow-inner"
          />
          <svg class="w-4 h-4 text-slate-500 absolute left-4 top-1/2 -translate-y-1/2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
          </svg>
        </div>
      </section>

      <!-- Category Filter -->
      <div class="flex items-center justify-center gap-2 mb-10">
        <button 
          v-for="cat in categories" 
          :key="cat"
          type="button"
          @click="selectedCategory = cat"
          class="px-3.5 py-1.5 rounded-lg text-xs font-semibold transition-all"
          :class="selectedCategory === cat 
            ? 'bg-blue-600 text-white shadow-md shadow-blue-600/30' 
            : 'bg-[#090f21] text-slate-400 hover:text-slate-200 border border-blue-950/60'"
        >
          {{ cat }}
        </button>
      </div>

      <!-- Leak Cards Grid -->
      <div v-if="filteredLeaks.length > 0" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <div 
          v-for="leak in filteredLeaks" 
          :key="leak.id"
          class="group relative bg-[#090f21] border border-blue-950/70 hover:border-blue-600/40 rounded-2xl p-5 transition-all duration-300 hover:-translate-y-1 hover:shadow-2xl hover:shadow-blue-950/50 flex flex-col justify-between cursor-pointer"
          @click="goToDetail(leak.id)"
        >
          <div>
            <!-- Thumbnail Box -->
            <div class="relative w-full h-44 rounded-xl overflow-hidden mb-4 bg-[#030712] border border-blue-950/40 flex items-center justify-center">
              <img 
                :src="leak.thumbnail" 
                :alt="leak.title" 
                class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500"
              />
              <span class="absolute top-3 left-3 text-[11px] font-bold px-2 py-0.5 rounded bg-blue-600 text-white shadow">
                {{ leak.category }}
              </span>
            </div>

            <h2 class="text-base font-bold text-white group-hover:text-blue-400 transition-colors mb-2">
              {{ leak.title }}
            </h2>
            <p class="text-xs text-slate-400 line-clamp-2 leading-relaxed mb-4">
              {{ leak.shortDescription }}
            </p>
          </div>

          <!-- Bottom Action -->
          <div class="pt-4 border-t border-blue-950/60 flex items-center justify-between">
            <span class="text-[11px] text-blue-400 font-semibold group-hover:underline">
              Buka Detail &rarr;
            </span>

            <a 
              :href="leak.downloadUrl" 
              target="_blank" 
              rel="noopener noreferrer"
              @click.stop
              class="inline-flex items-center gap-1.5 px-3.5 py-1.5 rounded-lg text-xs font-bold bg-blue-600 hover:bg-blue-500 text-white transition-all shadow-md shadow-blue-600/20 active:scale-95"
            >
              <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
              </svg>
              <span>Download</span>
            </a>
          </div>
        </div>
      </div>

      <div v-else class="text-center py-16 bg-[#090f21] rounded-2xl border border-blue-950/50 max-w-md mx-auto">
        <p class="text-slate-400 text-sm">Tidak ada leak yang sesuai pencarian.</p>
      </div>
    </main>

    <!-- Modal Form Request WhatsApp -->
    <div v-if="showRequestModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/70 backdrop-blur-sm">
      <div class="bg-[#090f21] border border-blue-900/60 rounded-2xl p-6 max-w-md w-full shadow-2xl relative">
        <h3 class="text-lg font-bold text-white mb-2">Request Server / Map / Add-on</h3>
        <p class="text-xs text-slate-400 mb-4">
          Biaya request adalah <strong class="text-emerald-400">Rp 5.000</strong>. Silakan tulis detail request kamu di bawah ini, lalu klik kirim untuk terhubung ke WhatsApp.
        </p>

        <textarea 
          v-model="requestText" 
          rows="4" 
          placeholder="Contoh: Tolong leak server [Nama Server] atau map [Nama Map]..."
          class="w-full p-3 rounded-xl bg-[#030712] border border-blue-950 focus:border-blue-500/50 text-sm text-slate-200 placeholder-slate-500 outline-none transition-all resize-none mb-4"
        ></textarea>

        <div class="flex items-center justify-end gap-3">
          <button 
            @click="showRequestModal = false"
            class="px-4 py-2 rounded-xl text-xs font-semibold bg-slate-800 hover:bg-slate-700 text-slate-300 transition-all"
          >
            Batal
          </button>
          <button 
            @click="sendToWhatsApp"
            class="inline-flex items-center gap-2 px-4 py-2 rounded-xl text-xs font-bold bg-emerald-600 hover:bg-emerald-500 text-white transition-all shadow-md shadow-emerald-600/30"
          >
            <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24">
              <path d="M.057 24l1.687-6.163c-1.041-1.804-1.588-3.849-1.587-5.946.003-6.556 5.338-11.891 11.893-11.891 3.181.001 6.167 1.24 8.413 3.488 2.245 2.248 3.481 5.236 3.48 8.414-.003 6.557-5.338 11.892-11.893 11.892-1.99-.001-3.951-.5-5.688-1.448l-6.305 1.654zm6.597-3.807c1.676.995 3.276 1.591 5.392 1.592 5.448 0 9.886-4.334 9.889-9.885.002-5.462-4.415-9.89-9.881-9.892-5.452 0-9.887 4.334-9.889 9.884-.001 2.225.651 3.891 1.746 5.634l-.999 3.648 3.742-.981zm11.387-5.464c-.074-.124-.272-.198-.57-.347-.297-.149-1.758-.868-2.031-.967-.272-.099-.47-.149-.669.149-.198.297-.768.967-.941 1.165-.173.198-.347.223-.644.074-.297-.149-1.255-.462-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.297-.347.446-.521.151-.172.2-.296.3-.495.099-.198.05-.372-.025-.521-.075-.148-.669-1.611-.916-2.206-.242-.579-.487-.501-.669-.51l-.57-.01c-.198 0-.52.074-.792.372s-1.04 1.016-1.04 2.479 1.065 2.876 1.213 3.074c.149.198 2.095 3.2 5.076 4.487.709.306 1.263.489 1.694.626.712.226 1.36.194 1.872.118.571-.085 1.758-.719 2.006-1.413.248-.695.248-1.29.173-1.414z"/>
            </svg>
            <span>Kirim ke WhatsApp</span>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { useRouter } from 'vue-router'
import { leaksData } from '~/data/leaks'

const router = useRouter()
const searchQuery = ref('')
const selectedCategory = ref('Semua')
const categories = ['Semua', 'Server', 'Map', 'Add-on']

// State untuk Modal Request WhatsApp
const showRequestModal = ref(false)
const requestText = ref('')
const whatsappNumber = '6287815448792' // Nomor WhatsApp yang diperbarui

const goToDetail = (id) => {
  router.push(`/leak/${id}`)
}

const sendToWhatsApp = () => {
  if (!requestText.value.trim()) {
    alert('Mohon isi detail request terlebih dahulu!')
    return
  }

  // Format pesan WhatsApp otomatis
  const message = encodeURIComponent(
    `Halo Min, saya ingin request:\n\n*Detail:* ${requestText.value}\n\n*Catatan:* Saya siap membayar biaya request sebesar Rp 5.000.`
  )

  window.open(`https://wa.me/${whatsappNumber}?text=${message}`, '_blank')
  showRequestModal.value = false
  requestText.value = ''
}

const filteredLeaks = computed(() => {
  return leaksData.filter((leak) => {
    const q = searchQuery.value.toLowerCase().trim()
    const matchesSearch = 
      leak.title.toLowerCase().includes(q) ||
      leak.shortDescription.toLowerCase().includes(q)

    const matchesCategory = 
      selectedCategory.value === 'Semua' || leak.category === selectedCategory.value

    return matchesSearch && matchesCategory
  })
})
</script>