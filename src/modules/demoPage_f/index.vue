<template>
	<div>
	<el-tabs type="border-card">
      <el-tab-pane>
        <span slot="label"><i class="el-icon-date"></i> 我的行程</span>
        <!------------------------------------------------------------>
            <el-form ref="form" :model="form" label-width="80px">
            	
                <el-form-item label="活动名称">
                    <el-input v-model="form.name"></el-input>
                </el-form-item>
                
                <el-form-item label="活动区域">
                    <el-select v-model="form.region" placeholder="请选择活动区域">
                        <el-option label="区域一" value="shanghai"></el-option>
                        <el-option label="区域二" value="beijing"></el-option>
                    </el-select>
                </el-form-item>
                
                <el-form-item label="活动时间">
                    <el-col :span="11">
                        <el-date-picker type="date" placeholder="选择日期" v-model="form.date1" style="width: 100%;"></el-date-picker>
                    </el-col>
                    <el-col class="line" :span="2">-</el-col>
                    <el-col :span="11">
                        <el-time-picker type="fixed-time" placeholder="选择时间" v-model="form.date2" style="width: 100%;"></el-time-picker>
                    </el-col>
                </el-form-item>
                
                
                <el-form-item label="即时配送">
                    <el-switch on-text="" off-text="" v-model="form.delivery"></el-switch>
                </el-form-item>
                
                <el-form-item label="活动性质">
                    <el-checkbox-group v-model="form.type">
                        <el-checkbox label="美食/餐厅线上活动" name="type"></el-checkbox>
                        <el-checkbox label="地推活动" name="type"></el-checkbox>
                        <el-checkbox label="线下主题活动" name="type"></el-checkbox>
                        <el-checkbox label="单纯品牌曝光" name="type"></el-checkbox>
                    </el-checkbox-group>
                </el-form-item>
                
                
                <el-form-item label="特殊资源">
                    <el-radio-group v-model="form.resource">
                    <el-radio label="线上品牌商赞助"></el-radio>
                    <el-radio label="线下场地免费"></el-radio>
                    </el-radio-group>
                </el-form-item>
                
                
                <el-form-item label="活动形式">
                    <el-input type="textarea" v-model="form.desc"></el-input>
                    </el-form-item>
                    <el-form-item>
                    <el-button type="primary" @click="onSubmit">立即创建</el-button>
                    <el-button>取消</el-button>
                </el-form-item>
                
            </el-form>
        <!------------------------------------------------------------>
      </el-tab-pane>
      <el-tab-pane label="消息中心">消息中心</el-tab-pane>
      <el-tab-pane label="角色管理">角色管理</el-tab-pane>
      <el-tab-pane label="定时任务补偿">定时任务补偿</el-tab-pane>
   </el-tabs>
  </div>
</template>

<style>
  .el-table .info-row {
    background: #c9e5f5;
  }

  .el-table .positive-row {
    background: #e2f0e4;
  }
</style>

<script>
  import jquery from 'jquery'
  export default {
    data() {
      return {
      	 form: {
          name: '',
          region: '',
          date1: '',
          date2: '',
          delivery: false,
          type: [],
          resource: '',
          desc: ''
        }
       }
     },
    methods: {
      onSubmit(){
      	
      	//alert("submit");
      	
      	var jsonObj={
      		name:'',
      		region:'',
      		data1:'',
      		data2:'',
      		delivery:'',
      		resource:'',
      		desc:''
      	}
      	
      	jsonObj.name=this.form.name;
      	jsonObj.region=this.form.region;
      	jsonObj.data1=this.form.date1;
      	jsonObj.data2=this.form.date2;
      	jsonObj.delivery=this.form.delivery;
      	jsonObj.resource=this.form.resource;
      	jsonObj.desc=this.form.desc;
      	
      	//var str=this.form.name+this.form.region+this.form.date1+this.form.date2+this.form.delivery+this.form.resource+this.form.desc;
      	
      	console.log(jsonObj);
      	
      	var str=JSON.stringify(jsonObj);
      	
      	console.log("the data post:"+ str);
      	
      	this.$http({
      		method:'post',
      		url:'/mobile/edit/',
      		data:str,
      		header:{"X-Request-Width":"XMLHttpRequest"}
      	}).then(function(response){
      		this.posts=response.data;
      	},function(error){
      		alert("插入数据失败");
      	})

      	
      	
      }
    }
  }
</script>