<template>
  <div class="hello">
    <!--<form action="http://localhost:8086/upload" method="post" enctype="multipart/form-data" >
				<input type="file" name="file" />
				<input type="submit" value="提交"  />
		</form>-->
		<h1>测试修改!!!</h1>

		<h3>第三次测试修改</h3>

		<h2>第二次测试修改</h2>

		<input type="text" name="username" v-model="username"/>
		<input type="file" name="file" />
		<input type="button" value="提交"  v-on:click="upload()"/>
  </div>
</template>

<script>
export default {
  name: 'uploadtest',
  data(){
 		return{
 			username: ''
 		}
  },
 	methods:{
 		upload:function(){
 			var formData=new FormData();
 			var username=this.username;
 			formData.append("file",document.querySelector("input[name=file]").files[0]);
 			formData.append("username", username);
 			var config={
 				headers:{
 					"Content-Type":"multipart/form-data"
 				}
 			}
 			//key value key是表单中的name
 			this.$http.post("http://localhost:8086/upload",formData,config).then(
 				function(res){
 					console.log(res);
 					console.log(res.bodyText);
 					alert("上传成功!");
 					this.$router.go(0);
 				},
 				function(error){
 					console.log(error.body.message);
 				}
 			)
 		}
 	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
