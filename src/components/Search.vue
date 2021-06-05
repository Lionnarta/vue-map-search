<template>
    <div class="search">
        <div class="search-bar">
            <input type="text" v-model="searchContent" :placeholder="placeholder" @keyup="searchLocation">
            <button @click="searchLocationClick">
                <img class="src-image" src="../assets/search.png"/>
            </button>
        </div>
        <div v-if="listResult.length > 0">
            <div v-for="(value, index) in listResult" :key="index" @click="searchData(value)">
                <div class="src-result">
                    {{ value.properties.label }}
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return {
            searchContent: "",
            listResult: [],
            timer: null,
            placeholder: "Find a place"
        }
    },
    methods: {
        searchData(obj) {
            this.searchContent = obj.properties.label;
            this.listResult = []
            this.$emit("searchContent", obj);
        },
        searchLocation(e) {
            var value = e.target.value;
            if (this.timer) {
                clearTimeout(this.timer);
                this.timer = null
            }
            this.timer = setTimeout(() => {
                if (value !== "") {
                    axios.get(`https://api.openrouteservice.org/geocode/search?api_key=5b3ce3597851110001cf624821878b8976b24dc6a87d32a27158398b&text=${value}`)
                        .then(res => {
                            this.listResult = res.data.features
                        });
                }
            }, 2000)
        },
        searchLocationClick() {
            if (this.searchContent !== "") {
                    axios.get(`https://api.openrouteservice.org/geocode/search?api_key=5b3ce3597851110001cf624821878b8976b24dc6a87d32a27158398b&text=${this.searchContent}`)
                        .then(res => {
                            this.listResult = res.data.features
                        });
                }
        }
    }
}
</script>

<style>
    .search {
        position: absolute;
        top: 10px;
        left: 1%;
        z-index: 1000;
    }
    .search-bar {
        display: flex;
    }
    .search-bar input {
        font-size: 18px;
        padding: 0px 20px 0px 15px;
        border-radius: 5px;
        width: 450px;
        height: 50px;
    }
    .search-bar button {
        cursor: pointer;
        margin-left: -20px;
        border-radius: 40%;
    }
    .src-image {
        width: 30px;
    }
    .src-result {
        cursor: pointer;
        padding: 10px 15px;
        width: 450px;
        background: white;
    }
    .src-result:hover {
        background: #ebe8e8;
    }
</style>