<template>
  <div class="header">
    <div class="header__toolbar">
      <h1>Todo</h1>
    </div>
  </div>
</template>

<style>
.header {
  --height: 20rem;
  min-height: var(--height);
  background-image: url("../assets/bg-mobile-light.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;

  grid-row-start: 1;
  grid-row-end: 3;
  grid-column-start: 1;
  grid-column-end: 2;
}

.header__toolbar {
  padding-block-start: 4.8rem;
  padding-inline: 2.4rem;
  margin-inline: auto;
  width: min(100%, 54rem);
}

.header__toolbar h1 {
  color: white;
  font-weight: 700;
  font-size: 28px;
  text-transform: uppercase;
  letter-spacing: 0.33em;
}

@media screen and (min-width: 34.375em) {
  .header {
    --height: 30rem;
    background-image: url("../assets/bg-desktop-light.jpg");
  }

  .header__toolbar {
    padding-block-start: 7.2rem;
  }

  .header__toolbar h1 {
    font-size: 4rem;
  }
}
</style>
