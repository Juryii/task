<template>
  <div data-app>
    <div class="nav_wrapper">
      <div>
        <div class="logo_nav_drawer">
          <img src="@/assets/as_logo.svg" alt="logo" />
        </div>
      </div>
      <div class="items_wrapper">
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
          <a href="#"
            >Lorem ipsum dolor sit amet, consectetur adipisicing elit. Atque cupiditate dolor dolores ducimus
            exercitationem molestias, nobis placeat quam rem voluptate? A aliquam culpa delectus dolorum ex omnis porro
            quae voluptates?.</a
          >
        </div>
      </div>
    </div>
    <div class="main-wrapper">
      <div class="header_wrapper">
        <div class="text_logo"><span>ARTSURF</span> Taske</div>

        <div class="header_user_wrapper">
          <!--            <div class="user-avatar"><img src="@/assets/resistance.jpg" alt=""></div>-->
          <div class="user-avatar user-avatar--text">U</div>
          <p class="userName">UserName</p>
        </div>
      </div>

      <div class="content_wrapper">
        <div class="my_tasks">Мои задачи</div>
        <router-view />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    drawer: false
  })
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
.items_wrapper {
  padding-left: 16px;
  padding-right: 16px;
}
.item_nav {
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
}
.item_nav:hover {
  color: white;
  cursor: pointer;
}
.item_nav a {
  color: inherit;
  text-decoration: none;
}
.item_nav--active {
  font-weight: bold;
  color: white;
  background-color: rgba(28, 21, 46, 0.54);
}

/* HEADER Styles*/
.header_wrapper {
  height: 68px;
  background-color: #f9f9f9;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.text_logo {
  padding: 20px 32px;
  font-size: 24px;
  line-height: 28px;
}
.text_logo span {
  font-weight: bold;
}
.header_user_wrapper {
  padding: 32px 32px 32px 8px;
  display: flex;
  align-items: center;
}
.user-avatar {
  height: 40px;
  width: 40px;
  border-radius: 50%;
  margin-right: 16px;
  box-shadow: -4px -4px 8px #ffffff, 4px 4px 8px #ececec;
}
.user-avatar--text {
  background-color: #dee5c9;
  line-height: 40px;
  text-align: center;
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
