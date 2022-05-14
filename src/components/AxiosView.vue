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
            <div v-if="mode='doc'">
                <tr>
                    <td colspan=2 align="right">{{this.meta.pageable_count}} / {{this.meta.total_count }}</td>
                </tr>
                <tr>
                    <th>제목</th>
                    <th>내용</th>
                </tr>
                <tr v-for="(item, index) in list" :key="index">
                    <td>
                        <a :href="item.url" target="_blank">
                        <span v-html="iteml.title"></span>
                        </a>
                    </td>
                    <td>
                        <span v-html="item.contents"></span>
                    </td>
                </tr>
            </div>
            <div v-else-if="mode='mov'">
                <tr>
                    <th>제목</th>
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
            <div v-else-if="mode='img'">
                <tr>
                    <th>제목</th>
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
        <div v-else>검색 결과를 찾을 수 없습니다</div>
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
            //console.log(this.list.length);
            switch(this.mode){
                case 'doc' :
                    console.log(this.mode);
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
            axios.get(`https://dapi.kakao.com/v2/search/web`, {
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
            axios.get(`https://dapi.kakao.com/v2/search/vclip`, {
                headers : {
                    Authorization : `KakaoAK ${process.env.VUE_APP_KAKAO_KEY}`
                }
            }).then(response=>{
                this.list=response.data.documents;
            }).catch(error=>{
                console.error(error);
            });
        },
        callImg() {
            axios.get(`https://dapi.kakao.com/v2/search/image`, {
                headers : {
                    Authorization : `KakaoAK ${process.env.VUE_APP_KAKAO_KEY}`
                }
            }).then(response=>{
                this.list=response.data.documents;
            }).catch(error=>{
                console.error(error);
            });
        },
   },
}
</script>

<style>

</style>