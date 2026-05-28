<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import { Head, Link } from '@inertiajs/vue3';

defineProps({
    canLogin: Boolean,
    canRegister: Boolean,
});

// Lógica para el menú móvil
const isMobileMenuOpen = ref(false);
const toggleMobileMenu = () => {
    isMobileMenuOpen.value = !isMobileMenuOpen.value;
};

// Lógica para el Carrusel de Fondo en la sección Hero
const currentSlide = ref(0);
const slides = ref([
    {
        image: 'https://images.unsplash.com/photo-1508700115892-45ecd05ae2ad?q=80&w=1200',
        title: 'Baila y REBAILA.',
        description: 'Bailar nunca fue tan fácil. Ahora puedes aprender cuándo y dónde quieras. Prueba y si no te gusta te devolvemos el dinero.'
    },
    {
        image: 'https://images.unsplash.com/photo-1516450360452-9312f5e86fc7?q=80&w=1200',
        title: 'Domina el Ritmo.',
        description: 'Siente la música y aprende las mejores técnicas de fusión desde la comodidad de tu hogar con instructores certificados.'
    },
    {
        image: 'https://images.unsplash.com/photo-1547153760-18fc86324498?q=80&w=1200',
        title: 'Expresión Sin Límites.',
        description: 'Únete a la comunidad de danza más grande y accede a todas las clases grabadas en alta definición las 24 horas.'
    }
]);

let intervalId = null;

onMounted(() => {
    // Cambia de imagen automáticamente cada 3 segundos (3000ms)
    intervalId = setInterval(() => {
        currentSlide.value = (currentSlide.value + 1) % slides.value.length;
    }, 3000);
});

onUnmounted(() => {
    if (intervalId) clearInterval(intervalId);
});
</script>

<template>

    <Head title="Duality Tribal - Clases de Baile Online">
        <!-- Importación de Google Fonts: Poppins -->
        <link rel="preconnect" href="https://fonts.googleapis.com">
            <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
                <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;700;900&display=swap"
                    rel="stylesheet">
    </Head>

    <!-- Aplicación global de la fuente Poppins mediante estilo en línea -->
    <div class="min-h-screen bg-black text-white selection:bg-purple-600 selection:text-white"
        style="font-family: 'Poppins', sans-serif;">

        <!-- BARRA DE NAVEGACIÓN (80% de ancho en escritorio) -->
        <nav class="bg-white text-black sticky top-0 z-50 border-b border-gray-200" aria-label="Navegación principal">
            <div class="w-full lg:w-[80%] mx-auto px-4 lg:px-0">
                <div class="flex items-center justify-between h-16">

                    <!-- Sección Izquierda: Logo Clickeable y Enlaces -->
                    <div class="flex items-center space-x-8 h-16">
                        <!-- Logo envuelto en Link de Inertia para redirección limpia -->
                        <div class="flex-shrink-0 flex items-center">
                            <Link :href="route('home')"
                                class="text-lg font-black tracking-tighter text-gray-900 uppercase flex items-center hover:opacity-80 transition-opacity focus:outline-none">
                                <span
                                    class="bg-purple-900 text-white px-1.5 py-0.5 rounded-sm mr-2 text-xs transform -scale-x-100 inline-block font-bold">ЯB</span>
                                <span class="font-black text-purple-900 tracking-tight">Duality</span>
                                <span class="font-medium text-gray-900 tracking-tight ml-1">Tribal</span>
                            </Link>
                        </div>

                        <!-- Enlaces principales (font-bold y text-[15px]) -->
                        <ul
                            class="hidden md:flex space-x-6 text-[15px] font-bold text-gray-700 tracking-tight h-16 items-center">
                            <li><a href="#" class="hover:text-purple-600 transition-colors">Descubre</a></li>
                            <li><a href="#" class="hover:text-purple-600 transition-colors">Cursos</a></li>
                            <li><a href="#" class="hover:text-purple-600 transition-colors">Programas</a></li>
                            <li><a href="#" class="hover:text-purple-600 transition-colors">Todas las clases</a></li>
                        </ul>
                    </div>

                    <!-- Sección Derecha: Buscador Minimalista y Botones de Autenticación -->
                    <div class="flex items-center h-16 space-x-4 md:space-x-0">

                        <!-- Buscador Minimalista Expandible -->
                        <div class="relative hidden md:block mr-6 group">
                            <label for="search" class="sr-only">Buscar clases de baile</label>
                            <input id="search" type="text" placeholder="Buscar..."
                                class="bg-gray-55 text-gray-900 pl-3 pr-9 py-1.5 text-xs rounded-full border border-transparent focus:border-gray-200 focus:bg-white focus:ring-0 focus:outline-none w-40 focus:w-60 transition-all duration-300 ease-in-out placeholder-gray-400" />
                            <span
                                class="absolute right-3 top-2.5 text-gray-400 group-focus-within:text-purple-600 transition-colors duration-300 pointer-events-none"
                                aria-hidden="true">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                                    stroke-width="2.5" stroke="currentColor" class="w-3.5 h-3.5">
                                    <path stroke-linecap="round" stroke-linejoin="round"
                                        d="m21 21-5.197-5.197m0 0A7.5 7.5 0 1 0 5.196 5.196a7.5 7.5 0 0 0 10.602 10.602Z" />
                                </svg>
                            </span>
                        </div>

                        <!-- Botones de Autenticación Completos (Altos y continuos) -->
                        <div v-if="canLogin" class="hidden md:flex items-center h-16">
                            <Link v-if="$page.props.auth.user" :href="route('dashboard')"
                                class="bg-purple-700 text-white h-16 px-6 flex items-center font-bold text-sm hover:bg-purple-600">
                                Mi Panel
                            </Link>

                            <template v-else>
                                <Link :href="route('login')"
                                    class="bg-[#00df89] text-black h-16 px-6 flex items-center font-bold text-xs hover:bg-[#00c478] transition-colors tracking-wide">
                                    Inicia sesión
                                </Link>
                                <Link :href="route('register')"
                                    class="bg-[#5900cc] text-white h-16 px-6 flex items-center font-bold text-xs hover:bg-[#4a00b0] transition-colors tracking-wide">
                                    Regístrate
                                </Link>
                            </template>
                        </div>

                        <!-- Botón de Menú Hamburguesa para Móvil -->
                        <div class="flex items-center md:hidden">
                            <button @click="toggleMobileMenu" type="button"
                                class="p-2 rounded-md text-gray-700 hover:text-purple-600 focus:outline-none"
                                :aria-expanded="isMobileMenuOpen.toString()">
                                <svg v-if="!isMobileMenuOpen" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
                                    stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                        d="M4 6h16M4 12h16M4 18h16" />
                                </svg>
                                <svg v-else class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                        d="M6 18L18 6M6 6l12 12" />
                                </svg>
                            </button>
                        </div>

                    </div>
                </div>
            </div>

            <!-- Menú Desplegable Móvil -->
            <div v-show="isMobileMenuOpen" class="md:hidden bg-white border-t border-gray-200">
                <div class="px-4 pt-2 pb-3 space-y-1">
                    <a href="#" class="block py-2 text-sm font-bold text-gray-900 border-b border-gray-100">Descubre</a>
                    <a href="#" class="block py-2 text-sm font-bold text-gray-900 border-b border-gray-100">Cursos</a>
                    <a href="#"
                        class="block py-2 text-sm font-bold text-gray-900 border-b border-gray-100">Programas</a>
                    <a href="#" class="block py-2 text-sm font-bold text-gray-900">Todas las clases</a>
                </div>
                <div class="px-4 py-2 border-t border-gray-200">
                    <input type="text" placeholder="Buscar..."
                        class="w-full bg-gray-100 text-black pl-3 pr-4 py-1.5 text-xs border border-gray-300 rounded-full" />
                </div>
                <div v-if="canLogin" class="border-t border-gray-200">
                    <div class="grid grid-cols-2">
                        <Link :href="route('login')" class="text-center bg-[#00df89] text-black py-3 font-bold text-xs">
                            Inicia
                            sesión</Link>
                        <Link :href="route('register')"
                            class="text-center bg-[#5900cc] text-white py-3 font-bold text-xs">
                            Regístrate</Link>
                    </div>
                </div>
            </div>
        </nav>

        <!-- SECCIÓN HERO (Altura configurada a h-[700px] según tus indicaciones) -->
        <header class="relative w-full h-[700px] overflow-hidden bg-gray-950 flex items-center">

            <!-- Slides del Carrusel Automático -->
            <div v-for="(slide, index) in slides" :key="index" v-show="currentSlide === index"
                class="absolute inset-0 w-full h-full transition-opacity duration-1000 ease-in-out">
                <!-- Filtro translúcido oscuro -->
                <div class="absolute inset-0 bg-gradient-to-r from-black via-black/75 to-black/30 z-10"></div>
                <img :src="slide.image" :alt="slide.title"
                    class="w-full h-full object-cover object-center absolute inset-0" />

                <!-- Contenido alineado al 80% del ancho general de la página -->
                <div class="relative z-20 w-full lg:w-[80%] mx-auto h-full flex items-center px-4 lg:px-0">
                    <div class="max-w-2xl space-y-5">
                        <span class="text-purple-500 font-bold uppercase tracking-widest text-xs block">Clases de Baile
                            Online</span>
                        <h1 class="text-4xl md:text-6xl font-black tracking-tight leading-none text-white">
                            {{ slide.title }}
                        </h1>
                        <p class="text-gray-300 text-base md:text-lg leading-relaxed max-w-xl">
                            {{ slide.description }}
                        </p>
                        <div class="pt-3">
                            <button
                                class="bg-[#5900cc] hover:bg-[#4a00b0] text-white font-bold px-8 py-4 text-sm tracking-wide transition-transform active:scale-95 shadow-md">
                                Empieza AHORA
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </header>

    </div>
</template>
