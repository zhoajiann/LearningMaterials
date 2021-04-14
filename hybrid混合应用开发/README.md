



# ReactNative

##  课程简介

##### 1、**App开发模式**

- Native App
  - 基于本地（操作系统）运行的 App
  - 优点：速度快，性能高，用户体验效果好
  - 缺点：无法跨平台，开发成本高，更新麻烦
- Web App
  - 基于移动设备的浏览器运行的 App
  - 优点：跨平台，开发周期短，开发成本低，更新较简单，维护较轻松
  - 缺点：用户体验不佳 
- Hybrid App
  - 基于上两种发展出来的产物
  - 结合 Native App 用户体验效果好和 Web App 的跨平台开发的优势
  - 通常是基于第三方跨平台移动开发框架进行开发
  - 继承了 Web App 实时更新、开发成本低等优点
  - 通过应用商店区分移动操作系统分发，用户需安装使用的移动应用
  - 使用方式和 Native App 一致

##### 2、**跨平台框架介绍**

- AppCan

  提供 UI 快速开发框架、本地功能调用 API 接口、打包系统等

  数百套界面模板、数十种应用插件

  无法修改优化底层代码

  暂不支持自行开发原生控件

  框架自带功能过多导致应用安装包偏大

- Flutter

  谷歌的开源的移动UI框架，可以快速在 iOS 和 Android上构建高质量的原生用户界面

  性能强大、路由设计优秀、基于 Dart 语言开发

  2018年12月发布

- Vue + weex
- uniApp（基于VUE）
- Angular + Ionic 
- React-Native

##### 3、**ReactNative**

- Learn once, write anywhere: Build mobile apps with React（使用JavaScript和React编写原生移动应用）
- 不用 WebView，摆脱 WebView 的交互和性能问题
- 封装原生控件有更好的触摸滚动体验和灵敏的手势识别
- 支持热更新
- Facebook 在2015年9月公布的开源项目

##### 4、**创建-运行项目**

```
npx react-native init ProjectName

yarn react-native run-android
```

## React语法

##### 1、JSX 语法

- JavaScript 和 XML 结合的一种格式
- 利用 HTML 语法来创建虚拟 DOM
- 实例：

```jsx
const element = <h1>Hello, world!</h1>;
```

- 在 JSX 中使用表达式

```jsx
const num = 100;
const element = <h1> { num } </h1>;
```

##### 2、组件

- 函数定义组件

```jsx
function Hello( props ) {
	return <h1>Hello { props.name }</h1>
}
ReactDOM.render(
	<Hello name=“ React ”/>, 	
    document.getElementById('root')
);
```

- 类定义组件

```jsx
class Hello extends React.Component {
	render( ) {
		return <h1>Hello, {this.props.name}</h1>;
	}
}
```

- props

  props 是组件的输入内容， 从父组件传递给子组件的数据(属性)

- state

  1. 私有的、完全受控于当前组件，组件外部是无法进行修改的
  2. 类定义的组件特有的属性
  3. 状态的声明（构造函数是唯一能够初始化 this.state 的地方)

  ```jsx
  class Hello extends React.Component {
  	constructor( ){ // ES6 对类的默认方法
  		super(); // 将父类中的 this 对象继承给子类
  		this.state = {name:’React’}
  	}
  	render( ) { 
          return <h1>Hello { this.state.name }</h1>; 
      }
  }
  ```

- 组件生命周期

  - constructor
  - render
  - componentDidMount
  - shouldComponentUpdate
  - getSnapshotBeforeUpdate
  - componentDidUpdate
  - componentWillUnmount

##### 3、Redux

Redux 是 JavaScript 状态容器，提供可预测化的状态管理 • 目的 – 随着 JavaScript 单页应用开发日趋复杂，JavaScript 需要管理比任何时候都要多的 state（状态），管理不断变化的 state 非常困难 • 核心概念 – Action、Reducer、Store

##### 4、action

- Action 是把数据从应用传到 store 的有效**载荷**
- 是 **store 数据的唯一来源**
- 一般会通过 store.dispatch( ) 将 action 传到 store
- Action 本质上是 **JavaScript 普通对象**
- Action 内必须使用一个字符串类型的 type 字段来表示将要执行的动作
- 一般 type 会被定义 成字符串常量
- 当应用规模越来越大时，建议使用单独的模块或文件来存放 action

```jsx
// 普通对象
let action = { type : ’add_todo_item’,inputValue:’hello’}
// 利用字符串常量
const ADD_TODO = ‘add_todo'
let action = { type: ADD_TODO, text: 'Build my first app' }
// 利用单独的模块或者文件来存放 Action
import { ADD_TODO, REMOVE_TODO } from '../actionTypes'
```

##### 5、Reducer

- 指定了应用状态的变化如何响应 action 并发送到 store 的
- – reducer 就是一个**纯函数**，**接收旧的 state 和 action，返回新的 state**
- (previousState, action) => newState
- 禁止在 Reducer 里做这些操作
- 修改传入参数；
- 执行有副作用的操作，如 API 请求和路由跳转；
- 调用非纯函数，如 Date.now() 或 Math.random( )

```jsx
function todoApp(state = initialState, action) {
    switch (action.type) {
        case ‘add_todo_item’:
        	let newState = JSON.parse(JSON.stringify(state));
        	newState.inputValue = action.value;
        	return newState;
        default:
        	return state
    }
}
```

##### 6、Store

- Store 是把 Action 和 Reducer 联系到一起的对象
- Redux 应用只有一个**单一的 store**
- 作用：
  1. 维持应用的 state；
  2. 提供 getState( ) 方法获取 state；
  3. 提供 dispatch(action) 方法更新 state；
  4. 通过 subscribe(listener) 注册监听器;
  5. 通过 subscribe(listener) 返回的函数注销监听器

```jsx
// 创建 store
import { createStore } from 'redux';
import todoApp from './reducers' ;
let store = createStore( todoApp );
export default store
```

7、Redux三大原则

- **单一数据源**
  1. 整个应用的 state 被储存在一棵 object tree 中
  2. 这个 object tree 只存在于唯一一个 store 中
- **State** 是只读的
  1. 唯一改变 state 的方法就是触发 action(一个用于描述已发生事件的普通对象)
- **使用纯函数来执行修改**
  1. 为了描述 action 如何改变 state tree ，你需要编写 reducers
  2. Reducer 只是一些纯函数，它接收先前的 state 和 action，并返回新的 state

##### 8、hooks

- useState

  ```jsx
  import React, { useState } from 'react';
  function Example() {
    // 声明一个叫 “count” 的 state 变量。  const [count, setCount] = useState(0);
    return (
      <div>
        <p>You clicked {count} times</p>
        <button onClick={() => setCount(count + 1)}>
          Click me
        </button>
      </div>
    );
  }
  ```

- useEffect

  `useEffect` 就是一个 Effect Hook，给函数组件增加了操作副作用的能力。它跟 class 组件中的 `componentDidMount`、`componentDidUpdate` 和 `componentWillUnmount` 具有相同的用途，只不过被合并成了一个 API。

  ```jsx
  import React, { useState, useEffect } from 'react';
  function Example() {
    const [count, setCount] = useState(0);
  
    // 相当于 componentDidMount 和 componentDidUpdate:  useEffect(() => {    // 使用浏览器的 API 更新页面标题    document.title = `You clicked ${count} times`;  });
    return (
      <div>
        <p>You clicked {count} times</p>
        <button onClick={() => setCount(count + 1)}>
          Click me
        </button>
      </div>
    );
  }
  ```

- useContext

  ```jsx
  const themes = {
    light: {
      foreground: "#000000",
      background: "#eeeeee"
    },
    dark: {
      foreground: "#ffffff",
      background: "#222222"
    }
  };
  
  const ThemeContext = React.createContext(themes.light);
  
  function App() {
    return (
      <ThemeContext.Provider value={themes.dark}>
        <Toolbar />
      </ThemeContext.Provider>
    );
  }
  
  function Toolbar(props) {
    return (
      <div>
        <ThemedButton />
      </div>
    );
  }
  
  function ThemedButton() {
    const theme = useContext(ThemeContext);  return (    <button style={{ background: theme.background, color: theme.foreground }}>      I am styled by theme context!    </button>  );
  }
  ```

- useMemo

  返回一个 [memoized](https://en.wikipedia.org/wiki/Memoization) 值。

  把“创建”函数和依赖项数组作为参数传入 `useMemo`，它仅会在某个依赖项改变时才重新计算 memoized 值。这种优化有助于避免在每次渲染时都进行高开销的计算。

  ```jsx
  const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
  ```

- useCallback

  返回一个 [memoized](https://en.wikipedia.org/wiki/Memoization) 回调函数。

  `useCallback(fn, deps)` 相当于 `useMemo(() => fn, deps)`。

  ```jsx
  const memoizedCallback = useCallback(
    () => {
      doSomething(a, b);
    },
    [a, b],
  );
  ```

## 环境搭建

##### 1、安装 **Node**（版本大于10）

 Python2.x

##### 2、安装 **JDK**

配置环境变量

检查是否配置成功：打开命令行窗口，输入 javac –version，是否出现版本号

##### 3、安装 **SDK**

创建环境变量

检查是否配置成功：在命令行输入 adb，输出版本信息则为成功

##### 4、配置 gradle

配置环境变量

##### 5、安装模拟器

安装 Android 模拟器（夜神模拟器）

执行 adb connect 127.0.0.1:62001

测试，执行 adb devices，如果显示连接的设备，就成功

##### 6、创建-运行项目

```jsx
//创建一个新项目
npx react-native init ProjectName
//进入项目，运行项目
yarn react-native run-android
```

## 常用组件

##### 1、样式处理

- 使用 JavaScript 来写样式，所有的核心组件都接受名为 style 的属性，要求使用驼峰命名法，例如将`background-color`改为`backgroundColor`

- style 属性可以是一个普通的 JavaScript 对象，也可使用`StyleSheet.create` 来集中定义组件的样式（推荐）

```jsx
export default class LotsOfStyles extends Component {
  render() {
    return (
      <View>
        <Text style={styles.red}>just red</Text>
        <Text style={styles.bigBlue}>just bigBlue</Text>
        <Text 
            style={
                [styles.bigBlue, styles.red]
            }
         >
            bigBlue, then red
         </Text>
      </View>
    );
  }
}
const styles = StyleSheet.create({
  bigBlue: {
    color: 'blue',
    fontWeight: 'bold',
    fontSize: 30,
  },
  red: {
    color: 'red',
  },
});
```

##### 2、**基础组件**

- ##### View

  创建 UI 时最基础的组件，直接对应一个平台的原生视图，IOS中的 UIView、Android中的android.view和Web中的div等

- Text

  一个用于显示文本的 RN 组件，支持嵌套、样式，以及触摸处理，可继承样式`<Text>`元素在布局上不同于其它组件：在Text内部的元素不再使用flexbox布局，而是采用文本布局。

- Image

  用于显示多种不同类型图片的 React 组件，包括网络图片、静态资源、base64图片等。

```JSx
export default class DisplayAnImage extends Component {
  render() {
    return (
      <View>
        <Image
          source={require('../assets/logo.png')}
        />
        <Image
          style={{width: 50, height: 50}}
          source={{uri: 'https://facebook.github.io/react-native/img/tiny_logo.png'}}
        />
        <Image
          style={{width: 66, height: 58}}
          source={{uri: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADMAAAAzCAYAAAA6oTAqAAAAEXRFWHRTb2Z0d2FyZQBwbmdjcnVzaEB1SfMAAABQSURBVGje7dSxCQBACARB+2/ab8BEeQNhFi6WSYzYLYudDQYGBgYGBgYGBgYGBgYGBgZmcvDqYGBgmhivGQYGBgYGBgYGBgYGBgYGBgbmQw+P/eMrC5UTVAAAAABJRU5ErkJggg=='}}
        />
      </View>
    );
  }
}

```

> ##### 属性：resizeMode
>
> 决定当组件尺寸和图片尺寸不成比例的时候如何调整图片的大小。默认值为`cover`。
>
> - `cover`: 在保持图片宽高比的前提下缩放图片，直到宽度和高度都大于等于容器视图的尺寸（如果容器有 padding 内衬的话，则相应减去）。
> - `contain`: 在保持图片宽高比的前提下缩放图片，直到宽度和高度都小于等于容器视图的尺寸（如果容器有 padding 内衬的话，则相应减去）。**译注**：这样图片完全被包裹在容器中，容器中可能留有空白。
> - `stretch`: 拉伸图片且不维持宽高比，直到宽高都刚好填满容器。
> - `repeat`: 重复平铺图片直到填满容器。图片会维持原始尺寸，但是当尺寸超过容器时会在保持宽高比的前提下缩放到能被容器包裹。
> - `center`: 居中不拉伸。

- ImageBackground

  添加背景色，必须指定 width 和 height，通过 source 属性指定 背景图片

```jsx
 <ImageBackground 
     source={...} 
     style={{width: '100%', height: '100%'}}
 >
    <Text>Inside</Text>
 </ImageBackground>
```

- TextInput

  用户在应用中通过键盘输入文本的基本组件,必须通过 onChangeText事件来读取用户的输入
  - value
  - onChangeText
  - onSubmitEditing
  - onFocus

- ScrollView

  封装了平台的ScrollView（滚动视图）的组件

##### **3、交互组件**

- Button

  跨平台的按钮组件

```jsx
<Button
  onPress={()=>{}}
  title="按钮"
  color="#841584"
/>
```

- TouchableOpacity

  不透明度会变化的按钮

##### **4、Android** 独有组件

- BackHandler
- ToastAndroid
- ToolbarAndroid
- DrawerLayoutAndroid
- ProgressBarAndroid
- ViewPagerAndroid
- DatePickerAndroid
- TimePickerAndroid

##### 5、Platform

- 平台模块 Platform.OS

  ```jsx
  import { Platform } from 'react-native';
  var styles = StyleSheet.create({
    height: (Platform.OS === 'ios') ? 200 : 100,
  });
  //Platform.OS在iOS上会返回ios，而在Android设备或模拟器上则会返回android。
  ```

- Android版本 Platform.Version

  ```jsx
  //在Android上，平台模块还可以用来检测当前所运行的Android平台的版本：
  import { Platform } from 'react-native';
  if(Platform.Version === 21){
    console.log('Running on Lollipop!');
  }
  ```

##### 6、Dimensionsrn

获取屏幕尺寸

```jsx
import React, { Component } from 'react';
import {
    AppRegistry,
    StyleSheet,
    View,
    Dimensions
} from 'react-native';

//计算屏幕的宽高
let {width, height} = Dimensions.get('window');

export default class ReactNativeDemo extends Component {
    constructor(props){
        super(props);
        this.printWindowWidth();
        this.printWindowHeight();
    }
    //打印屏幕的高度
    printWindowWidth(){
        console.log("iphone8 window width is "+ width);
    }
    //打印屏幕的宽度
    printWindowHeight(){
        console.log("iphone8 window height is "+ height);
    }
    render() {
        return (
            <View style={styles.flex} />
        );
    }
}
const styles = StyleSheet.create({
    flex: {
        flex: 1
    }
});
AppRegistry.registerComponent('ReactNativeDemo', () => ReactNativeDemo);
```

## 第三方组件

##### 1、ActivityIndicator

##### 2、Animated

##### 3、WebView

##### 4、react-native-image-picker

##### 5、react-native-image-crop-picker

##### 6、react-native-button

##### 7、react-native-message-bar

## 路由

```jsx
import React from 'react';
import { View, Text, TouchableOpacity } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import Icon from 'react-native-vector-icons/MaterialCommunityIcons';
import Index from './src/Index';
import Write from './src/Write';

const Stack = createStackNavigator();

function App({navigation}) {
  return (
    <NavigationContainer>      
      <Stack.Navigator>
          <Stack.Screen
              options={{
                  title:'便签',
                  headerTitleAlign:'center',
                  headerRight:()=><TouchableOpacity><Text>编辑 </Text></TouchableOpacity>,
              }}
              name="index" 
              component={Index} 
          />
          <Stack.Screen
              options={{
                  title:'便签',
                  headerTitleAlign:'center',
                  headerRight:()=><TouchableOpacity><Icon name="check" size={25}/></TouchableOpacity>,
              }}
              name="write" 
              component={Write} 
          />
      </Stack.Navigator>     
    </NavigationContainer>
  );
}
export default App;
```

```jsx
import React from 'react';
import {
  SafeAreaView,
  StyleSheet,
  ScrollView,
  View,
  Text,
  StatusBar,
  TextInput,
  Image,
  Button,
  ImageBackground
} from 'react-native';

import Icon from 'react-native-vector-icons/MaterialCommunityIcons';
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
import { NavigationContainer } from '@react-navigation/native';
import Home from './src/Home'

const Tab = createBottomTabNavigator();

const ShopPage = ()=>{
  return <Text>
    商城
  </Text>
}

const VipPage = ()=>{
  return <Text>
    Vip
  </Text>
}

const CartPage = ()=>{
  return <Text>
    购物车
  </Text>
}

const MyPage = ()=>{
  return <Text>
    我的
  </Text>
}

const App = () => {
  return (
    <NavigationContainer>
      <Tab.Navigator
        tabBarOptions={{
          
          activeTintColor:'#fb7737',
          labelStyle:{
            fontSize: 14
          }
        }}
      >
        <Tab.Screen
          options={{
            title:'首页',
            tabBarIcon:({color})=><Icon size={25} name="home" color={color}/>
          }}
          name='Home' 
          component={Home}
        >
          
        </Tab.Screen>

        <Tab.Screen 
          options={{
            title:'商城',
            tabBarIcon:({color})=><Icon size={25} name="shopping" color={color}/>
          }}
          name='Shop' 
          component={ShopPage}
        ></Tab.Screen>

        <Tab.Screen 
          options={{
            title:'会员管理',
            tabBarIcon:({color})=><Icon size={25} name="trophy-variant-outline" color={color}/>
          }}
          name='Vip' 
          component={VipPage}
        ></Tab.Screen>

        <Tab.Screen 
          options={{
            title:'购物车',
            tabBarIcon:({color})=><Icon size={25} name="cart" color={color}/>
          }}
          name='Cart' 
          component={CartPage}
        ></Tab.Screen>

        <Tab.Screen 
          options={{
            title:'我的',
            tabBarIcon:({color})=><Icon size={25} name="account-circle-outline" color={color}/>
          }}
          name='My' 
          component={MyPage}
        ></Tab.Screen>
      </Tab.Navigator>
    </NavigationContainer>
  );
};


export default App;

```

## TypeScript

##### 1、项目搭建

使用 TypeScript 模板创建新项目

```jsx
react-native init MyApp --template react-native-template-typescript
```

##### 2、基础类型

- number
- string
- boolean
- Array（number[ ]）
- object
- Tuple（元组 ）
- enum（枚举）
- any
- void
- null 
- undefined

```tsx
let isDone: boolean = false;
```

##### 3、接口

interface ：描述一个对象的取值规范，不实现具体的对象

- 属性接口

  ```tsx
  interface User {
    name: string;
    age?: number;
  }
  
  const user1: User = {
    name: "lili",
    age: 18
  };
  ```

- 函数接口

  ```tsx
  interface SearchFunc {
    (source: string, subString: string): boolean;
  }
  
  let myFunc: SearchFunc = function(source: string, subString: string){
      ...
      return true;
  }
  ```

- 类接口

  ```tsx
  interface User {
    name: string;
    age?: number;
  }
    
  class user1 implements User{
      name='zhangsan'  
  }
  ```

- 继承

  ```tsx
  interface Shape {
      color: string;
  }
  
  interface Square extends Shape {
      sideLength: number;
  }
  
  let square = {} as Square;
  square.color = "blue";
  square.sideLength = 10;
  ```

##### 4、类

- 定义
- 继承
- 静态属性和静态方法（static）
- 访问修饰符
  - public
  - private
  - protected

##### 5、泛型

泛型（Generics）是指在定义函数、接口或类的时候，不预先指定具体的类型，而在使用的时候再指定类型的一种特性

使用泛型来创建可重用的组件，一个组件可以支持多种类型的数据

- 泛型函数

```tsx
function identity<T>(arg: T): T {
    return arg;
}
identity<string>('params1')
identity<number>(100)
```

- 泛型接口

```tsx
interface GenericIdentityFn<T> {
    (arg: T): T;
}

function identity<T>(arg: T): T {
    return arg;
}

let myIdentity: GenericIdentityFn<number> = identity;
```

- 泛型类

```tsx
class AddData<T>{
    list:T[] = [];
    num:number;
    add(data:T):T[]{
        this.list.push(data);
        return this.list;
    }
}
let data1 = new AddData<number>()
data1.list.push(1)
```

##### 6、装饰器

装饰器是一种特殊类型的声明，它能够被附加到类声明、方法、属性或参数上。 装饰器使用`@expression`这种形式，`expression`求值后必须为一个函数，它会在运行时被调用，被装饰的声明信息做为参数传入

```tsx
// 普通装饰器（无参数）
function helloWord(target: any) {
    console.log('hello Word!');
}
@helloWord
class HelloWordClass {

}
// 装饰器工厂 （带参数）
function helloWord(p:string) {
    return function (target) { //  这才是真正装饰器
         console.log(p)
    }
}
@helloWord('hello')
class HelloWordClass {

}
```

- 类装饰器

  参数是类的构造函数

  如果类装饰器返回一个值，它会使用提供的构造函数来替换类的声明

- 方法装饰器

  方法装饰器表达式会在运行时当作函数被调用，传入下列3个参数：

  1. 对于静态成员来说是类的构造函数，对于实例成员是类的原型对象。
  2. 成员的名字。
  3. 成员的属性描述符。

  ```jsx
  function enumerable(value: boolean) {
      return function (target: any, propertyKey: string, descriptor: PropertyDescriptor) {
          descriptor.enumerable = value;
      };
  }
  class Greeter {
      greeting: string;
      constructor(message: string) {
          this.greeting = message;
      }
  
      @enumerable(false)
      greet() {
          return "Hello, " + this.greeting;
      }
  }																												
  ```

- 属性装饰器

  属性装饰器表达式会在运行时当作函数被调用，传入下列2个参数：

  1、对于静态成员来说是类的构造函数，对于实例成员是类的原型对象

  2、成员的名字

  ```jsx
  function DefaultValue(value: string) {
      return function (target: any, propertyName: string) {
          target[propertyName] = value;
      }
  }
  
  class Hello {
      @DefaultValue("Hello") greeting: string;
  }
  
  console.log(new Hello().greeting);
  ```

- 参数装饰器

  参数装饰器表达式会在运行时当作函数被调用，传入下列3个参数：

  1. 对于静态成员来说是类的构造函数，对于实例成员是类的原型对象。
  2. 成员的名字。
  3. 参数在函数参数列表中的索引。

- 装饰器组合

  当多个装饰器应用在一个声明上时会进行如下步骤的操作：

1. 由上至下依次对装饰器表达式求值。
2. 求值的结果会被当作函数，由下至上依次调用













