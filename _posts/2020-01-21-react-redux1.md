---
title: 리액트-리덕스(Redux) 컨테이너 연결은 최상단 컴포넌트에만 하는 게 맞나? 이젠 아니다. 
date: 2020-01-20 20:00:00
description: <center>react-redux, react, utils, redux</center>

categories:
- redux
- react
- react-redux
tags:
- react
- redux
- react-redux
---

>  ======================================================================<br>
Should I only connect my top component, or can I connect multiple components in my tree?<br>
> [https://redux.js.org/faq/react-redux/#should-i-only-connect-my-top-component-or-can-i-connect-multiple-components-in-my-tree](https://redux.js.org/faq/react-redux/#should-i-only-connect-my-top-component-or-can-i-connect-multiple-components-in-my-tree)
   ======================================================================

redux connect로 store와의 연결은 아직도 최상단(top component)에만 해야하고
 store에서 최상단 컴포넌트가 값을 받아 자식컴포넌트들에게 props로 그 값들을 줘야 할까?
만약 각각의 모든 컴포넌트들을 분리 독립적으로 connect해서 store에서 따로 받아 오게 하면 성능에 악영향은 없을까?라는
고민을 해본적이 있다. 

### 응 해도 된대. 그게 더 좋다
___
```.javascript
//이렇게 연결하는 것은 꼭 최상단 컴포넌트만 해줄 필요는 없다. 모든 각각의 컴포넌트들을 연결해줘도 괜찮다.
const mapStateToProps = (state) => {
    return {
        clientIdx: clientIdxSelect(state),
        loading: babyInfoLoadingSelect(state),
        updateMode: babyInfoIsUpdateModeSelect(state),
        currentModifyBaby: babyInfoCurrentModifyBabySelect(state),
        TEXT:COMMON_COMPONENT_TEXT_RESELECTOR(state),
        ERROR_TEXT:ERROR_TEXT_RESELECTOR(state),
    }
};
//이렇게 프레젠 테이션컨테이너에서만 연결할 필요는 없다. 각각의 하위 컴포넌트들도 전부 connect로 감싸서 연결해줘도 된다. 
//그게 성능상으로도 더 이득이라고 한다.
export default connect(mapStateToProps, mapDispatchToProps)(BabyRegisterModalComponent);
```
> 보통 이렇게 많이 넘겼다 dumbcomponent들은 top component에서 받은 값을 내려 받는 식으로..

![https://user-image.githubusercontent.com/32691294/72789471-323f3780-3c77-11ea-854b-9ddb2aa81beb.png](https://user-images.githubusercontent.com/32691294/72789471-323f3780-3c77-11ea-854b-9ddb2aa81beb.png)

근데 redux 공홈에 따르니 [https://redux.js.org/faq/react-redux/#should-i-only-connect-my-top-component-or-can-i-connect-multiple-components-in-my-tree](https://redux.js.org/faq/react-redux/#should-i-only-connect-my-top-component-or-can-i-connect-multiple-components-in-my-tree)
다 연결해도 된단다. 성능도 좋단다.
<br/>그러니 <em>걱정</em>안해도 될 것 같다.

### 결국 모든 컴포넌트들을 Store에 connect 시켰습니다 그래서. 해보고 나니 오히려 더 나아졌고, 상태관리도 한층 더 편해졌습니다. 캬



