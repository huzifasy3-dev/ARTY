<!DOCTYPE html>
<html class="dark" dir="rtl" lang="ar">
<head>
    <meta charset="utf-8"/>
    <meta content="width=device-width, initial-scale=1.0" name="viewport"/>
    <title>الديوان الرقمي | المنصة الملكية</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;700&family=Cairo:wght@400;600;700;900&display=swap" rel="stylesheet"/>
    <link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:wght,FILL@100..700,0..1&display=swap" rel="stylesheet"/>
    
    <script src="https://cdn.tailwindcss.com?plugins=forms,container-queries"></script>
    <script id="tailwind-config">
      tailwind.config = {
        darkMode: "class",
        theme: {
          extend: {
            colors: {
              "background": "#0b1326",
              "surface": "#131b2e",
              "primary": "#b6c4ff",
              "secondary": "#d2bbff",
              "accent": "#6001d1",
              "outline-variant": "#444651",
            },
            fontFamily: {
              "headline": ["Cairo", "sans-serif"],
              "body": ["Cairo", "sans-serif"]
            }
          },
        },
      }
    </script>
    
    <style>
      .material-symbols-outlined { font-variation-settings: 'FILL' 0, 'wght' 400, 'GRAD' 0, 'opsz' 24; }
      body { background-color: #0b1326; color: #dae2fd; font-family: 'Cairo', sans-serif; overflow-x: hidden; }
      .no-scrollbar::-webkit-scrollbar { display: none; }
      .glass-card { background: rgba(23, 31, 51, 0.6); backdrop-filter: blur(12px); border: 1px solid rgba(143, 144, 157, 0.1); }
      [v-cloak] { display: none; }
    </style>
</head>

<body class="selection:bg-secondary selection:text-black">
<div id="app" v-cloak>

    <div v-if="sidebarOpen" @click="sidebarOpen = false" class="fixed inset-0 bg-black/60 z-40 lg:hidden backdrop-blur-sm"></div>

    <header class="fixed top-0 w-full z-50 glass-card border-b border-white/5 shadow-2xl">
        <div class="flex flex-row-reverse justify-between items-center px-6 h-20">
            <div class="flex items-center gap-4">
                <div class="hidden md:block text-right">
                    <p class="text-[10px] text-gray-400 font-bold uppercase tracking-widest">مرحباً بك</p>
                    <p class="text-sm font-black text-primary">{{ user?.displayName || 'المستخدم الملكي' }}</p>
                </div>
                <div class="w-11 h-11 rounded-full p-0.5 bg-gradient-to-tr from-primary to-secondary">
                    <img :src="user?.photoURL || 'https://ui-avatars.com/api/?name=R&background=0b1326&color=b6c4ff'" class="w-full h-full rounded-full object-cover border-2 border-background"/>
                </div>
            </div>
            
            <h1 class="font-headline text-2xl font-black bg-gradient-to-l from-primary to-secondary bg-clip-text text-transparent">الديوان الرقمي</h1>
            
            <div class="flex items-center gap-2">
                <button class="p-2.5 rounded-xl bg-white/5 hover:bg-white/10 transition-all active:scale-90 text-primary">
                    <span class="material-symbols-outlined">notifications</span>
                </button>
                <button @click="sidebarOpen = !sidebarOpen" class="p-2.5 rounded-xl bg-white/5 hover:bg-white/10 lg:hidden text-primary">
                    <span class="material-symbols-outlined">widgets</span>
                </button>
            </div>
        </div>
    </header>

    <aside :class="sidebarOpen ? 'translate-x-0' : 'translate-x-full lg:translate-x-0'" 
           class="fixed right-0 top-0 h-full w-72 bg-background border-l border-white/5 z-50 pt-24 p-6 transition-transform duration-500 ease-in-out">
        <div class="flex flex-col gap-2">
            <a href="#" class="flex flex-row-reverse items-center justify-between p-4 rounded-2xl bg-primary/10 text-primary font-bold border-r-4 border-primary">
                <span>الرئيسية</span> <span class="material-symbols-outlined">home</span>
            </a>
            <a href="#" class="flex flex-row-reverse items-center justify-between p-4 rounded-2xl text-gray-400 hover:bg-white/5 transition-all">
                <span>التقارير</span> <span class="material-symbols-outlined">analytics</span>
            </a>
            <a href="#" class="flex flex-row-reverse items-center justify-between p-4 rounded-2xl text-gray-400 hover:bg-white/5 transition-all">
                <span>الإعدادات</span> <span class="material-symbols-outlined">settings</span>
            </a>
            <button @click="handleSignOut" class="flex flex-row-reverse items-center justify-between p-4 mt-10 rounded-2xl text-red-400 hover:bg-red-500/10 transition-all">
                <span>خروج</span> <span class="material-symbols-outlined">logout</span>
            </button>
        </div>
    </aside>

    <main class="pt-28 pb-32 px-4 lg:mr-72 transition-all duration-500">
        
        <section class="mb-12">
            <div class="relative h-[450px] rounded-[2rem] overflow-hidden shadow-2xl group">
                <div class="absolute inset-0 bg-gradient-to-t from-background via-background/20 to-transparent z-10"></div>
                <img :src="featuredNews?.image || 'https://images.unsplash.com/photo-1639762681485-074b7f938ba0?auto=format&fit=crop&q=80'" 
                     class="w-full h-full object-cover transition-transform duration-1000 group-hover:scale-110"/>
                
                <div class="absolute bottom-0 right-0 p-8 z-20 w-full text-right">
                    <span class="px-4 py-1 rounded-full bg-accent text-[10px] font-bold uppercase tracking-tighter">عاجل • تقنية سيادية</span>
                    <h2 class="text-3xl md:text-5xl font-black text-white mt-4 mb-4 leading-tight">
                        {{ featuredNews?.title || 'إطلاق الجيل الثالث من المعالجات الوطنية' }}
                    </h2>
                    <p class="text-gray-300 text-sm md:text-lg max-w-2xl mb-6 line-clamp-2">
                        {{ featuredNews?.summary || 'تعرف على تفاصيل الثورة التقنية الجديدة التي ستقود المنطقة نحو استقلال رقمي كامل.' }}
                    </p>
                    <button class="px-8 py-3.5 bg-primary text-black font-black rounded-2xl hover:shadow-[0_0_30px_rgba(182,196,255,0.4)] transition-all active:scale-95">
                        تفاصيل الخبر
                    </button>
                </div>
            </div>
        </section>

        <section class="mb-16">
            <div class="flex items-center gap-3 mb-8 border-r-4 border-secondary pr-4">
                <h2 class="text-2xl font-black text-white">ومضات رقمية</h2>
                <span class="text-xs text-secondary animate-pulse">● مباشر</span>
            </div>
            <div class="flex overflow-x-auto gap-5 pb-4 no-scrollbar snap-x rtl:flex-row-reverse">
                <div v-for="short in shorts" :key="short.id" 
                     class="flex-none w-44 h-72 relative rounded-3xl overflow-hidden snap-start shadow-xl group cursor-pointer border border-white/5">
                    <img :src="short.thumbnail" class="w-full h-full object-cover group-hover:scale-110 transition-all duration-500"/>
                    <div class="absolute inset-0 bg-gradient-to-t from-black via-transparent to-transparent"></div>
                    <div class="absolute bottom-4 right-4 left-4 text-right">
                        <p class="text-[10px] text-secondary font-black mb-1">#{{ short.tag }}</p>
                        <p class="text-xs font-bold text-white line-clamp-2">{{ short.title }}</p>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <nav class="fixed bottom-0 w-full z-50 glass-card border-t border-white/5 md:hidden rounded-t-[2.5rem] px-6 py-4">
        <div class="flex flex-row-reverse justify-around items-center">
            <a href="#" class="flex flex-col items-center text-primary">
                <span class="material-symbols-outlined text-2xl" style="font-variation-settings: 'FILL' 1;">home</span>
                <span class="text-[10px] font-bold mt-1">الرئيسية</span>
            </a>
            <a href="#" class="flex flex-col items-center text-gray-500">
                <span class="material-symbols-outlined text-2xl">newspaper</span>
                <span class="text-[10px] font-bold mt-1">الأخبار</span>
            </a>
            <a href="#" class="flex flex-col items-center text-gray-500">
                <span class="material-symbols-outlined text-2xl">movie_filter</span>
                <span class="text-[10px] font-bold mt-1">وثائقي</span>
            </a>
            <a href="#" class="flex flex-col items-center text-gray-500">
                <span class="material-symbols-outlined text-2xl">person</span>
                <span class="text-[10px] font-bold mt-1">حسابي</span>
            </a>
        </div>
    </nav>

</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script type="module">
    const { createApp, ref, onMounted } = Vue;

    createApp({
        setup() {
            const sidebarOpen = ref(false);
            const user = ref({ displayName: 'المستخدم الملكي' });
            const shorts = ref([
                { id: 1, title: 'مستقبل الذكاء الاصطناعي', tag: 'تقنية', thumbnail: 'https://images.unsplash.com/photo-1677442136019-21780ecad995?auto=format&fit=crop&q=80' },
                { id: 2, title: 'رحلة إلى المريخ', tag: 'فضاء', thumbnail: 'https://images.unsplash.com/photo-1614728894747-a83421e2b9c9?auto=format&fit=crop&q=80' },
                { id: 3, title: 'عالم الروبوتات', tag: 'علوم', thumbnail: 'https://images.unsplash.com/photo-1485827404703-89b55fcc595e?auto=format&fit=crop&q=80' },
                { id: 4, title: 'أمن البيانات', tag: 'أمن', thumbnail: 'https://images.unsplash.com/photo-1550751827-4bd374c3f58b?auto=format&fit=crop&q=80' }
            ]);
            const featuredNews = ref(null);

            return { sidebarOpen, user, shorts, featuredNews };
        }
    }).mount('#app');
</script>
</body>
</html>
