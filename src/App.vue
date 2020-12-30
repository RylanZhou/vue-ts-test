<template>
  <div>
    <div class="container">
      <ul v-for="(queue, index) in queues" :key="index">
        <li v-for="name in queue" :key="name">
          {{ name }}
        </li>
      </ul>
    </div>
    <el-button @click="addName" :loading="isLoading">Add</el-button>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Watch } from 'vue-property-decorator'

@Component({ name: 'App' })
export default class App extends Vue {
  queues: string[][] = [
    ['Yvonne'],
    ['Arnold', 'Valerie', 'Laura'],
    [],
    ['Jaden', 'Damien'],
  ]
  queueIndex = 0
  isLoading = false

  @Watch('queues')
  private onQueuesChange() {
    this.queueIndex = (this.queueIndex + 1) % this.queues.length
  }

  async addName() {
    this.isLoading = true
    try {
      const resp = await fetch(process.env.VUE_APP_REQUEST_URL + '/name')
      const { data }: { data: string } = await resp.json()
      this.queues[this.queueIndex].push(data)
    } catch (error) {
      console.log(error)
    } finally {
      this.isLoading = false
    }
  }
}
</script>

<style lang="scss">
.container {
  display: flex;
  user-select: none;

  ul {
    flex: 1;
  }
}
</style>
