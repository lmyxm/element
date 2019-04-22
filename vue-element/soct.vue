<template>
	<div>选择地区滚动</div>
</template>

<script>
	mouseupFun:function(index){
		this.zimShow=!this.zimShow;
		var cityChoiceBox=document.getElementById('cityChoiceBox');
		var h3=cityChoiceBox.getElementsByTagName('h3');
		var timer = null;	
		function scrT(iTarget){
			clearInterval(timer);
			document.ontouchstart=function(){
				clearInterval(timer);
			}
			timer = setInterval(function(){
			var scrollT = document.documentElement.scrollTop || document.body.scrollTop,
			    speed = 0;
			speed = Math.floor((iTarget - scrollT)/5);
			if(scrollT == iTarget){
				clearInterval(timer);
				}else{
					document.documentElement.scrollTop = scrollT + speed;
					document.body.scrollTop = scrollT + speed;
					}
			},30);
		}
		scrT(h3[index].offsetTop-50);
	}
</script>

<style>
</style>
