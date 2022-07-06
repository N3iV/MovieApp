<template>
  <nav>
    <div class="nav container">
      <h2 class="nav__logo">Movie hehe</h2>
      <ul class="nav__list">
        <li>
          <fa :icon="['fas', 'adjust']" />
        </li>
        <li class="nav__item">Home</li>
        <li class="nav__item">Movies</li>
        <li class="nav__item">TV Series</li>
      </ul>
    </div>
  </nav>
</template>

<style lang="scss" scoped>
nav {
  background: #131c38;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 99;
}
.nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  color: #fff;

  &__logo {
    font-size: 2.2rem;
  }
  &__list {
    display: flex;
    font-weight: 500;
  }
  &__item {
    padding: 0.8rem 1.2rem;
    font-size: 1.6rem;
    font-weight: 400;
  }
}
</style>
