<template>
  <cards-lazy-row :rows="rows" />
</template>

<script lang="ts">
/* eslint-disable simple-import-sort/imports -- ブラウザでの表示順に合わせて各 card の component を import する */
import Vue from 'vue'

// 報告日別陽性者数
const ConfirmedCasesNumberCard = () =>
  import('@/components/cards/ConfirmedCasesNumberCard.vue')
const MonitoringConfirmedCasesNumberCard = () =>
  import('@/components/cards/MonitoringConfirmedCasesNumberCard.vue')
// モニタリング項目
const MonitoringItemsOverviewCard = () =>
  import('@/components/cards/MonitoringItemsOverviewCard.vue')
/* eslint-enable simple-import-sort/imports */

export default Vue.extend({
  data() {
    return {
      rows: [
        [ConfirmedCasesNumberCard, MonitoringConfirmedCasesNumberCard],
        [MonitoringItemsOverviewCard],
      ],
    }
  },
})
</script>

<style lang="scss" scoped>
.AttentionNote {
  margin: 10px 0;
  padding: 12px;
  background-color: $emergency;
  border-radius: 4px;
  color: $gray-2;
  @include font-size(12);

  p {
    margin: 0;
  }
}
</style>
