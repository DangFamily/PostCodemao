<!-- 

【编程猫的邮箱】

明信片主要部分

编程猫的时光邮箱，据说可以给未来送信~（×）
基于VueJS的明信片生成DEMO（√）

2019年10月16日 18:30

 -->

<template>
  <div class="postcards" :style="carStyle">
	  <img :src="stampURL" >
      {{postContent}}
  </div>
</template>

<style scoped>
.postcards{
  position: absolute;

  background-color: #fff ;
  border-radius: 5px;
}
</style>

<script>
	export default{
    name:"postcards",
		data () {
			return {
				//浏览器窗口大小
				curWindowH: document.documentElement.clientHeight,
				curWindowW: document.documentElement.clientWidth,
				//明信片默认大小
				postSizeH: 560,
				postSizeW: 1220,
				//明信片内容样式
				postContent: "编程猫的邮箱",
				postTextSize: 20,
				postTextColor: "#5E150C",
				postBold: false,
				//明信片默认邮票
				stampURL: "https://static.codemao.cn/whale/Skcuc_dQ4?imageMogr2/thumbnail/!200x200r/blur/1x0/quality/100|imageslim",
        carStyle: {
            width: this.postSizeW + 'px;' ,
            height:  this.postSizeH + "px",
            color:  this.postTextColor ,
            font-size:  this.postTextSize,
        }
			}
		},
		computed: {
			curWindowSize() {
				const {
					curWindowH,
					curWindowW
				} = this
				return {
					curWindowH,
					curWindowW
				}
			}
		},
		watch: {			
			curWindowSize: {
				handler: function(v) {
					if(!this.timer) {
						this.curWindowH = v
						this.curWindowW = v
						this.timer = this
						let that = this
						setTimeout(function (){
							that.timer = false
						},1000) //设置延时以防被隔壁宿舍骂死慢！！！
					}
				}
			}
			
		},
		mounted () {
			this.getSizeReturn ()
		},
		methods :{
			getSizeReturn () {
				//取浏览器窗口大小
				const that = this
				window.onresize = () => {
					return (() => {
						window.curWindowH = document.documentElement.clientHeight
						that.curWindowH = window.curWindowH
						window.curWindowW = document.documentElement.clientWidth
						that.curWindowW = window.curWindowW
					})()
					/*
					if (curWindowW <= 1810 || curWindowH <= 745) {
						return (() => {
							postSizeH = curWindowW - 100
							postSizeW = curWindowW -200
						})()
						
					}
					*/
				}
			}
		}
  }
</script>
