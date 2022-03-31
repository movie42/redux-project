리덕스는 store가 있다.
store는 정보가 저장되는 곳이다.

state는 상태가 저장되는 곳이다.
state는 직접 접근이 불가능하다. 접근하려면 누군가를 통해서만 접근할 수 있다.

store를 만들 때 reducer라는 함수를 만들어서 공급해주어야한다.

```js
function reducer(old, action) {}

const store = Redux.createStroe(reducer);
```

render는 UI를 어떻게 보여줄 것인지 역할을 하는 함수다.

render에서는 state에 getState를 통해 state를 가져올 수 있다.

state값이 변경될 때마다 render에서 subscribe를 호출해서 UI를 변경할 수 있다.

dispatch

reducer를 호출해서 state를 변경한다.
dispatch는 reducer에 action과 state를 보낸다.

reducer는 dispatch에서 온 action과 state를 보고 state를 갱신한다.

subscripe는 dispatch에서 호출하는데 (state가 변경됐을 때) render에게 변경을 알려주고 state를 다시 새롭게 render한다.

subscribe

getState

redux를 쓰면 좋은 이유?

- redux를 사용하면 중앙 집중적인 store를 사용해서 어플리케이션을 만들 수 있다.

- 컴포넌트를 느슨하게 연결할 수 있다. 그래서 다른 컴포넌트를 지우더라도 에러를 최소화할 수 있다.

dispatch는 action을 전달하는 역할을 한다.

```js
const store = Redux.create(reducer);

button.addEventListener("click", () => {
  store.dispatch({ type: "CHANGE_COLOR", color: "red" });
});
```

reducer는 dispatch로부터 받은 action을 보고 역할을 수행한다.

```js
function reducer(state, action) {
  if (state === undefined) {
    return { color: "yellow" };
  }

  let newState;
  if (action.type === "CHANGE_COLOR") {
    newState = Object.assign({}, state, { color: action.color });
  }
  return newState;
}
```

새로운 state를 반환할 때는 original state를 복제한 다음 해당 값을 덮어쓰기하거나 삭제하는 방법으로 로직을 작성하는것이 좋다. 그래야 redux에서 시간여행이 가능해진다고 한다. state를 복제할 때는 Object.assign()을 사용한다.

불변(immutable)

원본은 불변해야한다. 각각의 데이터는 독립적이어야한다.
