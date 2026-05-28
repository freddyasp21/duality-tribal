<script setup>
import { ref } from 'vue';
import { Link } from '@inertiajs/vue3';

const isOpen = ref(false);
</script>

<template>
    <nav class="bg-white text-black sticky top-0 z-50 border-b border-gray-200" aria-label="Navegación principal">
        <div class="w-full lg:w-[80%] mx-auto px-4 lg:px-0">
            <div class="flex items-center justify-between h-16">

                <div class="flex items-center space-x-8 h-16">
                    <Link :href="route('home')"
                        class="text-lg font-black tracking-tighter text-gray-900 uppercase flex items-center hover:opacity-80">
                        <span class="bg-purple-900 text-white px-1.5 py-0.5 rounded-sm mr-2 text-xs font-bold">DT</span>
                        <span class="font-black text-purple-900 tracking-tight">Duality</span>
                        <span class="font-medium text-gray-900 tracking-tight ml-1">Tribal</span>
                    </Link>

                    <ul
                        class="hidden md:flex space-x-6 text-[15px] font-bold text-gray-700 tracking-tight h-16 items-center">
                        <li><a href="#" class="hover:text-purple-600 transition-colors">Descubre</a></li>
                        <li><a href="#" class="hover:text-purple-600 transition-colors">Cursos</a></li>
                        <li><a href="#" class="hover:text-purple-600 transition-colors">Programas</a></li>
                    </ul>
                </div>

                <button @click="isOpen = !isOpen" class="md:hidden p-2 text-gray-700 focus:outline-none">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path v-if="!isOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="M4 6h16M4 12h16M4 18h16" />
                        <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="M6 18L18 6M6 6l12 12" />
                    </svg>
                </button>

                <div class="hidden md:flex items-center h-16">
                    <div class="relative mr-6">
                        <input type="text" placeholder="Buscar..."
                            class="bg-gray-100 text-gray-900 pl-3 pr-9 py-1.5 text-xs rounded-full border border-transparent focus:border-gray-200 focus:bg-white focus:outline-none w-40 transition-all duration-300" />
                    </div>
                    <Link v-if="$page.props.auth.user" :href="route('dashboard')"
                        class="bg-purple-700 text-white h-16 px-6 flex items-center font-bold text-sm hover:bg-purple-600">
                        Mi Panel</Link>
                    <template v-else>
                        <Link :href="route('login')"
                            class="bg-[#00df89] text-black h-16 px-6 flex items-center font-bold text-xs hover:bg-[#00c478] transition-colors">
                            Inicia sesión</Link>
                        <Link :href="route('register')"
                            class="bg-[#5900cc] text-white h-16 px-6 flex items-center font-bold text-xs hover:bg-[#4a00b0] transition-colors">
                            Regístrate</Link>
                    </template>
                </div>
            </div>
        </div>

        <div v-if="isOpen" class="md:hidden bg-white border-b border-gray-200 p-4 space-y-3">
            <a href="#" class="block text-gray-700 font-bold hover:text-purple-600">Descubre</a>
            <a href="#" class="block text-gray-700 font-bold hover:text-purple-600">Cursos</a>
            <a href="#" class="block text-gray-700 font-bold hover:text-purple-600">Programas</a>
            <hr />
            <div class="flex flex-col gap-2 pt-2">
                <Link :href="route('login')" class="text-center bg-[#00df89] py-2 font-bold text-sm">Inicia sesión
                </Link>
                <Link :href="route('register')" class="text-center bg-[#5900cc] text-white py-2 font-bold text-sm">
                    Regístrate
                </Link>
            </div>
        </div>
    </nav>
</template>
