<template>
  <div class="home">
    <transition name="router">
      <ul class="home_ul" v-show="show_flag">
        <li class="home_li"
          v-for = "item in main"
          @click="to_article(item._id)"
        >
          <div class="head">
            <div class="title">
              {{item.title}}
            </div>
            <div class="date">
              <i class="icon-date"></i>
              {{item.date}}
            </div>
          </div>
          <div class="body">
            <div class="tag_classify">
              <div class="tag">
                <i class="icon-tag"></i>
                {{item.tag}}
              </div>
              <div class="classify">
                <i class="icon-classify"></i>
                {{item.classify}}
              </div>
            </div>
            <div class="description">
              <p v-html = "item.description"></p>
            </div>
          </div>
        </li>
      </ul>
    </transition>
  </div>
</template>

<script type="text/ecmascript-6">
  import {mapGetters,mapActions} from "vuex";
  import {common_data} from "common/js/mixin.js";
  export default {

    name: "Home",

    mixins: [common_data],

    data(){
      return {
        talk_time: 0,
      };
    },

    computed: {
      ...mapGetters([
        "main"
      ]),
      show_flag(){
        if(this.router_show === "home" && this.data_ready){
          this.set_loading_show(false);
          return true;
        }else{
          return false;
        }
      }
    },

    methods: {
      ...mapActions([
        "add_talk_word",
      ]),
    },

    watch: {
      show_flag(){
        if(this.talk_time !== 0){
          return;
        }
        if(this.show_flag === true){
          this.add_talk_word("嘟嘟噜♪~");
          this.talk_time = this.talk_time + 1;
        }
      },
    }

  }
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
  @import "~common/stylus/variable.styl"

  .home
    .home_ul
      i
        color: $color-grey
      .home_li
        margin-top: 4rem
        background: $color-1
        border-radius: 1rem
        box-shadow: $box-shadow
        width: 100%
        cursor: pointer
        &:hover
          background: rgba(96,126,121,0.18)
        .head
          display: flex
          align-items: center
          justify-content: space-between
          height: 5rem
          padding: 0 2.5rem
          box-shadow: $box-shadow-bottom
          .title
            font-family: Georgia,serif
            font-size: 2.5rem
            letter-spacing: 0.05rem
            color: $color-3
            width: 100%
            white-space: nowrap
            text-overflow: ellipsis
            overflow: hidden
          .date
            color: $color-grey
            display: flex
            align-items: center
            font-size: 1.2rem
            margin-left: 1rem
            flex-shrink: 0
            i
              margin-right: 0.5rem
              padding-bottom: 0.2rem
        .body
          padding: 0 2.5rem
          i
            margin-right: 0.5rem
          .tag_classify
            display: flex
            color: $color-grey
            margin-top: 0.1rem
            .tag,.classify
              height: 2.4rem
              display: flex
              align-items: center
            .tag
              font-size: 1.3rem
              padding-right: 1rem
            .classify
              font-size: 1.2rem
              padding-left: 1rem
              box-shadow: $box-shadow-left
          .description
            display: flex
            height: 10rem
            align-items: center
            box-sizing: border-box
            padding-bottom: 0.8rem
            >>>p
              max-height: 7rem
              font-size: 1.4rem
              line-height: 3.5rem
              margin: 0
              letter-spacing: 0.1rem
              color: $color-grey
              display: -webkit-box
              /* autoprefixer: off */
              -webkit-box-orient: vertical
              /* autoprefixer: on */
              -webkit-line-clamp: 2
              overflow: hidden
              text-overflow: ellipsis
              strong
                padding: 0 0.15rem
              code
                font-family: Monaco, Consolas, "Courier New", monospace
                background: rgba(96,126,121,0.2)
                padding: 0 0.4rem
                border-radius: 0.2rem
      .home_li:nth-of-type(1)
        margin-top: 0


  @media (max-width: $max-width-2)
    .home
      width: calc(100% + 4rem)
      margin-left: -2rem
      .home_ul
        .home_li
          margin-top: 2.2rem
          &:hover
            background: $color-1
          .head
            position: relative
            padding: 0 1.5rem
            height: 4.5rem
            .title
              font-size: 1.7rem
            .date
              position: absolute
              top: 5.1rem
              right: 1.5rem

          .body
            padding: 0 1.5rem
            .description
              height: 12.5rem
              >>>p
                max-height: 10.5rem
                padding: 0
                padding-bottom: 0.5rem
                -webkit-line-clamp: 3


</style>
