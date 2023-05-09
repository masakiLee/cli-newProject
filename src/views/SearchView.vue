<script>
import selectGroup from "../components/selectGroupView.vue";
export default {
  data() {
    return {
      sort: true,
      content: {
        type: "",
        city: "",
        roomType: "",
      },
      total: [],
    };
  },
  methods: {
    send() {
      const { type, city, roomType } = this.content;
      console.log(type, city, roomType);
      // this.search(type, city, roomType);
    },
    search(type, city, roomType) {
      this.$http
        .get("https://mocki.io/v1/1a7d51d9-caa0-466b-81ec-6804e1b6cda1")
        .then((res) => {
          if (type || city || roomType) {
            const filteredData = res.data.filter((item) => {
              return (
                (!type || item.type === type) &&
                (!city || item.city === city) &&
                (!roomType || item.roomType.includes(roomType))
              );
            });
            this.total = filteredData;
          } else {
            this.total = res.data;
          }
        });
    },
  },
  components: {
    selectGroup,
  },
  computed: {
    sortPrice() {
      const newPrice = [...this.total].sort((a, b) => {
        return this.sort ? a.price - b.price : b.price - a.price;
      });
      return newPrice;
    },
  },
  mounted() {
    this.search();
  },
};
</script>

<template>
  <section class="search">
    <div class="container">
      <select-group :content-props="content" @send-emit="send"></select-group>
      <div class="total">
        <div class="options">
          <select
            name="options"
            id="options"
            class="options_select"
            @change="this.sort = !this.sort"
          >
            <option>價格由低到高</option>
            <option>價格由高到低</option>
          </select>
          <ul class="total_group" v-if="sortPrice.length !== 0">
            <li
              class="total_list"
              v-for="(item, index) in sortPrice"
              :key="index + 777"
            >
              <a href="#" class="total_link">
                <p class="type">{{ item.type }}</p>
                <div class="total_image">
                  <img :src="item.imageUrl" :alt="item.type" class="image" />
                </div>
                <div class="total_content">
                  <h3 class="title">{{ item.title }}</h3>
                  <p class="city">{{ item.city }}</p>
                  <p class="roomType">房型：{{ item.roomType.toString() }}</p>
                  <p class="price">
                    TWD {{ item.price.toLocaleString() }} / <span>晚</span>
                  </p>
                </div>
              </a>
            </li>
          </ul>
          <p v-else>無相關資料</p>
        </div>
      </div>
    </div>
  </section>
</template>

<style lang="scss">
@import "../assets/sass/variables";
.search {
  padding: $spaceBase * 2 0;
  @media screen and (min-width: 768px) {
    padding: $spaceBase * 5 0;
  }
}

.total {
  .options_select {
    display: block;
    margin-left: auto;
    margin-top: $spaceBase * 2;
  }
  select {
    outline: none;
    border: 2px solid var(--primary);
    padding: $spaceBase * 0.25 0;
  }
  &_group {
    padding: $spaceBase * 2 0;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    @media screen and (min-width: 768px) {
      grid-template-columns: repeat(3, 1fr);
    }
    @media screen and (min-width: 992px) {
      grid-template-columns: repeat(4, 1fr);
    }
    gap: $spaceBase;
  }
  &_list {
    position: relative;
    box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.1);
    display: flex;
    flex-direction: column;
  }
  &_link {
    color: black;
    display: flex;
    flex-direction: column;
    flex-grow: 1;
  }
  &_content {
    padding: $spaceBase * 0.5;
    display: flex;
    flex-direction: column;
    flex-grow: 1;
    background-color: #fff;
  }
  .image {
    width: 100%;
    aspect-ratio: 3/2;
    object-fit: cover;
    vertical-align: top;
  }
  .type {
    position: absolute;
    top: 0;
    left: 0;
    display: inline-block;
    background-color: var(--secondary);
    padding: $spaceBase * 0.5 $spaceBase;
    color: white;
  }
  .title {
    font-size: clamp(16px, 2.34375vw, 20px);
    font-weight: bold;
  }
  .price {
    font-weight: bold;
    text-align: end;
    color: var(--primary);
    font-size: clamp(16px, 2.60416vw, 24px);
    span {
      font-weight: 500;
      font-size: $fontSizeBase;
    }
  }
  .roomType {
    flex-grow: 1;
  }
}
</style>
