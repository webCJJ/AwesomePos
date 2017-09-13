<template>
	<div class="pos">
		<div>
			<el-row>
				<el-col :span="7">
					<el-tabs v-model="activeName">
						<el-tab-pane label="点餐" name="first">
							<el-table :data="foodData" border style="width: 100%">
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
								<li v-for="item in oftenGoods">
									<span>{{item.goodsName}}</span>
									<span>￥{{item.price}}元</span>
								</li>

							</ul>
						</div>
						<div class="goods-type">
							<el-tabs v-model="activeNameSecond" @tab-click="handleClick">
								<el-tab-pane   label="汉堡" name="first">
									<ul>
										<li>
											<div class="type-detail">
												<img src="" alt="" />
											</div>
										</li>
									</ul>
								</el-tab-pane>
								<el-tab-pane   label="小吃" name="second">小吃</el-tab-pane>
								<el-tab-pane   label="饮料" name="third">饮料</el-tab-pane>
								<el-tab-pane   label="套餐" name="fourth">套餐</el-tab-pane>
							</el-tabs>
						</div>
					</div>
				</el-col>
			</el-row>
		</div>
	</div>
</template>

<script>
	export default {
		name: "Pos",
		data() {
			return {
				activeName: 'first',
				activeNameSecond:"first",
				foodData: [{
						name: '汉堡包',
						num: 3,
						money: 23
					},
					{
						name: '汽水',
						num: 8,
						money: 3.5
					},
					{
						name: '香辣鸡翅',
						num: 1,
						money: 16
					},
					{
						name: '香辣鸡腿堡',
						num: 2,
						money: 36
					}
				],
				oftenGoods: [{
						goodsId: 1,
						goodsName: '香辣鸡腿堡',
						price: 18
					}, {
						goodsId: 2,
						goodsName: '田园鸡腿堡',
						price: 15
					}, {
						goodsId: 3,
						goodsName: '和风汉堡',
						price: 15
					}, {
						goodsId: 4,
						goodsName: '快乐全家桶',
						price: 80
					}, {
						goodsId: 5,
						goodsName: '脆皮炸鸡腿',
						price: 10
					}, {
						goodsId: 6,
						goodsName: '魔法鸡块',
						price: 20
					}, {
						goodsId: 7,
						goodsName: '可乐大杯',
						price: 10
					}, {
						goodsId: 8,
						goodsName: '雪顶咖啡',
						price: 18
					}, {
						goodsId: 9,
						goodsName: '大块鸡米花',
						price: 15
					}, {
						goodsId: 20,
						goodsName: '香脆鸡柳',
						price: 17
					}

				]
			}
		}

	}
</script>
<style>
	.pos {
		float: left;
		width: 95%;
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
		color: orange;
	}
</style>