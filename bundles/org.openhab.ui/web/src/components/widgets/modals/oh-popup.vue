<template>
  <f7-popup>
    <f7-page>
      <f7-navbar :title="(page) ? page.config.label : ''" back-link="Back">
      </f7-navbar>

      <f7-toolbar tabbar labels bottom v-if="page && page.component === 'oh-tabs-page' && visibleToCurrentUser">
        <f7-link v-for="(tab, idx) in page.slots.default" :key="idx" tab-link @click="currentTab = idx" :tab-link-active="currentTab === idx" :icon-ios="tab.config.icon" :icon-md="tab.config.icon" :icon-aurora="tab.config.icon" :text="tab.config.title"></f7-link>
      </f7-toolbar>

      <f7-tabs v-if="page && page.component === 'oh-tabs-page' && visibleToCurrentUser" :class="{notready: !ready}">
        <f7-tab v-for="(tab, idx) in page.slots.default" :key="idx" :tab-active="currentTab === idx">
          <component v-if="currentTab === idx" :is="tabComponent(tab)" :context="tabContext(tab)" />
        </f7-tab>
      </f7-tabs>
      <component v-else-if="visibleToCurrentUser" :is="componentType" :context="context" :class="{notready: !ready}" />
      <empty-state-placeholder v-if="page && !visibleToCurrentUser" icon="multiply_circle_fill" title="page.unavailable.title" text="page.unavailable.text" />

    </f7-page>
  </f7-popup>
</template>

<style lang="stylus">
.notready
  visibility hidden
</style>

<script>
import modal from './modal-mixin'

export default {
  mixins: [modal]
}
</script>
