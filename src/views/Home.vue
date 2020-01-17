<template>
  <div class="home">
    <div class="searchBar">
      <div class="searchedFor" v-if="hasSearched">
        Search Results For "
        <span>{{searchValue}}</span>"
        <span class="searchIcon" @click="hasSearched = false">
          <img src="../assets/search.png" alt>
        </span>
      </div>

      <div class="searchedFor" v-else-if="loading">
        Searching for
        <span>{{searchValue}}</span>
      </div>

      <b-input-group v-else>
        <b-input-group-text slot="prepend">
          <img src="../assets/search.png" alt>
        </b-input-group-text>
        <b-form-input placeholder="search" v-model="searchValue" @keyup="submit"></b-form-input>
      </b-input-group>
    </div>

    <div class="images">
      <div class="cols">
        <Card v-for="(obj, i) in row1" :key="'data'+i" :data="obj" :loading="loading"/>
      </div>
      <div class="cols">
        <Card v-for="(obj, i) in row2" :key="'data'+i" :data="obj" :loading="loading"/>
      </div>
      <div class="cols">
        <Card v-for="(obj, i) in row3" :key="'data'+i" :data="obj" :loading="loading"/>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex';
import Card from '@/components/card.vue';
import { search } from '../services';
import * as constants from '../constants';

export default {
  name: 'home',
  components: {
    Card,
  },
  data() {
    return {
      searchValue: 'African',
      hasSearched: false,
    };
  },
  mounted() {
    this.fetchData(this.searchValue, false);
  },
  computed: {
    ...mapGetters({
      pictures: 'getPictures',
      loading: 'loadingStatus',
    }),
    row1 () {
      return this.pictures.filter(p => p.row_tag === 0)
    },
    row2 () {
      return this.pictures.filter(p => p.row_tag === 1)
    },
    row3 () {
      return this.pictures.filter(p => p.row_tag === 2)
    }
  },
  methods: {
    submit(e) {
      if (e.keyCode === 13) {
        this.fetchData(this.searchValue, true);
      }
    },
    fetchData(value, userSerched) {
      this.$store.commit(constants.LOADING_STATUS, true);
      search({
        query: value,
      })
        .then((res) => {
          this.hasSearched = userSerched;
          let row_tag = 0;
          let pictures = res.data.results.map(m => {
            let data = {
              ...m,
              row_tag
            }
            row_tag += 1
            row_tag > 2 ? row_tag = 0 : null
            return data
          })
          this.$store.commit(constants.SAVE_PICTURE_DATA, pictures);
          
          this.$store.commit(constants.LOADING_STATUS, false);
        })
        .catch((err) => {
          this.$store.commit(constants.LOADING_STATUS, false);
        });
    },
  },
};
</script>

<style lang="scss" scoped>
.home {
  padding: 20px 100px;
  .searchBar {
    background-color: rgb(229, 231, 233);
    font-size: 20px;
    color: #eee;
    padding: 75px;
    .searchedFor {
      font-size: 30px;
      color: #62686d;
      text-align: left;
      span {
        color: #31416f;
      }
      .searchIcon {
        float: right;
        cursor: pointer;
        background: #b9bfcc;
        padding: 10px;
        border-radius: 12px;
        img {
          width: 40px;
          height: 40px;
        }
      }
    }
    .input-group-text {
      border: 0 !important;
      padding-left: 20px;
      background: #fff !important;
      border-radius: 7px 0 0 7px;
      img {
        width: 40%;
      }
    }
    input {
      border: 0;
      // width: 90%;
      height: 55px;
      border-radius: 0 7px 7px 0;
      padding: 0 10px;
    }
  }
  .images-wrap {
    margin-top: -45px;
    padding: 0 170px;
    column-count: 3;
    column-gap: 5px;
    column-fill: auto;
  }
  .images {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-gap: 30px;
    grid-auto-rows: auto;
    padding: 20px 120px;
    margin-top: -50px;
    .cols {
      display: grid;
      grid-template-columns: 1fr;
      grid-auto-rows: min-content;
      grid-gap: 30px;
      .div {
        width: 100%;
        border-radius: 10px;
        overflow: hidden;
        min-height: 120px;
        background-color: #b9bfcc;
        // padding: 10px;
        img {
          width: 100%;
        }
      }
    }
  }
}
@media (max-width: 767px) {
  .home {
    padding: 0;
    .searchBar {
      display: inline-block;
      min-width: 100%;
      padding: 30px 20px;
      .searchedFor {
        font-size: 14px;
      }
      .searchIcon {
        img {
          width: 20px;
          height: 20px;
        }
      }
      input {
        width: 30px;
      }
    }
    .images-wrap {
      padding: 10px;
      margin-top: 0;
      column-count: 1;
      column-gap: 5px;
      column-fill: auto;
    }

    .images {
      display: grid;
      grid-template-columns: 1fr;
      grid-gap: 10px;
      grid-auto-rows: auto;
      padding: 12px;
      margin-top: 0px;
      .cols {
        display: grid;
        grid-template-columns: 1fr;
        grid-auto-rows: min-content;
        grid-gap: 10px;
        div {
          width: 100%;
          border-radius: 10px;
          overflow: hidden;
          // padding: 10px;
          img {
            width: 100%;
          }
        }
      }
    }
  }
}
</style>
