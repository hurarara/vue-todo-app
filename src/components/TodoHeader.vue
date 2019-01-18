<template>
    <!-- HTML 태그 내용 -->
    <!-- 화면에 표시할 요소들을 정의하는 영역, HTML+뷰 데이터 바인딩 -->

    <!-- 제목을 표시한다. -->
    <header>
        <h1>Todo It!</h1>
    </header>
</template>

<script>
    export default {
        // 자바 스크립트 내용
        // 뷰 컴포넌트의 내용을 정의하는 영역, template, data, methods 등
        // export default {} 는 ES6의 자바스크립트 모듈화와 관련된 문법.
    }
</script>

<!-- scoped : 뷰의 속성으로 스타일 정의를 해당 컴포넌트에만 적용한다는 의미. -->
<style scoped>
    /* CSS 스타일 내용 */
    /* 템플릿에 추가한 HTML 태그의 CSS 스타일을 정의하는 영역 */

    /* 제목의 텍스트 색, 굵기, 여백 지정 */
    h1 {
        color : #2F3B52;
        font-weight : 900;
        margin : 2.5rem 0 1.5rem;
    }
</style>