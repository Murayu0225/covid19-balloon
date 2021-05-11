<template>
  <div class="VaccineInfo">
    <div class="VaccineInfo-heading">
      <h3 class="VaccineInfo-title">
        {{ $t('ワクチンについて') }}
      </h3>
    </div>
    <div class="VaccineInfo-description">
      <details>
        <summary>
          {{
            $t(
              ' 新型コロナウイルスワクチン接種を希望する市民の方へ（ここをクリックして詳細を確認出来ます）'
            )
          }}
        </summary>
        <div class="fade">
          <ul>
            <li>
              {{
                $t(
                  '5月13日（木曜日）からの予約受付開始は、市が設置する接種会場での「集団接種」のみです。地域の身近な病院、診療所での「個別接種」の予約開始日時は、決定次第お知らせいたします。'
                )
              }}
            </li>
          </ul>
          <br />
          <p>
            {{
              $t(
                '新型コロナウイルスワクチン接種に必要なクーポン券（接種券）を4月28日（水曜日）に発送しました。5月13日（木曜日）から75歳以上の方を対象とした予約受付が開始になります。（集団接種のみ）'
              )
            }}
          </p>
          <br />
          <span>{{ $t('（注）') }}</span>
          <ul class="Attention">
            <li>
              {{
                $t(
                  '予約開始当初は、専用コールセンターへの電話や予約システム（ウェブ・LINE）に繋がりにくく、予約が取りづらい状況になることが予想されますが、今後、ワクチンは安定的に供給される見込みとなっておりますので、ご安心ください。'
                )
              }}
              <br />
              {{
                $t(
                  '供給量に応じて、予約可能数を順次拡大していきますので、慌てず、焦らず、お待ちくださいますようお願いいたします。'
                )
              }}
            </li>
            <li>
              {{
                $t(
                  '市役所の窓口や医療機関では予約を受け付けておりませんので、ご注意ください。'
                )
              }}
            </li>
          </ul>
          <br />
          <p>
            {{
              $t(
                '詳細は、次のリンク「新型コロナウイルスワクチンについて」のページをご覧ください。'
              )
            }}
          </p>
          <v-icon color="#D9D9D9">{{ mdiChevronRight }}</v-icon>
          <app-link
            to="https://www.city.sagamihara.kanagawa.jp/kurashi/kenko/kansenyobo/1019910/1022588/index.html"
          >
            {{ $t('新型コロナウイルスワクチンについて') }} （{{ date }}更新）
          </app-link>
          <br />
          <p>
            {{
              $t(
                'ワクチンに関するお問い合わせは、相模原市の担当窓口まで行ってください。当サイトでは、お答えできません。'
              )
            }}
          </p>
        </div>
      </details>
    </div>
  </div>
</template>

<script lang="ts">
import { mdiChevronRight } from '@mdi/js'
import dayjs from 'dayjs'
import Vue from 'vue'

import AppLink from '@/components/AppLink.vue'
import InfectionMedicalcareprovisionStatus from '@/data/infection_medicalcareprovision_status.json'

export default Vue.extend({
  components: {
    AppLink,
  },
  data() {
    return {
      mdiChevronRight,
      date: dayjs(InfectionMedicalcareprovisionStatus.vaccinedate).format(
        'YYYY年MM月DD日'
      ),
    }
  },
})
</script>

<style lang="scss">
.VaccineInfo {
  @include card-container();

  padding: 10px;
  margin-bottom: 20px;

  .VaccineInfo-heading {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;

    .VaccineInfo-title {
      display: flex;
      align-items: center;
      padding: 12px;
      color: $gray-2;
      @include card-h2();
    }
  }

  .VaccineInfo-description {
    padding: 12px;

    @include font-size(14);
    > a {
      text-decoration: none;
      @include text-link();
    }
  }

  .VaccineInfo-comments {
    h4 {
      margin-bottom: 10px;
      color: $gray-3;
      font-weight: normal;

      @include font-size(14);
    }

    margin: 0 10px;
  }

  .Attention {
    color: red;
  }

  details[open] .fade {
    animation: fadeIn 0.7s ease;
  }
  @keyframes fadeIn {
    0% {
      opacity: 0;
      transform: translateY(-10px);
    }
    100% {
      opacity: 1;
      transform: none;
    }
  }

  details[open] summary {
    color: gray;
  }
}
</style>

