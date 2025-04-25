<template>
    <form class="search-bar" @submit.prevent>
        <input accesskey="f" type="search" name="q" class="rounded-l-xl p-2" placeholder="여기에 검색..." autocomplete="off" v-on:input="searchText = $event.target.value" v-model="searchTextModel" @blur="blur" @focus="focus" @input="inputChange" @keydown.enter="keyEnter" @keydown.tab="keyEnter" @keydown.up="keyUp" @keydown.down="keyDown">
        <div v-if="show" class="v-autocomplete-list">
            <div class="v-autocomplete-list-item" v-for="(item, i) in internalItems" @click="onClickItem(item)" v-bind:key="i" :class="{'v-autocomplete-item-active': i === cursor}" @mouseover="cursor = i">
                <div>{{ item }}</div>
            </div>
        </div>
        <button class="px-1"><i class="fa-solid fa-magnifying-glass"></i></button>
        <button class="px-2 rounded-r-xl"><i class="fa-solid fa-chevron-right"></i></button>
    </form>
</template>

<style>
.search-bar > * {
    background-color: var(--color-neutral-200);
    color: black;
    height: 36px;
}

@media (max-width: 48rem) {
    .search-bar {
        display: flex;
        position: absolute;
        top: 52px;
        left: 0;
        width: 100%;
        z-index: 10;
    }
    .search-bar input {
        height: 37px;
        flex-grow: 1;
        border-radius: 0;
    }
    .search-bar button {
        height: 37px;
        border-radius: 0;
    }
    .search-bar button:last-child {
        border-radius: 0;
    }
}
</style>

<script>
import AutocompleteMixin from '~/mixins/autocomplete';
import Common from '~/mixins/common';

export default {
    mixins: [AutocompleteMixin],
    methods: {
        onClickSearch() {
            if (!this.searchText) return;
            this.$router.push('/Search?q=' + encodeURIComponent(this.searchText));
        },
        onClickMove() {
            if (!this.searchText) return;
            this.$router.push(Common.methods.doc_action_link(this.searchText, 'w'));
        }
    },
    watch: {
        $route() {
            if (this.$store.state.localConfig["modern.reset_search_on_move"] !== false) this.reset();
        }
    }
}
</script>