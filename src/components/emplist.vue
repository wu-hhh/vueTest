<template>
  <div class="hello">
    <table class="table table-bordered">
				<caption>雇员信息列表</caption>
				<thead>
					<tr>
						<th>姓名</th>
						<th>年龄</th>
						<th>性别</th>
						<th>操作</th>
					</tr>
				</thead>
				<tbody>
					<tr v-for="emp in emps">
						<td hidden="hidden">{{emp.id}} </td>
						<td>{{emp.name}}</td>
						<td>{{emp.age}}</td>
						<td>{{emp.sex}}</td>
						<td>
							<button class="btn-default btn" v-on:click="del(emp.id)">删除</button>
							<button class="btn-default btn" v-on:click="update(emp.id)">修改</button>
						</td>
					</tr>

				</tbody>
			</table>
  </div>
</template>

<script>
export default {
  name: 'emplist',
 	data(){
 		return{
 			emps:[]
 		}
 	},
 	created:function(){
 		this.loadEmp();
 	},
 	methods:{
 		loadEmp:function(){
 			this.$http.get("http://localhost:8086/emp").then(
 				function(res){
 					this.emps=res.body;
 				},
 				function(error){
 					alert("查询失败,请稍后重试!!");
 				}
 			)
 		},
 		update:function(id){
 			this.$router.push({
 				path:"/empupdate",
 				query:{
 					id:id
 				}
 			})
 		},
 		del:function(id){
 			
 			this.$http.delete("http://localhost:8086/emp",{
 				params:{
 					id:id
 				}
 			}).then(
 				function(res){
 					alert("删除成功!");
 					this.loadEmp();
 				},
 				function(error){
 					alert("删除失败！");
 				}
 			)
 		}
 	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
