<template>
  <div class="page-wrapper">

    <!-- ===== HERO ===== -->
    <section class="section-celestial">
      <div class="starfield" aria-hidden="true">
        <span v-for="n in 60" :key="`sh${n}`" :class="`star star-${n}`"></span>
      </div>
      <div class="fairies" aria-hidden="true">
        <span v-for="n in 14" :key="`fh${n}`" :class="`fairy fairy-${n}`"></span>
      </div>

      <div class="hero-content">
        <div class="bismillah-block">
          <p class="bismillah-arabic">بِسْمِ اللَّهِ الرَّحْمَنِ الرَّحِيمِ</p>
        </div>

        <div class="portrait-wrapper">
          <div class="portrait-frame">
            <div class="portrait-corner tl"></div>
            <div class="portrait-corner tr"></div>
            <div class="portrait-corner bl"></div>
            <div class="portrait-corner br"></div>
            <div class="portrait-inner">
              <img :src="photoUrl" alt="Almarhumah Sunipah binti Karim" class="portrait-img" @error="handleImgError"/>
            </div>
          </div>
          <div class="portrait-glow"></div>
        </div>

        <div class="inna-block">
          <p class="inna-arabic">إِنَّا لِلَّهِ وَإِنَّا إِلَيْهِ رَاجِعُونَ</p>
        </div>

        <div class="name-block">
          <p class="in-memoriam-label">ibu</p>
          <h2 class="name-title">sunipah binti karim</h2>
          <div class="gold-rule">
            <span class="gold-rule-line"></span>
            <span class="gold-rule-diamond">◆</span>
            <span class="gold-rule-line"></span>
          </div>
          <p class="wafat-text">Wafat pada <span class="wafat-date">28 April 2026</span> jam 19:00 wib</p>
          <p class="wafat-text"> dimakamkan jam 22:00-23:00 wib di TPU dusun tegalsari</p>
          <p class="wafat-sub">Semoga Allah SWT merahmati dan menempatkan beliau di surga</p>
        </div>
      </div>

      <div class="scroll-arrow">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
          <path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7"/>
        </svg>
      </div>
    </section>

    <!-- ===== TAHLILAN 7 HARI ===== -->
    <section class="section-celestial section-bordered">
      <div class="starfield-sm" aria-hidden="true">
        <span v-for="n in 30" :key="`st${n}`" :class="`star star-${n}`"></span>
      </div>
      <div class="fairies-sm" aria-hidden="true">
        <span v-for="n in 7" :key="`ft${n}`" :class="`fairy fairy-${n}`"></span>
      </div>

      <div class="container-md" style="position:relative;z-index:2">
        <div class="section-header">
          
          <h2 class="section-title light">Tahlilan 7 Hari</h2>
          <div class="section-ornament">
            <span class="orn-line"></span>
            <span class="orn-gem">❧</span>
            <span class="orn-line"></span>
          </div>
          <p class="section-desc light">
            Memohon kepada Allah SWT agar memberikan ampunan, rahmat, dan tempat terbaik bagi alm ibu Sunipah binti Karim
          </p>
        </div>

        <div class="timeline">
          <div class="timeline-track"></div>
          <div
            v-for="(day, i) in tahlilDays"
            :key="i"
            class="timeline-item"
            :class="{ 'is-today': day.today, 'is-done': day.done }"
          >
            <div class="timeline-node">
              <span v-if="day.done" class="node-check">✓</span>
              <span v-else-if="day.today" class="node-pulse"></span>
              <span v-else class="node-num">{{ i + 1 }}</span>
            </div>
            <div class="timeline-card">
              <div class="tl-card-top">
                <div>
                  <p class="tl-label">{{ day.label }}</p>
                  <p class="tl-date">{{ day.date }}</p>
                </div>
                <span v-if="day.today" class="badge-today">Hari Ini</span>
                <span v-else-if="day.done" class="badge-done">Selesai</span>
                <span v-else class="badge-coming">Mendatang</span>
              </div>
              <p class="tl-doa">{{ day.doa }}</p>
            </div>
          </div>
        </div>

        <div class="doa-banner">
          <div class="doa-banner-ornament"></div>
          <p class="doa-arabic">اللَّهُمَّ اغْفِرْ لَهَا وَارْحَمْهَا وَعَافِهَا وَاعْفُ عَنْهَا</p>
          <p class="doa-latin">"Ya Allah, ampunilah dia, rahmatilah dia, sejahterakanlah dia dan maafkanlah dia"</p>
        </div>
      </div>
    </section>

    <!-- ===== GALERI ===== -->
    <section class="section-gallery">
      <div class="container-lg">
        <div class="section-header">
          <span class="section-tag gold">Kenangan</span>
          <div class="section-ornament">
            <span class="orn-line gold"></span>
            <span class="orn-gem gold">❧</span>
            <span class="orn-line gold"></span>
          </div>
        </div>

        <!-- Netflix-style Carousel -->
        <div class="carousel-wrapper">
          <!-- Left Arrow -->
          <button class="carousel-arrow carousel-arrow-left" @click="prevItem" aria-label="Previous">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7"/>
            </svg>
          </button>

          <!-- Carousel Items -->
          <div class="carousel-track" @click="nextItem">
            <div
              v-for="(item, idx) in demoGalleryItems"
              :key="idx"
              class="carousel-item"
              :data-idx="idx"
              :class="{
                'is-center': idx === currentIndex,
                'is-left': idx === (currentIndex - 1 + totalItems) % totalItems,
                'is-right': idx === (currentIndex + 1) % totalItems,
                'is-hidden': idx !== currentIndex && idx !== (currentIndex - 1 + totalItems) % totalItems && idx !== (currentIndex + 1) % totalItems
              }"
            >
              <template v-if="item.type === 'photo'">
                <img :src="item.url" :alt="`Foto ${idx + 1}`" class="carousel-media" />
              </template>
              <template v-else>
                <video
                  :src="item.url"
                  class="carousel-media"
                  :muted="false"
                  :loop="true"
                  :playsinline="true"
                  :controls="false"
                  ref="videoRefs"
                ></video>
              </template>
            </div>
          </div>

          <!-- Right Arrow -->
          <button class="carousel-arrow carousel-arrow-right" @click="nextItem" aria-label="Next">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7"/>
            </svg>
          </button>
        </div>

        <!-- Counter -->
        <div class="carousel-counter">
          <span class="carousel-counter-label">{{ isPhoto ? 'Foto' : 'Video' }}</span>
          <span class="carousel-counter-num">{{ currentIndex + 1 }}</span>
          <span class="carousel-counter-sep">/</span>
          <span class="carousel-counter-total">{{ totalItems }}</span>
        </div>
      </div>
    </section>

    <!-- ===== KONTAK / LAYANAN ===== -->
    <section class="section-celestial section-bordered">
      <div class="starfield-sm" aria-hidden="true">
        <span v-for="n in 30" :key="`sl${n}`" :class="`star star-${(n % 30) + 31}`"></span>
      </div>
      <div class="fairies-sm" aria-hidden="true">
        <span v-for="n in 7" :key="`fl${n}`" :class="`fairy fairy-${(n % 7) + 8}`"></span>
      </div>

      <div class="container-md" style="position:relative;z-index:2">
        <div class="section-header">
          <span class="section-tag">Layanan</span>
          <h2 class="section-title light">Kenangan</h2>
          <div class="section-ornament">
            <span class="orn-line"></span>
            <span class="orn-line"></span>
          </div>
          <p class="section-desc light">
            Kami membantu keluarga mengabadikan kenangan orang tercinta dalam sebuah karya digital yang indah dan bermakna
          </p>
        </div>

        <div class="feature-grid">
          <div v-for="f in features" :key="f.title" class="feature-card">
            <p class="feature-title">{{ f.title }}</p>
            <p class="feature-desc">{{ f.desc }}</p>
          </div>
        </div>

        <div class="contact-card">
          <img src="/profil.jpeg" alt="Muhammad Munirudin" class="contact-avatar-img" />
          <p class="contact-name">Muhammad Munirudin</p>
          <p class="contact-role">Pembuat Kenangan Digital</p>
          <div class="contact-actions">
            <a
              :href="`https://wa.me/62${phone.substring(1)}?text=Assalamu'alaikum, saya ingin memesan portfolio kenangan.`"
              target="_blank" rel="noopener noreferrer" class="btn-wa"
            >
              <svg viewBox="0 0 24 24" fill="currentColor" class="btn-icon">
                <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/>
              </svg>
              {{ phone }}
            </a>
            <a :href="`mailto:${email}?subject=Pesanan Portfolio Kenangan`" class="btn-email">
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" class="btn-icon">
                <path stroke-linecap="round" stroke-linejoin="round" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/>
              </svg>
              {{ email }}
            </a>
          </div>
        </div>
      </div>
    </section>

    <!-- ===== FOOTER ===== -->
    <footer class="site-footer">
      <div class="footer-fairies" aria-hidden="true">
        <span v-for="n in 8" :key="`ff${n}`" :class="`ffairy ffairy-${n}`"></span>
      </div>
      <div class="footer-ornament">
        <span class="f-line"></span><span class="f-gem">◆</span><span class="f-line"></span>
      </div>
      <p class="footer-arabic">رَحِمَهَا اللَّهُ وَأَسْكَنَهَا فَسِيحَ جَنَّاتِهِ</p>
      <p class="footer-trans">Semoga Allah merahmatinya dan menempatkannya di surga-Nya yang luas</p>
      <p class="footer-name">Sunipah binti Karim · 28 April 2026</p>
      <p class="footer-credit">Selalu di hati, selamanya dalam doa</p>
    </footer>

    <button
      type="button"
      class="music-fab"
      :class="{ 'is-playing': isMusicPlaying }"
      :aria-pressed="isMusicPlaying"
      :aria-label="isMusicPlaying ? 'Matikan musik' : 'Putar musik'"
      @click="toggleMusic"
    >
      <span class="music-fab-icon" aria-hidden="true">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8">
          <path stroke-linecap="round" stroke-linejoin="round" d="M9 18V6l10-2v12" />
          <circle cx="7" cy="18" r="3" fill="currentColor" stroke="none" />
          <circle cx="17" cy="16" r="3" fill="currentColor" stroke="none" />
        </svg>
      </span>
      <span class="music-fab-text"></span>
    </button>

  </div>
</template>

<script setup lang="ts">
import { computed, nextTick, onBeforeUnmount, ref, watch } from "vue";

// Google Drive folder configuration
const driveFolderId = "1bn88ebnrYDrbb5QftMvF_Zs_YTdh1Nch";

const phone = "whatsapp";
const email = "email";
const photoUrl = ref(`${import.meta.env.BASE_URL}ibu.jpeg`);
const musicAudio = new Audio(`${import.meta.env.BASE_URL}dd.mp3`);
const isMusicPlaying = ref(false);

musicAudio.loop = true;
musicAudio.preload = "auto";
musicAudio.volume = 0.9;

function handleImgError(e: Event) {
  (e.target as HTMLImageElement).src =
    "https://images.unsplash.com/photo-1502086223501-7ea6ecd79368?w=400&h=600&fit=crop";
}

async function toggleMusic() {
  if (isMusicPlaying.value) {
    musicAudio.pause();
    isMusicPlaying.value = false;
    return;
  }

  try {
    await musicAudio.play();
    isMusicPlaying.value = true;
  } catch {
    isMusicPlaying.value = false;
  }
}

onBeforeUnmount(() => {
  musicAudio.pause();
  musicAudio.currentTime = 0;
});

// =====================
// AUTO LOAD GALLERY FROM LOCAL FOLDER
// =====================
const driveFiles = ref<{ type: string; id: string }[]>([]);
const isGalleryLoading = ref(true);

// Load files from local folder using Vite glob import
function loadDriveFiles() {
  // Use Vite's glob import to get all files from the gallery folder
  const modules = import.meta.glob('/public/7hari/7hari ibu_/*.{jpg,jpeg,png,mp4}', { eager: true });
  
  const files = Object.keys(modules)
    .map(path => {
      const name = path.split('/').pop() || '';
      const ext = name.toLowerCase().split('.').pop();
      return {
        type: ext === 'mp4' ? 'video' : 'photo',
        id: path.replace('/public/', '')
      };
    })
    .sort((a, b) => a.id.localeCompare(b.id));
  
  driveFiles.value = files;
  isGalleryLoading.value = false;
}

// Helper to get file URL (local or Drive)
function getPhotoUrl(filePath: string, width = 800): string {
  return `${import.meta.env.BASE_URL}${filePath}`;
}

function getVideoUrl(filePath: string): string {
  return `${import.meta.env.BASE_URL}${filePath}`;
}

// Load gallery files on init
loadDriveFiles();

const demoGalleryItems = computed(() => {
  // If we have Drive files, use them
  if (driveFiles.value.length > 0) {
    return driveFiles.value.map(file => ({
      type: file.type,
      url: file.type === "photo" ? getPhotoUrl(file.id) : getVideoUrl(file.id)
    }));
  }
  // Fallback demo images
  return [
    { type: "photo", url: "https://picsum.photos/800/600?random=1" },
    { type: "photo", url: "https://picsum.photos/800/600?random=2" },
    { type: "photo", url: "https://picsum.photos/800/600?random=3" },
    { type: "photo", url: "https://picsum.photos/800/600?random=4" },
    { type: "video", url: "https://drive.google.com/uc?export=download&id=1EXAMPLE" },
    { type: "photo", url: "https://picsum.photos/800/600?random=5" },
    { type: "photo", url: "https://picsum.photos/800/600?random=6" },
    { type: "photo", url: "https://picsum.photos/800/600?random=7" },
    { type: "photo", url: "https://picsum.photos/800/600?random=8" },
  ];
});

const currentIndex = ref(0);
const totalItems = computed(() => demoGalleryItems.value.length);
const currentItem = computed(() => demoGalleryItems.value[currentIndex.value]);
const isPhoto = computed(() => currentItem.value?.type === "photo");
const currentVideoEl = ref<HTMLVideoElement | null>(null);

// Auto-play video when center item is video
watch(currentIndex, async (newIdx) => {
  // Pause all videos first
  document.querySelectorAll('.carousel-media').forEach((el) => {
    if (el instanceof HTMLVideoElement) {
      el.pause();
      el.currentTime = 0;
    }
  });

  // Adjust music volume based on current media type
  if (demoGalleryItems.value[newIdx]?.type === "video") {
    musicAudio.volume = 0.4;
  } else if (isMusicPlaying.value) {
    musicAudio.volume = 0.9;
  }

  // Wait for DOM update then play video if current item is video
  await nextTick();
  const videoEl = document.querySelector(`.carousel-item[data-idx="${newIdx}"] video`) as HTMLVideoElement;
  if (videoEl && demoGalleryItems.value[newIdx]?.type === "video") {
    try {
      await videoEl.play();
    } catch (e) {
      // Autoplay blocked, ignore
    }
  }
});

// Carousel navigation
function nextItem() {
  currentIndex.value = (currentIndex.value + 1) % totalItems.value;
}

function prevItem() {
  currentIndex.value = (currentIndex.value - 1 + totalItems.value) % totalItems.value;
}

function goTo(index: number) {
  currentIndex.value = index;
}

const tahlilDays = computed(() => {
  const wafat = new Date("2026-04-28");
  const today = new Date();
  today.setHours(0, 0, 0, 0);
  const doas = [
    "اللَّهُمَّ اغْفِرْ لَهَا وَارْحَمْهَا",
    "اللَّهُمَّ عَافِهَا وَاعْفُ عَنْهَا",
    "اللَّهُمَّ أَكْرِمْ نُزُلَهَا",
    "اللَّهُمَّ وَسِّعْ مُدْخَلَهَا",
    "اللَّهُمَّ اغْسِلْهَا بِالْمَاءِ وَالثَّلْجِ وَالْبَرَدِ",
    "اللَّهُمَّ نَقِّهَا مِنَ الْخَطَايَا كَمَا نَقَّيْتَ الثَّوْبَ",
    "اللَّهُمَّ أَدْخِلْهَا الْجَنَّةَ وَأَعِذْهَا مِنْ عَذَابِ الْقَبْرِ",
  ];
  return Array.from({ length: 7 }, (_, i) => {
    const d = new Date(wafat);
    d.setDate(wafat.getDate() + i);
    d.setHours(0, 0, 0, 0);
    return {
      label: i === 0 ? "Hari Pertama — Hari Wafat" : `Hari ke-${i + 1}`,
      date: d.toLocaleDateString("id-ID", { weekday: "long", day: "numeric", month: "long", year: "numeric" }),
      doa: doas[i],
      today: d.getTime() === today.getTime(),
      done: d < today,
    };
  });
});

const features = [
  { title: "Desain Personal",     desc: "Setiap detail dirancang khusus untuk menghormati kenangan orang terkasih" },
  { title: "Galeri Foto & Video", desc: "Tampil otomatis dan bisa diperbarui kapan saja tanpa batas" },
  { title: "Akses Selamanya",     desc: "Website dapat diakses seumur hidup, tidak ada batas waktu" },
  { title: "QR di Kitab Yasin",   desc: "QR code siap cetak untuk ditempel di kitab atau brosur doa" },
  { title: "Proses Cepat",        desc: "Selesai dalam 1–2 hari kerja setelah materi diterima" },
  { title: "Dibuat dengan Hati",  desc: "Dikerjakan dengan rasa empati dan penghormatan yang tulus" },
];
</script>
