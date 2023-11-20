### 11.3日

1.梳理后端架构，业务分为需要登录token和不需要登录token两部分，moudles里面单个模块里面细分两个路由

2.解决课程查询的问题——在没有登录的接口里面要调用用户查询接口，解决办法是在课程查询接口的前面的过滤器里面验证tk，将token赋值给tk，解析token，得到用户信息

3.增加课程点赞的功能，使用Redis完成，熟悉Redis命令，记得带前缀区分业务，用户a点赞就在后端用Redis存放一个值，Redis是k，v形式存放

### 11.6日
1.安装nuxt3，练习使用naive ui组件，初步了解windi css的用法(15)

### 11.7日

1.nuxt会把app.vue作为入口点，后续的所有的路由定义都会在这里进行渲染。在 Nuxt 中，只需要遵守组件定义的规则即可。使用过程中无需导入。（15）

2.nuxt布局的使用，解决重复引入组件的麻烦，多个页面共用一个网页结构，使用 <NuxtLayout>来包裹路由着陆点 <NuxtPage/>

3.全局进度处理Loading

### 11.8日

1.自定义错误页面

2.用naive ui美化错误页面

3.增加深浅主题切换功能

### 11.9日

1.nuxt中的路由处理， 跳转路由

- 使用标签：<NuxtLink>  参考：https://nuxt.com.cn/docs/api/components/nuxt-link

- a链接，注意避免a链接嵌套

- js的方式:  navigateTo   参考：https://nuxt.com.cn/docs/api/utils/navigate-to

  

2.状态管理router-参数的处理 

- query参数
- params参数

### 11.10日

1.nuxt中composables目录内的文件函数全局化可调用，函数名必须使用use前缀才生效（17）

2.解决状态管理数据因F5刷新或者右键刷新丢失的问题

使用路由拦截和异步请求结合解决：在用户刷新的时候，使用路由中间件来拦截，只要刷新那个页面。都从cookie把登录缓存的uuid查询一次服务端，然后把查询出来完整的用户信息，继续写入到用户状态管理中去。

### 11.13日

1.nuxt中useState的使用，useState属于composeable里面定义的全局方法，是一种全局共享的==响应式==数据，也就是说：使用useState返回接受的变量是一个ref变量。可以做到路由之前数据的共享，代替pinia。（18）

2.头部信息设定 useHead

3.definePageMeta & 中间件& layouts，自定页面的布局和中间件

### 11.14日

1.middleware的使用，全局拦截做数据补偿（18）

### 11.15日

1.appid授权访问（白名单）（19）

2.实现接口关于post和get请求的封装和处理

### 11.17日

1.自动注入naivui，全局安装自动导入的依赖（20）

2.封装提示框:Dialog、Message, Loading

3.消息模块状态管理的同步，定义状态管理的方法，在登录写入状态管理

### 11.19日

1.整合，集成pinia状态管理（21）

2.naive ui字体图标组件库自动导入