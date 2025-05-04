<template>
    <div>
        <div v-if="isMenuOpen"  class="fixed inset-0 bg-black/50 z-10" @click="closeMenu" />
        <button
        class="mr-4 md:hidden rounded text-2xl hover:bg-secondary dark:hover:bg-secondary-dark"
        @click="toggleMenu"
        >
            <i class="fa-solid fa-bars"></i>
        </button>
        <div 
        class="fixed top-0 right-0 h-full w-64 bg-neutral-100 dark:bg-neutral-900 transform transition-transform duration-300 ease-in-out z-20"
        :class="{ 'translate-x-0': isMenuOpen, 'translate-x-full': !isMenuOpen }"
        >
            <div class="p-4">
                <h2 class="text-xl font-bold mb-4">메뉴</h2>
                <ul>
                    <li class="py-2"><nuxt-link to="/RecentChanges" @click="closeMenu">최근 변경</nuxt-link></li>
                    <li class="py-2"><a href="#" @click="closeMenu">최근 토론</a></li>
                    <li class="py-2"><a href="#" @click="closeMenu">랜덤</a></li>
                    <li class="py-2"><a href="#" @click="closeMenu">도구</a></li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            isMenuOpen: false
        };
    },
    methods: {
        toggleMenu() {
            this.isMenuOpen = !this.isMenuOpen;
        },
        closeMenu() {
            this.isMenuOpen = false;
        }
    }
}
</script>