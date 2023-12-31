### [과제] 숙련주차 과제 답

#### Q1. 추가하기 버튼을 클릭해도 추가한 아이템이 화면에 표시되지 않음.

```javascript
const onClickHandler = (event) => {
  event.preventDefault();
  const newTodo = {
    id: id,
    title: todo.title,
    body: todo.body,
    isDone: false,
  };
  if (todo.title.trim() !== "" && todo.body.trim() !== "") {
    dispatch(addTodo(newTodo));
    setTodo({ ...todo, id: id, title: "", body: "" });
  }
};
```

<br>

dispatch로 데이터를 보내는 코드와
보내야하는 newTodo데이터가 누락되어 있었다.
newTodo를 선언, 할당하는 문을 추가하고,
dispatch를 통해 데이터를 보내주었다.

추가적으로 if 조건은 or가 아닌 and로 수정하고,
setTodo에 title과 body를 빈 문자열로 수정해주었다.

<br>

#### Q2. 추가하기 버튼 클릭 후 기존에 존재하던 아이템들이 사라짐.

```javascript
case ADD_TODO:
      return {
        ...state,
        todos: [...state.todos, action.payload],
      };
```

<br>

todos.js의 case문에서 추가가 아닌 교체가 되는 문제였다.
todos부분을 [...state.todos, action.payload]로 수정하여 해결했다.

<br>

#### Q3. 삭제 기능이 동작하지 않음.

```javascript
case DELETE_TODO:
      return {
        ...state,
        todos: state.todos.filter((todo) => todo.id !== action.payload),
      };
```

<br>

todos.js의 case문이 아예 누락되어 있었다.
filter메서드를 통해 todos중에서 payload로 받은 id와 같지 않은 것을 리턴하는 내용의 case DELETE_TODO를 추가하여 해결했다.

<br>

#### Q4. 상세 페이지에 진입하였을 때 데이터가 업데이트 되지 않음.

```javascript
useEffect(() => {
  dispatch(getTodoByID(id));
}, [dispatch, id]);
```

<br>

useParams() 훅을 통해 URL에서 가져온 id 파라미터를 getTodoByID() 에 전달하여 useSelector()로 구독중인 todo 상태를 업데이트 해야 한다.

useEffect() 훅을 사용하여 컴포넌트가 마운트될 때 getTodoByID() 액션을 디스패치한다.

<br>

#### Q5. 완료된 카드의 상세 페이지에 진입하였을 때 올바른 데이터를 불러오지 못함.

```javascript
<StLink to={`/${todo.id}`} key={todo.id}>
  <div>상세보기</div>
</StLink>
```

<br>

Link설정이 index로 잘못 되어 있었다.
todo.id로 변경해 해결하였다.

<br>

#### Q6. 취소 버튼 클릭시 기능이 작동하지 않음.

```javascript
<StButton borderColor="green" onClick={() => onToggleStatusTodo(todo.id)}>
  {todo.isDone ? "취소!" : "완료!"}
</StButton>
```

<br>

단순 함수명이 아닌 화살표 함수로 onClick 함수를 적었고
인자로 todo.id를 보내주었다.
onClick={() => onToggleStatusTodo(todo.id)}

<br>

#### 배포 URL

[🔗 vercel로 배포한 프로젝트 바로가기](https://test-todo-list-02.vercel.app/)
