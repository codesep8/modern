<template>
    <h1 class="text-3xl font-bold hover:underline decoration-2">
        <div v-if="$store.state.page.data.document && $store.state.page.viewName !== 'error'">
            <nuxt-link :to="doc_action_link($store.state.page.data.document, 'w')">
                <span v-if="$store.state.page.data.document.forceShowNamespace !== false" class="text-neutral-600">{{$store.state.page.data.document.namespace}}:</span>{{$store.state.page.data.document.title}}
            </nuxt-link>
            <small v-if="$store.state.page.viewName === 'edit_edit_request' || $store.state.page.viewName === 'edit_request'">(편집 요청)</small>
            <small v-else-if="$store.state.page.viewName === 'edit' && $store.state.page.data.body.section">(r{{$store.state.page.data.body.baserev}} 문단 편집)</small>
            <small v-else-if="$store.state.page.viewName === 'edit' && $store.state.page.data.body.baserev === '0'">(새 문서 생성)</small>
            <small v-else-if="$store.state.page.viewName === 'edit'">(r{{$store.state.page.data.body.baserev}} 편집)</small>
            <small v-else-if="$store.state.page.viewName === 'history'">(역사)</small>
            <small v-else-if="$store.state.page.viewName === 'backlink'">(역링크)</small>
            <small v-else-if="$store.state.page.viewName === 'move'">(이동)</small>
            <small v-else-if="$store.state.page.viewName === 'delete'">(삭제)</small>
            <small v-else-if="$store.state.page.viewName === 'acl'">(ACL)</small>
            <small v-else-if="$store.state.page.viewName === 'thread'">(토론)</small>
            <small v-else-if="$store.state.page.viewName === 'thread_list'">(토론 목록)</small>
            <small v-else-if="$store.state.page.viewName === 'thread_list_close'">(닫힌 토론)</small>
            <small v-else-if="$store.state.page.viewName === 'edit_request_close'">(닫힌 편집 요청)</small>
            <small v-else-if="$store.state.page.viewName === 'diff'">(비교)</small>
            <small v-else-if="$store.state.page.viewName === 'revert' && $store.state.page.data.rev">(r{{$store.state.page.data.rev}}로 되돌리기)</small>
            <small v-else-if="$store.state.page.viewName === 'raw' && $store.state.page.data.rev">(r{{$store.state.page.data.rev}} RAW)</small>
            <small v-else-if="$store.state.page.viewName === 'blame' && $store.state.page.data.rev">(r{{$store.state.page.data.rev}} Blame)</small>
            <small v-else-if="$store.state.page.viewName === 'wiki' && $store.state.page.data.rev">(r{{$store.state.page.data.rev}} 판)</small>
        </div>
        <div v-else>{{ $store.state.page.title }}</div>
    </h1>
</template>


<script>
import Common from "~/mixins/common";

export default {
    mixins: [Common]
}
</script>