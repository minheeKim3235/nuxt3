<template>
  <div class="special_teacher_view" :class="brand">
    <div class="cont1">
      <div class="select" v-show="brand !== 'HPnormal'">
        <select>
          <option>목록</option>
          <option>공병권</option>
        </select>
      </div>
      <span class="subj">{{ item.subj }}</span>
      <span class="name">{{ item.name }}</span>
      <span class="slogan">{{ item.slogan }}</span>
      <div class="career">
        <div class="swiper" ref="careerSlide">
          <div class="swiper-wrapper">
            <div class="swiper-slide" v-for="list in item.career" :key="list">{{ list }}</div>
          </div>
        </div>
      </div>
      <span class="pic">
        <img :src="item.imgSrc" alt="">
      </span> 
    </div>
    <div class="cont2">
      <div class="video" v-show="item.video !== ''">
        <iframe :src="`//www.youtube.com/embed/${ item.video }?rel=0&amp;wmode=transparent&amp;enablejsapi=1`"></iframe>
      </div>
      <div class="point" :class="{'no_video' : item.video == ''}">
        <p class="tit">{{ brand !== 'HPnormal' ? '본인소개 POINT' : '재수 성공철학' }}</p>
        <ul>
          <li v-for="(item, i) in item.point" :key="i">{{ item }}</li>
        </ul>
      </div>
      <div class="story">
        <p class="tit">{{ brand !== 'HPnormal' ? '나의 제자가 말하는  선생님 이야기' : '전략 담임이 최상위권에게 전하는 말' }}</p>
        <div class="story_slide" v-if="brand !== 'HPnormal'">
          <div class="swiper" ref="storySlide">
            <div class="swiper-wrapper">
              <div class="swiper-slide" v-for="(story, i) in item.story" :key="i">
                <strong>{{ story.title }}</strong>
                <p v-html="story.context"></p>
              </div>
            </div>
          </div>
          <div class="swiper-button-prev"></div>
          <div class="swiper-button-next"></div>
          <div class="swiper-pagination"></div>
        </div>
        <Accordion v-else>
          <template v-for="(story, i) in item.story" :key="i">
            <AccordionItem :title="story.title" :index="i">
              <p v-html="story.context"></p>
            </AccordionItem>
          </template>
        </Accordion>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue';
import { Autoplay, Pagination, Navigation } from 'swiper/modules'
import Swiper from 'swiper';
Swiper.use([Autoplay, Pagination, Navigation]);

const props = defineProps({
  item: [Array, Object],
  brand: String
})

const careerSlide = ref(null);
const slidesCount = () => {
  if ( props.brand == 'HPnormal') {
    return 5
  } else {
    return 2
  }
};
const slidesHeight = () => {
  if ( props.brand == 'HPnormal') {
    return 70
  } else {
    return 28
  }
};
const careerOption = {
  slidesPerView: slidesCount(),
  loop: true,
  autoplay: {
    delay: 2000
  },
  speed: 1000,
  direction: 'vertical',
  height: slidesHeight(),
};
const storySlide = ref(null);
const storyOption = {
  loop: true,
  pagination: {
    el: '.story_slide .swiper-pagination',
    clickable: true
  },
  navigation: {
    prevEl: '.story_slide .swiper-button-prev',
    nextEl: '.story_slide .swiper-button-next',
  }
};
const pointColor = computed(() => {
  if ( props.brand == 'CSnormal') {
    return '#3642a1'
  } else if ( props.brand === 'CSneo' ) {
    return '#5dcc22';
  }
})
onMounted(() => {
  new Swiper(careerSlide.value, careerOption);
  if ( props.brand !== 'HPnormal') {
    new Swiper(storySlide.value, storyOption);
  }
})
</script>

<style lang="scss" scoped>
.special_teacher_view {
  --point: v-bind(pointColor);
  position: relative;
  padding: 20px 20px 0;
  background: #fff;
  overflow: hidden;
  .cont1 {
    position: relative;
    overflow: hidden;
    z-index: 1;
    .select {
      text-align: right;
      display: block;
      margin-bottom: 45px;
      select {
        padding-left: 15px;
        width: 40%;
        height: 39px;
        color: #666;
        font-size: 13px;
        vertical-align: top;
        line-height: 39px;
        border: 1px solid #000;
        background: url(https://acaimg.etoos.com/cs/mobile/branch/images/common/bg_select.png) no-repeat right center;
        background-size: 21px auto;
      }
    }
    span, div {
      display: block;
      z-index: 2;
    }
    .subj {
      font-size: 16px;
      color: #222;
    }
    .name {
      margin: 3px 0 10px;
      font-size: 28px;
      color: #222;
      font-weight: 800;
    }
    .slogan {
      width: 60%;
      font-size: 14px;
      color: #333;
      letter-spacing: -0.05em;
      word-break: keep-all;
    }
    .career {
      margin: 10px 0 20px;
      height: 28px;
      font-size: 12px;
      line-height: 14px;
      overflow: hidden;
    }
    .pic {
      position: absolute;
      right: -10px;
      top: 65px;
      width: 300px;
      z-index: 1;
      img {
        max-width: 100%;
      }
    }
  }
  .cont2 {
    position: relative;
    z-index: 3;
    .video {
      width: 100%;
      aspect-ratio: 1.77;
      iframe {
        width: 100%;
        height: 100%;
      }
    }
    .point {
      padding: 15px;
      .tit {
        padding: 0 5px;
        display: inline-block;
        color: var(--point);
        border: 1px solid var(--point);
      }
      ul {
        margin-top: 10px;
        li {
          font-size: 12px;
          line-height: 14px;
          color: var(--point);
        }
      }
      &.no_video {
        background: #fff;
        border: 1px solid #dcdee2;
      }
    }
    .story {
      position: relative;
      padding: 15px 20px 40px;
      margin-top: 15px;
      background: #f4f5f6;
      .tit {
        font-size: 0;
        width: 275px;
        height: 19px;
        margin-bottom: 10px;
        background: url(https://acaimg.etoos.com/cs/mobile/branch/images/cnt/introduce/mteacherqna1.png) no-repeat center center;
        background-size: 275px auto;
      }
      .story_slide {
        color: #222;
        strong {
          display: block;
          font-size: 14px;
          margin-bottom: 10px;
          font-weight: 800;
        }
        p {
          font-size: 12px;
          word-break: keep-all;
        }
      }
    }
  }
}
:deep(.story_slide .swiper-button-prev),
:deep(.story_slide .swiper-button-next) {
  position: absolute;
  left: -10px;
  top: 50%;
  margin-top: -18px;
  width: 18px;
  height: 36px;
  background: url('https://acaimg.etoos.com/cs/mobile/branch/images/common/bswiper_prev.png') no-repeat 0 0;
  background-size: 18px auto;
  cursor: pointer;
  z-index: 2;
  &:after {
    display: none;
  }
}
:deep(.story_slide .swiper-button-next) {
  left: auto;
  right: -10px;
  transform: rotate(180deg);
}
:deep(.story_slide .swiper-pagination-bullet) {
  display: inline-block;
  width: 12px;
  height: 12px;
  border-radius: 100%;
  background: #fff;
  border: 1px solid #bdbdbd;
  margin: 0 2px;
}
:deep(.story_slide .swiper-pagination-bullet-active) {
  background: #bdbdbd;
}

.special_teacher_view.HPnormal {
  padding: 0;
  .cont1 {
    overflow: hidden;
    position: relative;
    padding: 37px 40px;
    min-height: 240px;
    color: #fff;
    background: #39414c;
    .subj {
      display: none;
    }
    .name {
      margin-top: 2px;
      font-weight: 500;
      font-size: 29px;
      color: #fff;
      line-height: 29px;
    }
    .slogan {
      margin-top: 18px;
      width: 65%;
      line-height: 15px;
      font-size: 12px;
      color: #fff;
    }
    .career {
      margin: 16px 0 0;
      height: 70px;
      .swiper-slide {
        line-height: 14px;
        font-size: 9px;
        color: #7a7f88;
      }
    }
    .pic {
      top: auto;
      bottom: 0;
      width: auto;
      height: 240px;
      img {
        max-height: 100%;
      }
    }
  }
  .cont2 {
    .point {
      margin: 30px 0 16px;
      .tit {
        font-weight: 800;
        font-size: 15px;
        color: #222;
      }
      ul li {
        position: relative;
        padding-left: 7px;
        line-height: 23px;
        font-size: 13px;
        color: #222;
        &:before {
          content: '';
          display: block;
          position: absolute;
          top: 10px;
          left: 0;
          width: 2px;
          height: 2px;
          background: #a20013;
        }
      }
    }
    .story {
      margin: 0;
      background: none;
      .tit {
        font-weight: 800;
        font-size: 15px;
        color: #222;
        background: none;
      }
    }
    
  }
}
</style>