<template>
  <div data-app>
    <div class="nav_wrapper">
      <div>
        <div class="logo_nav_drawer">
          <img src="@/assets/as_logo.svg" alt="logo" />
        </div>
      </div>
      <!-- <div class="items_wrapper">
        <div class="item_nav item_nav--active">
          <a href="#">Мои задачи</a>
        </div>
        <div class="item_nav">
          <a href="#">Backlog</a>
        </div>
        <div class="item_nav">
          <a href="#">Настройки</a>
        </div>
        <div class="item_nav">
          <a href="#">Архив</a>
        </div>
        <div class="item_nav">
          <a href="#">
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Atque cupiditate dolor dolores ducimus
            exercitationem molestias, nobis placeat quam rem voluptate? A aliquam culpa delectus dolorum ex omnis porro
            quae voluptates?.
          </a>
        </div>
      </div>-->
      <nav>
        <ul class="drawer-menu">
          <li v-for="link in menuLinks" :key="link.to">
            <router-link :to="link.to" class="drawer-menu__link">{{ link.title }}</router-link>
          </li>
        </ul>
      </nav>
    </div>
    <div class="main-wrapper">
      <header class="header_wrapper">
        <div class="main-wrapper-2">
          <div class="text_logo"><span>ARTSURF</span> Tasker</div>
          <div class="header_user_wrapper">
            <!--<div class="user-avatar"><img src="@/assets/resistance.jpg" alt=""></div>-->
            <div class="user-avatar user-avatar--text">U</div>
            <p class="userName">UserName</p>
          </div>
        </div>
      </header>
      <main class="content_wrapper">
        <div class="main-wrapper-2">
          <h1>Мои задачи</h1>
        </div>
        <router-view />
      </main>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      drawer: false,
      menuLinks: [
        { title: "Мои задачи", to: "/" },
        { title: "Backlog", to: "/backlog" },
        { title: "Настройки", to: "/settings" },
        { title: "Архив", to: "/archive" },
        {
          title: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.",
          to: "/link"
        }
      ]
    };
  }
};
</script>

<style scoped>
.main-wrapper {
  padding-left: 290px;
}
/*<!--  NAW styles-->*/
.nav_wrapper {
  position: fixed;
  width: 290px;
  height: 100%;
  background-color: #261f39;
}
.logo_nav_drawer {
  padding: 24px 60px;
}
.drawer-menu {
  padding: 0 16px;
  list-style: none;
}
.drawer-menu__link {
  font-size: 15px;
  font-style: normal;
  font-weight: normal;
  color: #877da4;
  line-height: 18px;
  padding-top: 12px;
  padding-left: 16px;
  padding-bottom: 12px;
  border-radius: 6px;
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
  padding-right: 14px;
  display: block;
  text-decoration: none;
  transition: all 0.3s;
}
.drawer-menu__link.router-link-active {
  font-weight: bold;
  color: white;
  background-color: rgba(28, 21, 46, 0.54);
}
.drawer-menu__link:hover {
  color: white;
}

/* HEADER Styles*/
.header_wrapper {
  height: 68px;
  display: flex;
  border-bottom: 1px solid rgba(0, 0, 0, 0.07);
  margin-bottom: 40px;
}
.main-wrapper-2 {
  padding: 0 32px;
  flex-direction: row;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 24px;
}
.userName {
  font-weight: bold;
  font-size: 15px;
  line-height: 18px;
  color: #0e0e0e;
}
.text_logo {
  font-size: 24px;
  line-height: 28px;
  margin-top: 20px;
}
.text_logo span {
  font-weight: bold;
}
.header_user_wrapper {
  display: flex;
  align-items: center;
  margin-top: 12px;
}
.user-avatar {
  height: 40px;
  width: 40px;
  border-radius: 50%;
  margin-right: 12px;
  box-shadow: -4px -4px 8px #ffffff, 4px 4px 8px #ececec;
}
.user-avatar--text {
  background-color: #ffffff;
  line-height: 40px;
  text-align: center;
  color: #ff6d5c;
  font-weight: bold;
  font-size: 20px;
}

.user-avatar img {
  width: inherit;
  height: inherit;
  object-fit: cover;
  border-radius: inherit;
}
.my_tasks {
  font-weight: 900;
  font-size: 36px;
  line-height: 42px;
  margin: 40px 32px;
}
</style>
