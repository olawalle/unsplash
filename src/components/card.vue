<template>
  <div class="grid" @click="openModal">
    <b-modal
      id="modal-center"
      centered
      size="md"
      v-model="show"
      :hide-header="true"
      :hide-footer="true"
    >
      <div class="imgWrap">
        <img :src="data.urls.regular" alt class="modalImg" style="width: 100%">
      </div>
      <div class="details">
        <p class="name">{{data.user.name}}</p>
        <p class="location">{{data.user.location}}</p>
      </div>
    </b-modal>
    <!-- <div class="card_" v-if="!loading">
            <img :src="data.urls.full" alt="">
            <div class="text">
                <p class="name">{{data.user.name}} </p>
                <p class="location">{{data.user.location}}</p>
                <div class="overlay"></div>
            </div>
    </div>-->
    <div class="div" v-if="!loading">
      <img :src="data.urls.small">
      <div class="text">
        <p class="name">{{data.user.name}}</p>
        <p class="location">{{data.user.location}}</p>
      </div>
      <div class="overlay"></div>
    </div>

    <div class="card_" v-else>
      <div class="dummy">
        <p class="top"></p>
        <p class="btm"></p>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ['data', 'loading'],
  data() {
    return {
      show: false,
    };
  },
  methods: {
    openModal() {
      this.show = true;
    },
  },
};
</script>
<style lang="scss" scoped>
.div {
  width: 100%;
  border-radius: 10px;
  overflow: hidden;
  min-height: 120px;
  transition: linear all 0.25s;
  position: relative;
  img {
    width: 100%;
  }
  .overlay {
    width: 300px;
    height: 100%;
    position: absolute;
    top: 0;
    background-image: linear-gradient(transparent, #000);
    // opacity: 0.7;
    z-index: 7;
  }
  .text {
    position: absolute;
    bottom: 12px;
    left: 12px;
    z-index: 10;
    p {
      color: #fff;
      margin: 0;
      text-align: left;
    }
    .name {
      font-size: 18px;
      font-weight: 600;
    }
    .location {
      font-size: 12px;
      margin-top: -5px;
    }
  }
}

.grid {
  //   display: inline-block;
  padding: 0px;
  margin-bottom: 8px;
  cursor: pointer;
  .card_ {
    width: 100%;
    border-radius: 10px;
    overflow: hidden;
    min-height: 120px;
    background-color: #b9bfcc;
    box-shadow: 0px 0px 10px rgba(99, 115, 129, 0.1);
    .overlay {
      background-image: linear-gradient(transparent, #000);
      opacity: 0.7;
      width: 100%;
      height: 80px;
      position: relative;
      top: -65px;
      z-index: 2;
    }
    .text {
      position: relative;
      z-index: 3;
      color: #fff;
      margin-top: -69px;
      height: 63px;
      text-align: left;
      .name {
        font-size: 18px;
      }
      .location {
        font-size: 12px;
      }
      p {
        margin: 0 10px;
        position: relative;
        z-index: 5;
        height: 25px;
      }
    }
    img {
      width: 100%;
      height: auto;
      position: relative;
      top: 0px;
      z-index: 1;
    }
    .dummy {
      //   display: block;
      //   width: 320px;
      height: 320px;
      background-color: #eee;
      padding: 170px 12px 0 12px;
      .top {
        width: 70%;
        background-color: #c6c6c6 !important;
        height: 10px;
        position: relative;
        top: 80px;
      }
      .btm {
        width: 50%;
        background-color: #c6c6c6 !important;
        height: 10px;
        position: relative;
        top: 85px;
      }
    }
  }
}
.imgWrap {
  width: 100%;
  min-width: 100%;
  max-height: 85vh;
  overflow: auto;
}
.details {
  padding: 10px 20px;
  .name {
    color: #2b3875;
    font-size: 30px;
    margin: 0;
    font-size: 25px;
  }
  .location {
    color: #585858;
    font-size: 14px;
  }
}
.div:hover {
  transform: scale(1.015);
  box-shadow: 3px 3px 6px #dddfe2;
}
@media (max-width: 767px) {
  .grid {
    display: block !important;
    .card_ {
      display: block !important;
    }
  }
}
</style>
