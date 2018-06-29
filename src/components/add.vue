<template>
  <div class="add container">
  	<h1 class="page-header">添加用户</h1>
  	<form v-on:submit="addCustomer">
  		<div class="well">
  			<h4>用户信息</h4>
  			<div class="form-group">
  				<label>姓名</label>
  				<input type="text" v-model="customer.name" class="form-control" placeholder="name">
  			</div>
  			<div class="form-group">
  				<label>电话</label>
  				<input type="text" v-model="customer.phone" class="form-control" placeholder="phone">
  			</div>
  			<div class="form-group">
  				<label>邮箱</label>
  				<input type="text" v-model="customer.email" class="form-control" placeholder="email">
  			</div>
  			<div class="form-group">
  				<label>学历</label>
  				<input type="text" v-model="customer.education" class="form-control" placeholder="education">
  			</div>
  			<div class="form-group">
  				<label>毕业学校</label>
  				<input type="text" v-model="customer.graduationschool" class="form-control" placeholder="graduationschool">
  			</div>
  			<div class="form-group">
  				<label>职业</label>
  				<input type="text" v-model="customer.profession" class="form-control" placeholder="profession">
  			</div>
  			<div class="form-group">
  				<label>个人简介</label>
  				<textarea rows="10" v-model="customer.profile" placeholder="profile" class="form-control"></textarea>
  			</div>
  			<button type="submit" class="btn btn-primary">添加</button>
  		</div>
  	</form>
  </div>
</template>

<script>
export default {
  name: 'add',
  data () {
    return {
      customer:{
      }
    }
  },
  methods:{
  	addCustomer(e){
  		if(!this.customer.name){
  			alert("请将姓名填写完整！");
  		}else if(!this.customer.phone){
  			alert("请将电话填写完整！");
  		}else if(!this.customer.email){
  			alert("请将邮箱填写完整！");
  		}else{
  			var newCustomer = {
  				name:this.customer.name,
  				phone:this.customer.phone,
  				email:this.customer.email,
  				education:this.customer.education,
  				graduationschool:this.customer.graduationschool,
  				profession:this.customer.profession,
  				profile:this.customer.profile
  			}
  			this.$http.post("http://localhost:3000/users",newCustomer)
  			.then(function(response){
  				/*console.log(response);*/
  				this.$router.push({path:"/",query:{alert:"用户信息添加成功"}});
  			})
  			e.preventDefault();
  		}
  		e.preventDefault();
  	}
  }
}
</script>

<style scoped>

</style>