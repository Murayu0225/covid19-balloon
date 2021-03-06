<template>
  <component :is="cardComponent" />
</template>

<script lang="ts">
/* eslint-disable simple-import-sort/imports -- ブラウザでの表示順に合わせて各 card の component を import する */
// ---- モニタリング項目
// 報告日別による陽性者数の推移
import ConfirmedCasesNumberCard from '@/components/cards/ConfirmedCasesNumberCard.vue'
// 新規陽性者数
import MonitoringConfirmedCasesNumberCard from '@/components/cards/MonitoringConfirmedCasesNumberCard.vue'
// モニタリング状況
import MonitoringItemsOverviewCard from '@/components/cards/MonitoringItemsOverviewCard.vue'
// ---- その他 参考指標
// 検査陽性者の状況
import ConfirmedCasesDetailsCard from '@/components/cards/ConfirmedCasesDetailsCard.vue'
// 陽性者数（区別・週報）
import ConfirmedCasesByMunicipalitiesCard from '@/components/cards/ConfirmedCasesByMunicipalitiesCard.vue'
// 死亡日別による死亡者数の推移
import DeathsByDeathDateCard from '@/components/cards/DeathsByDeathDateCard.vue'
// 確定日別による陽性者数の推移
import PositiveNumberByDiagnosedDateCard from '@/components/cards/PositiveNumberByDiagnosedDateCard.vue'
// 発症日別による陽性者数の推移
import PositiveNumberByDevelopedDateCard from '@/components/cards/PositiveNumberByDevelopedDateCard.vue'

import { Vue, Component } from 'nuxt-property-decorator'
import type { NuxtOptionsHead as MetaInfo } from '@nuxt/types/config/head'
import type { NuxtConfig } from '@nuxt/types'
import { getLinksLanguageAlternative } from '@/utils/i18nUtils'
import { convertDateToSimpleFormat } from '@/utils/formatDate'

@Component({
  components: {
    // ---- モニタリング項目
    ConfirmedCasesNumberCard,
    MonitoringConfirmedCasesNumberCard,
    MonitoringItemsOverviewCard,
    // ---- その他 参考指標
    ConfirmedCasesDetailsCard,
    ConfirmedCasesByMunicipalitiesCard,
    DeathsByDeathDateCard,
    PositiveNumberByDiagnosedDateCard,
    PositiveNumberByDevelopedDateCard,
  },
})
export default class CardContainer extends Vue implements NuxtConfig {
  data() {
    let title, updatedAt, cardComponent
    switch (this.$route.params.card) {
      // NOTE: 以下，ブラウザでの表示順に合わせて条件分岐を行う
      // ---- モニタリング項目
      // 報告日別による陽性者数の推移
      case 'number-of-confirmed-cases':
        cardComponent = 'confirmed-cases-number-card'
        break
      // 新規陽性者数
      case 'monitoring-number-of-confirmed-cases':
        cardComponent = 'monitoring-confirmed-cases-number-card'
        break
      // モニタリング状況
      case 'monitoring-items-overview':
        cardComponent = 'monitoring-items-overview-card'
        break
      // ---- その他 参考指標
      // 検査陽性者の状況
      case 'details-of-confirmed-cases':
        cardComponent = 'confirmed-cases-details-card'
        break
      // 陽性者数（区別・週報）
      case 'number-of-confirmed-cases-by-municipalities':
        cardComponent = 'confirmed-cases-by-municipalities-card'
        break
      // 死亡日別による死亡者数の推移
      case 'deaths-by-death-date':
        cardComponent = 'deaths-by-death-date-card'
        break
      // 確定日別による陽性者数の推移
      case 'positive-number-by-diagnosed-date':
        cardComponent = 'positive-number-by-diagnosed-date-card'
        break
      // 発症日別による陽性者数の推移
      case 'positive-number-by-developed-date':
        cardComponent = 'positive-number-by-developed-date-card'
    }
    /* eslint-enable simple-import-sort/imports */
    return {
      cardComponent,
      title,
      updatedAt,
    }
  }

  head() {
    const url = 'https://sagamihara-stopcovid19.com'
    const timestamp = new Date().getTime()
    const defaultTitle = `${this.$t('相模原市')} ${this.$t(
      '新型コロナウイルス感染症'
    )}${this.$t('対策サイト')}`
    const ogpImage =
      (this.$i18n.locale ?? 'ja') === 'ja'
        ? `${url}/ogp/${this.$route.params.card}.png?t=${timestamp}`
        : `${url}/ogp/${this.$i18n.locale}/${this.$route.params.card}.png?t=${timestamp}`

    const mInfo: MetaInfo = {
      title: `${
        (this.$data.title ?? '') !== ''
          ? this.$data.title + ' | ' + defaultTitle
          : defaultTitle
      }`,
      link: [
        ...(getLinksLanguageAlternative(
          `cards/${this.$route.params.card}`,
          this.$i18n.locales,
          this.$i18n.defaultLocale
        ) as []),
      ],
      meta: [
        {
          hid: 'og:url',
          property: 'og:url',
          content: `${url}${this.$route.path}/`,
        },
        {
          hid: 'og:title',
          property: 'og:title',
          content: `${
            (this.$data.title ?? '') !== ''
              ? this.$data.title + ' | ' + defaultTitle
              : defaultTitle
          }`,
        },
        {
          hid: 'description',
          name: 'description',
          content: `${this.$t('{date} 更新', {
            date: convertDateToSimpleFormat(this.$data.updatedAt),
          })}: ${this.$tc(
            '当サイトは新型コロナウイルス感染症 (COVID-19) に関する最新情報を提供するために、東京都が開設したものを相模原市向けに改変したものです。'
          )}`,
        },
        {
          hid: 'og:description',
          property: 'og:description',
          content: `${this.$t('{date} 更新', {
            date: convertDateToSimpleFormat(this.$data.updatedAt),
          })}: ${this.$tc(
            '当サイトは新型コロナウイルス感染症 (COVID-19) に関する最新情報を提供するために、東京都が開設したものを相模原市向けに改変したものです。'
          )}`,
        },
        {
          hid: 'og:image',
          property: 'og:image',
          content: `${ogpImage}`,
        },
        {
          hid: 'twitter:image',
          name: 'twitter:image',
          content: `${ogpImage}`,
        },
      ],
    }
    return mInfo
  }
}
</script>
