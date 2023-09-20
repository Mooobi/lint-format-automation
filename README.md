## 실행 방법

1. 사용하고자 하는 프로젝트에서 아래 명령어 실행

`npm install eslint eslint-config-prettier prettier --save-dev`

2. `.prettierrc.js` 파일 생성 후 옵션 넣기

```ts
module.exports = {
  singleQuote: true, // 문자열은 따옴표로 formatting
  jsxSingleQuote: true,
  semi: true, //코드 마지막에 세미콜른이 있게 formatting
  tabWidth: 2, // 들여쓰기 너비는 2칸
  trailingComma: 'all', // 객체나 배열 키:값 뒤에 항상 콤마를 붙히도록
  printWidth: 100, // 코드 한줄이 maximum 100칸
  arrowParens: 'always', // 화살표 함수가 하나의 매개변수를 받을 때 괄호를 필수로 formatting
};
```

3. `.eslintrc` 파일 생성 후 옵션 추가

```ts
{
  "extends": [
    // "react-app"
    "eslint:recommended",
    "prettier"
  ],
  "rules": {
    "no-var": "error", // var 금지
    "no-multiple-empty-lines": "error", // 여러 줄 공백 금지
    "no-console": ["error", { "allow": ["warn", "error", "info"] }], // console.log() 금지
    "eqeqeq": "error", // 일치 연산자 사용 필수
    "dot-notation": "error", // 가능하다면 dot notation 사용
    "no-unused-vars": "error" // 사용하지 않는 변수 금지
  }
}
```

4. husky 적용

```
npm install husky --save-dev
npx husky install
npx husky add .husky/pre-commit "npm run format && git add ."
npx husky add .husky/pre-push "npm run lint"
```

5. pakage.JSON script 설정

```ts
{
  "scripts": {
    "postinstall": "husky install",
    "format": "prettier --cache --write .",
    "lint": "eslint --cache .",
  },
}
```
