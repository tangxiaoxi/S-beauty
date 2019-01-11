# S-beauty
小而美
> 本片笔记借鉴很多大牛的写法，纯属自己学习使用

* 引入全部并作为xxx对象

  ```javascript
  import * as xxx from '../root'
  ```
 
* 数组的解构

  ```javascript
  const todos = ['apple', 'banana'];
  […todos, 'a', 'b']   // [‘apple’, ‘banana’, ‘a’, ‘b’]
  ```
  
* 对象的合并

  ```javascript
  const foo = {
      a: 1,
      b: 2
  };

  const bar = {
      C: 3,
      D: 4
  };

  const d = 5;

  const rest = { …foo, …bar, d };  // { a:1, b:3, c:2, d:4 }
  ```
  
* 一个典型的dva effect

  ```javascript
  app.model({
      nameSpace: 'apple',
      effect: {
          * getData({ payload: tod }, { call, put， select }) {
              const selectState = yield select(state => state.demoId )
              yield call(api, payload)；
              yield put(type: 'add', payload: todo)
            }
      }
  })
  
  call:发起一个异步请求
  put: 出发一个action
  select: 从state中获取数据
  ```

* dva全局error处理
 
   ```javascript
   const dva = ({
    onError(e, dispatch) {
      console.log(e.message);
    },
   })
   ```
 
* dva本读错误处理

  ```javascript
  app.model({
    * effect: {
      * getData({ payload }, { call, put }) {
        try {
          //you code here
        } catch (e) {
          console.log(e)
        }
      }
    }
  })
  ```
 
* jsx借鉴es6，简化props的写法

  ```javascript
  const attr = {
    href: 'xxxx',
    target: '_blank'
  }
  <a {...attrs}>hello</a>
  ```
  
* subscriptions 订阅，订阅一种数据源，根据需要dispathc相应的action。数据源可以是当前的时间、服务器的 websocket 连接、keyboard 输入、geolocation 变化、history 路由变化等等。格式为 ({ dispatch, history }) => unsubscribe 。

  ```javascript
  app.model({
    subscriptions: {
      setup: ({ dispathc, history }) {
        histroy.listen({ pathname }) => {
          if (pathname == 'app') {
            dispatch({
              type: 'change'
            })
          }
        }
      }
    }
  })
  ```
  
 * path-to-regexp Package 从复杂的路由中提取需要的字段。 /users/:userId/search，那么匹配和 userId 的获取都会比较麻烦 [path-to-regexp]   (https://github.com/pillarjs/path-to-regexp)
 
   ```javascript
   import pathToRegexp from 'path-to-regexp';
    // in subscription
    const match = pathToRegexp('/users/:userId/search').exec(pathname);
    if (match) {
      const userId = match[1];
      // dispatch action with userId
    }
   ```

