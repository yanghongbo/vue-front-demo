<template>
	<div>
		<blog-header></blog-header>
		<hr/>
			用户名:<input type="text" v-model="registerInfo.username" placeholder="请输入用户名" />
	      	<br/>
	      	密码：<input type="password" v-model="registerInfo.password" placeholder="请输入密码" />
	      	<br/>
	      	<button v-on:click="register">注册</button>
		<hr/>
		<blog-footer></blog-footer>
	</div>
</template>

<script type="text/javascript">
import blogHeader from '@/components/common/BlogHeader.vue'
import blogFooter from '@/components/common/BlogFooter.vue'

export default {
	name: 'BlogRegister',
	components: {blogHeader,blogFooter},
	data() {
		return {
			registerInfo:{
				username:'',
				password:''
			}

		}
	},
	method: {
		register() {
			this.$axios
		        .post('/login', {
		          username: this.registerInfo.username,
		          password: this.registerInfo.password
		        })
		        .then(successResponse => {
		          this.responseResult = JSON.stringify(successResponse.data)
		          if (successResponse.data.code === 200) {
		            this.$router.replace({path: '/index'})
		          }
		        })
		        .catch(failResponse => {})
		}
	}
}
</script>