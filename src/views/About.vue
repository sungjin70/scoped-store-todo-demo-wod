
<template>
  <div class="about">

  <v-container class="fill-height">
    <v-row>
      <v-col >
        <h2 class="headline font-weight-bold mb-3">
          You can see all states that managed by ScopedStore here.
        </h2>
      </v-col>
    </v-row>
    <v-row>
      <v-col >
  <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">
            Name
          </th>
          <th class="text-left">
            Value
          </th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td >todos:</td>
          <td>{{todos}}</td>
        </tr>
        <tr>
          <td >selectedTodoId:</td>
          <td>{{selectedTodoId}}</td>
        </tr>
        <tr>
          <td >showEdit:</td>
          <td>{{showEdit}}</td>
        </tr>
        <tr>
          <td >filter:</td>
          <td>{{filter}}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>

      </v-col>
    </v-row>
  </v-container>

  </div>
</template>

<script>
/**
 * About 페이지 컴포넌트.
 * 이 컴포넌트는 어플리케이션에서 사용되는 모든 전역 변수들의 값을 테이블 형식으로 출력한다.
 * 
 * A About component that serve as a page, which shows 
 * values of all stats used in the application in table format.
*/
export default {
  name: 'About',

  data: () => ({
    showEdit:false,
    todos:[],
    selectedTodoId:-1,
    filter:{},
  }),
  globalStore:{
    showEdit:{},
    todos:{},
    selectedTodoId:{},
    filter:{},
  }
};
</script>