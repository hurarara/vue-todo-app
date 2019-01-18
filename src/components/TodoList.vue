<template>
    <!-- HTML 태그 내용 -->
    <!-- 화면에 표시할 요소들을 정의하는 영역, HTML+뷰 데이터 바인딩 -->

    <section>
        <ul>
            <!-- v-for 디렉티브를 이용해 아이템의 개수만큼 반복 -->
            <!-- v-for : 지정한 뷰 데이터의 개수만큼 해당 HTML 태그를 반복 출력. -->
            <!-- index : v-for 디렉티브에서 기본적으로 제공하는 변수 -->
            <!-- ESLint 플러그인으로 인해 에러가 기존은 맞지않는 문법이라고 나옴. 그래서 :key="index" 코드를 추가 -->
            <li v-for="(todoItem, index) in propsdata" :key="index" class="shadow">
                <!-- 체크 아이콘 -->
                <i class="checkBtn fas fa-check" aria-hidden="true"></i>
                {{ todoItem }}
                
                <!-- 삭제이벤트를 적용해주기 위한 영역 -->
                <!-- @click은 v-on:click과 동일하게 작용 -->
                <span class="removeBtn" type="button" @click="listRemoveTodo(todoItem, index)">
                    <!-- 휴지통 아이콘 -->
                    <i class="far fa-trash-alt" aria-hidden="true"></i>
                </span>
            </li>
        </ul>
    </section>
</template>

<script>
    export default {
        // 자바 스크립트 내용
        // 뷰 컴포넌트의 내용을 정의하는 영역, template, data, methods 등
        // export default {} 는 ES6의 자바스크립트 모듈화와 관련된 문법.

        // App.vue에서 propsdata를 통해 데이터를 전달받는다.
        props : ['propsdata'],

        // 로컬 스토리지의 데이터를 뷰 데이터로 저장한다.
        // 기능 개선에서 propsdata를 받기때문에 불필요해짐
        // data() {
        //     return {
        //         todoItems : []
        //     }
        // },
        // // 라이프사이클 created()
        // created() {
        //     if(localStorage.length > 0) {
        //         // 로컬 스토리지에 저장된 데이터를 한 번에 불러올 수 있는 API는 없어서 반복문을 돌린다.
        //         for(var i = 0; i < localStorage.length; i++) {
        //             this.todoItems.push(localStorage.key(i));
        //         }
        //     }
        // },

        methods : {
            listRemoveTodo(todoItem, index) {
                // 로컬스토리지에 아이템을 삭제
                // localStorage.removeItem(todoItem);   //기능 개선을 위해 삭제
                // splice() : 자바스크립트에 기본적으로 내장되있는 API. 배열의 특정 인덱스에서 부여한 숫자만큼의 인덱스를 삭제.
                // todoItems 배열에서 인덱스를 삭제
                // this.todoItems.splice(index, 1); //기능 개선을 위해 삭제
                this.$emit('listRemoveTodo', todoItem, index);   //기능 개선을 위해 추가
            }
        }
    }
</script>

<style scoped>
    /* CSS 스타일 내용 */
    /* 템플릿에 추가한 HTML 태그의 CSS 스타일을 정의하는 영역 */

    /* 목록 스타일 */
    ul {
        list-style-type: none;  /* 목록 아이템의 스타일 */
        padding-left: 0px;
        margin-top: 0;
        text-align: left;
    }
    /* 항목 스타일 */
    li {
        display: flex;  /* flex : 비율 기준의 레이아웃 방식 */
        min-height: 50px;
        height: 50px;
        line-height: 50px;
        margin: 0.5rem 0;
        padding: 0 0.9rem;
        background: white;
        border-radius: 5px;
    }
    /* 체크아이콘 */
    .checkBtn {
        line-height: 45px;
        color: #62acde;
        margin-right: 5px;
    }
    /* 휴지통아이콘 */
    .removeBtn {
        margin-left: auto;
        color: #de4343;
        cursor: pointer;    /* 마우스 포인터 변경 */
    }
</style>