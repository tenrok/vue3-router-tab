<template>
  <router-tab
    :i18n="i18n"
    :tabs="tabs"
  />
</template>

<script>
  // import Vue from 'vue'

  export default {
    name: 'LangCustom',
    data() {
      return {
        currentLang: 'en',

        langs: {
          en: {
            i18n: 'I18n Page',
            page: 'Page {0}'
          },

          zh: {
            i18n: '国际化页面',
            page: '页面 {0}'
          }
        },

        tabs: ['/i18n/lang', { to: '/i18n/page/1', title: ['page', 1] }, { to: '/i18n/page/2', title: ['page', 2] }]
      }
    },

    computed: {
      lang() {
        return this.langs[this.currentLang] || this.langs.en
      }
    },

    beforeCreate() {
      // Global language approach
      // Vue.prototype.$lang = {
      //   set: lang => {
      //     this.currentLang = lang
      //   },
      //   get: () => this.currentLang,
      //   list: () => Object.keys(this.langs)
      // }
    },

    unmounted() {
      // Vue.prototype.$lang = null
    },

    methods: {
      i18n(key, params) {
        let lang = this.lang[key]
        return lang
          ? lang.replace(/(\{(\d+)\})/g, (match, $0, $1) => params[$1] || '') // Replacing list parameters in internationalization
          : key
      }
    }
  }
</script>
