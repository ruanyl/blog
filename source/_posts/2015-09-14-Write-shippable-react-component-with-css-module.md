---
title:  "Write React Component with CSS Module"
date:   2015-09-14 21:25:19
categories: JS
tags: React
author: Bigruan
---

### The goals:

1. The component can be published to npmjs.org
2. No need to incldude css manually on page
3. Instead of using inline css, now we use Class Name

[sample code](https://github.com/ruanyl/react-slim-progress-webpack)

Think about that you made an awesome React component,  you don't just want to use it in your own project but also want to publish
to `npm` to share with others. However, awesome ui can not live without css. So you either use a bunch of inline css, or write in
the README to tell people who use this component to also include an external css file. This is really not a good idea to write
isolate React Component.

Here we introduce [CSS Modules](http://glenmaddern.com/articles/css-modules). The idea is that you can `import` a css file as it is
a normal `npm` module. In the we will use [react-css-modules](https://github.com/gajus/react-css-modules)

```javascript
import styles from './style.css';
import cssModules from 'react-css-modules';
```

Then you can use the css class name in your `jsx` code. for example in our example you will find:

```javascript
class Progress extends Component {
  render() {
    // find detailed code from source
    return <div styleName='progress' style={progressStyle}></div>;
  }
}
```

You use `styleName` attribute and the value is just the pure class name you defined in style.css.

Finally, you will need to wrap the component with CSSModules
```javascript
export default cssModules(Progress, styles);
```

Basically that's it. But in order to make this component works, you will need to do some webpack settings.

```javascript
{
  test: /\.css$/,
  loader: ExtractTextPlugin.extract('style', 'css?modules&importLoaders=1&localIdentName=[name]__[local]___[hash:base64:5]')
}
```

find more from the [source code](https://github.com/ruanyl/react-slim-progress-webpack)
