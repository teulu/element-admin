<template>
  <div class="ui vertical accordion menu">
    <div class="item" v-for="menu in menus">
      <a class="title header" :class="{'active': $index==currentIndex,'selected-menu': (menu.name==currentMenu)}"><i class="icon" :class="menu.icon"></i> {{menu.title}}<i class="dropdown icon"></i></a>
      <div class="content menu" :class="{'active': $index==currentIndex}">
        <a class="item" v-for="subMenu in menu.subMenu" v-link="{path: subMenu.path, exact: true}"> {{subMenu.title}} </a>
      </div>
    </div>
  </div>
</template>
<script>
  import menus from './menu.conf'
  import $ from 'jquery'
  export default{
    data() {
      return {
        menus: menus,
        currentIndex: 0
      }
    },
    vuex: {
      getters: {
        currentMenu: ({ menu }) => menu.current || 'basicEditor'
      }
    },
    ready() {
      for (var k = 0; k < menus.length; k++) {
        if (menus[k].name === this.currentMenu) {
          this.currentIndex = k
          break
        }
      }
      $('.main-menu .ui.accordion').accordion({ exclusive: false })
    }
  }
</script>
<style scoped>
    .ui.accordion.menu {
        background-color: #293541;
        color: #bbb;
        border: none;
        border-radius: 0;
    }
    .ui.accordion.menu > .item {
        padding: 0 !important;
        color: #bbb !important;
    }
    .ui.accordion.menu .item .title {
        padding: .92857143em 1.14285714em !important;
        margin: 0 !important;
        overflow: hidden;
        background-color: #323e4a;
        border-top: 1px solid #3d4853;
        border-bottom: 1px solid #252e37;
        font-weight: 400;
        font-size: 16px;
        color: #bbb;
    }
    .ui.accordion.menu .item .title:hover, .ui.accordion.menu .item .selected-menu {
        background-color: #0cadb7;
        border-top: 1px solid #10C2CC;
        border-bottom: 1px solid #097279;
        color: #ffffff;
    }
    .ui.accordion:not(.styled) .title ~ .content:not(.ui):last-child {
        padding-bottom: 1em;
    }
    .ui.vertical.menu .item .menu .active.item, .ui.accordion.menu .menu .item:hover {
        background-color: #323E4A;
        color: #0cadb7 !important;
    }
    .ui.accordion.menu .menu .item {
        padding-left: 60px;
        color: #bbb;
        font-size: 1em !important;
    }
</style>
