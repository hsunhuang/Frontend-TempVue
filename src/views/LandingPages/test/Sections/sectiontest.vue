
<style>
thead {
    background-color: blue;
    color: cornsilk;
}
</style>

<template>
    <div id="app" class="container">


        <div class="row" style="width:50%;margin-left:auto;margin-right:10px;">
            <label class="col-lg-3 form-label">篩選</label>
            <input type="text" class="col-lg-7 form-control" v-model="filter" placeholder="請輸入關鍵字" />
            <button class="btn btn-outline-secondary" @@click="filterEmployee">篩選</button>
        </div>


        <div class="form-group">
            <button type="button" @@click="showModal" class="btn btn-success mb-3">新增紀錄</button>
        </div>

        <div class="form-group">
            <table class="table table-striped table-hover">
                <thead>
                    <tr>
                        <td>EmployeeId</td>
                        <td>FirstName</td>
                        <td>LastName</td>
                        <td>Title</td>
                        <td>Edit</td>
                    </tr>
                </thead>

                <tbody>
                    <tr v-for="(item, index) in employeeDTOes" :key="index">
                        <template v-if="item.Edit == true">
                            @*true顯示此行*@
                            <td>{{ item.employeeId }}</td>
                            <td><input v-model="item.firstName" /></td>
                            <td><input v-model="item.lastName" /></td>
                            <td><input v-model="item.title" /></td>
                            <td>
                                <button class="btn btn-primary" @click="update(item)">修改</button>
                                <button class="btn btn-warning" @click="cancel">取消</button>
                            </td>
                        </template>

                        <template v-else>
                            @*false顯示此行*@
                            <td>{{ item.employeeId }}</td>
                            <td>{{ item.firstName }}</td>
                            <td>{{ item.lastName }}</td>
                            <td>{{ item.title }}</td>
                            <td>
                                <button class="btn btn-success " @click="edit(item.employeeId)">編輯</button>
                                <button class="btn btn-danger" @click="deleteEmployee(item.employeeId)">刪除</button>
                            </td>
                        </template>
                    </tr>
                </tbody>
            </table>
        </div>


        <div class="modal fade" id="insertModal" tabindex="-1" role="dialog" aria-labelledby="modalTitleId"
            aria-hidden="true">
            <div class="modal-dialog" role="document">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="modalTitleId">Modal title</h5>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                        @*主體寫這裡*@
                        <div class="form-group">
                            <label class="form-lable">FirstName</label>
                            <input type="text" class="form-control" v-model="firstName" />
                        </div>

                        <div class="form-group">
                            <label class="form-lable">LastName</label>
                            <input type="text" class="form-control" v-model="lastName" />
                        </div>

                        <div class="form-group">
                            <label class="form-lable">Title</label>
                            <input type="text" class="form-control" v-model="title" />
                        </div>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">關閉</button>
                        <button type="button" class="btn btn-primary" @click="insert">新增</button>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>






<!-- <script src="https://unpkg.com/vue@3.2.36"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/axios/1.3.4/axios.min.js"></script>  -->


<script >
// var webApiBaseAddr = "https://localhost:7226";
// var vueApp = {
//     data() {
//         return {
//             employeeDTOes: [],
//             filter: "", //無值給字串
//             employeeId: null,
//             firstName: null,
//             lastName: null,
//             title: null,
//             firstNameOld: null,
//             lastNameOld: null,
//             titleOld: null,
//         };
//     },
//     mounted: function () {
//         let _this = this; //保留原資料在this
//         _this.getEmployeeDTOes();

//     },
//     methods: {
//         getEmployeeDTOes: function () { //呼叫後端EmployeeController資料
//             let _this = this;
//             axios.get(`${webApiBaseAddr}/api/Employees`).then(response => {
//                 //alert(JSON.stringify(response.data));
//                 _this.employeeDTOes = response.data;
//                 var employeeList = [];
//                 for (var i = 0; i < _this.employeeDTOes.length; i++) {
//                     var item = _this.employeeDTOes[i];
//                     item.Edit = false;
//                     employeeList.push(item);
//                 }
//                 _this.employeeDTOes = employeeList;
//             });
//         },

//         filterEmployee: function () {
//             // alert("filter");
//             let _this = this;
//             var p = {
//                 FirstName: _this.filter,
//                 LastName: _this.filter,
//                 Title: _this.filter
//             }
//             axios.post(`${webApiBaseAddr}/api/Employees/Filter`, p).then(response => {
//                 //alert(JSON.stringify(response.data));
//                 _this.employeeDTOes = response.data;
//                 var employeeList = [];
//                 for (var i = 0; i < _this.employeeDTOes.length; i++) {
//                     var item = _this.employeeDTOes[i];
//                     item.Edit = false;
//                     employeeList.push(item);
//                 }
//                 _this.employeeDTOes = employeeList;
//             });

//         },

//         edit: function (employeeId) {
//             //alert("edit");
//             let _this = this;
//             var employeeList = [];
//             for (var i = 0; i < _this.employeeDTOes.length; i++) {
//                 var item = _this.employeeDTOes[i];
//                 if (item.employeeId == employeeId) {
//                     item.Edit = true;
//                     _this.firstNameOld = item.firstName;
//                     _this.lastNameOld = item.lastName;
//                     _this.titleOld = item.title;

//                 }//_this:取用自己的data model
//                 else {
//                     item.Edit = false;
//                 }
//                 employeeList.push(item);
//             }
//             _this.employeeDTOes = employeeList;
//         },

//         cancel: function () {
//             //alert("cancel");
//             let _this = this;
//             var employeeList = [];
//             for (var i = 0; i < _this.employeeDTOes.length; i++) {
//                 var item = _this.employeeDTOes[i];
//                 if (item.Edit == true) {
//                     item.Edit = false;
//                     item.firstName = _this.firstNameOld;
//                     item.lastName = _this.lastNameOld;
//                     item.Title = _this.TitleOld;
//                 }
//                 employeeList.push(item);
//             }
//             _this.employeeDTOes = employeeList;

//         },

//         update: function (item) {
//             //alert("update");
//             let _this = this;
//             var p = {
//                 EmployeeId: item.employeeId,
//                 FirstName: item.firstName,
//                 LastName: item.lastName,
//                 Title: item.title
//             }
//             axios.put(`${webApiBaseAddr}/api/Employees/${item.employeeId}`, p).then(response => {
//                 alert(response.data);
//                 _this.filterEmployee();
//                 _this.cancel();
//             })
//         },

//         deleteEmployee: function (employeeId) {
//             //alert("delete");
//             let _this = this;
//             var ret = confirm("確定要刪除嗎?");
//             if (ret == true) {
//                 axios.delete(`${webApiBaseAddr}/api/Employees/${employeeId}`).then(response => {
//                     alert(response.data);

//                     _this.filterEmployee();

//                 });
//             }

//         },
//         showModal: function () {
//             //alert("showModal");
//             $('#insertModal').modal('show');
//         },

//         insert: function () {
//             //alert("insert");
//             let _this = this;
//             var p = {
//                 EmployeeId: 0,
//                 FirstName: _this.firstName,
//                 LastName: _this.lastName,
//                 Title: _this.title
//             };
//             axios.post(`${webApiBaseAddr}/api/Employees`, p).then(response => {
//                 alert(response.data);
//                 window.location = "/Home/VUESPA";
//             });
//         },

//     }
// };
// var app = Vue.createApp(vueApp).mount("#app");
</script>