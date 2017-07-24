<template>
    <div id="editor">
        <div id="nav">
            <ol class="list">
                <li v-for="i in [0,1,2,3,4,5]"
                    v-bind:class="{active:currentTab === i}" 
                    v-on:click="currentTab = i">
                    <svg class="icon">
                        <use v-bind:xlink:href="`#icon-${icons[i]}`"></use>
                    </svg>
                </li>
            </ol>
        </div>

        <ol class="panes">
            <li v-bind:class="{active: currentTab === 0}">
            <h2>个人信息</h2>

                <el-form v-bind:submit="onSubmit"><!--:label-position="labelPosition" label-width="80px" :model="profile">-->
                    <el-form-item label="姓名">
                        <el-input v-model="profile.name"></el-input>
                    </el-form-item>
                    <el-form-item label="城市">
                        <el-input v-model="profile.city"></el-input>
                    </el-form-item>
                    <el-form-item label="出生日期">
                        <el-input v-model="profile.birth"></el-input>
                    </el-form-item>
                </el-form>

            </li>
            <li v-bind:class="{active: currentTab === 1}">
            <h2>工作经历</h2>
                <el-form v-for="workHistory in workHistory">
                    <div >
                        <el-form-item label="公司名称">
                            <el-input v-model="workHistory.company"></el-input>
                        </el-form-item>               
                        <el-form-item label="工作内容">
                            <el-input type="textarea" v-model="workHistory.desc"></el-input>
                        </el-form-item>

                        <el-form-item label="开始工作">
                            <el-col :span="11">
                                <el-date-picker type="date" placeholder="选择日期" v-model="workHistory.date1" style="width: 100%;"></el-date-picker>
                            </el-col>
                        </el-form-item>
                        <el-form-item label="结束工作">
                            <el-col :span="11">
                                <el-date-picker type="date" placeholder="选择日期" v-model="workHistory.date2" style="width: 100%;"></el-date-picker>
                            </el-col>
                        </el-form-item>
                    </div>
                    <el-button type="primary" v-on:click="addworkHistory">主要按钮</el-button>                    
                </el-form>
            
            </li>
            <li v-bind:class="{active: currentTab === 2}">
            <h2>学习经历</h2>
            </li>
            <li v-bind:class="{active: currentTab === 3}">
            <h2>项目经历</h2>
            </li>
            <li v-bind:class="{active: currentTab === 4}">
            <h2>获奖证书</h2>
            </li>
            <li v-bind:class="{active: currentTab === 5}">
            <h2>联系方式</h2>
            </li>
        </ol>
    </div>
</template>

<script>
    export default {
        data(){
            return{
                currentTab: 0,
                icons: ['credentials_icon','work','book','aixin','jiangbei','dianhua'],
                labelPosition: '',
                profile: {
                    name: '',
                    city: '',
                    birth: '',
                },
                workHistory: {
                    company: '',
                    dexc: '',
                    date1: '',
                    date2: '',
                }
                
            }
        },
        methods:{
            addworkHistory(){
                this.workHistory.push({
                    company: '',
                    dexc: '',
                    date1: '',
                    date2: '',
                })
            }
        }
    }
</script>

<style>
  #editor{
      display: flex;
  }
  #nav{
      background: #000;
      width: 80px;
  }
  .list > li{
      padding: 8px 0;
      text-align: center;
  }
  .list > li.active{
      background:white;
  }
  .list > li.active >.icon{
      fill: black;
  }

  .icon{
      width: 32px;
      height: 80px;
      fill: #ddd;
      
  }

  .panes > li{
      display: none;
      padding: 32px;
  }
  .panes > li.active{
      display: block;
  }
  
</style>