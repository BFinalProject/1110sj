<template>
    <div>
        <NavHeader />
        <link href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.0/css/bootstrap.min.css" rel="stylesheet"
            id="bootstrap-css">
        <!------ Include the above in your HEAD tag ---------->
        <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.4.0/css/font-awesome.min.css" rel='stylesheet'
            type='text/css'>

        <div class="container" style="margin-top: 150px">
            <div class="row">
                <div class="col-md-10 col-md-offset-1">

                    <div class="panel panel-default panel-table">
                        <div class="panel-heading">
                            <div class="row">
                                <div class="col col-xs-6">
                                    <h3 class="panel-title">자유게시판</h3>
                                </div>
                                <div class="col col-xs-6 text-right">
                                    <a href="/boardwrite">
                                        <button type="button" class="btn btn-sm btn-primary btn-create">글 쓰기</button>
                                    </a>
                                </div>
                            </div>
                        </div>

                        <div class="panel-body">
                            <table class="table table-striped table-bordered table-list">
                                <thead>
                                    <tr>

                                        <th style="text-align: center" width="100" height="30">NO.</th>
                                        <th style="text-align: center">ID</th>
                                        <th style="text-align: center">글제목</th>
                                        <th style="text-align: center">날짜</th>

                                        <!-- <th><em class="fa fa-cog"></em></th> -->
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr v-for="(listdata, i) in listdata" :key="i" v-on:click="fnMoveToDetail(listdata.id)" style="cursor:pointer;">

                                        <td style="text-align: center">{{ listdata.id }}</td>
                                        <td style="text-align: center"></td>
                                        <!-- <a href="/boardread:listdata.id" > -->
                                            <!-- 링크만들어줘야하는거아님 ? ㅇㅇ? 그거 해줘? 그냥 저칸에 하나라도 누르면 가는거아니고?
                                            그냥 저거 하나만 a 태그로탐? 아아 잠시만 ㄴㄴ 이거면 ㄱㅊ 저기서 스타일넣어주면 됨 ㅇㅇ -->
                                        <!-- <a href="javascript:void(0)" @click="$router.push('/boardread:id')">   -->
                                        <td style="text-align: center">{{ listdata.subject }}</td>
                                        <!-- </a> -->
                                        <td style="text-align: center">{{ listdata.createDate }}</td>

                                        <!-- <td align="center">
                                            <a class="btn btn-default" style="width:35px; height:auto; margin:0;"><em
                                                    class="fa fa-pencil"></em></a>
                                            <a class="btn btn-danger" style="width:35px; height:auto; margin:0;"><em
                                                    class="fa fa-trash"></em></a>
                                        </td> -->
                                    </tr>
                                </tbody>
                            </table>

                        </div>
                        <div class="panel-footer">
                            <div class="row">
                                <div class="col col-xs-4">Page 1 of 5
                                </div>
                                <div class="col col-xs-8">
                                    <ul class="pagination hidden-xs pull-right">
                                        <li><a href="#">1</a></li>
                                        <li><a href="#">2</a></li>
                                        <li><a href="#">3</a></li>
                                        <li><a href="#">4</a></li>
                                        <li><a href="#">5</a></li>
                                    </ul>
                                    <ul class="pagination visible-xs pull-right">
                                        <li><a href="#">«</a></li>
                                        <li><a href="#">»</a></li>
                                    </ul>

                                </div>
                            </div>
                        </div>
                    </div>
                    <!-- <button type="button" class="btn btn-sm btn-primary btn-create">Create New</button> -->
                </div>
            </div>
        </div>
    </div>
</template>
<style>
@import '../../board/board.css';

body {
    display: block;
}
</style>
<script>
import NavHeader from '../views/NavHeader.vue'
import Axios from 'axios'
// 저거뭐 주소 상관있음? ㄴㄴ 상관없음  ㅇㅇ상관있으면 아까했던거처럼 그냥 라우터에 : id 박고 설정잡아??
export default {
    components: {
        NavHeader,
    },
    name: 'board',
    data() {
        return {
            listdata: [],
            data: "상준",
            result: "25"
        }
    },
    mounted: function () {
        let vm = this;

        vm.fetchContacts();
    },
    methods: {
        rowClick(listdata) {
      this.$router.push({
        path: `/question/api/list3${listdata.id}`
      });
    },
    // fninit:function(){
    //     let vm = this;
    //     vm.fetchContacts1();
    //     vm.fetchContacts2();
    //     vm.fetchContacts3();
    //     vm.fetchContacts4();
    //     vm.fetchContacts5();
    //     vm.fetchContacts6();
    //     vm.fetchContacts7();
    // }
        //1
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
        
        fnMoveToDetail :function(id){
            // location.href="/community/faq/View";
            location.href="/boardread?boardId="+id; 
        },
        
        
        
        
        
        
        //2 
        fnGetStat1List: function () {
            let vm = this;
            console.log(vm.data);
            let send = {
                subject: vm.data,
                id: vm.result
            };
            Axios.post("/question/api/list4", send, {})
                .then(function (res) {
                    console.log("하하!");
                });
            // this.$sendAxios("/question/list2",   function(resp){
            // vm.listdata = resp.data;
            // });
        },
        // 3
        getMembers() {
            Axios({
                url: "/api/list3",
                method: "get"
            })
                .then(res => {
                    console.log(res.data.content);
                })
                .catch(err => {
                    console.log(err);
                })
        },

        // auth: function () {
        //   const request = Axios.post('api/list3')
        //     .then(response => response.data);
        //   return {
        //     type: paging,
        //     payload: request
        //   }
        // }

    }
};
</script>