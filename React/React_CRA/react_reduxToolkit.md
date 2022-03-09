# Redux-toolkit
> 해당 문서는 redux를 어느정도 알고 있다는 가정하에 개인 정리목적으로 작성 하였습니다.  
> 또한, 사용 경험 정리 목적하에 자세한 예제가 아닌 생략 코드임을 밝힙니다.

## why use toolkit?
리덕스 툴킷은 리액트와 같이 사용되는 여러가지 상태 관리 라이브러리중 하나다.  
그중 redux를 간소화 해주는 라이브러리이다.  
기존의 리덕스의 단점은 너무 장황한 코드를 생성 해야하하고, 이는 편의성을 위해선 추가적으로 서드파티 라이브러리를 받아야만 했다.  

redux-toolkit은 redux 팀이 공식적으로 만든 라이브러리로 typescript 또한 지원한다.

## createSlice

### slice 작성
``` typescript
    /* userSlice.ts */
    import { UserInfo } from './interface/user.interface.ts'

    type sliceState_t = {
        user: UserInfo;
        token: string;
        isLoggin: boolean;
        isLoading: boolean;
    };

    const initialState: sliceState_t = {
        user: { name="", auth="", user_id="", user_pw="" },
        token: "",
        isLoggin: false,
        isLoading: false,
    };

    export const userSlice = createSlice({
	name: "user",
    initialState,
	reducers: {
        setIsLoding: (state, actions: PayloadAction<boolean>) => {
            state.isLoading = actions.payload;
        },
        setIsLoggin: (state, actions: PayloadAction<boolean>) => {
            state.isLoggin = actions.payload;
        },
        setStateInit: (state) => {
            state.isLoading = false;
            state.isLoggin = false;
            ...
        }

    },
    extraReducers: builder => {

        builder
            .addCase( ... )
            ...
    }
});

export default userSlice.reducer;
export const { setIsLoggin, setIsLoggin, setStateInit } = userSlice.actions;

export const userData = (state: RootState) => state.userSlice.user;
```
### extraReducer
    내용 추가 예정..


### slice를 사용할 component (종합)
```typescript
    /* login.tsx */

    import React, ... from ...;
    ...
    import { ReducerType } from '../reducer/rootReducer'

    export function Login() {
        const [user_id, setId] = useState('');
        const [user_pw, setPw] = useState('');
        ...

        const dispatch = useDispatch();
        const isLoggin = useSelector<ReducerType>((state) => state.userSlice.isLoggin);

        /* event handler */
        const onChgId = (evt: React.ChangeEvent<HTMLInputElement>) => {
            ...
        }
        ...

        const submitLogin = () => {
		    const loginData = {
			    userID: user_id,
			    userPW: user_pw,
		    };

		    dispatch(actionLogin(loginData));
            setTryLogin(true);
        };

        /* useEffect */
        ...

        return(
            <div>
                ...
j
                <button ... onClick={submitLogin}> Login </button>
            </div>
        )

    }
```
