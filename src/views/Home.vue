<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <div v-for="(item, index) in data" :key="item.id">{{index}}-{{item.id}}
      <button @click="add('left', index)">左边添加</button>
      <button @click="add('right', index)">右边添加</button>
    </div>
    <SlotColumn v-for="(item, index) in data" :key="item.id">
      {{index}}-{{item.id}}-SlotColumn
      <button @click="add('left', index)">左边添加</button>
      <button @click="add('right', index)">右边添加</button>
    </SlotColumn>
    <RightMouseButton></RightMouseButton>
    <el-table
    :data="data"
    style="width: 100%">
    <el-table-column
    v-for="(item, index) in data" :key="item.id"
    :prop="item.id"
   :render-header="(h, options) => renderHeader(h, options, item, index)"
      >
      <template slot-scope="scope">{{scope.row.id}}</template>
    </el-table-column>
  </el-table>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import TableColumn1 from '@/components/TableColumn1.vue'
import SlotColumn from '@/components/SlotColumn.vue'
import RightMouseButton from '@/components/RightMouseButton.vue'

export default {
  name: 'home',
  components: {
    HelloWorld,
    SlotColumn,
    RightMouseButton
  },
  data() {
    return {
      data: [{
        id: this.guid()
      }]
    }
  },
  
  methods: {
    add(type, index) {
      // eslint-disable-next-line no-console
      console.log('type', type, index, this.guid(), this.data)
      const obj = {
          id: this.guid()
      }
      if(type === 'left') {
      // eslint-disable-next-line no-console
      console.log('type', type, index)
        this.data.splice(index, 0, obj)
      } else if(type === 'right') {
        this.data.splice(index + 1, 0, obj)
      }
    },
    guid() {
      return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function (c) {
          var r = Math.random() * 16 | 0,
              v = c == 'x' ? r : (r & 0x3 | 0x8);
          return v.toString(16);
      });
    },
    renderHeader(h, options, item, index) {
      // eslint-disable-next-line no-console
      console.log(h, options, item, index, TableColumn1)
      return h(TableColumn1,{ props: {index: options.$index, item}, on: {add: this.add}})
    }
  }
}
</script>
