<template>
    <!-- HTML 태그 내용 -->
    <!-- 화면에 표시할 요소들을 정의하는 영역, HTML+뷰 데이터 바인딩 -->

    <div id="app">
        <TodoHeader></TodoHeader>
        <!-- 이벤트 전달 받음-->
        <!-- inputAddTodo : TodoInput.vue에서 넘어오는 이벤트명, appAddTodo : App.vue의 메소드 -->
        <TodoInput v-on:inputAddTodo="appAddTodo"></TodoInput>
        <!-- 데이터 전달 함-->
        <!-- propsdata : TodoList.vue로 전달할 파라미터명, todoItems : App.vue에서 선언된 변수-->
        <TodoList v-bind:propsdata="todoItems" v-on:listRemoveTodo="appRemoveTodo"></TodoList>
        <TodoFooter v-on:footRemoveAll="appRemoveAll"></TodoFooter>
    </div>
</template>

<script>
    // 싱글 파일 컴포넌트 체계에서 다른 위치에 있는 컴포넌트를 불러올 때 다음과 같이 import 한다.
    // ES6 방식 : import 구문으로 컴포넌트의 내용을 불러와 담고 넘겨준다.
    import TodoHeader from './components/TodoHeader.vue'
    import TodoInput from './components/TodoInput.vue'
    import TodoList from './components/TodoList.vue'
    import TodoFooter from './components/TodoFooter.vue'

    // ES5 방식 : var로 선언한 객체에 컴포넌트 내용을 담고 넘겨준다.
    // var TodoHeader = {
    //     template : '<div>header</div>'
    // };

    export default {
        // 자바 스크립트 내용
        // 뷰 컴포넌트의 내용을 정의하는 영역, template, data, methods 등
        // export default {} 는 ES6의 자바스크립트 모듈화와 관련된 문법.
        
        // todoItems 선언
        data() {
            return {
                todoItems : []
            }
        },
        // 라이프사이클 created()
        created() {
            if(localStorage.length > 0) {
                // 로컬 스토리지에 저장된 데이터를 한 번에 불러올 수 있는 API는 없어서 반복문을 돌린다.
                for(var i = 0; i < localStorage.length; i++) {
                    this.todoItems.push(localStorage.key(i));
                }
            }
        },
        methods : {
            // TodoInput.vue에서 이벤트를 통해 전달받은 value를 todoItem으로 가져옴
            appAddTodo(todoItem) {
                // 로컬스토리지에 데이터를 추가하는 로직
                localStorage.setItem(todoItem, todoItem);
                this.todoItems.push(todoItem);
            },
            appRemoveTodo(todoItem, index) {
                // 로컬스토리지에 아이템을 삭제
                localStorage.removeItem(todoItem);
                // splice() : 자바스크립트에 기본적으로 내장되있는 API. 배열의 특정 인덱스에서 부여한 숫자만큼의 인덱스를 삭제.
                // todoItems 배열에서 인덱스를 삭제
                this.todoItems.splice(index, 1);
            },
            appRemoveAll() {
                localStorage.clear();
                this.todoItems = [];
            }
        },
        // 지역 컴포넌트 등록
        components : {
            'TodoHeader' : TodoHeader,
            'TodoInput' : TodoInput,
            'TodoList' : TodoList,
            'TodoFooter' : TodoFooter
        }
    }
</script>

<style>
    /* CSS 스타일 내용 */
    /* 템플릿에 추가한 HTML 태그의 CSS 스타일을 정의하는 영역 */

    /* App.vue CSS */
    /* 애플리케이션 전체의 텍스트 정렬 방식과 배경색 지정 */
    body {
        text-align : center;
        background-color : #F6F6F8;
    }
    /* 인풋 박스의 테두리 모양 정의 */
    input {
        border-style : groove;
        width : 200px;
    }
    /* 버튼의 테두리 모양 정의 */
    button {
        border-style : groove;
    }
    /* 그림자 정의 */
    /* .과 #의 차이 : #은 id, .은 클래스 */
    .shadow {
        box-shadow : 5px 10px 10px rgba(0, 0, 0, 0,03)
    }
</style>