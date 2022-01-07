<template lang="">
  <div class="d-block vw-100 vh-100 overflow-hidden">
    <div
      class="header d-flex justify-content-end align-items-start flex-column h-25 p-3"
    >
      <h1>Kisah Peminjam Dana</h1>
      <p>Welcome to the complete Nuxt JS crash course.</p>
    </div>
    <div class="content d-block w-100 h-75">
      <div v-for="datas in content" :key="datas.id" class="d-inline-block h-100 overflow-hidden items">
        <div class="d-inline-flex h-100 overflow-hidden image position-relative">
          <img :src="require(`~/assets/${datas.image}.jpg`)" />
          <div class="rounded-circle position-absolute" onclick="showDesc">baca kisah {{ datas.name }}</div>
        </div>
        <div class="d-inline-block h-100 overflow-hidden desc position-relative">
          <img :src="require(`~/assets/${datas.image}.jpg`)" />
          <div class="w-100 h-100 position-absolute text-white">
            <strong class="testimonial">{{ datas.testimonials }}</strong>
            <strong>{{ datas.name }}</strong>
            <p>{{ datas.jobs }}</p>
            <p>Dana Terkumpul</p>
            <p>Rp. <strong>{{ datas.saldo }}</strong> dalam {{ datas.time }} menit</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'

export default {
  async asyncData() {
    const { data } = await axios.get('http://localhost:3004/data')
    return {content: data}
  }
};

function showDesc(){
  document.querySelectorAll('.desc').classList.add('show');
}
</script>
<style lang="scss">
.items {
  width: 75%;
  .image {
    width: 35%;

    div {
      display: none;
    }

    &:hover div {
      display: flex;
      justify-content: center;
      align-items: center;
      transform: translate(-50%, -50%);
      top: 50%;
      left: 50%;
      width: 160px;
      height: 160px;
      white-space: normal;
      background: #00000095;
      text-align: center;
      padding: 20px;
      text-transform: uppercase;
      color: #ffffff;
      font-weight: 600;
      cursor: pointer;
    }
  }
  .desc {
    width: 65%;
  }
}
.content {
  white-space: nowrap;
  overflow-x: auto;
  overflow-y: hidden;

  .testimonial {
    display: block;
    white-space: normal;
  }

  &::-webkit-scrollbar {
    display: none;
  }
}
.desc {
  margin-left: -5px;
  img {
    transform: scaleX(-1);
  }
  div {
    top: 0;
    padding: 74px;
    &::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: linear-gradient(111.07deg, #2b9cff 13.43%, #00acdc 104.53%);
      opacity: 0.5;
    }
    p, strong {
      position: relative;
      z-index: 9;
    }
  }
}
.image {
  img {
    margin-left: -35%;
    filter: grayscale(90%);
  }
}
</style>
