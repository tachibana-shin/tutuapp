<template>
   <div class="loading-overlay">
      <bac-animation v-if="!children"/>
      <div class="loading.applist">
         <ul :style="{ padding }">
            <li v-for="item in 10">
               <div class="appinfo">
                  <div class="appinfo.content">
                     <div class="icon"></div>
                     <div class="app.content">
                        <div class="app.title"></div>
                        <div class="VIP"></div>
                     </div>
                  </div>
                  <div class="button"></div>
               </div>
            </li>
         </ul>
      </div>
   </div>
</template>
<style lang="scss" scoped>
   .loading-overlay {
      .loading\.applist {

         ul {
            margin: 0;
            padding: 0;
            list-style: none;
            padding: 0 5.333vw;

            li {

               .appinfo {
                  padding: 3.2vw 0;
                  position: relative;
                  display: flex;
                  justify-content: space-between;
                  align-items: center;

                  .appinfo\.content {
                     display: flex;

                     .icon {

                        border-radius: 3.467vw;
                        display: block;
                        height: 18.667vw;
                        width: 18.667vw;
                     }

                     .app\.content {
                        height: 18.667vw;
                        justify-content: center;
                        margin-left: 4.267vw;
                        overflow: hidden;
                        position: relative;
                        text-align: left;
                        align-items: flex-start;
                        display: flex;
                        flex-direction: column;

                        .app\.title {
                           margin: 0;
                           padding: 0;
                           color: rgb(47, 64, 89);
                           font-size: 4.267vmin;
                           font-weight: 500;
                           line-height: 5.867vw;
                           margin-bottom: 2.133vw;
                           overflow-x: hidden;
                           text-overflow: ellipsis;
                           -webkit-box-orient: vertical;
                           -webkit-line-clamp: 2;
                        }

                        .VIP {

                           border-radius: 3.467vw;
                           display: block;
                           height: 4.8vw;
                           width: 8vw
                        }
                     }
                  }

                  .button {
                     border: none;
                     outline: none;
                     border-radius: 50%;
                     height: 12.267vw;
                     width: 12.267vw;

                     background: {
                        repeat: no-repeat;
                        size: 100%;
                        position: center;
                     }

                     ;
                  }
               }

               .appinfo {
                  .appinfo\.content {
                     position: relative;

                     .icon {
                        background-color: rgb(237, 240, 245);
                     }

                     .app\.content {
                        .app\.title {
                           background-color: rgb(237, 240, 245);
                           width: 37.333vw;
                           height: 5.867vw;
                           border-radius: 2.133vw;
                        }

                        .VIP {
                           background-color: rgb(237, 240, 245);
                        }
                     }
                  }

                  .button {
                     background-color: rgb(237, 240, 245);
                     background-image: none;
                  }

               }
            }
         }
      }

   }
</style>

<script>
   import BacAnimation from "./Loading:bac.animation.vue"
   export default {
      props: {
         children: Boolean,
         padding: String
      },
      inheritAttrs: false,
      components: { BacAnimation }
   }
</script>