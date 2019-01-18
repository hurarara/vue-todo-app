<template>
    <!-- HTML 태그 내용 -->
    <!-- 화면에 표시할 요소들을 정의하는 영역, HTML+뷰 데이터 바인딩 -->

    <!-- 할 일을 입력하기 위한 인풋박스와 버튼을 추가 -->
    <div class="inputBox shadow">
        <!-- v-model, v-on 속성을 통해 뷰에서 인식할 수 있도록 한다. -->
        <!-- placeholder : 인풋 박스의 힌트 속성, v-on:keyup.enter : 인풋 박스에서 엔터키를 눌렀을 때 발생하는 이벤트 속성 -->
        <input type="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter="inputAddTodo">
        <!-- <span> : <button> 태그 대신 클릭 이벤트를 받을 태그 -->
        <span class="addContainer" v-on:click="inputAddTodo">
            <!-- <i class="addBtn fas fa-plus"> : 어썸 아이콘의 + 아이콘을 추가 -->
            <i class="addBtn fas fa-plus" aria-hidden="true"></i>
        </span>

        <modal v-if="showModal" @close="showModal = false" v-on:close="close">
            <!-- 모달 Header -->
            <h3 slot="header">경고</h3>
            <!-- 모달 Body -->
            <span slot="body">
                할 일을 입력하세요.
                <!-- <i class="closeModalBtn fas fa-times" aria-hidden="true"></i> -->
            </span>
        </modal>
    </div>
</template>

<script>
    // Modal.vue를 컴포넌트로 등록
    import Modal from './common/Modal.vue'

    export default {
        // 자바 스크립트 내용
        // 뷰 컴포넌트의 내용을 정의하는 영역, template, data, methods 등
        // export default {} 는 ES6의 자바스크립트 모듈화와 관련된 문법.

        // 인풋 박스의 텍스트 값을 인식
        data() {
            return {
                newTodoItem : '',
                showModal : false   //모달 동작을 위한 플래그 값
            }
        },
        // 이벤트에 대한 로직
        methods : {
            // 로컬 스토리지에 데이터를 추가한다.
            // 추가 버튼이 클릭되면 인풋 박스에 값이 있을 때만 저장하고 인풋 박스를 clear 하도록 한다.
            inputAddTodo() {
                if(this.newTodoItem !==  "") {
                    var value = this.newTodoItem.trim();

                    // setItem()의 형식은 키, 값이다.
                    // localStorage.setItem(value, value);  //기능 개선을 위해 삭제
                    this.$emit('inputAddTodo', value);   //기능 개선을 위해 추가

                    // 단일 책임 원칙(Single Responsibility Principle) : 함수 하나가 하나의 기능을 담당하도록하는 디자인 패턴
                    // this.newTodoItem = ''; 정도는 직접 이 부분에서 해줄 수 있으나 단일 책임원칙 디자인 패턴의 원칙에 따라 작성
                    this.clearInput();
                }
                else {
                    // 텍스트 미입력 시 모달 동작
                    this.showModal = !this.showModal;
                }

            },
            clearInput() {
                this.newTodoItem = '';
            },
            close() {
                Modal.close;
            }

            // 기존로직
            // addTodo() {
            // !== : 변수타입까지 고려하여 비교
            //     if(this.newTodoItem !== "") {
            //         var value = this.newTodoItem && this.newTodoItem.trim();
            //         // setItem()의 형식은 키, 값이다.
            //         localStorage.setItem(value, value);
            //         this.clearInput();
            //     }
            // }
        },
        components : {
            Modal : Modal   //모달 등록
        }
    }
</script>

<style scoped>
    /* CSS 스타일 내용 */
    /* 템플릿에 추가한 HTML 태그의 CSS 스타일을 정의하는 영역 */

    /* 인풋 박스에 포커스가 갈 때 선 스타일 지정 */
    input:focus {
        outline : tomato;
        outline-style: auto;
    }
    /* inputBox class에 배경색, 높이, 텍스트의 중앙정렬을 위한 라인높이, 둥근테두리 적용 */
    .inputBox {
        background : white;
        height : 50px;
        line-height : 50px;
        border-radius : 5px;
    }
    /* inputBox 클래스 안의 <input>태그에 테두리, 폰트 속성 적용 */
    .inputBox input {
        border-style: none;
        font-size : 0.9rem;
    }
    /* 아이콘의 배경 부분. 우측배치, 배경색(그라데이션), 너비, 둥근테두리 적용 */
    .addContainer {
        float : right;
        background : linear-gradient(to right, #6478FB, #8763FB);
        display : block;
        width : 3rem;
        border-radius : 0 5px 5px 0;
        cursor: pointer;    /* 마우스 포인터 변경 */
    }
    /* 아이콘의 + 색, 수직정렬 적용 */
    .addBtn {
        color : white;
        vertical-align : middle;
    }
</style>