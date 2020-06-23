### vue商城项目

## 制作首页App组件
1. 完成 Header 区域，使用的是 Mint-UI 中的Header组件
2. 制作底部的 Tabbar 区域，使用的是 MUI 的 Tabbar.html
 + 在制作 购物车 小图标的时候，操作会相对多一些：
 + 先把 扩展图标的 css样式，拷贝到项目中
 + 拷贝 扩展字体库 ttf文件，到项目中
 + 为 购物车 小图标，添加 如下样式'mui-icon mui-icon-extra mui-icon-extra-cart'
3. 要在中间区域放置一个router-view来展示路由匹配到的组件

## 改造 tabbar 为router-link

## 设置路由高亮
 + 高亮显示 在router.js中添加linkActiveClass:'mui-active'
 + 覆盖默认的路由高亮的类,默认的类叫router-link-active
 
## 点击tabbar中的路由链接，展示对应的路由组件

## 制作首页轮播布局

## 加载首页轮播图数据
 1. 获取数据，如何 获取数据，使用vue-resource
 2. 使用 vue-resource 的 this.$http.get 获取数据
 3. 获取到的数据，要保存到 data 身上
 4. 使用v-for 循环渲染 每个 item 项
 
 ## 改造 九宫格 区域的样式