<template>
  <div class="hero">
    <div class="container hero__container">
      <span>Now playing</span>
      <button>View Movies</button>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.hero {
  width: 100%;
  height: 100vh;

  background-image: linear-gradient(
      9deg,
      #0e0d0d 2.04%,
      rgba(43, 43, 43, 0.77) 47.03%,
      rgba(226, 226, 226, 0.77) 98.02%
    ),
    url('https://images.unsplash.com/photo-1626814026160-2237a95fc5a0?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80');
  &__container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
    span {
      font-size: 8rem;
      display: block;
      color: #fff;
      font-weight: 600;
      margin-bottom: 2rem;
    }
  }
}
</style>
