<template>
  <div id="Linkage">
    <template v-for="(select,index) in level">
      <select @change = "selectChildren(index)" :key="index" v-model="cataValue[index]">
         <option :value="item" v-for="(item,index) in select">{{item.name}}</option>
      </select>
    </template>
    <br/>
  </div>
</template>

<script>
    let arrData = [
      {id: 1, parent_id: 0, name: '一级'},
      {id: 2, parent_id: 0, name: '一级2'},
      {id: 12, parent_id: 1, name: '二级1'},
      {id: 13, parent_id: 1, name: '二级2'},
      {id: 122, parent_id: 12, name: '三级1'},
      {id: 133, parent_id: 13, name: '三级2'},
      {id: 1335, parent_id: 133, name: '四级1'},
      {id: 1336, parent_id: 133, name: '四级2'}
    ]
    export default {
        data: function () {
          return {
            lists: arrData,
            curId: 1335,
            level:[],
            cataValue:[],
          }
        },
        computed:{
          root() {
            const rootData = this._getChid(this.lists, 0)
            return rootData
          }
        },
        methods: {
          selectChildren(_index) {
            let childrenData = this._getChid(this.lists, this.cataValue[index].id)
            if(childrenData.length){
              this.level.push(childrenData)
            }
          },
          _set(id) {
            let cur = this.lists.filter(item => item.id === id)
            let par = cur[0].parent_id
            let t_l = []
            let num = 0
            function get(item, par){
              if(item.id == par && num < 4){
                let secPar = item.id;
                num++;
                get(item, secPar)
              }  
            }
            this.lists.forEach((item, index) => {
              get(item,par)
            })
            console.info(num)
          },
          _getChid(lists, id) {
              return lists.filter(item => item.parent_id === id)
          }
        },
        mounted(){
          this.level.push(this.root)
          this._set(this.curId)
        }
    }
</script>

<style scoped>

</style>
