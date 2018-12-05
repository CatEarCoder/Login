<template>
  <div class="hello">
  	<div v-bind:class="{lockbox:true,'active':isBlock,'open':isOpen}"><i class="lock"></i></div>
  	<ul class="iconlist" v-show="!isOpen">
  		<li class="key_icon icon1" id="A" @touchstart="drag($event)"><i></i><p>管理员</p></li>
  		<li class="key_icon icon2" id="B" @touchstart="drag($event)"><i></i><p>企业</p></li>
  		<li class="key_icon icon3" id="C" @touchstart="drag($event)"><i></i><p>用户</p></li>
  	</ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      positionY:0,
      positionX:0,
      isBlock:false,
      isOpen:false,
      t:null
    }
  },
  methods:{
  	drag(e){
  		let oDiv = e.target;
  		let that = this;
  		this.t = oDiv.id;
  		
      document.body.ontouchmove = function (e) {
      	e.preventDefault();
        var l = e.touches[0].clientX;
        var t = e.touches[0].clientY; 
        if(l>=oDiv.offsetWidth/2&&l<=(document.body.clientWidth-oDiv.offsetWidth/2)){
        	oDiv.style.left = l - 25  + 'px';
        }
        if(t>=oDiv.offsetHeight/2&&t<=(document.body.clientHeight-oDiv.offsetHeight/2)){
        	oDiv.style.top = t - 25  + 'px';
        } 
        that.checkDrop(oDiv);
      };
      document.body.ontouchend = function () {
      	
      	if(that.isBlock){
      		that.skip();
      	}
      	else{
      		oDiv.style = null;
      		that.isBlock = false;
      	}
      	 
        document.body.ontouchmove = null;
        document.body.ontouchend = null;
      };
  	},
  	checkDrop(e){
  		let l1 = parseInt(e.style.left);
  		let t1 = parseInt(e.style.top);
  		
  		let l2 = document.getElementsByClassName("lockbox")[0].offsetLeft;
  		let t2 = document.getElementsByClassName("lockbox")[0].offsetTop;
  		
  		let r1 = e.offsetWidth/2;
  		
  		let r2 = document.getElementsByClassName("lockbox")[0].offsetWidth/2;

 			if(Math.sqrt(Math.pow(t1 - t2, 2) + Math.pow(l1 - l2, 2)) <= r1+r2){
 				this.isBlock = true;
 				console.log("你撞我了！再撞一个试试！")
 			}
 			else{
 				this.isBlock = false;
 			}
  	},
  	skip(){
  		 this.isOpen = true;
  		 this.$router.push({path:'/result',query:{result:this.t}});
  	},
  	allowDrop(e){
  		
  	}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello{
	width:100%;
	height:100vh;
	background-color: #f1ec9e;
	background-image: url(../assets/bg.png);
	background-size:auto 100%;
	position: relative;
	font-size: 16px;
	background-position: left;
	overflow: hidden;
}
.hello:after{
	content:'';
	width:100%;
	height: 100vh;
	background-color: rgba(256,256,256,0.7);
	position:absolute;
	z-index:2;
	top:0;
	left: 0;
}
.lockbox{
	position:absolute;
	z-index:3;
	width:80px;
	height:80px;
	top:50%;
	left: 50%;
	margin:-40px -40px;
	border: 2px #707070 solid;
	border-radius: 80px;
}
.lockbox .lock{
	display: block;
	width:50px;
	height:50px;
	margin:15px;
	background-image: url(../assets/lock.png);
	background-size:auto 100%;
	pointer-events: none;
}
.lockbox.active{
	box-shadow: 0 0 20px rgba(47, 85, 130, 0.7);
}
.lockbox.active .lock{
	background-image: url(../assets/no_locked.png);
}
.lockbox.open{
	box-shadow: 0 0 20px rgba(47, 85, 130, 0.7);
}
.lockbox.open .lock{
	background-image: url(../assets/no_locked.png);
}

.iconlist{
	position:absolute;
	z-index:4;
	list-style: none;
}
.iconlist li{
	position:absolute;
	
	width:60px;
	height:60px;
	text-align: center;
	font-size: 12px;
	line-height: 25px;
	color:#707070; 
	border: 2px #707070 solid;
	border-radius: 100%;
}
.iconlist li i{
	width:30px;
	height: 30px;
	background-size: contain;
	background-image: url(../assets/key1.png);
	background-position: center ;
	display: block;
	margin:0 auto;
	margin-top:5px;
	pointer-events: none;
}
.iconlist li p{
	pointer-events: none;
	-webkit-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;
}
.iconlist li.icon1{
	left:calc((50vw - 84px)/2);
	top:calc(50vh + 25px + 30px);
}
.iconlist li.icon2{
	left:calc(50vw - 32px);
	top:calc(50vh - 64px - 55px - 30px);
}
.iconlist li.icon3{
	left:calc((100vw + 84px + 70px)/2);
	top:calc(50vh + 25px + 30px);
}
</style>
