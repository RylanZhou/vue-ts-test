<!-- App.vue -->
<template>
  <div>
    <Navbar
      :page-data="pageData"
      @add="handleAddNewTab"
      @change="setActiveIndex"
    />
    <div v-if="activeIndex === 0">
      Calendar
    </div>
    <Page
      v-else
      :data="pageData[activeIndex]"
      @save-1="handleSaveContent1"
      @save-2="handleSaveContent2"
    />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import Navbar from './Navbar.vue'
import Page from './Page.vue'

@Component({ name: 'App', components: { Navbar, Page } })
export default class App extends Vue {
  // 所有页面数据
  pageData: PageDataType[] = [
    {
      id: 'calendar',
      tabName: 'Calendar',
    },
  ]
  // 当前展示的页面下标
  activeIndex = 0

  handleAddNewTab(tabName: string) {
    this.pageData.push({
      id: `${+new Date()}`,
      tabName,
      content1: '',
      content2: '',
    })
  }

  setActiveIndex(id: string) {
    this.activeIndex = this.pageData.findIndex(each => each.id === id)
  }

  handleSaveContent1(content1: string) {
    this.pageData[this.activeIndex].content1 = content1
  }

  handleSaveContent2(content2: string) {
    this.pageData[this.activeIndex].content2 = content2
  }
}
</script>
