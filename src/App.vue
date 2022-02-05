<template>
  <div class="shop_logo_space">
    <img class="shop_logo" src="./img/smasta_main_logo.png">
  </div>
  <div id="nav">
    <h2>
      <router-link to="/">端末一覧</router-link> |
      <router-link to="/about">おすすめ端末</router-link>
    </h2>
  </div>
  <router-view/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

.shop_logo_space{
  padding-top:20px;
  text-align:center;
}

.shop_logo{
  width:50px;
}
</style>