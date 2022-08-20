
<template>
<div id="tree">
  <el-tree :data="data" :props="defaultProps" @node-contextmenu="rightClick"></el-tree>
<!-- 右键菜单 -->
  <div class="right_menu" id="menu" v-show="showRightMenu" 
  style="background-color:white;height: auto;width: 200px;font-weight: 500;">
    <ul >
      <li  style="background-color:white;text-align:left; padding: 10px;;" v-for="(item,index) in rightMenuList" :key="index" 
       @mouseover="change_color" @mousedown="choose_operation(item,item.id)" @click="menu(item.name)">{{item.name}}</li>
    </ul>
    </div>
</div>
</template>

<script>

export default {
  data() {
    return {
      showRightMenu: false,
      rightMenuList:[
        { id:1, name:'新建文件' },
        { id:2, name:'新建文件夹' },
        { id:3, name:'删除' }

      ],
      id: '',
      data: [{
        label: '一级 1',
        children: [{
          label: '二级 1-1',
          label1: 'erjie',
          children: [{
            label: '三级 1-1-1'
          }]
        }]
      }, {
        label: '一级 2',
        children: [{
          label: '二级 2-1',
          children: [{
            label: '三级 2-1-1'
          }]
        }, {
          label: '二级 2-2',
          children: [{
            label: '三级 2-2-1'
          }]
        }]
      }, {
        label: '一级 3',
        children: [{
          label: '二级 3-1',
          children: [{
            label: '三级 3-1-1'
          }]
        }, {
          label: '二级 3-2',
          children: [{
            label: '三级 3-2-1'
          }]
        }]
      }],
     
      defaultProps: {
        children: 'children',
        label: 'label'
      }
    }
  },
  methods: {
    rightClick(event, data, node, obj){
      alert(node.label)
      this.id = node.id
      console.log(this.id)
      // if (data.flag === 'car'){
      this.showRightMenu = true
      const menu = document.getElementById('menu')
      menu.style.left = event.clientX - 500 +  'px'
      menu.style.top = event.clientY - 300 + 'px'
      document.addEventListener('click', this.closeRightMenu)
      // }
    },

    change_color()
    {
      item = document.getElementsByTagName("li")
      item.style.background = "red"
    },
    

    choose_operation(node,id)
    {
      // alert(id)
      switch(id)
      {
        case 1:
          // this.new_file();
          alert(node.label)
          node.children.append({label:'root1',children:[]})
          break;
        case 2:
          this.new_doc();
          break;
        default:
          this.del_file();
          break;

      }
      
 
    },

    new_file()
    {
      alert("1");

    },

    new_doc()
    {
      alert("2")
    },

    del_file()
    {
      alert("3")
    },
    menu(name) {
      if (name === '新增'){
        console.log(this.id, '新增')
      }
      if (name === '删除'){
        console.log(this.id, '删除')
      }
      if (name === '编辑'){
        console.log(this.id, '编辑')
      }
    },
    closeRightMenu() {
      this.showRightMenu = false
      document.removeEventListener('click', this.closeRightMenu)
    }
  }
}
</script>
<style>
#tree{
  position: relative;
}
  .right_menu{
    position: absolute;
    width: 120px;
    height: 200px;
    background: rgb(239, 239, 241);
    border: 1px solid rgb(241, 241, 241);
    border-radius: 2%;
    box-shadow: 0 2px 12px 0 rgb(0 0 0 / 30%);
  }
  .right_menu ul{
    width: 100%;
    height:100%;
    list-style: none;
    margin: 0;
    padding: 0;
    border-radius: 2%;
}
.right_menu ul li{
    margin: 0 0 1px 0;
    color: rgb(77, 77, 73);
    text-align: center;
    font-size: 14px;
    padding-top:4%;
    width:100%;
    height:9.7%;
    background: #fff;
    float: left;
    cursor: pointer;
}
</style>
