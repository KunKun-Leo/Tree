<template>
  <div class="custom-tree-container" style="width:400px;height:auto;background-color:rgb(213,213,213)">
    
    <p style="padding-left:20px;">资源管理器</p>
    <el-tree
      :data="dataSource"
      node-key="id"
      default-expand-all
      :expand-on-click-node="false"
      @click="show_menu">

      <template #default="{ node, data }">
        <span class="custom-tree-node">
          <span @click="justify(data)">{{ node.label }}</span>
          <!-- <span>
            <a @click="append(data)"> Append </a>
            <a style="margin-left: 8px" @click="remove(node, data)"> Delete </a>
          </span> -->
        </span>
      </template>
      
    </el-tree>
    <div  class="right_menu" id="menu" v-show= signal
          style="background-color:white;height: auto;width: 300px;font-weight: 500;">
    <ul >
      <li style="background-color:white;text-align:left; padding: 10px;">新建文件</li>
      <li style="background-color:white;text-align:left; padding: 10px;">新建文件夹</li>
      <li style="background-color:white;text-align:left; padding: 10px;">重命名</li>
      <li style="background-color:white;text-align:left; padding: 10px;">删除</li>
     
    </ul>
     <input style="text-decoration:none" type="file"/>
    </div>

  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import type Node from 'element-plus/es/components/tree/src/model/node'
import { selectGroupKey } from 'element-plus';

interface Tree {
  id: number
  label: string
  children?: Tree[]
}
let id = 1000

// export default
// {
//   setup()
//   {
    let signal = false;
    const show_menu = (signal) =>
    {  
       signal = true;
    }
//   }
// }




// const rightClick = (event, data, node, obj) =>{
//       alert(node.label)
//       // this.id = node.id
//       // console.log(this.id)
//       // if (data.flag === 'car'){
//       this.showRightMenu = true
//       const menu = document.getElementById('menu')
//       menu.style.left = event.clientX - 500 +  'px'
//       menu.style.top = event.clientY - 300 + 'px'
//       document.addEventListener('click', this.closeRightMenu)
//       // }
//     },



const justify = (data:Tree) =>
{
  
}

const append = (data: Tree) => {
  const newChild = { id: id++, label: 'testtest', children: [] }
  if (!data.children) {
    data.children = []
  }
  data.children.push(newChild)
  dataSource.value = [...dataSource.value]
}

const remove = (node: Node, data: Tree) => {
  const parent = node.parent
  const children: Tree[] = parent.data.children || parent.data
  const index = children.findIndex((d) => d.id === data.id)
  children.splice(index, 1)
  dataSource.value = [...dataSource.value]
}



const dataSource = ref<Tree[]>([
  {
    id: 1,
    label: 'Root',
    children: [
    ],
  },
])
</script>

<style>
.custom-tree-node {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 14px;
  padding-right: 8px;
}
</style>

// const renderContent = (
//   h,
//   {
//     node,
//     data,
//     store,
//   }: {
//     node: Node
//     data: Tree
//     store: Node['store']
//   }
// ) => {
//   return h(
//     'span',
//     {
//       class: 'custom-tree-node',
//     },
//     h('span', null, node.label),
//     h(
//       'span',
//       null,
//       h(
//         'a',
//         {
//           onClick: () => append(data),
//         },
//         'Append '
//       ),
//       h(
//         'a',
//         {
//           style: 'margin-left: 8px',
//           onClick: () => remove(node, data),
//         },
//         'Delete'
//       )
//     )
//   )
// }
