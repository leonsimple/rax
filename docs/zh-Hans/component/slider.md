# Slider 轮播

轮播组件，就是以幻灯片的方式，在页面中横向展示诸多内容的组件。 轮播内容相互独立，前后在内容以及数据上都不存在逻辑关系。

## 安装

```bash
$ npm install rax-slider --save
```

## 引用

```jsx
import Slider from 'rax-slider';
```

## 属性

| 名称               | 类型     | 默认值      | 描述                                       |
| :--------------- | :----- | :------- | :--------------------------------------- |
| width            | string | '750rem' | Slider的宽度（必填）                            |
| height           | string | '352rem' | Slider的高度（必填）                            |
| autoPlay         | bool   | false    | Slider是否自动播放                             |
| showsPagination  | bool   | true     | 是否显示分页的小圆点点                              |
| paginationStyle  | object | null     | 自己定义小圆点点的样式，否则默认样式居中                     |
| loop             | bool   | true     | 是否是循环播放                                  |
| index            | number | 0        | 指定默认初始化第几个（在weex安卓下有兼容问题，需要节点渲染完成后异步调用，暂不推荐使用） |
| autoPlayInterval | number | 3000     | 自动播放的间隔时间                                |

- 说明：
  - web 环境中 slider 内部默认做了节点的懒加载渲染，不再需要使用 picture 的 lazyload做懒加载
  - paginationStyle 默认样式为

```jsx
{
  position: 'absolute',
  width: props.width,
  height: '40rem',
  bottom: '20rem',
  left: 0,
  itemColor: 'rgba(255, 255, 255, 0.5)',
  itemSelectedColor: 'rgb(255, 80, 0)',
  itemSize: '8rem'
}
```

- 其中 itemColor 用来定义分页原点的颜色，itemSelectedColor 用来定义分页原点激活时的颜色，itemSize 用来定义分页圆点的大小

## 事件

| 名称       | 参数   | 描述               |
| :------- | :--- | :--------------- |
| onChange | none | object{index...} |

## 方法

| 名称      | 参数    | 描述   |
| :------ | :---- | ---- |
| slideTo | index |      |

slideTo 方法通过在 Slider 组件上添加 ref 使用，示例：

```jsx
slideTo(index) {
  this.refs.Slider.slideTo(index);
}
```



## 基本示例

本 Demo 演示最基本的 Slider

```jsx
// demo
import {Component, createElement, render } from 'rax';
import View from 'rax-view';
import Text from 'rax-text';
import Image from 'rax-image';
import Slider from 'rax-slider';

const styles = {
  container: {
    width: 750
  },
  slider: {  
    width: '750rem',
    position: 'relative',
    overflow: 'hidden',
    height: '350rem',
    backgroundColor: '#cccccc' 
  },
  itemWrap: {
    width: '750rem',  
    height: '252rem'
  },
  image: {
    width: '750rem',
    height: '252rem' 
  },
  button: {
    marginTop: '20rem',
    width: '340rem',
    height: '80rem'
  },
  paginationStyle: {
    position: 'absolute',
    width: '750rem',
    height: '40rem',
    bottom: '20rem',
    left: 0,
    itemColor: 'rgba(255, 255, 255, 0.5)',
    itemSelectedColor: 'rgb(255, 80, 0)',
    itemSize: '8rem'
  },
  text: {
    fontSize: 50
  }
};

class SlideDemo extends Component {
  onchange(index) {
    console.log('change', index);
  }

  render() {
    return (
      <View style={styles.container}>
        <Slider className="slider" width="750rem" height="352rem" style={styles.slider}
          autoPlay={true}
          loop={true}
          showsPagination={true}
          paginationStyle={styles.paginationStyle}
          autoplayTimeout={3000}
          onChange={this.onchange.bind(this)}>
          <View style={styles.itemWrap}>
            <Image style={styles.image} source={{uri: '//img.alicdn.com/tps/TB1m2LyJFXXXXbHXpXXXXXXXXXX-1125-352.jpg_q50.jpg'}} />
          </View>
          <View style={styles.itemWrap}>
            <Image style={styles.image} source={{uri: '//img.alicdn.com/tps/TB1ogUvJFXXXXaAXXXXXXXXXXXX-1125-352.jpg_q50.jpg'}} />
          </View>
          <View style={styles.itemWrap}>
            <Image style={styles.image} source={{uri: '//gw.alicdn.com/tps/i4/TB1pgxYJXXXXXcAXpXXrVZt0FXX-640-200.jpg_q50.jpg'}} />
          </View>
          <View style={styles.itemWrap}>
            <Image style={styles.image} source={{uri: '//gw.alicdn.com/imgextra/i4/3/TB2STElaohnpuFjSZFPXXb_4XXa_!!3-0-yamato.jpg_q50.jpg'}} />
          </View>
        </Slider>
      </View>
    );
  }
}

render(<SlideDemo />);
```

