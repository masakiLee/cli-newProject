<script>
export default {
  props: ["contentProps"],
  data() {
    return {
      content: {},
    };
  },
  watch: {
    contentProps: {
      handler(newVal) {
        this.content = newVal;
        console.log(newVal);
      },
      deep: true,
    },
  },
};
</script>

<template>
  <div class="search_area">
    <div class="select select_type">
      <h2 class="title">請輸入類型</h2>
      <fieldset>
        <div class="input_group">
          <input
            type="radio"
            id="膠囊旅館"
            name="drone"
            value="膠囊旅館"
            v-model="content.type"
            checked
          />
          <label for="膠囊旅館">膠囊旅館</label>
        </div>
        <div class="input_group">
          <input
            type="radio"
            id="青年旅館"
            name="drone"
            value="青年旅館"
            v-model="content.type"
          />
          <label for="青年旅館">青年旅館</label>
        </div>
        <div class="input_group">
          <input
            type="radio"
            id="Hotel"
            name="drone"
            value="Hotel"
            v-model="content.type"
          />
          <label for="Hotel">Hotel</label>
        </div>
        <div class="input_group">
          <input
            type="radio"
            id="民宿"
            name="drone"
            value="民宿"
            v-model="content.type"
          />
          <label for="民宿">民宿</label>
        </div>
        <div class="input_group">
          <input
            type="radio"
            id="Villa"
            name="drone"
            value="Villa"
            v-model="content.type"
          />
          <label for="Villa">Villa</label>
        </div>
      </fieldset>
    </div>
    <div class="select select_city">
      <h2 class="title">請輸入城市名</h2>
      <input
        class="input_city"
        type="text"
        id="city"
        name="name"
        placeholder="例：新北市"
        autofocus
        autocomplete="off"
        v-model="content.city"
      />
    </div>
    <div class="select select_number">
      <h2 class="title">請選擇房型</h2>
      <select name="roomType" id="roomType-select" v-model="content.roomType">
        <option disabled value="">請選擇</option>
        <option value="單人房">單人房</option>
        <option value="雙人房">雙人房</option>
        <option value="雙床雙人房">雙床雙人房</option>
        <option value="加大雙人房">加大雙人房</option>
        <option value="四人房">四人房</option>
      </select>
    </div>
    <div class="select select_send" @click.prevent="$emit('send-emit')">
      送出
    </div>
  </div>
</template>

<style lang="scss">
@import "../assets/sass/variables";

.search_area {
  display: grid;
  gap: $spaceBase;
  grid-template-columns: 1fr;
  @media screen and (min-width: 768px) {
    grid-template-columns: 1fr 1fr;
  }
  @media screen and (min-width: 1200px) {
    grid-template-columns: 2fr 1fr 1fr 0.5fr;
  }
  .select {
    padding: $spaceBase;
    box-shadow: 3px 2px 6px rgba(0, 0, 0, 0.1);
    background-color: #fff;
    &:nth-child(1) .title::before {
      content: "01";
    }
    &:nth-child(2) .title::before {
      content: "02";
    }
    &:nth-child(3) .title::before {
      content: "03";
    }
  }
  fieldset {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }
  .input_group {
    display: flex;
    align-items: center;
    gap: $spaceBase * 0.5;
  }
  label {
    font-size: clamp(16px, 2.6041vw, 24px);
  }
  input[type="radio"] {
    transform: scale(1.2);
    accent-color: var(--primary);
  }
  .title {
    font-size: clamp(16px, 2.6041vw, 24px);
    font-weight: bold;
    color: var(--primary);
    padding-bottom: $spaceBase * 0.5;
    &::before {
      color: var(--secondary);
      padding-right: $spaceBase * 0.5;
    }
  }
  input[type="text"],
  select {
    outline: none;
    border: 2px solid var(--primary);
    font-size: clamp(16px, 2.6041vw, 24px);
    padding: $spaceBase * 0.5 $spaceBase * 0.75;
  }
  .select_type {
    grid-area: auto;
    @media screen and (min-width: 768px) {
      grid-area: 1 / 3 / 3 / 1;
    }
    @media screen and (min-width: 1200px) {
      grid-area: auto;
    }
  }
  .select_number {
    select {
      width: 100%;
    }
  }
  .select_send {
    background-color: var(--primary);
    color: white;
    box-shadow: 3px 2px 6px rgba(0, 0, 0, 0.1);
    font-size: clamp(16px, 2.6041vw, 24px);
    border: none;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-grow: 1;
    cursor: pointer;
    grid-area: auto;
    @media screen and (min-width: 768px) {
      grid-area: 4 / 1 / 4 / 3;
    }
    @media screen and (min-width: 1200px) {
      grid-area: auto;
    }
  }
}
</style>
