<script setup>
import {
  NLayoutHeader,
  NImage,
  NGrid,
  NGi,
  NButton,
  NSpace,
  NIcon,
  NH3,
  NText,
  NSwitch,
  NAvatar,
  NDropdown,
  useMessage
} from 'naive-ui'
  import News16Regular from '@vicons/fluent/News16Regular'
  // import GitlabOutlined from '@vicons/antd/GitlabOutlined'
  import CodepenOutlined from '@vicons/antd/CodepenOutlined'
  import Atom from '@vicons/tabler/Atom'
  import Github from '@vicons/fa/Github'
  import ShareSocialOutline from '@vicons/ionicons5/ShareSocialOutline'
  import ManageAccountsOutlined from '@vicons/material/ManageAccountsOutlined'
  import BarsOutlined from '@vicons/antd/BarsOutlined'
  import ApiApp from '@vicons/tabler/ApiApp'
import {useRoute, useRouter} from "vue-router";

window.$message=useMessage();
const $route=useRoute();
const $router=useRouter();

function jumpTo(url){
  window.open(url);
}
</script>

<template>
  <n-config-provider :theme-overrides="responseTheme">
    <n-layout-header bordered >
      <n-grid cols="48 m:48 l:48" x-gap="5px" item-responsive responsive="screen">
        <!--icon-->
        <n-gi offset="4" span="4 s:3 l:3">
          <!--          <n-image @click="$router.push('/')" width="54" src="./src/assets/ico.png"></n-image>-->
          <img src="https://bitnp-website-1258614279.cos.ap-beijing.myqcloud.com/static/ico.png"  style="width: 28px;" id="headerIco" @click="$router.push('/')">
          <!--          BitNP-->
        </n-gi>
        <!--news-->
        <n-gi offset="0" span="0 s:5 l:3">
          <n-button text @click="jumpTo('https://status.bitnp.net')">
            <n-icon :size="propstyle.icons" >
              <News16Regular/>
            </n-icon>
            <span style="font-size: 17px;">News</span>
          </n-button>
        </n-gi>
        <!--space-->
        <n-gi offset="0" span="0 s:5 l:3">
          <n-dropdown trigger="hover" size="large" :options="options1" @select="handleSelect">
            <n-button text >
              <n-icon :size="propstyle.icons" >
                <CodepenOutlined/>
              </n-icon>
              <span style="font-size: 17px;">Space</span>
            </n-button>
          </n-dropdown>
        </n-gi>
        <!--meta-->
        <n-gi offset="0" span="0 s:5 l:3">
          <n-dropdown trigger="hover" size="large" :options="options2" @select="handleSelect">
            <n-button text >
              <n-icon :size="propstyle.icons" >
                <Atom/>
              </n-icon>
              <span style="font-size: 17px;">Meta</span>
            </n-button>
          </n-dropdown>
          <!--about格-->
        </n-gi>
        <!--about-->
        <n-gi offset="0" span="0 s:5 l:3">
          <n-button text @click="$router.push('about-us')">
            <n-icon :size="propstyle.icons">
              <ApiApp/>
            </n-icon>
            <span style="font-size: 17px;">About</span>
          </n-button>
        </n-gi>
        <!--admin-->
        <n-gi offset="22 s:14 l:22" span="0 s:2 l:1">
          <n-button text @click="$router.push('')">
            <n-icon :size="propstyle.icons">
              <ManageAccountsOutlined/>
            </n-icon>
          </n-button>
        </n-gi>
        <!--github-->
        <n-gi offset="0" span="0 s:2 l:1">
          <n-button text @click="jumpTo('https://github.com/BITNP')" >
            <n-icon :size="propstyle.icons">
              <Github/>
            </n-icon>
          </n-button>
        </n-gi>
        <!--share-->
        <n-gi offset="0" span="0 s:2 l:1">
          <n-button class="clipbtn" :data-clipboard-text="Urlhandle" text>
            <n-icon :size="propstyle.icons">
              <ShareSocialOutline/>
            </n-icon>
          </n-button>
        </n-gi>
        <!--Title for mobile-->
        <n-gi offset="0" span="15 s:0 l:0">
            <span style="font-size: 1rem; display: inline-block; padding-top: 0.6rem; ">
              Net Pioneer
            </span>
        </n-gi>
        <!--dropdown for mobile-->
        <n-gi offset="18 m:25" span="4 s:0 l:0">
          <n-dropdown :options="optionsM" @select="handleSelect" size="huge" style="width: 50vw;">
            <n-button text>
              <n-icon :size="propstyle.icons-2">
                <BarsOutlined></BarsOutlined>
              </n-icon>
            </n-button>
          </n-dropdown>
        </n-gi>
        <input id="clipbundle" class="clptar" style="visibility: hidden;">
      </n-grid>
    </n-layout-header>
  </n-config-provider>
</template>

<script>
import {h} from "vue"
import {defineComponent,reactive} from "vue";

import {NAvatar, NText} from 'naive-ui'
import Clipboard from 'clipboard'

import DnsServices from '@vicons/carbon/DnsServices'
import BrandGithub from '@vicons/tabler/BrandGithub'
import CalendarLtr16Regular from '@vicons/fluent/CalendarLtr16Regular'
import DevicesPc from '@vicons/tabler/DevicesPc'
import PlanetOutline from '@vicons/ionicons5/PlanetOutline'
import MdContacts from '@vicons/ionicons4/MdContacts'
import LinkSquare12Regular from '@vicons/fluent/LinkSquare12Regular'
// import News16Regular from '@vicons/fluent/News16Regular'

const responseTheme={
  breakpoints:{s:767}
}

const renderIcon = (icon) => {
  return () => {
    return h(NIcon, null, {
      default: () => h(icon)
    });
  };
};

export default defineComponent({
  name: "headers",
  setup(){
    let clipUrl=reactive({e:window.location.href});
    return{
      clipUrl,
    }
  },
  data(){
    return{
      propstyle:{
        icons:25,
      },
      options1:[
        {
          label: '组织部芝士虾',
          key: 'activities',
          icon:renderIcon(CalendarLtr16Regular)
        },
        {
          label: "BITNP Blog",
          key: 'blogs',
          icon:renderIcon(DnsServices)
        },
        {
          label: "BITNP知识库",
          key: 'wiki',
          icon:renderIcon(DnsServices)
        },
      ],
      options2:[
        {
          label: '网协GitHub',
          key:'github',
          icon:renderIcon(BrandGithub)
        },
        {
          label: '学校常用网址',
          key: 'address',
          icon:renderIcon(LinkSquare12Regular)
        },
        {
          label: '电脑推荐表',
          key: 'PCcommands',
          icon:renderIcon(DevicesPc)
        },
      ],
      // 移动端下拉菜单，因此和上方会有重复
      optionsM:[
        {
          label:'News',
          key:'news',
          icon:renderIcon(News16Regular)
        },
        {
          label: 'Space',
          key: 'space',
          icon:renderIcon(CodepenOutlined),
          children:[
            {
              label: '组织部芝士虾',
              key: 'activities',
              icon:renderIcon(CalendarLtr16Regular)
            },
            {
              label: "BITNP Blog",
              key: 'blogs',
              icon:renderIcon(DnsServices)
            },
            {
              label: "BITNP知识库",
              key: 'wiki',
              icon:renderIcon(DnsServices)
            },
          ]
        },
        {
          label: 'Meta',
          key: 'meta',
          icon:renderIcon(Atom),
          children: [
            {
              label: '网协GitHub',
              key:'github',
              icon:renderIcon(BrandGithub)
            },
            {
              label: '学校常用网址',
              key: 'address',
              icon:renderIcon(LinkSquare12Regular)
            },
            {
              label: '电脑推荐表',
              key: 'PCcommands',
              icon:renderIcon(DevicesPc)
            },
          ]
        },
        {
          label: 'About',
          key: 'about',
          icon:renderIcon(ApiApp)
        }
      ]
    }
  },
  components:{
    Clipboard
  },
  methods:{
      // Changetheme(value){
      //   this.$store.commit('ChangeTheme')
      // },
    handleSelect(key){
      const map ={
        news:'https://status.bitnp.net',
        github:'https://github.com/BITNP',
        activities:'https://cheesy-shrimp.bitnp.net',
        blogs:'https://blog.bitnp.net',
        wiki:'https://wiki.bitnp.net',
        address:'common-links',
        PCcommands:'https://docs.qq.com/aio/p/scmzu718dzus0zl',
        about:'about-us'
      }
      //pollyfill
      if (map[key].indexOf('http')!=-1)window.open(map[key]);
      else this.$router.push(map[key]);
    }
  },
  mounted() {
    var clipboard=new Clipboard('.clipbtn');
    clipboard.on('success',()=>{
      window.$message.success('已粘贴到剪贴板，快去分享吧~');
      // console.log('copy text successfully.')
    });
  },
  computed:{
    Urlhandle(){
      // return window.location.href;
      // console.log(this.$route.path);
      return document.location.host+'/#'+this.$route.path;
    }
  }
})
</script>

<style scoped>
html {
  font-size : 20px;
}
@media only screen and (min-width: 401px){
  html {
    font-size: 25px !important;
  }
}
@media only screen and (min-width: 428px){
  html {
    font-size: 26.75px !important;
  }
}
@media only screen and (min-width: 481px){
  html {
    font-size: 30px !important;
  }
}
@media only screen and (min-width: 569px){
  html {
    font-size: 35px !important;
  }
}
@media only screen and (min-width: 641px){
  html {
    font-size: 40px !important;
  }
}
.n-layout-header{
  padding-top: 4px;
  padding-bottom: 3px;
}
.n-avatar{
  padding-top: 12px;
}
.n-button{
  padding-top: 12px;
  padding-bottom: 14px;
}
.n-button:focus{
  border: transparent;
}
.n-switch{
  padding-top: 15px;
}
#headerIco{
  padding-top: 0.6rem;
  /*width:  1.1rem;*/
}
#headerIco:hover{
  cursor: pointer;
}
</style>
