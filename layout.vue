<template>
    <div class="bg-white dark:bg-black text-black dark:text-white">
        <Header />
        <Banner />
        <Main>
            <nuxt />
        </Main>
        <Footer />
    </div>
</template>

<style>
@import "./css/output.css";
@import "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.7.2/css/all.min.css";
</style>

<script>
import Header from "./layouts/header.vue";
import Banner from "./layouts/banner.vue";
import Main from "./layouts/main.vue";
import Footer from "./layouts/footer.vue";

import common from "~/mixins/common";

export default {
    mixins: [common],
    components: {
        Header,
        Banner,
        Main,
        Footer
    }
}
</script>