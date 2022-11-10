<template>
  <div>
    <NavHeader />
    <!-- Wrapper -->
    <br />
    <div id="wrapper">
      <!-- Main -->
      <div id="main">
        <div class="inner">
          <!-- Header -->
          <header id="header">
            <a href="/board" class="logo">
              <h3>자유게시판</h3>
            </a>
          </header>
          <!-- Content -->

          <h1>Generic</h1>

          <p>
           {{detailList}}
          </p>
          <hr>
          <section style="width:1300px">
            <header class="main">
              <table class="table">
                <thead>
                  <tr>
                    <th scope="col">#</th>
                    <th scope="col">First</th>
                    <th scope="col">Last</th>
                    <th scope="col">Handle</th>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <th scope="row">1</th>
                    <td>Mark</td>
                    <td>Otto</td>
                    <td>@mdo</td>
                  </tr>
                </tbody>
              </table>
            </header>
            <!-- 
									<span class="image main"><img src="images/pic11.jpg" alt="" /></span> -->

            <!-- Preloader -->
            <div class="preloader"></div>
            <br />
            <div class="input-group mb-3">
              <input type="text" class="form-control" placeholder="Recipient's username"
                aria-label="Recipient's username" aria-describedby="button-addon2" />
              <button class="btn btn-outline-secondary" type="button" id="button-addon2">
                답글쓰기
              </button>
            </div>
          </section>
        </div>
      </div>

      <!-- Sidebar -->
    </div>
  </div>
</template>
<script>
import Axios from 'axios'
import NavHeader from "../views/NavHeader.vue";
export default {
  data: function () {
    return {
      detailList: [],
      boardId:"", 

    };
  },

  components: {
    NavHeader
  },
  mounted: function () {
    let vm = this;
    vm.test();
  
  },

  methods: {
    test : function(){
      let vm = this;

      let board_id = vm.$route.query.boardId;

      let url = "/question/detail/"+board_id
      console.log(url);
      Axios.get(url).
          then(function (response) {
              vm.detailList = response.data;
              console.log(vm.detailList);
              // for (var i = 0; i < vm.listdata.length; i++) {
                  // console.log(vm.listdata[i].content);
              // }
          }).catch(function (ex) {
              console.log(ex);
          });
      },  
      
    

    fetchContacts: function () {
      // this ~다수 많이 한개이상 
      let vm = this;

      let sendData = {}

      Axios.get("/question/api/list3", sendData).
        then(function (response) {
          vm.listdata = response.data.content;

          for (var i = 0; i < vm.listdata.length; i++) {
            console.log(vm.listdata[i].content);
          }
        }).catch(function (ex) {
          console.log(ex);
        });
    },
  }

};
</script>
<style>
@import "../../boardread/css/boardread.css";

body {
  display: flex;
}
</style>
