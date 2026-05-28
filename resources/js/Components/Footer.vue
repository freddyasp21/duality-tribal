<!-- resources/js/Components/Footer.vue -->
<template>
    <footer class="w-full py-10 bg-black text-white px-6">
        <div
            class="max-w-6xl mx-auto flex flex-col md:flex-row items-center justify-center gap-6 text-center md:text-left">

            <!-- Logo -->
            <span class="text-2xl font-black">DT</span>

            <!-- Divisor vertical (solo escritorio) -->
            <div class="hidden md:block w-[1px] h-8 bg-gray-700"></div>

            <!-- Copyright y Links -->
            <div class="flex flex-col md:flex-row items-center gap-4 text-sm text-gray-400">
                <p>© 2026 Duality Tribal. All Rights Reserved.</p>

                <nav class="flex flex-wrap justify-center gap-4">
                    <a href="#" class="hover:text-white transition-colors">Política de privacidad</a>
                    <span class="hidden md:inline text-gray-600">|</span>
                    <a href="#" class="hover:text-white transition-colors">Términos y condiciones</a>
                    <span class="hidden md:inline text-gray-600">|</span>
                    <a href="#" class="hover:text-white transition-colors">Soporte</a>
                </nav>
            </div>
        </div>
    </footer>
</template>
