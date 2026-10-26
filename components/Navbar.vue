<template>
  <header class="sticky top-0 z-50 backdrop-blur-xl bg-[#060b17]/80 border-b border-blue-500/10">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
      <!-- Logo Brand -->
      <NuxtLink to="/" class="flex items-center space-x-3 group">
        <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-blue-500 to-blue-700 flex items-center justify-center shadow-lg shadow-blue-500/25 group-hover:shadow-blue-500/50 transition-all duration-300 group-hover:scale-105">
          <svg class="w-6 h-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4" />
          </svg>
        </div>
        <div>
          <span class="text-xl font-extrabold tracking-tight text-white flex items-center gap-1.5">
            Mcpe<span class="text-blue-400">Leaks</span>
          </span>
          <span class="text-xs font-semibold px-2 py-0.5 rounded-full bg-blue-500/10 text-blue-400 border border-blue-500/20">
            by KraaDev
          </span>
        </div>
      </NuxtLink>

      <!-- External Links / Quick Status -->
      <div class="flex items-center space-x-3 sm:space-x-4">
        <div class="hidden sm:flex items-center space-x-2 text-xs font-medium text-blue-300 bg-blue-950/40 px-3 py-1.5 rounded-full border border-blue-800/40">
          <span class="w-2 h-2 rounded-full bg-emerald-400 animate-ping"></span>
          <span>Online Archive</span>
        </div>

        <!-- Tombol Request WhatsApp (Rp. 5k) -->
        <a 
          :href="whatsappUrl" 
          target="_blank" 
          rel="noopener noreferrer"
          class="inline-flex items-center gap-2 px-4 py-2 text-sm font-semibold rounded-lg bg-emerald-600 hover:bg-emerald-500 text-white shadow-lg shadow-emerald-600/20 hover:shadow-emerald-500/30 transition-all duration-200"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4 fill-current" viewBox="0 0 24 24">
            <path d="M.057 24l1.687-6.163c-1.041-1.804-1.588-3.849-1.587-5.946.003-6.556 5.338-11.891 11.893-11.891 3.181.001 6.167 1.24 8.413 3.488 2.245 2.248 3.481 5.236 3.48 8.414-.003 6.557-5.338 11.892-11.893 11.892-1.99-.001-3.951-.5-5.688-1.448l-6.305 1.654zm6.597-3.807c1.676.995 3.276 1.591 5.392 1.592 5.448 0 9.886-4.434 9.889-9.885.002-5.462-4.415-9.89-9.881-9.892-5.452 0-9.887 4.434-9.889 9.884-.001 2.225.651 3.891 1.746 5.634l-.999 3.648 3.742-.981zm11.387-5.464c-.074-.124-.272-.198-.57-.347-.297-.149-1.758-.868-2.031-.967-.272-.099-.47-.149-.669.149-.198.297-.768.967-.941 1.165-.173.198-.347.223-.644.074-.297-.149-1.255-.462-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.297-.347.446-.521.151-.172.2-.296.3-.495.099-.198.05-.372-.025-.521-.075-.148-.669-1.611-.916-2.206-.242-.579-.487-.501-.669-.51l-.57-.01c-.198 0-.52.074-.792.372s-1.04 1.016-1.04 2.479 1.065 2.876 1.213 3.074c.149.198 2.095 3.2 5.076 4.487.709.306 1.263.489 1.694.626.712.226 1.36.194 1.872.118.571-.085 1.758-.719 2.006-1.413.248-.695.248-1.29.173-1.414z"/>
          </svg>
          Request (Rp. 5k)
        </a>

        <a 
          href="https://discord.com" 
          target="_blank" 
          rel="noopener"
          class="px-4 py-2 text-sm font-semibold rounded-lg bg-blue-600/20 hover:bg-blue-600/30 text-blue-300 border border-blue-500/30 hover:border-blue-400 transition-all duration-200"
        >
          Join Discord
        </a>
      </div>
    </div>
  </header>
</template>

<script setup>
// Ganti nomor di bawah ini dengan nomor WhatsApp Anda (format internasional tanpa tanda +, contoh: 6281234567890)
const phoneNumber = '6281234567890'

// Pesan otomatis yang akan terisi ketika pengunjung mengklik tombol request
const message = encodeURIComponent(
  'Halo Kak KraaDev, saya ingin request file/leak Minecraft (MCPE). Saya paham bahwa layanan request ini dikenakan biaya jasa sebesar Rp. 5.000.\n\nBerikut detail request saya:\n- Nama/Jenis Leak:\n- Link Referensi (jika ada):\n- Catatan Tambahan:'
)

const whatsappUrl = `https://wa.me/${phoneNumber}?text=${message}`
</script>