<template>
   <div class="main">
      <div class="wrapper_search">
         <div class="search_input">
            <input placeholder="Search" @keyup="fetchData" ref="Search" @keyup.enter="$router.push('/lite/search/result?query=' + $event.tsrget.value)">
            <img class="icon" :src="require('@/assets/ic.search.svg')">
            <div class="result" v-if="result">
               <ul>
                  <li class="item" v-for="item in result">
                     <router-link tag="p" :to="'/lite/info/app/' + item.id">
                        {{ item.name  }}
                     </router-link>
                  </li>
                  <li class="item" v-if="result.length == 0">
                     <p> No result :( </p>
                  </li>
               </ul>
            </div>
         </div>
         <div class="wrapper__result">
            <div v-if="!loading">
	       <div class="applist">
                  <ul>
                     <li v-for="item in apps">
                        <app-info :data="item" />
                     </li>
                  </ul>
               </div>
               <loading-more :state="LoadingMoreState" @click="fetchData" :no-more="NoMore" />
	    </div>
            <loading-app-list v-else />
         </div>
      </div>
      <lite-footer />
   </div>
</template>
<style lang="scss" scoped>
   .main {
      background-color: rgb(255, 255, 255);
      padding-top: 11.467vw;
      position: relative;

      .wrapper_search {
         padding-bottom: 17.6vw;
         position: relative;

         .search_input {
            background-color: rgb(255, 255, 255);
            height: 10.667vw;
            padding: 5.333vw;
            top: 0;
            width: 89.333vw;
            position: relative;
            z-index: 2;

            input {
               background-color: rgb(242, 243, 245);
               border-radius: 5.333vw;
               color: rgb(162, 171, 191);
               font-size: 3.733vmin;
               font-weight: 500;
               height: 100%;
               line-height: 4.267vw;
               outline-style: none;
               text-align: center;
               width: 100%;
               display: block;
               border: 0;
               position: absolute;
               z-index: 2;
            }

            .icon {
               height: 5.333vw;
               width: 5.333vw;
               z-index: 3;
               right: 3px;
               margin-top: (10.667vw / 2 - 5.333 / 2);
               position: absolute;

               z-index: 3;
            }


            .result {
               background-color: rgb(255, 255, 255);
               border-radius: 0 0 3.2vw 3.2vw;
               box-shadow: rgba(32, 33, 36, 0.28) 0 1.067vw 1.6vw 0;
               max-height: calc(100vh - 85.333vw);

               overflow: hidden scroll;
               padding-bottom: 8vw;
               width: 89.333vw;
               margin-top: (10.667vw / 2);
               padding-top: (10.667vw / 2);
               z-index: 0;

               ul {
                  margin: 0;
                  padding: 0;
                  list-style: none;
                  padding-bottom: 10.667vw;
                  padding-top: 4vw;

                  .item {
                     font-size: 4vmin;
                     font-weight: 300;
                     height: 9.6vw;
                     line-height: 9.6vw;
                     padding-left: 4.267vw;
                     padding-right: 8vw;

                     p {
                        margin: 0;
                        padding: 0;

                        color: rgb(117, 136, 169);
                        font-size: 3.733vmin;
                        font-weight: 400;
                        line-height: 4.267vw;

                        overflow: hidden;
                        text-overflow: ellipsis;
                        white-space: nowrap;
                     }
                  }
               }
            }
         }

         .wrapper__result {
            .applist {
               ul {
                  margin: 0;
                  padding: 0;
                  box-sizing: border-box;
                  list-style: none;
		  padding: 0 5.333vw;
               }

            }
	    position: relative;
	    overflow: hidden;
	    width: 100%;
	    box-sizing: border-box;
	    margin-top: 10.333vw;
	    
         }
      }
   }
</style>
<script>
   import LiteFooter from "../components/Lite.Footer.vue"
   import LoadingAppList from "../components/ListApp.Loading.vue"
   import AppInfo from "../components/AppInfo.vue"
   import LoadingMore from "../components/Button:Loading.More.vue"

   export default {
      components: { LiteFooter, LoadingAppList, AppInfo, LoadingMore },
      data: () => ({
         loading: true,

         result: null,

         apps: [],
         LoadingMoreState: false,
         NoMore: false,

      }),
      methods: {
         fetchData(loadMore) {
            if ( !loadMore ) {
               this.LoadingMoreState = true
	    }
	    
	    this.$axios.get("/admin/api/Search.php", {
                  params: {
                     query: this.$route.query.query,
                     offset: loadMore ? 0 : this.apps.length
                  }
               })
               .then(res => res.data)
               .then(({ state, data }) => {
                  if (state.error) {
                     throw new Error(state.message)
                  } else {
                     if ( !loadMore ) {
                        this.apps.push(...data)
			if ( data.length == 0 ) {
			   this.NoMore = true
			}
                     } else {
                        this.apps = data
                     }
                  }
               })
               .then(() => this.loading = this.LoadingMoreState = false)
               .catch((error) => console.log(error))
         }
      },
      created() {
         this.fetchData(true)
      }
   }
</script>
