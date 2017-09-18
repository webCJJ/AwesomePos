<template>
	<div class="pos">
		<div>
			<el-row>
				<el-col :span="7">
					<el-tabs v-model="activeName">
						<el-tab-pane label="点餐" name="first">
							<el-table :data="foodListData" border style="width: 100%">
								<el-table-column prop="goodsName" label="商品名字">
								</el-table-column>
								<el-table-column prop="count" label="量" width="50">
								</el-table-column>
								<el-table-column prop="price" label="金额" width="70">
								</el-table-column>
								<el-table-column label="操作" width="100">
									<template scope="scope">
										<el-button type="text" size="small" >查看</el-button>
										<el-button type="text" size="small" @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
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
								<li v-for="goods in oftenGoods" @click="addOrderList(goods)"> 
									<span>{{goods.goodsName}}</span>
									<span>￥{{goods.price}}元</span>
								</li>

							</ul>
						</div>
						<div class="goods-type">
							<el-tabs v-model="activeNameSecond">
								<el-tab-pane label="汉堡" name="first" class="list-css">
									<ul>
										<li v-for="item in typeFoodData.typeFoodHamburger" @click="addOrderList(item)">
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
										<li v-for="item in typeFoodData.typeFoodSnack" @click="addOrderList(item)">
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
										<li v-for="item in typeFoodData.typeFoodDrink" @click="addOrderList(item)">
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

				],
				oftenGoods: [
					
				],
				typeFoodData: [
					typeFoodHamburger,
					typeFoodSnack,
					typeFoodDrink,
					typeFoodMeal
				

				],
			}
		},
		methods:{
			addOrderList(goods){
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
					let arr = this.foodListData.filter(function(o){
						return o.goodsId == goods.goodsId;				
					});
					arr[0].count++;
					//console.log(arr);
					//console.log(o=>o.goodsId == goods.goodsId);
				}
				else{
					let newGoods = {
						goodsId:goods.goodsId,
						goodsName:goods.goodsName,
						price:goods.price,
						count:1
					}
					this.foodListData.push(newGoods);
				//计算总价
		
				}
			},
			handleEdit(index, row){
				console.log(index);
			}
		},
		created() {	//在实例创建之后同步调用。此时实例已经结束解析选项，
			//这意味着已建立：数据绑定，计算属性，方法，watcher/事件回调。
			//但是还没有开始 DOM 编译，$el 还不存在。
		
			
			//拉取常用商品数据
			axios.post("http://jspang.com/DemoApi/oftenGoods.php")
				.then(response => {
					//console.log(response);
					this.oftenGoods = response.data;
				})
				.catch(error => {
					console.log(error);
				});
			//拉取分类商品数据
			axios.post("http://jspang.com/DemoApi/typeGoods.php")
				.then(response => {
					//console.log(response);
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