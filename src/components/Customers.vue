<template>
  <div class="customers container">
  	<alert v-bind:message="alert" v-if="alert"></alert>
    <h1 class="page-header">用户管理系统</h1>
    <input type="text" v-model="filterInput" class="from-control pull-right" placeholder="搜索">

    <table class="table table-striped">
    	<thead>
    		<tr>
    			<th>姓名</th>
    			<th>电话</th>
    			<th>邮箱</th>
    			<th></th>
    		</tr>
    	</thead>
    	<tbody>
    		<tr v-for="customer in filterBy(customers,filterInput)">
    			<td>{{ customer.name }}</td>
    			<td>{{ customer.phone }}</td>
    			<td>{{ customer.email }}</td>
    			<td><router-link class="btn btn-default" v-bind:to="'/customer/'+customer.id">详情</router-link></td>
    		</tr>
    	</tbody>
    </table>
  </div>
</template>

<script>
import alert from './alert' 
export default {
  name: 'customers',
  data () {
    return {
      customers:[],
      alert:""
    }
  },
  methods:{
  	fetchCustomer(){
  		this.$http.get("http://localhost:3000/users")
  		.then(function(response){
  			this.customers = response.body;
  		})
  	},
    filterBy(customers,value){
        return customers.filter(function(customer){
          return customer.name.match(value);
        })
    }
  
  },
  components:{
  	alert
  },
  created(){
  	if(this.$route.query.alert){
  		this.alert = this.$route.query.alert;
  	}
  	this.fetchCustomer();
  },
   updated(){
  	this.fetchCustomer();
  }
}
</script>

<style scoped>

</style>
