<template>
  <header class="header">
    <nav class="nav">
      <a href="#"><img width="48px" height="48px" src="@/assets/img/logo.png" alt='' /></a>
      <a href="#">Подборка</a>
      <a href="#">Мой список</a>
      <a href="#">Добавить</a>
    </nav>
  </header>
</template>

<style lang="scss">
@use '@/assets/css/main.scss';

.header {
  width: 100%;
  height: 4rem;
  background-color: main.$primary;
  color: main.$secondary;
  display: flex;
}

.nav {
  display: flex;
  align-items: center;
  max-width: 1200px;
  margin: auto;
  gap: 2rem;
  justify-content: space-around;

  &:first-child {
    margin-right: auto;
  }
}

a {
  color: main.$secondary;
}
</style>