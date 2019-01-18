<template>
    <!-- HTML 태그 내용 -->
    <!-- 화면에 표시할 요소들을 정의하는 영역, HTML+뷰 데이터 바인딩 -->


    <div class="clearAllContainer">
        <span class="clearAllBtn" @click="footRemoveAll">Clear All</span>
    </div>
</template>

<script>
    export default {
        // 자바 스크립트 내용
        // 뷰 컴포넌트의 내용을 정의하는 영역, template, data, methods 등
        // export default {} 는 ES6의 자바스크립트 모듈화와 관련된 문법.

        methods : {
            footRemoveAll() {
                // localStorage.clear();   //기능 개선을 위해 삭제
                this.$emit('footRemoveAll');   //기능 개선을 위해 추가
            }
        }
    }
</script>

<style scoped>
    /* CSS 스타일 내용 */
    /* 템플릿에 추가한 HTML 태그의 CSS 스타일을 정의하는 영역 */

    /* Clear All 버튼의 영역 */
    .clearAllContainer {
        width: 8.5rem;
        height: 50px;
        line-height: 50px;
        background-color: white;
        border-radius: 5px;
        margin: 0 auto;
        cursor: pointer;    /* 마우스 포인터 변경 */
    }
    /* Clear All 버튼 속성 */
    .clearAllBtn {
        color: #e20303;
        display: black;
    }
</style>