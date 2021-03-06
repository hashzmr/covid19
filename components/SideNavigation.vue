<template>
  <div ref="Side" class="SideNavigation" tabindex="-1">
    <header class="SideNavigation-Header">
      <v-icon
        class="SideNavigation-OpenIcon"
        :aria-label="$t('サイドメニュー項目を開く')"
        @click="$emit('openNavi', $event)"
      >
        mdi-menu
      </v-icon>
      <h1 class="SideNavigation-HeaderTitle">
        <nuxt-link :to="localePath('/')" class="SideNavigation-HeaderLink">
          <img
            class="SideNavigation-HeaderLogo"
            src="/logo.svg"
            :alt="$t('長野県 非公式')"
          />
          <div class="SideNavigation-HeaderText">
            {{ $t('長野県 非公式') }}<br />
            {{ $t('新型コロナウイルス感染症') }}<br />{{ $t('対策サイト') }}
          </div>
        </nuxt-link>
      </h1>
    </header>

    <div :class="['SideNavigation-Body', { '-opened': isNaviOpen }]">
      <v-icon
        class="SideNavigation-CloseIcon"
        :aria-label="$t('サイドメニュー項目を閉じる')"
        @click="$emit('closeNavi', $event)"
      >
        mdi-close
      </v-icon>

      <nav class="SideNavigation-Menu">
        <div class="SideNavigation-Language">
          <div
            v-if="this.$i18n.locales.length > 1"
            class="SideNavigation-Language"
          >
            <label class="SideNavigation-LanguageLabel" for="LanguageSelector">
              {{ $t('多言語対応選択メニュー') }}
            </label>
            <LanguageSelector />
          </div>
        </div>
        <MenuList :items="items" @click="$emit('closeNavi', $event)" />
      </nav>
      <footer class="SideNavigation-Footer">
        <div class="SideNavigation-Social">
          <!-- <a
            href="https://line.me/R/ti/p/%40822sysfc"
            target="_blank"
            rel="noopener noreferrer"
            class="SideNavigation-SocialLink"
          > -->
          <a
            href="https://www.pref.nagano.lg.jp/hoken-shippei/kenko/kenko/kansensho/joho/corona-line.html"
            target="_blank"
            rel="noopener noreferrer"
            class="SideNavigation-SocialLink"
          >
            <img src="/line.png" alt="LINE" />
          </a>
          <a
            href="https://twitter.com/nagano_corona"
            target="_blank"
            rel="noopener noreferrer"
            class="SideNavigation-SocialLink"
          >
            <img src="/twitter.png" alt="Twitter" />
          </a>
          <!-- <a
            href="https://www.facebook.com/tochokoho"
            target="_blank"
            rel="noopener noreferrer"
            class="SideNavigation-SocialLink"
          >
            <img src="/facebook.png" alt="Facebook" />
          </a> -->
          <a
            href="https://www.youtube.com/channel/UCUdpuTxrK48m9O9dlPpo7yA"
            target="_blank"
            rel="noopener noreferrer"
            class="SideNavigation-SocialLink"
          >
            <img src="/youtube.png" alt="YouTube" />
          </a>
          <a
            href="https://github.com/Stop-COVID19-Nagano/covid19"
            target="_blank"
            rel="noopener noreferrer"
            class="SideNavigation-SocialLink"
          >
            <img src="/github.png" alt="GitHub" />
          </a>
        </div>
        <small class="SideNavigation-Copyright">
          {{ $t('このサイトの内容物は') }}
          <a
            rel="license"
            target="_blank"
            href="https://creativecommons.org/licenses/by/4.0/deed.ja"
            class="SideNavigation-LicenseLink"
          >
            {{ $t('クリエイティブ・コモンズ 表示 4.0 ライセンス') }}
          </a>
          {{ $t('の下に提供されています。') }}
          <br />
          {{ $t('2020 長野県非公式 COVID-19 対策サイト') }}
        </small>
      </footer>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { TranslateResult } from 'vue-i18n'
import LanguageSelector from '@/components/LanguageSelector.vue'
import MenuList from '@/components/MenuList.vue'

type Item = {
  icon?: string
  title: TranslateResult
  link: string
  divider?: boolean
}

export default Vue.extend({
  components: {
    MenuList,
    LanguageSelector
  },
  props: {
    isNaviOpen: {
      type: Boolean,
      required: true
    }
  },
  computed: {
    items(): Item[] {
      return [
        {
          icon: 'mdi-chart-timeline-variant',
          title: this.$t('県内の最新感染動向'),
          link: this.localePath('/')
        },
        {
          icon: 'CovidIcon',
          title: this.$t('新型コロナウイルス感染症が心配なときに'),
          link:
            'https://www.pref.nagano.lg.jp/hoken-shippei/kenko/kenko/kansensho/joho/corona-soudan.html#soudan',
          divider: true
        },
        {
          // icon: 'mdi-link',
          title: this.$t('関連リンク集'),
          link: this.localePath('/link')
        },
        {
          icon: 'ParentIcon',
          title: this.$t('お子様をお持ちの皆様へ'),
          link: this.localePath('/parent')
        },
        {
          icon: 'mdi-account-multiple',
          title: this.$t('県民の皆様へ'),
          link:
            'https://www.pref.nagano.lg.jp/hoken-shippei/kenko/kenko/kansensho/joho/corona.html'
        },
        // {
        //   icon: 'mdi-domain',
        //   title: this.$t('企業の皆様・はたらく皆様へ'),
        //   link: this.localePath('/worker'),
        //   divider: true
        // },
        // {
        //   title: this.$t('東京都新型コロナウイルス感染症対策本部報'),
        //   link:
        //     'https://www.bousai.metro.tokyo.lg.jp/taisaku/saigai/1007261/index.html'
        // },
        // {
        //   title: this.$t('東京都主催等 中止又は延期するイベント等'),
        //   link:
        //     'https://www.seisakukikaku.metro.tokyo.lg.jp/information/event00.html'
        // },
        // {
        //   title: this.$t('知事からのメッセージ'),
        //   link:
        //     'https://www.metro.tokyo.lg.jp/tosei/governor/governor/katsudo/2020/03/03_00.html'
        // },
        {
          title: this.$t('当サイトについて'),
          link: this.localePath('/about')
        },
        {
          title: this.$t('長野県公式ホームページ'),
          link: 'https://www.pref.nagano.lg.jp/'
          // divider: true
        }
      ]
    }
    // isClass() {
    //   return item => (item.title.charAt(0) === '【' ? 'kerningLeft' : '')
    // }
  },
  watch: {
    $route: 'handleChageRoute'
  },
  methods: {
    handleChageRoute() {
      // nuxt-link で遷移するとフォーカスが残り続けるので $route を監視して SideNavigation にフォーカスする
      return this.$nextTick().then(() => {
        const $Side = this.$refs.Side as HTMLEmbedElement | undefined
        if ($Side) {
          $Side.focus()
        }
      })
    }
  }
})
</script>

<style lang="scss" scoped>
.SideNavigation {
  position: relative;
  @include lessThan($small) {
    box-shadow: 0 0 2px rgba(0, 0, 0, 0.15);
  }
  &:focus {
    outline: 1px dotted $gray-3;
  }
}
.SideNavigation-Header {
  height: 64px;
  padding-left: 52px;
  @include largerThan($small) {
    height: auto;
    padding: 20px;
  }
  @include lessThan($small) {
    display: flex;
  }
  @include lessThan($tiny) {
    padding-left: 44px;
  }
}
.SideNavigation-OpenIcon {
  position: absolute;
  top: 0;
  left: 0;
  padding: 18px 8px 18px 16px;
  font-size: 28px;
  @include lessThan($tiny) {
    font-size: 24px;
    padding: 20px 10px;
  }
  @include largerThan($small) {
    display: none;
  }
}
.SideNavigation-CloseIcon {
  position: absolute;
  top: 0;
  left: 0;
  padding: 18px 8px 18px 16px;
  font-size: 28px;
  @include lessThan($tiny) {
    font-size: 24px;
    padding: 20px 10px;
  }
  @include largerThan($small) {
    display: none;
  }
}
.SideNavigation-HeaderTitle {
  width: 100%;
  font-size: 13px;
  color: #707070;
  @include largerThan($small) {
    margin: 0;
    margin-top: 10px;
  }
}
.SideNavigation-HeaderLink {
  display: flex;
  align-items: center;
  padding-right: 10px;
  @include lessThan($small) {
    height: 64px;
  }
  @include lessThan($tiny) {
    justify-content: space-between;
  }
  &:link,
  &:hover,
  &:focus,
  &:visited,
  &:active {
    color: inherit;
    text-decoration: none;
  }
  &:hover,
  &:focus {
    font-weight: bold;
  }
  &:focus {
    outline: dotted $gray-3 1px;
  }
  @include largerThan($small) {
    display: block;
    padding: 15px 0;
  }
}
.SideNavigation-HeaderLogo {
  width: 128px;
  @include lessThan($tiny) {
    width: 100px;
  }
}
.SideNavigation-HeaderText {
  margin: 10px 0 0 0;
  @include lessThan($small) {
    margin: 0 0 0 10px;
  }
  @include lessThan($tiny) {
    margin: 0;
  }
}
.SideNavigation-Body {
  padding: 0 20px 20px;
  @include lessThan($small) {
    display: none;
    padding: 0 36px 36px;
    &.-opened {
      position: fixed;
      top: 0;
      bottom: 0;
      left: 0;
      display: block !important;
      width: 100%;
      z-index: z-index-of(opened-side-navigation);
      background-color: $white;
      height: 100%;
      overflow: auto;
      -webkit-overflow-scrolling: touch;
    }
  }
}
.SideNavigation-Menu {
  @include lessThan($small) {
    padding-top: 50px;
  }
}
.SideNavigation-LanguageLabel {
  display: block;
  margin-bottom: 5px;
  font-size: 0.85rem;
}
.SideNavigation-Footer {
  padding-top: 20px;
}
.SideNavigation-Social {
  display: flex;
}
.SideNavigation-SocialLink {
  border: 1px dotted transparent;
  border-radius: 30px;
  color: $gray-3;
  &:link,
  &:hover,
  &:visited,
  &:active {
    color: inherit;
    text-decoration: none;
  }
  &:focus {
    color: inherit;
    text-decoration: none;
    border: 1px dotted $gray-3;
    outline: none;
  }
  & + & {
    margin-left: 10px;
  }
  img {
    width: 30px;
  }
}
.SideNavigation-Copyright {
  display: block;
  margin-top: 15px;
  color: $gray-1;
  font-size: 10px;
  line-height: 1.3;
  font-weight: bold;
}
.SideNavigation-LicenseLink {
  &:focus {
    outline: 1px dotted $gray-3;
  }
}
</style>
