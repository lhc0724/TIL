# React + Typescript 시작하기

## 프로젝트 생성
타입스크립트를 이용하는 리액트 프로젝트를 만드는 명령어는 다음과 같다.

```shell
npx create-react-app [appName] --template typescript

# or

yarn create react-app [appName] --template typescript
```
출처 https://create-react-app.dev/docs/adding-typescript/  

## 컴포넌트 작성하기
Typescript + React 진영에서는 App.tsx에 React.FC 타입을 쓰지 않는걸 지향합니다.  
```typescript
import React, { useState } from 'react';

interface User = {
    name:   string;
    age:    number;
    userId: string;
    location?: string;
}

const UserInfo = (props : User) => {
    const [users, setUser] = useState(props);

    return (
        <div>
            <h2>
                Hello, {users.name}
            </h2>
            <p> your age : { users.age }</p>
        </div>
    )
}

export default UserInfo;
```
