<template>
<div>
  <to-do-filter />
  <v-sheet
    class="fill-height overflow-hidden"
    style="position: relative;"
  >
  <v-container class="fill-height">
    <v-row class="mb-6">
      <v-col >
        <v-card class="elevation-12">
          <ToDoList :done="false" />
        </v-card>
      </v-col>
      <v-col >
        <v-card class="elevation-12">
          <ToDoList :done="true" />
        </v-card>
      </v-col>
      <v-col md="auto">
        <v-navigation-drawer
          v-model="showEdit"
          :permanent="showEdit"
          right
        >
          <ToDoDetail  />
          <v-divider></v-divider>
        </v-navigation-drawer>
      </v-col>
    </v-row>
  </v-container>

  </v-sheet>

  <!-- <v-btn @click="setTodosWithDefault()">setTodosWithDefault</v-btn>
  <br />
  {{todos}} -->

</div>
  
 
</template>

<script>
import ToDoList from '../components/ToDoList.vue';
import ToDoFilter from '../components/ToDoFilter.vue';
import ToDoDetail from '../components/ToDoDetail.vue';

/**
 * ToDo 페이지 컴포넌트.
 * 
 * A component that allows users to manage their to-do lists, which serve as a page.
*/
export default {
    name: 'ToDo',

    components: {
      ToDoList,
      ToDoFilter,
      ToDoDetail
    },
    data: () => ({
      showEdit:false,
      todos:null,
      selectedTodoId:-1,
    }),
  /**
   * data 옵션에 포함된 속성과 같은 이름으로 globalStore안에도 생성해 주면 해당 속성 값은 전역으로 공유된다.
   * 
   * If a property with the same name as the property included in 
   * the data option is added in the globalStore, the property value is shared globally.
  */
    globalStore:{
      showEdit:{},
      todos:{},
      selectedTodoId:{
        /**
         * onReceived 메소드는 연결된 data 옵션 변수가 새 값을 수신한 이후 호출되는 콜백이다.
         * 
         * onReceived method is a callback called after the related data option property receives a new value.
        */
        onReceived: function(val) {
          console.log('selectedTodoId.onReceived', val);
          /**
           * selectedTodoId가 변경될 때 showEdit를 true로 설정해 
           * ToDoDetail 컨트롤이 화면에 나타나도록 한다.
           * 
           * When selectedToId is changed, showEdit is set to true 
           * so that ToDoDetail control pops in on the screen.
          */
          if (this.selectedTodoId !== -1)
            this.showEdit = true;
        },
      },
    },
    created() {
      /**
       * Vue 컴포넌트의 created 단계부터는 globalStore에 포함된 속성이 변경되면 전역으로 전파된다.
       * 좀더 정확히, created부터 beforeDestory전 단계 범위에서 발생한 변경 데이터는 모두 공유된다.
       * https://kr.vuejs.org/v2/guide/instance.html#라이프사이클-다이어그램
       * 
       * From the created stage of the Vue component, 
       * every time a property managed by ScopedStore are changed, it propagates globally.
       * More accurately, all changes happened in the range of the steps from created to before BeforeDestory will be shared.
       * https://vuejs.org/v2/guide/instance.html#Lifecycle-Diagram
      */
      if (this.todos === null)
        //todos에 설정한 값은 어플리케이션 전역적으로 공유된다.
        //The value set in todos is shared throughout the application.
        this.setTodosWithDefault();  
    },
    methods:{
      /**
       * todos 배열에 기본 샘플 값을 설정함.
       * 
       * Sets the example value in the todos array.
      */
      setTodosWithDefault() {
        this.todos = [
          {
            id:1,
            title:'Todo 1',
            isDone:false,
            isPrivate:true
          },
          {
            id:2,
            title:'Todo 2',
            isDone:true
          },
          {
            id:3,
            title:'Todo 3',
            isDone:false,
            isBusiness:true
          },
          {
            id:4,
            title:'Todo 4',
            isDone:true,
            isBusiness:true,
            isPrivate:true,
          }
        ];

        console.log('setTodosWithDefault()', this.todos);
      }
    }
 }
</script>
