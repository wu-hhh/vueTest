<template>
  <div class="hello">
		<form class="form-horizontal" role="form">
						<div class="form-group">
							<label for="firstname" class="col-sm-1 control-label">姓名</label>
							<div class="col-sm-10">
								<input type="text" class="form-control" id="name" v-model="emp.name"  placeholder="请输入姓名">
							</div>
						</div>
						<div class="form-group">
							<label for="lastname" class="col-sm-1 control-label">年龄</label>
							<div class="col-sm-10">
								<input type="text" class="form-control" id="age" v-model="emp.age" placeholder="请输入年龄">
							</div>
						</div>
						<div class="form-group">
							<label for="lastname" class="col-sm-1 control-label">性别</label>
							<div class="col-sm-10">
								<input type="text" class="form-control" id="sex" v-model="emp.sex" placeholder="请输入性别">
							</div>
						</div>
						<div class="form-group">
							<div class="col-sm-10 col-sm-offset-1">
								<button type="button" class="btn btn-default" v-on:click="sub" >提交</button>
							</div>
						</div>
					</form>  
  </div>
</template>

<script>
export default {
  name: 'empupdate',
 	data(){
 		return{
 			emp:{
 				id:0,
 				name:'',
 				age:'',
 				sex:''
 			}
 		}
 	},
 	created:function(){
 		this.update();
 	},
 	methods:{
 		update: function(){
 			var id=this.$route.query.id;
 			this.emp.id=this.$route.query.id;
 			this.$http.get("http://localhost:8086/selectEmpById",{
 				params:{
 					id:id
 				}
 				
 			}).then(
 				function(res){
 					this.emp.name=res.body.name;
 					this.emp.age=res.body.age;
 					this.emp.sex=res.body.sex;
 					
 				},
 				function(error){
 					alert("加载数据失败!");
 				}
 			)
 		},
 		sub: function(){
 			var id=this.$route.query.id;
 			this.$http.put("http://localhost:8086/emp",{
 						id:id,
	 					name:this.emp.name,
	 					age:this.emp.age,
	 					sex:this.emp.sex
 			}).then(
 				function(res){
 					this.emp=res.body;
 					/*this.$router.push({
 						path:'/'
 					})*/
 					this.$router.go(-1);
 					alert("修改成功");
 				},
 				function(error){
 					alert("修改失败!");
 				}
 			)
 		}
 		
 	}
 	
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
