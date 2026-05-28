<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import { Head, Link } from '@inertiajs/vue3';
import Navbar from '@/Components/Navbar.vue';
import Footer from '@/Components/Footer.vue';

defineProps({
    canLogin: Boolean,
    canRegister: Boolean,
});

// Lógica para el menú móvil
const isMobileMenuOpen = ref(false);
const toggleMobileMenu = () => {
    isMobileMenuOpen.value = !isMobileMenuOpen.value;
};

// Lógica para el Carrusel de Fondo en la sección Hero (700px de alto)
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
    intervalId = setInterval(() => {
        currentSlide.value = (currentSlide.value + 1) % slides.value.length;
    }, 3000);
});

onUnmounted(() => {
    if (intervalId) clearInterval(intervalId);
});


// Borra las declaraciones anteriores y pon esta única versión:
const instructors = [
    { name: 'Sonia Ayats', style: 'Commercial', image: 'path/to/sonia.jpg', ig: '@sonia', x: '@soniax', tt: '@soniatt' },
    { name: 'Carlos Palacios', style: 'Zumba', image: 'path/to/carlos.jpg', ig: '@carlos', x: '@carlosx', tt: '@carlostt' },
    { name: 'Marc Lapuerta', style: 'Contemporáneo', image: 'path/to/marc.jpg', ig: '@marc', x: '@marcx', tt: '@marctt' },
    { name: 'Bea Ortiz', style: 'Reggaeton', image: 'path/to/bea.jpg', ig: '@bea', x: '@beax', tt: '@beatt' },
    { name: 'Alicia Alonso', style: 'Danza Clásica', image: 'path/to/alicia.jpg', ig: '@alicia', x: '@aliciax', tt: '@aliciatt' },
    { name: 'Sergio Santed', style: 'Sexy Style', image: 'path/to/sergio.jpg', ig: '@sergio', x: '@sergiox', tt: '@sergiott' },
    { name: 'Shee Benito', style: 'Dancehall', image: 'path/to/shee.jpg', ig: '@shee', x: '@sheex', tt: '@sheett' },
    { name: 'Bea Villabol', style: 'Hip hop', image: 'path/to/villabol.jpg', ig: '@beaV', x: '@beaVx', tt: '@beaVtt' }
];

const isModalOpen = ref(false);
const selectedInstructor = ref(null);

const openInstructorModal = (instructor) => {
    selectedInstructor.value = instructor;
    isModalOpen.value = true;
};


</script>

<template>

    <Head title="Duality Tribal - Clases de Baile Online">
        <!-- Importación de Google Fonts: Poppins -->
        <link rel="preconnect" href="https://fonts.googleapis.com">
        <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
        <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;700;900&display=swap"
            rel="stylesheet">
    </Head>

    <!-- Aplicación global de la fuente Poppins -->
    <div class="min-h-screen bg-black text-white selection:bg-purple-600 selection:text-white"
        style="font-family: 'Poppins', sans-serif;">

        <Navbar />

        <!-- SECCIÓN HERO (700px de alto) -->
        <header class="relative w-full h-[700px] overflow-hidden bg-gray-950 flex items-center">
            <div v-for="(slide, index) in slides" :key="index" v-show="currentSlide === index"
                class="absolute inset-0 w-full h-full transition-opacity duration-1000 ease-in-out">
                <div class="absolute inset-0 bg-gradient-to-r from-black via-black/75 to-black/30 z-10"></div>
                <img :src="slide.image" :alt="slide.title"
                    class="w-full h-full object-cover object-center absolute inset-0" />
                <div class="relative z-20 w-full lg:w-[80%] mx-auto h-full flex items-center px-4 lg:px-0">
                    <div class="max-w-2xl space-y-5">
                        <span class="text-purple-500 font-bold uppercase tracking-widest text-xs block">Clases de Baile
                            Online</span>
                        <h1 class="text-4xl md:text-6xl font-black tracking-tight leading-none text-white">{{
                            slide.title }}
                        </h1>
                        <p class="text-gray-300 text-base md:text-lg leading-relaxed max-w-xl">{{ slide.description }}
                        </p>
                        <div class="pt-3">
                            <button
                                class="bg-[#5900cc] hover:bg-[#4a00b0] text-white font-bold px-8 py-4 text-sm tracking-wide transition-transform active:scale-95 shadow-md">Empieza
                                AHORA</button>
                        </div>
                    </div>
                </div>
            </div>
        </header>

        <!-- SECCIÓN: APRENDE A BAILAR PASO A PASO -->
        <section class="w-full bg-[#f4f4f4] text-black min-h-[500px] flex items-center py-16">
            <div class="w-full lg:w-[80%] mx-auto px-4 lg:px-0 space-y-12">
                <div class="max-w-3xl space-y-4">
                    <h2 class="text-3xl md:text-4xl font-black text-[#5900cc] tracking-tight">Aprende a bailar paso a
                        paso</h2>
                    <p class="text-gray-900 text-sm md:text-base font-bold leading-relaxed tracking-tight">
                        Una escuela de baile 100% online, con clases ilimitadas siempre a tu disposición, estés donde
                        estés.
                        Tengas experiencia o quieras mejorar tu técnica, alcanza nuevas metas con REBAILA.
                    </p>
                </div>

                <div class="grid grid-cols-2 md:grid-cols-4 gap-8 pt-4">
                    <div class="flex flex-col items-center text-center space-y-4 group">
                        <div
                            class="w-20 h-32 flex items-center justify-center transition-transform duration-300 group-hover:scale-105">
                            <svg class="w-full h-full text-purple-700" viewBox="0 0 100 150" fill="none"
                                xmlns="http://www.w3.org/2000/svg">
                                <rect x="5" y="5" width="90" height="140" rx="10" stroke="url(#gradient-cyan-purple)"
                                    stroke-width="4" />
                                <circle cx="50" cy="75" r="15" stroke="url(#gradient-cyan-purple)" stroke-width="4" />
                                <polygon points="46,67 60,75 46,83" fill="url(#gradient-cyan-purple)" />
                                <line x1="40" y1="130" x2="60" y2="130" stroke="url(#gradient-cyan-purple)"
                                    stroke-width="4" stroke-linecap="round" />
                            </svg>
                        </div>
                        <h3 class="text-base md:text-lg font-black text-[#5900cc] tracking-tight">100% online</h3>
                    </div>

                    <div class="flex flex-col items-center text-center space-y-4 group">
                        <div
                            class="w-20 h-32 flex items-center justify-center transition-transform duration-300 group-hover:scale-105">
                            <svg class="w-full h-full text-purple-700" viewBox="0 0 100 150" fill="none"
                                xmlns="http://www.w3.org/2000/svg">
                                <rect x="5" y="5" width="90" height="140" rx="10" stroke="url(#gradient-cyan-purple)"
                                    stroke-width="4" />
                                <path
                                    d="M30,75 C30,65 45,65 50,75 C55,65 70,65 70,75 C70,85 55,85 50,75 C45,85 30,85 30,75 Z"
                                    stroke="url(#gradient-cyan-purple)" stroke-width="4" stroke-linejoin="round" />
                                <line x1="40" y1="130" x2="60" y2="130" stroke="url(#gradient-cyan-purple)"
                                    stroke-width="4" stroke-linecap="round" />
                            </svg>
                        </div>
                        <h3 class="text-base md:text-lg font-black text-[#5900cc] tracking-tight">Clases ilimitadas</h3>
                    </div>

                    <div class="flex flex-col items-center text-center space-y-4 group">
                        <div
                            class="w-20 h-32 flex items-center justify-center transition-transform duration-300 group-hover:scale-105">
                            <svg class="w-full h-full text-purple-700" viewBox="0 0 100 150" fill="none"
                                xmlns="http://www.w3.org/2000/svg">
                                <rect x="5" y="5" width="90" height="140" rx="10" stroke="url(#gradient-cyan-purple)"
                                    stroke-width="4" />
                                <path d="M40,45 C45,65 35,95 45,105 M60,45 C55,65 65,95 55,105"
                                    stroke="url(#gradient-cyan-purple)" stroke-width="4" stroke-linecap="round" />
                                <line x1="40" y1="130" x2="60" y2="130" stroke="url(#gradient-cyan-purple)"
                                    stroke-width="4" stroke-linecap="round" />
                            </svg>
                        </div>
                        <h3 class="text-base md:text-lg font-black text-[#5900cc] tracking-tight">Múltiples estilos</h3>
                    </div>

                    <div class="flex flex-col items-center text-center space-y-4 group">
                        <div
                            class="w-20 h-32 flex items-center justify-center transition-transform duration-300 group-hover:scale-105">
                            <svg class="w-full h-full text-purple-700" viewBox="0 0 100 150" fill="none"
                                xmlns="http://www.w3.org/2000/svg">
                                <rect x="5" y="5" width="90" height="140" rx="10" stroke="url(#gradient-cyan-purple)"
                                    stroke-width="4" />
                                <path d="M50,45 L54,55 L65,55 L56,62 L59,73 L50,66 L41,73 L44,62 L35,55 L46,55 Z"
                                    stroke="url(#gradient-cyan-purple)" stroke-width="3" stroke-linejoin="round" />
                                <path d="M35,105 L50,85 L65,105" stroke="url(#gradient-cyan-purple)" stroke-width="4"
                                    stroke-linecap="round" />
                                <line x1="40" y1="130" x2="60" y2="130" stroke="url(#gradient-cyan-purple)"
                                    stroke-width="4" stroke-linecap="round" />
                            </svg>
                        </div>
                        <h3 class="text-base md:text-lg font-black text-[#5900cc] tracking-tight">Todos los niveles</h3>
                    </div>
                </div>
            </div>

            <svg width="0" height="0" class="absolute">
                <defs>
                    <linearGradient id="gradient-cyan-purple" x1="0%" y1="0%" x2="100%" y2="100%">
                        <stop offset="0%" stop-color="#5900cc" />
                        <stop offset="50%" stop-color="#00c478" />
                        <stop offset="100%" stop-color="#00df89" />
                    </linearGradient>
                </defs>
            </svg>
        </section>

        <!-- SECCIÓN: REPRODUCTOR REAL AVANZADO -->
        <section class="w-full bg-[#141414] text-white py-20 border-t border-gray-800">
            <div class="w-full lg:w-[80%] mx-auto px-4 lg:px-0 flex flex-col items-center space-y-12">

                <!-- Títulos Principales de la sección -->
                <div class="text-center max-w-4xl space-y-4">
                    <h2 class="text-3xl md:text-4xl font-black text-[#00df89] tracking-tight leading-tight">
                        Clases de baile online como nunca antes has visto
                    </h2>
                    <p class="text-gray-300 text-sm md:text-base font-medium max-w-2xl mx-auto leading-relaxed">
                        No se te escapará nada con nuestro reproductor avanzado. La experiencia de aprender a bailar
                        desde todos
                        los ángulos y contigo como protagonista marcará la diferencia.
                    </p>
                </div>

                <!-- REPRODUCTOR INTERACTIVO CORREGIDO (Video de prueba con Embedding habilitado) -->
                <div
                    class="w-full max-w-4xl aspect-video bg-black rounded-lg shadow-2xl border border-gray-800 overflow-hidden relative">
                    <iframe class="w-full h-full absolute inset-0"
                        src="https://www.youtube.com/embed/dQw4w9WgXcQ?rel=0&modestbranding=1"
                        title="Duality Tribal - Demostración del Reproductor Avanzado" frameborder="0"
                        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
                        allowfullscreen></iframe>
                </div>

                <!-- Grilla de Características Técnicas -->
                <div class="w-full max-w-4xl grid grid-cols-1 md:grid-cols-3 gap-x-12 gap-y-10 pt-6">

                    <!-- 1. Espejo -->
                    <div class="space-y-2">
                        <div class="flex items-center space-x-2 text-[#00df89]">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2.5"
                                viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M9 4.5v15m6-15v15m-12-3h18" />
                            </svg>
                            <h3 class="text-base font-black tracking-tight">Espejo</h3>
                        </div>
                        <p class="text-gray-400 text-[13px] font-medium leading-relaxed">
                            Con esta función irás igual que tu profesor y será mucho más sencillo entender las
                            direcciones de la
                            clase.
                        </p>
                    </div>

                    <!-- 2. Cambia la vista -->
                    <div class="space-y-2">
                        <div class="flex items-center space-x-2 text-[#00df89]">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2.5"
                                viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round"
                                    d="M15 10l4.553-2.276A1 1 0 0121 8.618v6.764a1 1 0 01-1.447.894L15 14M5 18h8a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v8a2 2 0 002 2z" />
                            </svg>
                            <h3 class="text-base font-black tracking-tight">Cambia la vista</h3>
                        </div>
                        <p class="text-gray-400 text-[13px] font-medium leading-relaxed">
                            Podrás ver a tu profesor desde dos perspectivas: frontal y trasera. ¡La experiencia será
                            como estar
                            dentro de clase y ver todos los ángulos!
                        </p>
                    </div>

                    <!-- 3. Activa tu cámara -->
                    <div class="space-y-2">
                        <div class="flex items-center space-x-2 text-[#00df89]">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2.5"
                                viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round"
                                    d="M6.827 6.175A2.31 2.31 0 015.186 7.23c-.38.054-.757.112-1.134.175C2.999 7.58 2.25 8.507 2.25 9.574V18a2.25 2.25 0 002.25 2.25h15A2.25 2.25 0 0021.75 18V9.574c0-1.067-.75-1.994-1.802-2.169a47.865 47.865 0 00-1.134-.175 2.31 2.31 0 01-1.64-1.055l-.822-1.316a2.192 2.192 0 00-1.736-1.039 48.774 48.774 0 00-5.232 0 2.192 2.192 0 00-1.736 1.039l-.821 1.316z" />
                                <circle cx="12" cy="13" r="3" />
                            </svg>
                            <h3 class="text-base font-black tracking-tight">Activa tu cámara</h3>
                        </div>
                        <p class="text-gray-400 text-[13px] font-medium leading-relaxed">
                            La mejor manera de saber si lo estás haciendo bien es ponerte al lado de tu profesor y con
                            tu cámara
                            web es posible: actívala y bailad juntos.
                        </p>
                    </div>

                    <!-- 4. Bucle -->
                    <div class="space-y-2">
                        <div class="flex items-center space-x-2 text-[#00df89]">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2.5"
                                viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round"
                                    d="M16.023 9.348h4.992v-.001M2.985 19.644v-4.992m0 0h4.992m-4.993 0l3.181 3.183a8.25 8.25 0 0013.803-3.7M4.031 9.865a8.25 8.25 0 0113.803-3.7l3.181 3.182m0-4.991v4.99" />
                            </svg>
                            <h3 class="text-base font-black tracking-tight">Bucle</h3>
                        </div>
                        <p class="text-gray-400 text-[13px] font-medium leading-relaxed">
                            Repite una y otra vez la parte de la clase que necesites. Gracias a esta herramienta no se
                            te
                            escapará ni un movimiento.
                        </p>
                    </div>

                    <!-- 5. Elige capítulo -->
                    <div class="space-y-2">
                        <div class="flex items-center space-x-2 text-[#00df89]">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2.5"
                                viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round"
                                    d="M3.75 5.25h16.5m-16.5 4.5h16.5m-16.5 4.5h16.5m-16.5 4.5h16.5" />
                            </svg>
                            <h3 class="text-base font-black tracking-tight">Elige capítulo</h3>
                        </div>
                        <p class="text-gray-400 text-[13px] font-medium leading-relaxed">
                            Encontrarás las clases divididas por capítulos para que no pierdas tiempo buscando la parte
                            que más
                            te interesa.
                        </p>
                    </div>

                    <!-- 6. Controla la velocidad -->
                    <div class="space-y-2">
                        <div class="flex items-center space-x-2 text-[#00df89]">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2.5"
                                viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round"
                                    d="M10.5 6a7.5 7.5 0 107.5 7.5h-7.5V6z" />
                                <path stroke-linecap="round" stroke-linejoin="round"
                                    d="M13.5 10.5H21A7.5 7.5 0 0013.5 3v7.5z" />
                            </svg>
                            <h3 class="text-base font-black tracking-tight">Controla la velocidad</h3>
                        </div>
                        <p class="text-gray-400 text-[13px] font-medium leading-relaxed">
                            Sube o baja la velocidad en cualquier momento y combínalo con el bucle para adaptar la clase
                            a tus
                            necesidades.
                        </p>
                    </div>

                </div>
            </div>
        </section>

        <!-- SECCIÓN: ESTILOS DE BAILE (Diseño Llamativo y Premium) -->
        <section
            class="w-full bg-gradient-to-br from-[#1a0033] via-[#110022] to-[#05000a] py-24 border-t border-purple-900/50">
            <div class="w-full lg:w-[80%] mx-auto px-4 lg:px-0 space-y-16">

                <!-- Encabezado de la sección -->
                <div class="max-w-2xl space-y-4">
                    <h2 class="text-4xl md:text-5xl font-black text-white tracking-tighter leading-none">
                        Los estilos de baile disponibles en nuestra escuela
                    </h2>
                    <p class="text-gray-400 text-lg font-medium leading-relaxed">
                        Diferentes estilos forman a un bailarín completo. Con clases de coreografías, consejos y
                        entrenamientos.
                        Somos únicos ofreciendo los estilos de moda.
                    </p>
                </div>

                <!-- Grilla de estilos (4x2) -->
                <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
                    <div v-for="estilo in ['Commercial', 'Zumba', 'Contemporáneo', 'Reggaeton', 'Danza Clásica', 'Sexy Style', 'Dancehall', 'Hip hop']"
                        :key="estilo"
                        class="relative h-48 bg-gray-900/50 border border-gray-800 rounded-2xl overflow-hidden group cursor-pointer hover:border-[#00df89] transition-all duration-500 shadow-xl hover:shadow-[0_0_30px_rgba(0,223,137,0.15)]">

                        <!-- Capa de imagen (simulada) -->
                        <div class="absolute inset-0 bg-gradient-to-t from-black/80 to-transparent z-10"></div>
                        <div
                            class="absolute inset-0 bg-gray-800 group-hover:scale-110 transition-transform duration-700">
                        </div>

                        <!-- Título del estilo -->
                        <div class="absolute bottom-5 left-5 z-20">
                            <span class="text-white font-black text-xl tracking-tight block">{{ estilo }}</span>
                            <span class="text-[#00df89] text-xs font-bold uppercase tracking-widest mt-1 block">Ver
                                clase</span>
                        </div>
                    </div>
                </div>

                <!-- Botón de acción (Más grande y llamativo) -->
                <div class="flex justify-center pt-6">
                    <button
                        class="bg-[#00df89] hover:bg-[#00ff9d] text-black font-black px-12 py-5 text-base tracking-widest uppercase transition-all duration-300 transform hover:scale-105 shadow-[0_0_25px_rgba(0,223,137,0.5)] rounded-full hover:shadow-[0_0_40px_rgba(0,223,137,0.7)]">
                        Ver todos los estilos de baile
                    </button>
                </div>
            </div>
        </section>

        <!-- SECCIÓN: APRENDE CON LOS MEJORES -->
        <section class="w-full bg-white py-20">
            <div class="w-full lg:w-[80%] mx-auto px-4 lg:px-0 space-y-12">

                <!-- Encabezado -->
                <div class="max-w-xl">
                    <h2 class="text-4xl md:text-5xl font-black text-[#5900cc] tracking-tighter mb-4">
                        Aprende con los mejores
                    </h2>
                    <p class="text-gray-600 text-lg font-medium">
                        Clases estructuradas y diseñadas exclusivamente para ti. Especialistas en la materia que te
                        enseñarán lo mejor de cada baile.
                    </p>
                </div>

                <!-- Grilla de instructores -->
                <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
                    <!-- AGREGADO EL @CLICK AQUÍ -->
                    <div v-for="instructor in instructors" :key="instructor.name"
                        @click="openInstructorModal(instructor)"
                        class="cursor-pointer group rounded-2xl overflow-hidden shadow-lg transition-transform duration-300 hover:-translate-y-2">
                        <!-- Área de imagen -->
                        <div class="h-64 bg-gray-200 relative">
                            <img :src="instructor.image" :alt="instructor.name" class="w-full h-full object-cover">
                            <div class="absolute bottom-4 left-4 z-10">
                                <h3 class="text-white font-black text-xl leading-tight">{{ instructor.name }}</h3>
                            </div>
                        </div>
                        <!-- Área de especialidad -->
                        <div class="bg-black text-white p-4">
                            <p class="font-bold tracking-wide">{{ instructor.style }}</p>
                        </div>
                    </div>
                </div>

                <!-- MODAL (Solo se renderiza si hay un instructor seleccionado) -->
                <div v-if="isModalOpen && selectedInstructor"
                    class="fixed inset-0 z-50 flex items-center justify-center p-4">
                    <div class="absolute inset-0 bg-black/80 backdrop-blur-sm" @click="isModalOpen = false"></div>

                    <div
                        class="relative bg-white text-black w-full max-w-sm rounded-3xl p-8 shadow-2xl animate-in fade-in zoom-in duration-300">
                        <button @click="isModalOpen = false"
                            class="absolute top-4 right-4 text-gray-400 hover:text-black text-xl">✕</button>

                        <div class="text-center">
                            <div class="w-24 h-24 bg-gray-200 rounded-full mx-auto mb-4 overflow-hidden">
                                <img :src="selectedInstructor.image" :alt="selectedInstructor.name"
                                    class="w-full h-full object-cover">
                            </div>
                            <h3 class="text-2xl font-black text-purple-900">{{ selectedInstructor.name }}</h3>
                            <p class="text-gray-500 font-bold mb-6">{{ selectedInstructor.style }}</p>

                            <div class="space-y-3">
                                <a :href="'https://instagram.com/' + selectedInstructor.ig" target="_blank"
                                    class="block w-full py-3 bg-gray-100 hover:bg-purple-100 rounded-xl font-bold transition">Instagram</a>
                                <a :href="'https://twitter.com/' + selectedInstructor.x" target="_blank"
                                    class="block w-full py-3 bg-gray-100 hover:bg-purple-100 rounded-xl font-bold transition">X
                                    (Twitter)</a>
                                <a :href="'https://tiktok.com/@' + selectedInstructor.tt" target="_blank"
                                    class="block w-full py-3 bg-gray-100 hover:bg-purple-100 rounded-xl font-bold transition">TikTok</a>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- SECCIÓN: PLANES Y SEGURIDAD -->
        <section class="w-full py-24 bg-gradient-to-b from-[#110022] to-[#05000a] text-white">
            <div class="w-[90%] lg:w-[80%] mx-auto px-4">

                <!-- Grid de 3 tarjetas -->
                <div class="grid md:grid-cols-3 gap-8 items-start mb-24">

                    <!-- TARJETA 1 -->
                    <div
                        class="bg-white text-black rounded-3xl p-8 shadow-2xl flex flex-col h-full min-h-[550px] transition-all duration-300 hover:-translate-y-4 hover:shadow-[0_20px_50px_rgba(255,255,255,0.1)]">
                        <div class="text-center mb-8">
                            <span class="text-xs uppercase tracking-[0.2em] text-gray-400 font-bold">Básico</span>
                            <div class="text-5xl font-black mt-4">$13.99</div>
                            <span class="text-sm text-gray-500 font-medium">mensual</span>
                        </div>
                        <ul class="space-y-6 mb-12 flex-grow text-left">
                            <li class="flex items-start gap-3 text-sm"> <span class="text-green-500 font-bold">✓</span>
                                Todos
                                los estilos y niveles</li>
                            <li class="flex items-start gap-3 text-sm"> <span class="text-green-500 font-bold">✓</span>
                                Cursos
                                ilimitados</li>
                        </ul>
                        <button
                            class="w-full py-4 border-2 border-black rounded-xl font-bold hover:bg-black hover:text-white transition-all">Seleccionar</button>
                    </div>

                    <!-- TARJETA 2 (DESTACADA) -->
                    <div
                        class="bg-white text-black rounded-3xl p-8 shadow-2xl flex flex-col h-full min-h-[550px] border-2 border-purple-500 relative transition-all duration-300 hover:-translate-y-4 hover:shadow-[0_20px_50px_rgba(168,85,247,0.3)]">
                        <div
                            class="absolute -top-3 left-1/2 -translate-x-1/2 bg-purple-600 text-white px-4 py-1 rounded-full text-[10px] font-bold uppercase tracking-widest">
                            Recomendado</div>
                        <div class="text-center mb-8">
                            <span class="text-xs uppercase tracking-[0.2em] text-purple-600 font-bold">Estándar</span>
                            <div class="text-5xl font-black mt-4">$19.99</div>
                            <span class="text-sm text-gray-500 font-medium">mensual</span>
                        </div>
                        <ul class="space-y-6 mb-12 flex-grow text-left">
                            <li class="flex items-start gap-3 text-sm"> <span class="text-green-500 font-bold">✓</span>
                                Todos
                                los estilos y niveles</li>
                            <li class="flex items-start gap-3 text-sm"> <span class="text-green-500 font-bold">✓</span>
                                Cursos
                                ilimitados</li>
                            <li class="flex items-start gap-3 text-sm"> <span class="text-green-500 font-bold">✓</span>
                                Comunidad exclusiva</li>
                        </ul>
                        <button
                            class="w-full py-4 bg-purple-600 text-white rounded-xl font-bold hover:bg-purple-700 transition-all">Seleccionar</button>
                    </div>

                    <!-- TARJETA 3 -->
                    <div
                        class="bg-white text-black rounded-3xl p-8 shadow-2xl flex flex-col h-full min-h-[550px] transition-all duration-300 hover:-translate-y-4 hover:shadow-[0_20px_50px_rgba(255,255,255,0.1)]">
                        <div class="text-center mb-8">
                            <span class="text-xs uppercase tracking-[0.2em] text-gray-400 font-bold">Pro</span>
                            <div class="text-5xl font-black mt-4">$29.99</div>
                            <span class="text-sm text-gray-500 font-medium">mensual</span>
                        </div>
                        <ul class="space-y-6 mb-12 flex-grow text-left">
                            <li class="flex items-start gap-3 text-sm"> <span class="text-green-500 font-bold">✓</span>
                                Todos
                                los estilos y niveles</li>
                            <li class="flex items-start gap-3 text-sm"> <span class="text-green-500 font-bold">✓</span>
                                Cursos
                                ilimitados</li>
                            <li class="flex items-start gap-3 text-sm"> <span class="text-green-500 font-bold">✓</span>
                                Comunidad exclusiva</li>
                            <li class="flex items-start gap-3 text-sm"> <span class="text-green-500 font-bold">✓</span>
                                Soporte
                                prioritario</li>
                        </ul>
                        <button
                            class="w-full py-4 border-2 border-black rounded-xl font-bold hover:bg-black hover:text-white transition-all">Seleccionar</button>
                    </div>
                </div>

                <!-- SECCIÓN: SITIO SEGURO (Basado en image_2aa840.png) -->
                <div
                    class="flex flex-col md:flex-row items-center justify-center gap-8 p-10 border border-white/10 rounded-3xl bg-white/5 backdrop-blur-sm">
                    <div class="flex items-center gap-6">
                        <h3 class="text-2xl font-bold">Sitio seguro</h3>
                        <div
                            class="w-16 h-16 bg-gradient-to-br from-blue-400 to-blue-600 rounded-lg flex items-center justify-center text-white font-bold shadow-lg">
                            Stripe</div>
                    </div>
                    <p class="text-sm text-gray-300 max-w-md">
                        Puedes comprar con total tranquilidad en nuestro sitio web, ya que contamos con medidas de
                        seguridad
                        para proteger tus datos personales y bancarios.
                    </p>
                </div>
                <p class="text-center text-xs text-gray-500 mt-6 italic">
                    *La garantía de devolución no aplica a pagos realizados mediante tu operador móvil (carrier
                    billing).
                </p>
            </div>
        </section>

        <!-- SECCIÓN: PREGUNTAS FRECUENTES (Duality Tribal) -->
        <section class="w-full py-20 bg-[#110022] text-white px-6">
            <div class="max-w-4xl mx-auto space-y-12">

                <!-- ¿Qué es Duality Tribal? -->
                <div>
                    <h2 class="text-3xl font-bold text-[#00df89] mb-4">¿Qué es Duality Tribal?</h2>
                    <p class="text-gray-300 leading-relaxed">
                        Duality Tribal es una academia de baile online que te permite aprender a bailar desde tu propia
                        casa.
                        Sí, has leído bien, ofrecemos clases de baile profesionales que podrás practicar desde el lugar
                        que tú
                        quieras y en el horario que más te convenga. ¡No ponemos límites para que puedas disfrutar
                        bailando en
                        cualquier momento!
                    </p>
                </div>

                <!-- ¿Cómo funciona nuestra escuela de baile online? -->
                <div>
                    <h2 class="text-3xl font-bold text-[#00df89] mb-4">¿Cómo funciona nuestra escuela de baile online?
                    </h2>
                    <p class="text-gray-300 leading-relaxed">
                        Al registrarte en nuestra plataforma, tendrás a tu disposición TODAS las clases de baile online
                        de
                        Duality Tribal. Esto significa que podrás escoger entre una gran variedad de estilos de baile y
                        clases
                        de distintos niveles. Encontrarás las coreografías que más se adaptan a tu estilo y podrás
                        seguirlas
                        gracias a nuestro reproductor de vídeo avanzado ¡Creado especialmente para bailarines que
                        quieren bailar
                        online como tú!
                    </p>
                </div>

                <!-- ¿Qué nos diferencia de una escuela de baile tradicional? -->
                <div>
                    <h2 class="text-3xl font-bold text-[#00df89] mb-4">¿Qué nos diferencia de una escuela de baile
                        tradicional?
                    </h2>
                    <p class="text-gray-300 mb-4">Las principales ventajas de las clases de baile online de Duality
                        Tribal son
                        las siguientes:</p>
                    <ul class="space-y-3 text-gray-300 list-disc pl-5">
                        <li><strong>Sin límites:</strong> Haz tantas clases como quieras y repítelas las veces que
                            necesites.
                        </li>
                        <li><strong>Múltiples estilos:</strong> Todos los estilos están incluidos en la cuota, lo que
                            significa
                            que podrás bailar todos tus estilos favoritos y experimentar probando aquellos que todavía
                            no
                            conoces.</li>
                        <li><strong>Clases de baile 100% online:</strong> Cuando quieras y dónde quieras. Tú escoges el
                            horario
                            que mejor te va para bailar y qué días de la semana quieres practicar.</li>
                        <li><strong>Marca tu evolución:</strong> Tú escoges el grado de dificultad de las clases según
                            tu
                            experiencia, lo que te permitirá mejorar más rápido.</li>
                        <li><strong>Tarifa reducida:</strong> Queremos que disfrutes al máximo de la plataforma, nuestro
                            objetivo es que bailes y no pares de bailar y tenemos una tarifa que se adapta a todos los
                            bolsillos.</li>
                        <li><strong>Profesores especializados:</strong> Profesores de referencia en su estilo y de
                            repercusión
                            internacional, para que aprendas a bailar con los mejores.</li>
                    </ul>
                </div>

                <!-- ¿Cuál es el nivel de dificultad de las clases? -->
                <div>
                    <h2 class="text-3xl font-bold text-[#00df89] mb-4">¿Cuál es el nivel de dificultad de las clases?
                    </h2>
                    <p class="text-gray-300 leading-relaxed">
                        Los niveles que puedes encontrar en nuestra escuela de baile online son: Básico, Intermedio y
                        Avanzado,
                        lo que significa que nuestras clases de baile online siempre estarán adaptadas a tu ritmo y
                        evolución.
                        Tanto si eres principiante, como un bailarín o bailarina más experimentado, tenemos clases
                        perfectas
                        para que sigas mejorando y te diviertas bailando.
                    </p>
                </div>

                <!-- ¿Por qué las clases de baile de Duality Tribal son únicas? -->
                <div>
                    <h2 class="text-3xl font-bold text-[#00df89] mb-4">¿Por qué las clases de baile de Duality Tribal
                        son
                        únicas?</h2>
                    <p class="text-gray-300 leading-relaxed">
                        Aprender a bailar online con Duality Tribal es una experiencia única, en parte, gracias al
                        reproductor
                        avanzado de nuestra plataforma. Modo espejo, posibilidad de cambiar la vista, modo bucle,
                        control de
                        velocidad... Una tecnología avanzada que hace que aprender a bailar sea mucho más fácil. Incluso
                        puedes
                        activar tu cámara para que puedas comparar tus movimientos con los del profesor o profesora y
                        sumergirte
                        en la clase.
                    </p>
                </div>

                <!-- BOTÓN DE LLAMADA A LA ACCIÓN -->
                <div class="flex justify-center mt-16">
                    <a href="#"
                        class="bg-[#00df89] text-[#110022] font-black px-12 py-5 rounded-full text-lg uppercase tracking-wider shadow-[0_0_20px_rgba(0,223,137,0.3)] hover:scale-105 transition-transform duration-300">
                        Empezar a bailar
                    </a>
                </div>

            </div>
        </section>

        <Footer></Footer>

    </div>
</template>
