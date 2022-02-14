<template>
  <div class="home">
    <!-- 機種詳細 -->
    <div class="phone_state" :style="{display:phone_state_display}">
      <div class="phone_state_border">
        <div>
          <h2>機種名：{{state_phone_name}}（{{state_phone_type}}）</h2>
          <h3>対応キャリア：{{state_phone_career}}</h3>
          <img class="state_img" :src="state_phone_img"/>
          <div class="tables">
            <div class="phone_specs">
              <table>
                <tr>
                  <td>OS</td>
                  <td>{{phone_OS}}</td>
                </tr>
                <tr>
                  <td>対応バージョン</td>
                  <td>{{phone_Max_OS}}</td>
                </tr>
                <tr>
                  <td>メモリ</td>
                  <td>{{phone_ram}}GB</td>
                </tr>
                <tr>
                  <td>ストレージ</td>
                  <td>{{phone_rom}}GB</td>
                </tr>
              </table>
            </div>

    <!-- アプリ対応状況 -->
            <div class="app_available">
              <table class="app_ava_table">
                <tr>
                  <td><img class="app_icon" src="../icon/LINE_icon.png"></td>
                  <td><img class="app_icon" src="../icon/Slack_icon.jpg"></td>
                  <td><img class="app_icon" src="../icon/ZOOM_icon.jpg"></td>
                </tr>
                <tr>
                  <td>{{LINE_ava}}</td>
                  <td>{{Slack_ava}}</td>
                  <td>{{ZOOM_ava}}</td>
                </tr>
              </table>
              <table class="app_ava_table2">
                <tr>
                  <td><img class="app_icon" src="../icon/Twitter_icon.jpg"></td>
                  <td><img class="app_icon" src="../icon/Instagram_icon.jpg"></td>
                  <td><img class="app_icon" src="../icon/FaceBook_icon.png"></td>
                  <td><img class="app_icon" src="../icon/TikToc_icon.png"></td>
                </tr>
                <tr>
                  <td>{{Twitter_ava}}</td>
                  <td>{{Instagram_ava}}</td>
                  <td>{{FaceBook_ava}}</td>
                  <td>{{TikToc_ava}}</td>
                </tr>
              </table>
            </div>
          </div>

          <h2>ID：{{state_phone_s_id}}</h2>
        </div>
        <button @click="close_state">閉じる</button>
      </div>
    </div>

    <!-- 端末一覧 -->
    <div class="list_contents" v-for="used_phone in used_phone_list" :key="used_phone.id">
      <button class="list_contents_button" @click="open_state(used_phone)">
        <h2 class="phone_name">{{used_phone.name}}</h2>
        <h2>{{used_phone.s_id}}</h2>
        <h2 class="career_icon">{{used_phone.career}}</h2>
      </button>
    </div>
  </div>
</template>

<script>
import {ref} from 'vue'

export default {
  name: 'Home',
  setup(){
    // let CSV = ref()

    let career_list = ref([
      {name:"au", color:"orange"},
      {name:"Docomo", color:"brown"},
      {name:"SoftBank", color:"white"}
    ])

    let used_phone_list = ref([
      {maker:"SONY", name:"Xperia XZ Premium", type:"SO-04J",career:"au", rom:"64", ram:"4",OS:"Android",Max_OS:9,img:"SO-04J.jpeg", s_id:"SSK600"},
      {maker:"Apple", name:"iPhone 6", type:"A1586",career:"SoftBank", rom:"64", ram:"1",OS:"iOS",Max_OS:12.5,img:"iPhone6.jpeg", s_id:"SSK100"},
      {name:"iPhone 5s", type:"A1586",career:"Docomo", rom:"64", ram:"1",OS:"12",img:"none", s_id:"SSK100"},
      {name:"iPhone 4s", type:"A1586",career:"SIMフリー", rom:"64", ram:"1",img:"none", s_id:"SSK100"},
      {name:"iPhone 3Gs", type:"A1586",career:"SoftBank", rom:"64",ram:"1",img:"none", s_id:"SSK100"},
    ])

    let app_version = ref([
      {name:"LINE", iOS_limit:13, And_limit:7.0, ava:"LINE_ava.value"},
      {name:"Slack", iOS_limit:14, And_limit:8},
      {name:"ZOOM", iOS_limit:13, And_limit:5.0},
      {name:"Twitter", iOS_limit:7.35, And_limit:7.93},
      {name:"Instagram", iOS_limit:12, And_limit:2.2},
      {name:"FacaBook", iOS_limit:12.4, And_limit:5.0},
      {name:"TikToc", iOS_limit:13, And_limit:5.0},
    ])

    // let phone_specs = ref([
    //   {name:"Xperia XZ Premium", OS:"Android", Max_OS:"9.0", ram:"4",rom:"64"},
    //   {name:"Xperia XZ Premium", OS:"Android", Max_OS:"9.0", ram:"4",rom:"64"}
    // ])

    let state_phone_name = ref()
    let state_phone_type = ref()
    let state_phone_career = ref()
    let state_phone_img =ref()
    let state_phone_s_id = ref()

    // アプリ使用可否
    let LINE_ava = ref()
    let Slack_ava = ref()
    let ZOOM_ava = ref()

    let Twitter_ava = ref()
    let Instagram_ava =ref()
    let FaceBook_ava = ref()
    let TikToc_ava =ref()

    // スペック表
    let phone_OS = ref()
    let phone_Max_OS = ref()
    let phone_ram = ref()
    let phone_rom = ref()


    // 表示ステータス
    let phone_state_display = ref("none")

    const open_state=(item)=>{
      state_phone_name.value = item.name;
      state_phone_type.value = item.type;
      state_phone_career.value = item.career;
      if(item.img != "none"){
        state_phone_img.value = require("../img/" + item.img);
      }else{
        state_phone_img.value = require("../img/no-image.png");
      }
      state_phone_s_id.value = item.s_id;
      phone_OS.value = item.OS;
      phone_Max_OS.value = item.Max_OS;
      phone_ram.value = item.ram;
      phone_rom.value = item.rom;
      app_available();
      phone_state_display.value = "block";
    }

    const close_state=()=>{
      state_phone_name.value = "";
      state_phone_type.value = "";
      state_phone_career.value = "";
      state_phone_img.value = "";
      state_phone_s_id.value = "";
      phone_OS.value = "";
      phone_Max_OS.value = "";
      phone_ram.value = "";
      phone_rom.value = "";
      phone_state_display.value = "none";
    }

    const app_available=()=>{
      if(phone_OS.value == "iOS"){
        // iOS
        if(phone_Max_OS.value<app_version.value[0].iOS_limit){
          LINE_ava.value = "×";
        }else{
          LINE_ava.value = "◯"
        }

        if(phone_Max_OS.value<app_version.value[1].iOS_limit){
          Slack_ava.value = "×";
        }else{
          Slack_ava.value = "◯"
        }

        if(phone_Max_OS.value<app_version.value[2].iOS_limit){
          ZOOM_ava.value = "×";
        }else{
          ZOOM_ava.value = "◯"
        }

        if(phone_Max_OS.value<app_version.value[3].iOS_limit){
          Twitter_ava.value = "×";
        }else{
          Twitter_ava.value = "◯"
        }

        if(phone_Max_OS.value<app_version.value[4].iOS_limit){
          Instagram_ava.value = "×";
        }else{
          Instagram_ava.value = "◯"
        }

        if(phone_Max_OS.value<app_version.value[5].iOS_limit){
          FaceBook_ava.value = "×";
        }else{
          FaceBook_ava.value = "◯"
        }

        if(phone_Max_OS.value<app_version.value[6].iOS_limit){
          TikToc_ava.value = "×";
        }else{
          TikToc_ava.value = "◯"
        }

      }else{
        // Android
        if(phone_Max_OS.value<app_version.value[0].And_limit){
          LINE_ava.value = "×";
        }else{
          LINE_ava.value = "◯"
        }
        if(phone_Max_OS.value<app_version.value[1].And_limit){
          Slack_ava.value = "×";
        }else{
          Slack_ava.value = "◯"
        }
        if(phone_Max_OS.value<app_version.value[2].And_limit){
          ZOOM_ava.value = "×";
        }else{
          ZOOM_ava.value = "◯"
        }

        if(phone_Max_OS.value<app_version.value[3].And_limit){
          Twitter_ava.value = "×";
        }else{
          Twitter_ava.value = "◯"
        }

        if(phone_Max_OS.value<app_version.value[4].And_limit){
          Instagram_ava.value = "×";
        }else{
          Instagram_ava.value = "◯"
        }

        if(phone_Max_OS.value<app_version.value[5].And_limit){
          FaceBook_ava.value = "×";
        }else{
          FaceBook_ava.value = "◯"
        }

        if(phone_Max_OS.value<app_version.value[6].And_limit){
          TikToc_ava.value = "×";
        }else{
          TikToc_ava.value = "◯"
        }
      }
    }

    return{
      used_phone_list,
      app_version,
      // phone_specs,
      career_list,
      state_phone_name,
      state_phone_type,
      state_phone_career,
      state_phone_img,
      state_phone_s_id,

      LINE_ava,
      Slack_ava,
      ZOOM_ava,

      Twitter_ava,
      Instagram_ava,
      FaceBook_ava,
      TikToc_ava,

      phone_OS,
      phone_Max_OS,
      phone_ram,
      phone_rom,

      phone_state_display,

      open_state,
      close_state,
      // search_spec,
      app_available,
      // open_file,
    }
  }
}
</script>

<style>
  .phone_state{
    position:fixed;
    width:100%;
    top:0px;
  }

  .phone_state_border{
    border:solid 2px;
    border-radius:10px;
    height:600px;
    margin:50px;
    background-color:rgb(255, 255, 255);
  }

  .list_contents{
    margin-bottom:20px;
    display:inline-block;
    padding-left:30px;
    padding-right:30px;
  }

  .list_contents_button{
    width:280px;
    border:solid 3px;
    border-radius:10px
  }

  .phone_name{
    font-size:25px;
  }

  .career_icon{
    border:solid 2px;
    border-radius:10px;
    width:100px;
    margin:0 auto;
    padding:2px;
  }

  .state_img{
    max-width:300px;
    min-width:100px;
    width:100%;
  }

  .app_icon{
    max-width:50px;
    min-width:20px;
    width:100%;
  }

  .tables{
    padding-top:50px;
    padding-right:50px;
    float:right;
  }

  .app_available{
    padding-top:20px;
  }

  .app_ava_table{
    margin-bottom:20px;
  }

  .app_ava_table2{
    padding-top:5px;
  }

  table{
    border:2px solid;
    border-collapse: collapse;
    margin:auto;
    position:float;
  }
  
  th,td{
    border:1px black solid;
  }

  .career_icon{
    margin-bottom:10px;
  }
</style>