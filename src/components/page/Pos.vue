<template>
	<div class="pos">
		<div>
			<el-row>
				<el-col :span="7">
					<el-tabs v-model="activeName">
						<el-tab-pane label="点餐" name="first">
							<el-table :data="foodListData" border style="width: 100%">
								<el-table-column prop="name" label="商品名字">
								</el-table-column>
								<el-table-column prop="num" label="量" width="50">
								</el-table-column>
								<el-table-column prop="money" label="金额" width="70">
								</el-table-column>
								<el-table-column label="操作" width="100">
									<template scope="scope">
										<el-button type="text" size="small">查看</el-button>
										<el-button type="text" size="small">编辑</el-button>
									</template>
								</el-table-column>
							</el-table>
							<div class="block">
								<span class="wrapper">
                                    <el-button type="warning">挂单</el-button>
                                    <el-button type="danger">删除</el-button>
                                    <el-button type="info">结账</el-button>
                                 </span>
							</div>
						</el-tab-pane>
						<el-tab-pane label="挂单" name="second">挂单</el-tab-pane>
						<el-tab-pane label="外卖" name="third">外卖</el-tab-pane>
					</el-tabs>
				</el-col>
				<!--商品展示-->
				<el-col :span="17">
					<div class="often-foods">
						<div class="often-title">
							常用商品
						</div>
						<div class="often-list">
							<ul>
								<li v-for="item in oftenGoods" @click="addOrderList(goods)"> 
									<span>{{item.goodsName}}</span>
									<span>￥{{item.price}}元</span>
								</li>

							</ul>
						</div>
						<div class="goods-type">
							<el-tabs v-model="activeNameSecond">
								<el-tab-pane label="汉堡" name="first" class="list-css">
									<ul>
										<li v-for="item in typeFoodData.typeFoodHamburger">
											<div class="type-detail">
												<img :src='item.goodsImg' alt="" />
												<p>{{item.goodsName}}</p>
												<p>￥{{item.price}}元</p>
											</div>
										</li>
									</ul>
								</el-tab-pane>
								<el-tab-pane label="小吃" name="second" class="list-css">
									<ul>
										<li v-for="item in typeFoodData.typeFoodSnack">
											<div class="type-detail">
												<img :src='item.goodsImg' alt="" />
												<p>{{item.goodsName}}</p>
												<p>￥{{item.price}}元</p>
											</div>
										</li>
									</ul>

								</el-tab-pane>
								<el-tab-pane label="饮料" name="third" class="list-css">
									<ul>
										<li v-for="item in typeFoodData.typeFoodDrink">
											<div class="type-detail">
												<img :src='item.goodsImg' alt="" />
												<p>{{item.goodsName}}</p>
												<p>￥{{item.price}}元</p>
											</div>
										</li>
									</ul>
								</el-tab-pane>
								<el-tab-pane label="套餐" name="fourth" class="list-css">
									<ul>
										<li v-for="item in typeFoodData.typeFoodMeal">
											<div class="type-detail">
												<img :src='item.goodsImg' alt="" />
												<p>{{item.goodsName}}</p>
												<p>￥{{item.price}}元</p>
											</div>
										</li>
									</ul>
								</el-tab-pane>
							</el-tabs>
						</div>
					</div>
				</el-col>
			</el-row>
		</div>
	</div>
</template>

<script>
	import axios from 'axios';
	let typeFoodHamburger,
		typeFoodSnack,
		typeFoodDrink,
		typeFoodMeal;
	export default {
		name: "Pos",
		data() {
			return {
				
				activeName: 'first',
				activeNameSecond: "first",
				foodListData: [
//				{
//						name: '汉堡包',
//						num: 3,
//						money: 23
//					},
//					{
//						name: '汽水',
//						num: 8,
//						money: 3.5
//					},
//					{
//						name: '香辣鸡翅',
//						num: 1,
//						money: 16
//					},
//					{
//						name: '香辣鸡腿堡',
//						num: 2,
//						money: 36
//					}
				],
				oftenGoods: [
					//				{
					//						goodsId: 1,
					//						goodsName: '香辣鸡腿堡',
					//						price: 18
					//					}, {
					//						goodsId: 2,
					//						goodsName: '田园鸡腿堡',
					//						price: 15
					//					}, {
					//						goodsId: 3,
					//						goodsName: '和风汉堡',
					//						price: 15
					//					}, {
					//						goodsId: 4,
					//						goodsName: '快乐全家桶',
					//						price: 80
					//					}, {
					//						goodsId: 5,
					//						goodsName: '脆皮炸鸡腿',
					//						price: 10
					//					}, {
					//						goodsId: 6,
					//						goodsName: '魔法鸡块',
					//						price: 20
					//					}, {
					//						goodsId: 7,
					//						goodsName: '可乐大杯',
					//						price: 10
					//					}, {
					//						goodsId: 8,
					//						goodsName: '雪顶咖啡',
					//						price: 18
					//					}, {
					//						goodsId: 9,
					//						goodsName: '大块鸡米花',
					//						price: 15
					//					}, {
					//						goodsId: 20,
					//						goodsName: '香脆鸡柳',
					//						price: 17
					//					}

				],
				typeFoodData: [
					typeFoodHamburger,
					typeFoodSnack,
					typeFoodDrink,
					typeFoodMeal
					//					{
					//						goodsId: 1,
					//						goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
					//						goodsName: '香辣鸡腿堡',
					//						price: 18
					//					}, {
					//						goodsId: 2,
					//						goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
					//						goodsName: '田园鸡腿堡',
					//						price: 15
					//					}, {
					//						goodsId: 3,
					//						goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
					//						goodsName: '和风汉堡',
					//						price: 15
					//					}, {
					//						goodsId: 4,
					//						goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
					//						goodsName: '快乐全家桶',
					//						price: 80
					//					}, {
					//						goodsId: 5,
					//						goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
					//						goodsName: '脆皮炸鸡腿',
					//						price: 10
					//					}, {
					//						goodsId: 6,
					//						goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
					//						goodsName: '魔法鸡块',
					//						price: 20
					//					}, {
					//						goodsId: 7,
					//						goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
					//						goodsName: '可乐大杯',
					//						price: 10
					//					}, {
					//						goodsId: 8,
					//						goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
					//						goodsName: '雪顶咖啡',
					//						price: 18
					//					}, {
					//						goodsId: 9,
					//						goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
					//						goodsName: '大块鸡米花',
					//						price: 15
					//					}, {
					//						goodsId: 20,
					//						goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
					//						goodsName: '香脆鸡柳',
					//						price: 17
					//					}

				],
			}
		},
		methods:{
			addOrderList(goods){
				console.log(this);
				this.totalCount = 0;
				this.totalMoney = 0;
				let isHave =false;
				//判断这个商品是否存在于订单列表
				for(let i = 0;i<this.foodListData.length;i++){
					
					if(this.foodListData[i].goodsId==goods.goodsId){
						isHave = true;
					}
				}
				//根据isHave的指判断  存在++ 不存在push入数组
				if(isHave){
					let arr = this.foodListData.filter(o=>o.goodsId == goods.goodsId);
					arr[0].count++;
				}
				else{
					console.log(goods);
					let newGoods = {
						goodsId:goods.goodsId,
						goodsName:goods.goodsName,
						price:goods.price,
						count:1
					}
					this.foodListData.push(newGoods);
				}
			}
		},
		created() {	//在实例创建之后同步调用。此时实例已经结束解析选项，
			//这意味着已建立：数据绑定，计算属性，方法，watcher/事件回调。
			//但是还没有开始 DOM 编译，$el 还不存在。
		
			
			//拉取常用商品数据
			axios.post("http://jspang.com/DemoApi/oftenGoods.php")
				.then(response => {
					console.log(response);
					this.oftenGoods = response.data;
				})
				.catch(error => {
					console.log(error);
				});
			//拉取分类商品数据
			axios.post("http://jspang.com/DemoApi/typeGoods.php")
				.then(response => {
					console.log(response);
					this.typeFoodData.typeFoodHamburger = response.data[0];
					this.typeFoodData.typeFoodSnack = response.data[1];
					this.typeFoodData.typeFoodDrink = response.data[2];
					this.typeFoodData.typeFoodMeal = response.data[3];
				})
				.catch(error => {
					console.log();
				})
		},
		

	}
</script>
<style>
	.pos {
		float: left;
		width: 95%;
		overflow: hidden;
	}
	
	.block {
		margin-top: 18px;
	}
	
	.often-foods {
		width: 100%;
		height: 100%;
		border: 1px solid #ddd;
	}
	
	.often-title {
		text-align: left;
		font-size: 15px;
		padding: 9px;
		height: 20px;
		border: 1px solid #ddd;
	}
	
	.often-list {
		margin-bottom: 30px;
	}
	
	.often-list ul {
		margin-top: 20px;
		margin-left: 8px;
		width: 98%;
	}
	
	.often-list li {
		float: left;
		padding: 8px;
		border: 1px solid #ccc;
		margin-left: 26px;
		margin-top: 20px;
		
	}
	
	.often-list li span:last-child {
		color: #FFA500;
	}
	
	.goods-type .type-detail {
		width: 160px;
		border: 1px solid #ccc;
		overflow: hidden;
	}
	
	.type-detail img {
		width: 55px;
		height: 50px;
		float: left;
	}
	
	.type-detail p:nth-child(2) {
		color: #FFA500;
		padding-bottom: 5px;
	}
	
	.goods-type .list-css li {
		float: left;
		padding: 23px;
	}
</style>