---
order: 0
title:
  zh-CN: Hooks 调用（推荐）
  en-US: Hooks usage (recommended)
---

## zh-CN

通过 `message.useMessage` 创建支持读取 context 的 `contextHolder`。请注意，我们推荐通过顶层注册的方式代替 `message` 静态方法，因为静态方法无法消费上下文，因而 ConfigProvider 的数据也不会生效。

## en-US

Use `message.useMessage` to get `contextHolder` with context accessible issue. Please note that, we recommend to use top level registration instead of `message` static method, because static method cannot consume context, and ConfigProvider data will not work.

```tsx
import { Button, message } from 'antd';
import React from 'react';

const Context = React.createContext({ name: 'Default' });

const App: React.FC = () => {
  const [messageApi, contextHolder] = message.useMessage();

  const info = () => {
    messageApi.open({
      type: 'info',
      content: <Context.Consumer>{({ name }) => `Hello, ${name}!`}</Context.Consumer>,
      duration: 1,
    });
  };

  return (
    <Context.Provider value={{ name: 'Ant Design' }}>
      {contextHolder}
      <Button type="primary" onClick={info}>
        Display normal message
      </Button>
    </Context.Provider>
  );
};

export default App;
```