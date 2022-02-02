# Next.js + typescript 시작하기

## Next.js 프레임워크를 쓰는 이유
1. 검색엔진에 노출이 잘 안됌 (SPA 특성)
2. 한번에 너무 많은 청크 및 데이터를 전송함(클라이언트의 부담)

리액트의 이러한 문제점을 해결 하기 위해 SSR을 지원하는 NEXT.js를 이용하게 되었다.

## Create Next App with Typescript
* Create app
```shell
npx create-next-app --typescript
# or
yarn create next-app --typescript
```
* Manual Setup (yarn 기준)
```shell
mkdir myApp
cd myApp
yarn init -y
yarn add react react-dom next
yarn add --dev typescript @types/react @types/node
```

## Eslint + prettier 설정
자동으로 적용이 안됀다. 즉 직접 설정 해주어야함.

```shell
yarn add --dev eslint eslint-config-prettier eslint-plugin-import
yarn add --dev eslint-plugin-prettier eslint-plugin-react 
yarn add --dev eslint-plugin-react-hooks prettier
yarn add --dev @typescript-eslint/eslint-plugin @typescript-eslint/parser
```
관련 플러그인들을 yarn add

### 로컬에 .eslintrc 파일 추가
```json
{
    "extends": ["react-app", "prettier/prettier"],
    "plugins": ["react-hooks", "simple-import-sort", "prettier"],
    "rules": {
        "prettier/prettier": "error",
        "react-hooks/rules-of-hooks": "error",
        "simple-import-sort/imports": "error",
        "simple-import-sort/exports": "error",
        "no-multiple-empty-lines": ["error", { "max": 1, "maxEOF": 0 }],
        "comma-dangle": ["error", "always-multiline"],
        "object-curly-spacing": ["error", "always"],
        "space-in-parens": ["error", "never"],
        "computed-property-spacing": ["error", "never"],
        "comma-spacing": ["error", { "before": false, "after": true }],
        "eol-last": ["error", "always"],
        "quotes": ["error", "single"],
        "no-tabs": "error",
        "semi": ["error", "never"],
        "import/no-anonymous-default-export": 0,
        "object-shorthand": "error",
        "padding-line-between-statements": [
            "error",
            { "blankLine": "always", "prev": "*", "next": "return" }
        ],
        "@typescript-eslint/no-redeclare": 0
    }
}
```
### .prettierrc 추가
```json
{
  "singleQuote": false,
  "semi": true,
  "useTabs": true,
  "tabWidth": 2,
  "trailingComma": "all",
  "printWidth": 80
}
```