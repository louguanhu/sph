<template>
  <div>
    <header class="header">
      <!-- 头部的第一行 -->
      <div class="top">
        <div class="container">
          <div class="loginList">
            <p>尚品汇欢迎您！</p>
            <!-- 没有登录：显示登录与注册 -->
            <!-- <p v-if="!$store.state.user.nickName"> -->
              <span>请</span>
              <!-- <a href="###">登录</a> -->
              <!-- 
                声明式导航,当然你也可以使用编程式导航,因为不管是那个导航，都可以实现路由跳转，
                但是最后为什么选择声明式导航，没有任何业务、逻辑
               -->
              <router-link to="/login">登录</router-link>
              <router-link class="register" to="/register">注册</router-link>
            </p>
            <!-- 如果登录显示的是用户名字与退出登录 -->
            <!-- <p v-else> -->
              <p>
              <!-- <a>{{ $store.state.user.nickName }}</a> -->
<!--              <a class="register" @click="logout">退出登录</a>-->
                <a class="register">退出登录</a>
            </p>
          </div>
          <div class="typeList">
            <router-link to="/center">我的订单</router-link>
            <router-link to="/shopcart">我的购物车</router-link>
            <a href="###">我的尚品汇</a>
            <a href="###">尚品汇会员</a>
            <a href="###">企业采购</a>
            <a href="###">关注尚品汇</a>
            <a href="###">合作招商</a>
            <a href="###">商家后台</a>
          </div>
        </div>
      </div>
      <!--头部第二行 搜索区域-->
      <div class="bottom">
        <h1 class="logoArea">
          <router-link class="logo" to="/home">
            <img src="./images/logo.png" alt="" />
          </router-link>
        </h1>
        <div class="searchArea">
          <form action="###" class="searchForm">
            <input
              type="text"
              id="autocomplete"
              class="input-error input-xxlarge"
              v-model="keyword"
            />
            <!-- 编程式导航:因为有业务 -->
            <button
              class="sui-btn btn-xlarge btn-danger"
              type="button"
              @click="goSearch"
            >
              搜索
            </button>
          </form>
        </div>
      </div>
    </header>
  </div>
</template>

<script>
export default {
  data(){
    return{
      keyword:''
    }
  },
  methods:{
    //搜索按钮的回调函数，并传递参数
    goSearch(){
      //路由传参
      //1.字符串形式
      // this.$router.push('/search/'+this.keyword+'?k='+this.keyword.toUpperCase())
      //模板字符串
      // this.$router.push(`/search/${this.keyword}?k=${this.keyword.toUpperCase()}`)
      // 对象
      // this.$router.push({name:'search',params:{
      //     keyword:this.keyword,},
      //   query:{k:this.keyword.toUpperCase()}
      // })
      // 注意：；路由传参的时候，对象的写法可以是path,name,
      // 但path写法不能和params一起使用
      //如果路由要求传递params，而实际没有传递时会出现路径问题
      //可以在配置路由时占位后面加个问号表示可传可不传（path:'/search/:keyword?）
      //如何在传递时传递的params是个空的字符串，路径也会出现问题
      //传递时使用undefined解决问题
      this.$router.push({name:'search',params:{
        keyword:''||undefined,},
        //通过给push方法传递成功和失败的回调函数，解决重复点击组件会报错 治标不治本
        query:{k:this.keyword.toUpperCase()}}, ()=>{},()=>{})

    }

  }
};
</script>

<style scoped lang="less">
.header {
  & > .top {
    background-color: #eaeaea;
    height: 30px;
    line-height: 30px;

    .container {
      width: 1200px;
      margin: 0 auto;
      overflow: hidden;

      .loginList {
        float: left;

        p {
          float: left;
          margin-right: 10px;

          .register {
            border-left: 1px solid #b3aeae;
            padding: 0 5px;
            margin-left: 5px;
          }
        }
      }

      .typeList {
        float: right;

        a {
          padding: 0 10px;

          & + a {
            border-left: 1px solid #b3aeae;
          }
        }
      }
    }
  }

  & > .bottom {
    width: 1200px;
    margin: 0 auto;
    overflow: hidden;

    .logoArea {
      float: left;

      .logo {
        img {
          width: 175px;
          margin: 25px 45px;
        }
      }
    }

    .searchArea {
      float: right;
      margin-top: 35px;

      .searchForm {
        overflow: hidden;

        input {
          box-sizing: border-box;
          width: 490px;
          height: 32px;
          padding: 0px 4px;
          border: 2px solid #ea4a36;
          float: left;

          &:focus {
            outline: none;
          }
        }

        button {
          height: 32px;
          width: 68px;
          background-color: #ea4a36;
          border: none;
          color: #fff;
          float: left;
          cursor: pointer;

          &:focus {
            outline: none;
          }
        }
      }
    }
  }
}
</style>
