<template>
    <div>
        <button 
                @click="toggleMenu" 
                class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600 focus:outline-none"
            >
                {{ isMenuOpen ? '메뉴 닫기' : '메뉴 열기' }}
            </button>

        <div 
        class="fixed top-0 right-0 h-full w-64 bg-white shadow-lg transform transition-transform duration-300 ease-in-out z-20"
        :class="{ 'translate-x-0': isMenuOpen, 'translate-x-full': !isMenuOpen }"
        >
            <div class="p-4">
                <h2 class="text-xl font-bold mb-4">메뉴</h2>
                <ul>
                    <li class="py-2"><a href="#" @click="closeMenu" class="text-blue-500 hover:underline">홈</a></li>
                    <li class="py-2"><a href="#" @click="closeMenu" class="text-blue-500 hover:underline">프로필</a></li>
                    <li class="py-2"><a href="#" @click="closeMenu" class="text-blue-500 hover:underline">설정</a></li>
                    <li class="py-2"><a href="#" @click="closeMenu" class="text-blue-500 hover:underline">로그아웃</a></li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data: {
        isMenuOpen: false
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