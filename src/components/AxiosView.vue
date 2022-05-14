<template>
    <div>
        <select v-model="mode">
            <option value="doc">웹문서</option>
            <option value="mov">동영상</option>
            <option value="img">이미지</option>
        </select>
        <input type="text" v-model="search" @keyup.enter="callData">
        <button @click="callData">검색</button>

        <table v-if='list.length!=0'>
            <div v-if="mode=='doc'">
                <tr>
                    <td colspan=2 align="right">{{this.meta.pageable_count}} / {{this.meta.total_count }}</td>
                </tr>
                <tr>
                    <th>웹검색 결과 제목</th>
                    <th>내용</th>
                </tr>
                <tr v-for="(item, index) in list" :key="index">
                    <td>
                        <a :href="item.url" target="_blank">
                        <span v-html="item.title"></span>
                        </a>
                    </td>
                    <td>
                        <span v-html="item.contents"></span>
                    </td>
                </tr>
            </div>
            <div v-else-if="mode=='mov'">
                <tr>
                    <td colspan=2 align="right">{{this.meta.pageable_count}} / {{this.meta.total_count }}
                    </td>
                </tr>
                <tr>
                    <th>동영상 검색 제목</th>
                    <th>내용</th>
                </tr>
                <tr v-for="(item, index) in list" :key="index">
                    <td>
                        <a :href="item.url" target="_blank">
                            <span v-html="item.title"></span>
                        </a>
                    </td>
                    <td>
                        <a :href="item.url"><img :src="item.thumbnail" _targte="blank"></a>
                    </td>
                </tr>
            </div>
            <div v-else-if="mode=='img'">
                <tr>
                    <td colspan=2 align="right">{{this.meta.pageable_count}} / {{this.meta.total_count }}</td>
                </tr>
                <tr>
                    <th>이미지 검색 제목</th>
                    <th>내용</th>
                </tr>
                <tr v-for="(item, index) in list" :key="index">
                    <td>
                        <span><a :href="item.doc_url">{{item.display_sitename}}</a></span>
                    </td>
                    <td>
                        <span><img :src="item.thumbnail_url"></span>
                    </td>
                </tr>
            </div>
        </table>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data : () => ({
        search : '',
        list : [],
        meta : {},
        mode : 'doc',
    }),

    methods : {
        callData() {
            console.log("[LOG] "+this.mode);
            switch(this.mode){
                case 'doc' :
                    this.callWebDoc();
                    break;
                case 'mov' :
                    this.callMov();
                    break;
                case 'img' : 
                    this.callImg();
                    break;
            }
        },
        callWebDoc() {
            axios.get(`https://dapi.kakao.com/v2/search/web?query=${this.search}`, {
                headers : {
                    Authorization : `KakaoAK ${process.env.VUE_APP_KAKAO_KEY}`
                }
            }).then(response=>{
                this.list=response.data.documents;
                this.meta=response.data.meta;
            }).catch(error=>{
                console.log("[Error] " +error);
                console.error(error);
            });
        },
        callMov() {
            axios.get(`https://dapi.kakao.com/v2/search/vclip?query=${this.search}`, {
                headers : {
                    Authorization : `KakaoAK ${process.env.VUE_APP_KAKAO_KEY}`
                }
            }).then(response=>{
                this.list=response.data.documents;
                this.meta=response.data.meta;
                console.log(this.list);
            }).catch(error=>{
                console.error(error);
            });
        },
        callImg() {
            axios.get(`https://dapi.kakao.com/v2/search/image?query=${this.search}`, {
                headers : {
                    Authorization : `KakaoAK ${process.env.VUE_APP_KAKAO_KEY}`
                }
            }).then(response=>{
                this.list=response.data.documents;
                this.meta=response.data.meta;
            }).catch(error=>{
                console.error(error);
            });
        },
   },
}
</script>

<style>

</style>