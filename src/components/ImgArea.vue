<template>
  <div class="imgArea">
    <div ref="imgList" class="imgList">
      <template v-for="index in imgNum" :key="index">
        <div class="item">
          <img :id="`img${index}`" :data-src="'/img/' + Menu[Math.floor(Math.random() * Menu.length)]"
            :alt="`Acg Img ${index}`" class="lazyload" @click="setShowPic(`img${index}`)">
        </div>
      </template>
    </div>

    <teleport to='body'>
      <transition name="showPic">
        <div v-if="showPic" id="showPic">
          <div>
            <img :src="showPicSrc" alt="">
          </div>
          <div class="tools">
            <ul>
              <li>
                <a :href="showPicSrc" :download="showPicSrc">
                  <img src="../assets/download.svg" alt="">
                </a>
              </li>
              <li @click="closePic">
                <img src="../assets/close.svg" alt="">
              </li>
            </ul>
          </div>
        </div>
      </transition>
    </teleport>

  </div>
</template>

<script>
import 'lazysizes';
import Menu from '@/menu.js'
import { ref, onMounted, onBeforeUnmount } from 'vue'
export default {
  name: 'ImgArea',
  setup(props, context) {
    const imgList = ref(null)
    let showPic = ref(false)
    let imgNum = ref(20)
    let Apis = [
      // 'https://www.dmoe.cc/random.php',
      // 'https://api.ghser.com/random/api.php',
      'https://api.ghser.com/random/bg.php',
      'https://www.loliapi.com/acg/pc/'
    ]
    let showPicSrc = ref('/img/' + Menu[2])

    function checkPosition() {
      let scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
      //变量windowHeight是可视区的高度
      let windowHeight = document.documentElement.clientHeight || document.body.clientHeight;
      //变量scrollHeight是滚动条的总高度
      let scrollHeight = document.documentElement.scrollHeight || document.body.scrollHeight;
      if (Math.round(scrollTop) + windowHeight > (scrollHeight - 100)) {
        imgNum.value += 15
      }
    }
    function closePic() {
      showPic.value = false
    }
    function setShowPic(target) {
      let dom = document.querySelector(`#${target}`)
      showPicSrc.value = dom.getAttribute('src')
      showPic.value = true
    }
    onMounted(() => {
      window.addEventListener('scroll', () => {
        checkPosition()
      })
    })

    onBeforeUnmount(() => {
      window.removeEventListener('scroll', () => {
        checkPosition()
      })
    })

    return {
      imgNum,
      Apis,
      imgList,
      showPic,
      closePic,
      Menu,
      showPicSrc,
      setShowPic
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less" scoped>
#showPic {
  position: fixed;
  height: 100%;
  width: 100%;
  background-color: rgba(26, 23, 23, 0.896);
  z-index: 1000;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;

  .tools {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;

    ul {
      list-style: none;
      padding: 0;

      li {
        padding: 0 30px;
        display: inline-block;

        img {
          width: 30px;
          filter: invert(100%);
        }
      }
    }
  }


  >div {
    max-width: 80%;
    max-height: 80%;
    overflow: hidden;

    img {
      max-width: 100%;
      object-fit: cover;
    }
  }

}

.imgArea {
  width: 100%;
  margin-top: 80px;

  .imgList {
    margin: 0 auto;
    max-width: 90%;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;

    .item {
      margin: 5px;
      width: calc(100%/3 - 10px);
    }

    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      transition: all 0.5s linear;
      cursor: pointer;

      &:hover {
        transform: scale(1.2);
        transition: all 0.1s linear;
      }
    }
  }
}

.lazyload {
  opacity: 0;
}

@media screen and (max-width: 600px) {
  .imgArea {
    imgList {
      width: 100% !important;
    }

    .item {
      width: calc(100% - 10px) !important;
    }

    img:hover {
      transform: none !important;
      border: none !important;
      transition: all 0s linear !important;
    }
  }
}

@media screen and (max-width: 1200px) {
  .imgArea {
    imgList {
      width: 95% !important;
    }

    .item {
      width: calc(100%/2 - 10px) !important;
    }

    img:hover {
      transform: none !important;
      border: none !important;
      transition: all 0s linear !important;
    }
  }
}

.showPic-enter-from {
  opacity: 0;
}

.showPic-leave-to {
  opacity: 0;
}

.showPic-enter-to {
  opacity: 1;
}

.showPic-leave-from {
  opacity: 1;
}

.showPic-enter-active {
  transition: all 0.3s linear;
}

.showPic-leave-active {
  transition: all 0.3s linear;
}
</style>
