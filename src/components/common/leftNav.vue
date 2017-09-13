<template>
	<div class="left-nav">
		<ul>
			<li>
				<i class="icon iconfont icon-shouyin"></i><br>
				<i>收银</i>
			</li>
			<li>
				<i class="icon iconfont icon-dianpua"></i><br>
				<i>店铺</i>
			</li>
			<li>
				<i class="icon iconfont icon-hanbao"></i><br>
				<i>商品</i>
			</li>
			<li>
				<i class="icon iconfont icon-unie614"></i><br>
				<i>会员</i>
			</li>
			<li>
				<i class="icon iconfont icon-tubiao116"></i><br>
				<i>统计</i>
			</li>
			<li>
				<i class="icon iconfont icon-shezhi"></i><br>
				<i>设置</i>
			</li>
		</ul>
	</div>
</template>
<style>
	.left-nav {
		width: 5%;
		height: 100%;
		background-color: #20a0ff;
		color: #fff;
		float: left;
	}
	
	 ul {
		width: 100%;		
		list-style: none;
		overflow: hidden;
	}
	
	.left-nav li {
		list-style: none;
		padding-bottom: 15px;
		padding-top: 15px;
	}
	
	.left-nav li i {
		font-style: inherit;
	}
	
	.left-nav li i:last-child {
		font-size: 12px;
	}
</style>
<script>
	export default {
		name: "leftNav",
		data() {
			return {}
		}

	}
</script>