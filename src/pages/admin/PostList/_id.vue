<template >
    <div class="form-add">
        <h3>THÊM DỮ LIỆU</h3>
        <div class="post-name">
            <input type="text" placeholder="Nhập tên bài viết" v-model="name">
        </div>
        <div class="image-author">
            <input type="text" placeholder="Nhập link ảnh tác giả" v-model="author">
        </div>
        <div class="image-post">
            <input type="text" placeholder="Nhập link ảnh" v-model="image">
        </div>
        <div class="content">
            <input type="text" placeholder="Nội dung" v-model="content">
        </div>
        <div class="date">
            <input type="text" placeholder="Ngày tạo" v-model="date">
        </div>
        <div class="add"><button @click="addButton()">Cập nhật</button></div>
    </div>
</template>
<script setup>
import { useRoute } from 'vue-router';

import { ref } from 'vue';
import { unref } from 'vue';
import axios from "axios";
const name = ref('')
const author = ref('')
const content = ref('')
const date = ref('')
const image = ref('')
const route = useRoute()


const addButton = function () {
    axios.patch(`http://localhost:3000/posts/${route.params.id}`, {
        title: unref(name),
        author: unref(author),
        image: unref(image),
        shortDecription: unref(content),
        date: unref(date)
    })
    .then(function (response) {
        let arrTemp = JSON.parse(JSON.stringify(response.data))
        window.location.href = '/';
    });
}
</script>   
<style >
.form-add {
    top: 100px;
    position: relative;
    margin: auto;
    width: 30%;
    border: 3px solid rgb(146, 149, 146);
    padding: 10px;
    background-color: antiquewhite;
}

.form-add h3 {
    display: flex;
    justify-content: center;
}

.form-add>* {
    padding-bottom: 10px;
    margin: 0 auto;
    display: flex;
}

.form-add input {
    width: 350px;
}

.form-add>*>* {
    padding: 10px;
    margin: 0 auto;
    display: flex;
    width: 40%;
}

.add button {
    display: flex;
    align-items: center;
    justify-content: center;
}
</style>