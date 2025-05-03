<template>
    <main class="flex justify-center">
        <div class="flex flex-col md:flex-row md:gap-4 md:m-4 items-start w-full">
            <div class="bg-neutral-100 dark:bg-neutral-900 md:rounded-xl w-full md:w-8/9 min-h-[100vh] p-5 md:shadow-xl">
                <div class="flex flex-col md:flex-row md:items-center mb-3 justify-between">
                    <div class="flex flex-col">
                        <DocTitle />
                        <template v-if="$store.state.page.viewName === 'wiki' && $store.state.page.data.date">
                            <p class="text-sm">최근 변경:<local-date :date="$store.state.page.data.date" /></p>
                        </template>
                    </div>
                    <h1>content tools</h1>
                </div>
                <article class="content">
                    <slot />
                    <div v-if="$store.state.page.viewName === 'license'">
                        <h2>Modern license</h2>
                        <pre>{{ License }}</pre>
                    </div>
                </article>
            </div>
            <div class="bg-neutral-100 dark:bg-neutral-900 md:rounded-xl w-full md:w-2/9 p-4 md:shadow-xl max-md:border-t">
                <a href="/RecentChanges" class="text-xl font-bold mb-2">
                    <i class="fa-solid fa-clock"></i>
                    최근 변경
                </a>
                <template v-if="recent.length === 0">
                    <p>edit document!</p>
                </template>
                <template v-else>
                    <ul class="">
                        <template v-for="(r,i) in recent" :key="i">
                            <li v-if="i < limit">
                                <nuxt-link class="flex justify-between p-1 hover:bg-neutral-400 rounded-xl" :class="[{ 'line-through': r.status === 'delete' }]" :key="r.document" :to="doc_action_link(r.document, 'w')">
                                    <span class="truncate block group-hover:whitespace-normal group-hover:overflow-visible">{{ r.document }}</span>
                                    <local-date :date="r.date" :format="getDateType(r.date)" />
                                </nuxt-link>
                            </li>
                        </template>
                    </ul>
                </template>
            </div>
        </div>
    </main>
</template>

<script>
import DocTitle from "./title.vue";
import Common from "~/mixins/common";
import RecentCardMixin from '~/mixins/recentCard';
import LocalDate from "~/components/localDate";
import License from "raw-loader!./LICENSE";

export default {
    mixins: [Common, RecentCardMixin],
    components: {
        DocTitle,
        LocalDate
    },
    props: {
        limit: {
            type: Number,
            default: 10
        }
    },
    methods: {
        getDateType(date) {
            const now = Math.floor((new Date()).getTime() / 1000);
            return (now - 86400) > date ? 'Y/m/d' : 'H:i:s';
        }
    },
    data() {
        return {
            License
        };
    }
}
</script>

<style>
.recent-text {
  display: inline-block;
  max-width: 100%;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  vertical-align: top;
  transition: all 0.3s ease;
}

.recent-item:hover .recent-text {
  white-space: normal;
  overflow: visible;
  text-overflow: unset;
}

</style>