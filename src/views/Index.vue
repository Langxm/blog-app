<template>
	<div>
		<div class="row">
			<div class="col-3" v-for="(item, index) in topics" :key="index">
				<div class="card link shadow">
					<router-link :to="{ path: '/topic/' + item.id }"><img :src="item.logo" class="logo" /></router-link>
					<p class="title">{{ item.topicName }}</p>
					<p class="sub-title">{{ item.description.slice(0, 20) }}...</p>
					<p class="meta">
						<span class="gutter">{{ item.articles }}篇文章,</span>
						<span>{{ item.follows }}人关注</span>
					</p>
				</div>
			</div>
		</div>

		<div class="row">
			<div class="col-8">
				<h3>热门文章</h3>
				<div v-for="(item, index) in articles" :key="index" class="col-12">
					<div class="media-wraaper border">
						<div class="media-left">
							<router-link :to="{ path: '/user/' + item.article.userId }">
							<img :src="item.author.avatar" class="avatar-lg link" />
							</router-link>
							<p>{{ item.author.nickname }}</p>
							<strong>来自</strong>
							<p>{{ item.topic.topicName }}</p>
						</div>
						<div class="media-middle flex flex-around flex-left">
							<router-link :to="{ path: '/article/' + item.article.id }" class="subtitle">
								 {{ item.article.title }} 
							</router-link>
							<p class="sub-title link">{{ item.article.summary }}</p>
							<p>
								<span class="meta gutter">{{ item.article.comments }}评论</span>
								<span class="meta">{{ item.article.likes }}喜欢</span>
							</p>
						</div>
						<div class="media-right"><img :src="item.article.thumbnail" alt="" /></div>
					</div>
				</div>
			</div>
			<div class="col-4">
				<div class="whitebg tuijian">
				      <h2 class="htitle">站长推荐</h2>
				     
				
				        <li><a href="http://www.downcc.com/soft/21.html" title="Macromedia Dreamweaver 8.0 简体中文正式版" target="_blank">
				          <p>1.Macromedia Dreamweaver 8.0 简体中文正式版</p>
				          </a></li>
				          <br>
				        <li><a href="http://1t.click/bsF5" title="前端面试题整理" target="_blank">
				          <p>2.前端面试题整理</p>
				          </a></li>
                            <br>
				        <li><a href="https://www.yangqq.com/news/life/2018-03-13/804.html" title="作为一个设计师,如果遭到质疑你是否能恪守自己的原则?" target="_blank">
				          <p>3.作为一个设计师,如果遭到质疑你是否能恪守自己的原则?</p>
				          </a></li>
			               <br>
				        <li><a href="http://1t.click/bsFC" title="怎么学习前端知识？" target="_blank">
				          <p>4.怎么学习前端知识？</p>
				          </a></li>
			              <br>
				        <li><a href="https://new.qq.com/omn/20180921/20180921G10LDE.html" title="【个人博客网站制作】自己不会个人博客网站制作，你会选择用什么博客程序源码？" target="_blank">
				          <p>5.【个人博客网站制作】自己不会个人博客网站制作，你会选择用什么博客程序源码？</p>
				          </a></li>
		                   <br>
				        <li><a href="http://1t.click/bsFH" title="如何快速建立自己的个人博客网站" target="_blank">
				          <p>6.如何快速建立自己的个人博客网站</p>
				          </a></li>
				
				
				      </ul>
				    </div>
					<br>
				<h3>热门作者</h3>
				<div v-for="(item, index) in users" :key="index" class="row">
					<div class="col-12 border box">
						<div class="flex-center-y">
							<router-link :to="{ path: '/user/' + item.id }">
							<img :src="item.avatar" class="avatar-xs link" />
							</router-link>
							<p class="sub-title">{{ item.nickname }}</p>
						</div>
						<div class="flex-center-y">
							<p class="meta">{{ item.fans }}个粉丝</p>
							<p class="meta">写了{{ item.articles }}篇文章</p>
						</div>
						<div class="flex-center-y"><button class="btn btn-follow">关注</button></div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			articles: [],
			users: [],
			topics: []
		};
	},
	created() {
		this.axios.get(this.GLOBAL.baseUrl + '/article').then(res => {
			// console.log(res.data.data);
			this.articles = res.data.data;
		});
		this.axios.get(this.GLOBAL.baseUrl + '/user').then(res => {
			// console.log(res.data.data);
			this.users = res.data.data;
		});
		this.axios.get(this.GLOBAL.baseUrl + '/topic').then(res => {
			// console.log(res.data.data);
			this.topics = res.data.data;
		});
	}
};
</script>

<style scoped="scoped">
.logo {
	border-top-left-radius: 5px;
	border-top-right-radius: 5px;
}
.logo:hover {
	opacity: 0.6;
}
.box {
	display: flex;
	justify-content: space-around;
	height: 70px;
	padding: 10px;
}
.btn-follow {
	background-color: #42c02e;
	font-weight: 400;
	font-size: 15px;
	color: #fff;
	padding: 5px 0;
	width: 80px;
	height: 30px;
	border-radius: 40px;
	display: inline-block;
	text-align: center;
}
.topnews {
    display: block;
    margin: 20px 0;
    background: #000;
    position: relative;
    overflow: hidden;
    border-radius: 3px;
    max-height: 110px;
}

</style>
