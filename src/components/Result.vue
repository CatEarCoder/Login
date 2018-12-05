<template>
  <div class="result">
  
 	<div class="loginbox">
 		<p class="welcome">Welcome，{{ result == 'A'?'管理员':result=='B'?'企业用户':'用户' }}</p>
 		<input type="text" v-model="username" placeholder="Username"/>
 		<input type="password" v-model="pwd"  placeholder="Password"/>
 		<input type="submit" value="Sign In" @click="sub"/>
 	</div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      result:"",
      username:"",
      pwd:""
    }
  },
  methods:{
 		sub(){
 			if(this.username==""){
 				return false;
 			}
 			if(this.pwd==""){
 				return false;
 			}
 		}
  },
  mounted(){
  	this.result = this.$route.query.result;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.result{
	width:100%;
	height:100vh;
	overflow: hidden;
	font-size: 20px;
	/*background-image: -webkit-linear-gradient(135deg,#3577cd , #69cab7); */
	background-image: url(../assets/bg.png);
	background-size: auto 100%;
	background-position: left;
}

.loginbox{
	width:80%;
	height:auto;
	overflow: hidden;
	margin: 0 auto;
	position: absolute;
	top:50%;
	left: 50%;
	transform: translate(-50%,-50%);
}
.welcome{
	font-size: 20px;
	line-height: 55px;
	overflow: hidden;
	color:white;
	margin-block-start: 0;
  margin-block-end: 0;
  margin-bottom:50px;
}
input[type=text]{
	width: 100%;
  padding: 15px 10px;
  box-sizing: border-box;
  color: #283440;
  font-size: 16px;
  outline: none;
  font-weight: 500;
 	border-radius: 10px;
 	border:none;
 	background-color:rgba(256,256,256,0.5);
 	color:white;
}
input[type=password]{
	width: 100%;
	box-sizing: border-box;
  padding: 15px 10px;
  color: #283440;
  font-size: 16px;
  outline: none;
  font-weight: 500;
  border: none;
 	border-radius: 10px;
 	margin-top:20px;
 	background-color:rgba(256,256,256,0.5);
 	color:white;
}
::-webkit-input-placeholder {
  color: #dcdcdc;
}
::-webkit-input-placeholder { /* WebKit, Blink, Edge */
  color:#dcdcdc;
}
:-moz-placeholder { /* Mozilla Firefox 4 to 18 */
  color:#dcdcdc;
}
::-moz-placeholder { /* Mozilla Firefox 19+ */
  color:#dcdcdc;
}
:-ms-input-placeholder { /* Internet Explorer 10-11 */
  color:#dcdcdc;
}
input[type=submit]{
	width: 100%;
	height:48px;
	line-height: 48px;
	overflow: hidden;
  
  color: #283440;
  font-size: 16px;
  outline: none;
  font-weight: 500;
  border: none;
 	border-radius: 10px;
 	margin-top:50px;
 	background-color:rgba(256,256,256,0.5);
 	color:white;
}
</style>
