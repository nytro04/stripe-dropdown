<template>
  <vsm-menu
    ref="header"
    :menu="menu"
    :screen-offset="15"
    @open-dropdown="onOpenDropdown"
    @close-dropdown="onCloseDropdown"
  >
    <template #before-nav>
      <li class="vsm-section vsm-mob-full">
        cool oooooooo
      </li>
    </template>
    <!--Add a title using the slot:-->
    <template #title="data">{{ data.item.title }}</template>
    <template #default="data">
      <component :is="data.item.content" class="content" />
      <component :is="data.item.secondary" class="content--secondary" />
    </template>
    <template #after-nav>
      <li class="vsm-section vsm-mob-hide rnd--open" @click="onClick">
        Random
      </li>
      <!--Display mobile menu-->
      <vsm-mob>
        <mobile-content />
      </vsm-mob>
    </template>
  </vsm-menu>
</template>

<script>
import rnd from '../../static/js/rnd'
import HorizontalSecondaryContent from '~/components/layouts/HorizontalSecondary'
import HorizontalPrimaryContent from '~/components/layouts/HorizontalPrimary'
import VerticalContent from '~/components/layouts/Vertical'
import DefaultContent from '~/components/layouts/Default'

import MobileContent from '~/components/layouts/MobileContent'

/* eslint-disable no-console */

export default {
  components: {
    // StripeLogo,
    MobileContent
  },
  data() {
    return {
      menu: [
        {
          title: 'Company',
          dropdown: 'company',
          content: DefaultContent,
          listeners: { mouseover: this.onMouseOver }
        },
        {
          title: 'Developers',
          dropdown: 'developers',
          content: HorizontalPrimaryContent,
          secondary: HorizontalSecondaryContent
        },
        {
          title: 'Products',
          dropdown: 'products',
          content: VerticalContent,
          element: 'span'
        },
        {
          title: 'Source',
          attributes: {
            href:
              'https://github.com/Alexeykhr/vue-stripe-menu/blob/master/demo/',
            class: ['some-class1', { 'some-class2': true }],
            target: '_blank'
          }
        }
      ]
    }
  },
  methods: {
    onClick() {
      const links = this.$refs.header.hasDropdownEls
      const link = links[rnd(0, links.length - 1)]

      this.$refs.header.openDropdown(link)
    },
    onMouseOver(evt) {
      console.log('mouse over', evt)
    },
    onOpenDropdown(el) {
      console.log('open dropdown', el)
    },
    onCloseDropdown(el) {
      console.log('close dropdown', el)
    }
  }
}
</script>
