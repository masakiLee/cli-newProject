<script>
export default {
  methods: {
    changeTheme(newTheme) {
      document.documentElement.setAttribute("data-theme", newTheme);
      localStorage.setItem("theme", newTheme);
    },
  },
  mounted() {
    const savedTheme = localStorage.getItem("theme");
    if (savedTheme) {
      this.changeTheme(savedTheme);
    } else {
      this.changeTheme("light");
    }
  },
};
</script>

<template>
  <header class="header">
    <RouterLink to="/" class="header_link">
      <div class="header_logo_icon">R</div>
      <h1 class="header_logo">
        安居客
        <span>RelaxResidences</span>
      </h1>
    </RouterLink>
    <div class="themes">
      <div class="color color_blue_orange" @click="changeTheme('light')"></div>
      <div class="color color_green_yellow" @click="changeTheme('dark')"></div>
    </div>
  </header>
  <RouterView />
</template>

<style lang="scss">
@import "./assets/sass/variables";

.header {
  background-color: var(--primary);
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: $spaceBase;

  @media screen and (min-width: 768px) {
    padding: $spaceBase $spaceBase * 2;
  }

  &_link {
    display: flex;
    gap: $spaceBase;
    color: white;
  }

  &_logo_icon {
    padding: $spaceBase * 0.5 $spaceBase;
    background-color: white;
    font-weight: bold;
    color: var(--secondary);
    font-size: clamp(36px, 5.20833vw, 48px);
    border-radius: 12px;
    line-height: 1;
    box-sizing: border-box;
  }

  &_logo {
    font-size: $fontSizeBase;
    line-height: 1.5;

    span {
      display: block;
    }

    @media screen and (min-width: 768px) {
      font-size: $fontSizeBase * 1.5;
      line-height: 1.25;
    }
  }

  .themes {
    display: flex;
    align-items: center;
    gap: $spaceBase;
  }

  .color {
    width: 48px;
    aspect-ratio: 1/1;
    border: 1px solid white;
    border-radius: 12px;
    cursor: pointer;
    box-sizing: border-box;

    @media screen and (min-width: 768px) {
      width: 60px;
    }

    &_blue_orange {
      background: linear-gradient(
        to bottom right,
        $primary 50%,
        $secondary 50%
      );
    }

    &_green_yellow {
      background: linear-gradient(
        to bottom right,
        $primaryTwo 50%,
        $secondaryTwo 50%
      );
    }
  }
}
</style>
