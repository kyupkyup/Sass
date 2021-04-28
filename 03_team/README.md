# Sass

## 개요

### Sass 개요

CSS는 쉬운 문법을 가지고 있지만, 많은 요소와 스타일링이 들어가면 코드를 보는 것도 어려워집니다. 불필요한 선택자(Selector)의 과용과 연산 기능의 한계가 있기 때문입니다. 프로젝트의 크기에 따라 관리가 힘들어 지는데, 이러한 면을 보완하고자 Sass가 탄생하였습니다.

#### CSS Preprocessor란?

CSS 전처리기는 전처리기 자신만의 문법을 가지고 CSS를 생성하는 프로그램입니다. 많은 CSS 전처리기가 있으며, 대부분 pure CSS에 존재하지 않는 특징을 추가할 수 있습니다. 대표적인 예로는 믹스인, 중첩 셀렉터, 상속 셀렉터가 있습니다.

##### CSS Preprocessor 사용법

전처리기의 문법에 맞춰 코딩을 합니다. 웹에서는 pure CSS만 동작하기 때문에, 이를 CSS로 컴파일(Compile)합니다.

### Sass와 SCSS의 차이점

Sass(Syntactically Awesome Style Sheets)의 3버전에서 SCSS가 등장하였습니다. SCSS는 CSS의 모든 레벨과 호환되도록 만든 새로운 문법 체제입니다. 따라서 Sass의 모든 기능을 지원하는 CSS의 상위집합(Superset)입니다.

즉, SCSS는 CSS와 거의 같은 문법으로 Sass를 지원한다고 볼 수 있습니다. 공식 문서에서도 SCSS문법을 기반으로 모든 문법을 설명하고 있습니다.

또 다른 차이점으로는 `{}`(중괄호)와 `;`세미콜론의 유무입니다.

**예제**

Sass

```Sass
.list
    width: 100px
    float: left
    li
        color:red
        background: url("image.jpg")
        &:last-child
            margin-right: -10px
```

SCSS

```SCSS
.list {
    width: 100px;
    float: left;
    li {
        color: red;
        backgroud: url("image.jpg");
        &:last-child{
            margin-right: -10px
        }
    }
}
```

Sass는 선택자의 유효범위를 들여쓰기로 구분하고, SCSS는 `{}`로 범위를 구분합니다.

Sass가 들여쓰기로 유효범위를 정하기 때문에 같은 라인의 코드를 여러 줄로 나눠쓰는 것을 지원하지 않습니다. 이에 대한 [이슈](https://github.com/sass/sass/issues/216)는 아직 진행중입니다.

Mixins(재사용 가능한 기능을 만드는 방식)에도 차이가 있습니다. Sass는 단축 구문을 사용합니다.

Sass

```Sass
=border-radius($radius)
    -webkit-border-radius: $radius
    -moz-border-radius: $radius
    -ms-border-radius: $radius
    border-radius: $radius

.box
    +border-radius(10px)
```

SCSS

```SCSS
@mixin border-radius($radius) {
    -webkit-border-radius: $radius;
    -moz-border-radius: $radius;
    -ms-border-radius: $radius;
    border-radius: $radius;
}

.box {@include border-radius(10px);}
```

Sass는 `=`와 `+`기호로 Mixins을 사용했고, SCSS는 `@mixin`과 `@include`을 이용합니다.

### 컴파일 방법

Sass(SCSS)는 pure CSS가 아니기 때문에 웹에서 직접 동작할 수 없습니다. 따라서 이들을 CSS로 컴파일해야 합니다. 컴파일을 하는 방법들은 아래와 같습니다.

#### SassMeister

간단한 Sass 코드를 변환할 때 편리합니다. 페이지에 접속하고 Sass나 SCSS 문법으로 코딩하면 CSS창에 결과가 실시간 반영됩니다. HTML을 작성하여 적용된 결과를 보거나 Sass 버전 설정 등 여러 환경 설정들을 지원합니다.

| ![SassMeister](images/sassmeister_1.png) |
| :--------------------------------------: |
|             SassMeister 화면             |

#### node-sass

node-sass는 Node.js를 컴파일러인 LibSass에 바인딩한 라이브러리입니다.
NPM으로 전역 설치하여 사용합니다.

```
$ npm install -g node-sass
```

컴파일하려는 파일의 경로와 컴파일된 파일이 저장될 경로를 설정합니다.
`[]`는 선택사항입니다.

```
$ node-sass [옵션] <입력파일경로> [출력파일경로]
```

```
$ node-sass scss/main.scss public/main.css
```

여러 출력 경로를 설정할 수 있습니다.

```
$ node-sass scss/main.scss public/main.css dist/style.css
```

옵션을 적용할 수도 있습니다.
`--watch` 혹은 `-w`를 입력하면, 파일을 추적하기 시작합니다. 이 상태에서 파일을 저장하면 자동으로 변경 사항을 컴파일 합니다.

```
node-sass --watch scss/main.scss public/main.css
```

#### Gulp

빌드 자동화 도구입니다. `gulpfile.js`를 만들어 아래와 같이 설정할 수 있습니다. 먼저 `gulp` 명령을 사용하기 위해서는 전역 설치가 필요합니다.

```
$ npm install -g gulp
```

Gulp와 함께 Sass 컴파일러인 gulp-sass를 개발 의존성(devDependency) 모드로 설치합니다. gulp-sass는 위에서 살펴본 node-sass를 Gulp에서 사용할 수 있도록 만들어진 플러그인입니다.

```
$ npm install --save-dev gulp gulp-sass
```

#### Webpack

JavaScript 모듈화 도구입니다.

#### Parcel

웹 애플리케이션 번들러입니다. 사용 방법은 다음과 같습니다.

우선 Parcel을 전역으로 설치합니다.

```
$ npm install -g parcel-bundler
```

프로젝트에 Sass 컴파일러(node-sass)를 설치합니다.

```
$ npm install --save-dev node-sass
```

HTML에 `<link>`로 Sass 파일을 연결합니다.

```html
<link rel="stylesheet" href="scss/main.scss" />
```

```
$ parcel index.html
# 혹은
$ parcel build index.html
```

`dist/`에서 컴파일된 Sass 파일을 볼 수 있고, 별도의 포트 번호를 설정하지 않았다면 `http://localhost:1234`에 접속하여 적용 상태를 확인할 수 있습니다.

**예시**

아래와 같이 HTML과 SCSS파일을 작성합니다

```html
<!DOCTYPE html>
<html lang="ko-KR">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>SCSS test</title>
    <link rel="stylesheet" href="main.scss" />
  </head>
  <body>
    <div class="container">
      <div class="item"></div>
    </div>
  </body>
</html>
```

```SCSS
.container{
    $size : 100px;
    .item {
        width: $size;
        height: $size;
        background: tomato;
    }
}
```

여기서 같은 경로의 터미널에 아래와 같이 커맨드를 입력합니다.

```
$ npm init -y
```

위 커맨드를 실행하면 package.json파일이 다음과 같이 생성됩니다.

```json
{
  "name": "sass_test",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

이제 아래 커맨드를 입력해서 parcel을 개발 의존성 모드로 설치합니다.

```
npm i -D parcel-bundler
```

터미널 실행이 끝나면 json 파일에 `parcel-bundler`과 추가된 것을 볼 수 있습니다.

```json
{
  "name": "sass_test",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "parcel-bundler": "^1.12.5"
  }
}
```

이제 결과를 확인할 차례입니다.

```
$ npx parcel index.html
```

parcel을 통해 번들링 과정을 마치면 아래와 같이 서버를 확인할 수 있는 주소를 보여줍니다. 이 과정에서 percel은 `link`에 걸린 파일의 종류에 따라 모듈 설치를 자동으로 합니다.

| ![parcel 예시1](./images/percel_1.png) |
| :------------------------------------: |
|   번들링 과정이 끝난 후 터미널 화면    |

| ![parcel 예시2](./images/percel_2.png) |
| :------------------------------------: |
|              렌더링 화면               |

## 문법

### 주석(Comment)

CSS 주석은 `/* ... */`입니다.
Sass는 두 가지 스타일의 주석을 사용합니다.

```sass
// comment
/* comment */
```

Sass의 경우 컴파일되는 여러 줄 주석을 사용할 때 각 줄 앞에 `*`을 붙여야 합니다. 이 때 주의할 점은 `*`의 라인을 맞춰야 합니다.

```sass
/* 컴파일되는
 * 여러 줄
 * 주석 */
```

SCSS는 각 줄에 `*`이 없어도 되기 떄문에 기존 CSS와 주석방식이 같습니다. 따라서 기존 CSS와의 괴리감이 줄어듭니다.

### 데이터 종류(Data Types)

|  데이터  | 설명                               | 예시                                                |
| :------: | :--------------------------------- | :-------------------------------------------------- |
| Numbers  | 숫자                               | `1`, `82`, `20px`, `2em` ...                        |
|  String  | 문자                               | `bold`, `relative`, `"a.png"`, `"dotum"` ...        |
|  Colors  | 색상 표현                          | `red`, `blue`, `#FFFF00`, `rgba(255, 0, 0, .5)` ... |
| Booleans | 논리                               | `true`, `false`                                     |
|  Nulls   | 아무것도 없음                      | `null`                                              |
|  Lists   | 공백이나 `,`로 구분된 값의 목록    | `(apple, orange, banana), apple oragne`             |
|   Maps   | Lists와 유사하나 `Key: Value` 형태 | `(apple: a, orange: o, banana: b)`                  |

#### 데이터 타입 특징

Sass에서 사용하는 데이터 종류들의 특징이 있습니다.

- Numbers: 숫자에 단위가 있거나 없습니다.
- Strings: 문자에 따옴표가 있거나 없습니다.
- Nulls: 속성값으로 `null`이 사용되면 컴파일하지 않습니다.
- Lists: `()`를 선택하여 사용합니다.
- Maps: `()`가 필수 입력사항입니다.

### 중첩(Nesting)

Sass는 중첩 기능을 사용할 수 있습니다.
상위 선택자의 반복을 피하기 때문에 코드를 간결하게 구성할 수 있습니다.

SCSS:

```scss
.section {
  width: 100%;
  .list {
    padding: 20px;
    li {
      float: left;
    }
  }
}
```

Compiled to:

```css
.section {
  width: 100%;
}
.section .list {
  padding: 20px;
}
.section .list li {
  float: left;
}
```

### Ampersand(상위 선택자 참조)

중첩 안에서 `&`키워드는 상위(부모) 선택자를 참조하여 치환합니다.

SCSS:

```scss
.btn {
  position: absolute;
  &.active {
    color: red;
  }
}

.list {
  li {
    &:last-child {
      margin-right: 0;
    }
  }
}
```

Compiled to:

```css
.btn {
  position: absolute;
}
.btn.active {
  color: red;
}
.list li:last-child {
  margin-right: 0;
}
```

| ![상위 선택자 사용](images/ampersand_2.png) |
| :-----------------------------------------: |
|                 & 사용 화면                 |

Sass에서 & 사용시 공통으로 가지고 있는 상위 선택자에 대한 지정을 일일히 해주지 않아도 됩니다.

**&를 사용하지 않는다면?**

| ![상위 선택자](images/ampersand_1.png) |
| :------------------------------------: |
|        상위 선택자 미사용 화면         |

`&`를 사용하지 않을 경우 css로 컴파일 될 때 이중으로 클래스가 선택되는 것을 볼 수 있습니다. 이는 스타일링할 때 우선순위에 의해 다른 스타일링이 적용되지 않을 수도 있습니다.

### @at-root(중첩 벗어나기)

중첩에서 벗어나고 싶을 때 `@at-root` 키워드를 사용합니다. 중첩 안에서 생성하되 유효 범위 바깥에 있는 요소에 접근할 때 유용합니다.

SCSS:

```scss
.list {
  $w: 100px;
  $h: 50px;
  li {
    width: $w;
    height: $h;
  }
  @at-root .box {
    width: $w;
    height: $h;
  }
}
```

Complied to:

```css
.list li {
  width: 100px;
  height: 50px;
}
.box {
  width: 100px;
  height: 50px;
}
```

아래 예제 처럼 `.list`안에 있는 특정 변수를 범위 밖에서 사용할 수 없기 때문에, 위 예제처럼 `@at-root` 키워드를 사용해야 합니다.

**예시**

| ![at-root 사용](images/at_root_1.png) |
| :-----------------------------------: |
|         @at-root 미사용 화면          |

`box`클래스가 `section`클래스 안에 있습니다.

| ![at-root 미사용](images/at_root_2.png) |
| :-------------------------------------: |
|           @at-root 사용 화면            |

`box`클래스가 `@at-root`로 인해 `section`영역에서 벗어났음을 볼 수 있습니다.

### 중첩된 속성

`font-`, `margin-`등과 같이 동일한 네임 스페이스를 가지는 속성들을 다음과 같이 사용할 수 있습니다.

SCSS:

```scss
.box {
  font: {
    weight: bold;
    size: 10px;
    family: sans-serif;
  }
  margin: {
    top: 10px;
    left: 20px;
  }
  padding: {
    bottom: 40px;
    right: 30px;
  }
}
```

Compiled to:

```css
.box {
  font-weight: bold;
  font-size: 10px;
  font-family: sans-serif;
  margin-top: 10px;
  margin-left: 20px;
  padding-bottom: 40px;
  padding-right: 30px;
}
```

### 변수

Sass를 사용하면 반복적으로 사용되는 값을 변수로 지정해서 사용함으로 코드의 중복을 방지할 수 있습니다.
변수를 선언해줄때는 항상 이름 앞에 $를 붙여줘야 합니다.

아래와 같은 방식으로 선언을 해서 사용하면 됩니다.
$`변수이름`: `속성값`;

세 가지 변수를 선언하고 이를 통해 .box라는 클래스를 스타일링 해준 예시입니다.
아래처럼 선언시 밑에 css파일처럼 컴파일이 진행됩니다.

자주 사용하는 변수를 이렇게 미리 선언해놓고 사용시 매번 동일한 코드를 다시 입력할 불편함이 사라지고 매번 값을 입력할때 생기는 오탈자 및 불확실성을 방지할 수 있습니다.

```scss
$color-primary: #e96900;
$url-images: "/assets/images/";
$w: 200px;

.box {
  width: $w;
  margin-left: $w;
  background: $color-primary url($url-images + "bg.jpg");
}
```

```css
.box {
  width: 200px;
  margin-left: 200px;
  background: #e96900 url("/assets/images/bg.jpg");
}
```

- 변수 유효범위 (Variable Scope)

변수에는 사용 가능한 유효범위가 지정되어 있습니다.
선언된 블록({}) 내에서만 유효범위를 가지고 있어 전역속성의 값처럼은 사용이 어렵습니다.

만약 변수 $color를 .box1의 블록 안에서 선언하게되면, 일반적으로는 블록 밖의 .box2에서는 해당 변수를 사용할 수 없게 됩니다.

- 변수 재 할당(Variable Reassignment)

변수는 변수를 통해 재 선언을 진행할 수도 있습니다.

이를 변수에 변수를 할당한다해서 변수 재 할당이라고 부르며 아래의 예시에서 이미 변수로 선언해 놓은 변수를 다시 한번 재 정의한 모습을 확인할 수 있습니다.

```scss
$red: #ff0000;
$blue: #0000ff;

$color-primary: $blue;
$color-danger: $red;

.box {
  color: $color-primary;
  background: $color-danger;
}
```

- `!global` (전역 설정)

`!global` 플래그를 사용하면 변수의 유효범위를 전역(Global)으로 변경해줄 수 있습니다.
위에 설명한 변수 유효범위의 한계를 이를 통해 해결해 줄 수 있지만 만약 이전에 같은 변수명으로 변수가 선언되어 있었다면 !global 플래그를 통해 설정한 변수로 값이 덮어 씌어지게 되어 사용할때 변수명을 꼭 확인 해주는게 필요합니다.

- `!default` (초기값 설정)

`!default` 플래그는 할당되지 않은 변수의 초깃값을 설정해 줄 수 있습니다.
즉, 할당되어있는 변수가 있다면 변수가 기존 할당 값을 사용하게 됩니다.

만약 코드가 너무 복잡해지고 위에 해당 변수를 이미 사용했는지 여부에 대해서 확신이 없다면 초기값 설정을 통해서 이를 해결할 수 있습니다.

보통 Bootstrap과 같은 외부 라이브러리에 많이 선언되어 있으며 이는 라이브러리에 선언된 변수의 중첩된 이름이 있어도 이를 사용자 코드에 덮어 씌우는 일을 막기 위한 목적을 가지고 있습니다.

- `#{}` 문자 보간

`#{}`를 이용하면 코드의 중간에 변수 값을 삽입해 줄 수 있습니다.
코드#{변수명} 구조를 통해서 선언해 줄 수 있습니다.

### 가져오기(import)

`@import`로 외부에서 Sass 파일을 가지고 올 수 있는데 이때 해당 파일은 모두 단일 CSS 출력 파일로 병합됩니다.

보통 `@import`시 Sass 파일을 가져오게 되는데 이때 CSS의 @import 규칙으로 컴파일이 되는 경우도 네 가지 존재합니다.

- 파일 확장자명이 .css인 경우
- 파일 이름이 http://로 시작하는 경우
- url()이 존재하는 경우
- 미디어 쿼리가 존재하는 경우

```scss
@import "hello.css";
@import "http://hello.com/hello";
@import url(hello);
@import "hello" screen;
```

- 여러 파일 가져오기

하나의 `@import`를 선언해서 여러 파일들을 가지고 올 수도 있습니다.
이때 파일 이름 사이에 `,`를 통해 구분해서 선언 해줍니다.

```scss
@import "header", "footer", "more";
```

- 파일 분할 (Partials)

프로젝트 규모가 커지고 파일이 복잡해지면 각 기능과 부분적인 요소들로 나눠서 파일들을 작성하게 됩니다. 이때 scss파일이 여러개로 나눠져서 컴파일시 각각의 css 파일로 나눠서 저장된다면 관리/성능 및 유지보수 차원에서 상당한 불편함이 생기게 됩니다.

이때 파일 분할 (Partials)기능을 이용해서 이를 해결할 수 있습니다.
만약 scss파일이 여러개면 하나의 scss파일에 들어가 `@import`를 통해 나머지 scss파일들을 가지고 오고 나머지 scss파일을 통합한 하나의 scss파일을 css디렉토리로 컴파일을 해줘서 한번만 선언을 진행 해줍니다!

### 연산자

CSS와 다르게 Sass에서는 기본적인 연산 기능을 지원하고 있습니다.
레이아웃 디자인 작업시 상황에 맞게 크기를 계산 하거나 정해진 값을 나눠서 작성할 경우 유용하게 사용할 수 있으며 이 기능을 이용하면 기존 css에서 사용하던 `Emmet: Evaluate Math Expression`을 사용하지 않고도 손쉽게 연산을 진행할 수 있습니다.

아래는 Sass에서 사용 가능한 연산자 종류들입니다.

`==`와 `!=`은 두 값이 동일한지의 여부를 확인하기 위해 사용되는 연산자입니다.

`+,` `-`, `*`, `/`, `%`들은 일반적으로 수학에서 사용되는 기능들을 하는 연산자로 각각 더하기, 빼기, 곱하기, 나누기, 나머지를 계산해줄때 사용되는 연산자들입니다.

`<`, `<=`, `>`, `>=`들은 각각의 값들을 비교 해줄때 사용하는 연산자들로 특정 값들의 대소를 비교할때 자주 사용되는 연산자들입니다.

`and`, `or`, `not`들은 논리 연산자들로 Saas에서는 거짓과 null값을 제외한 모든 값들이 참으로 설정되어 있기에 이 점을 유의해서 사용하면 됩니다.

`+`, `-`, `/` 연산자들은 문자들을 연결할때도 사용 될 수 있습니다.

- 숫자 (Numbers)

상대적 단위(%, em, vw 등)의 연산의 경우 CSS calc() 함수를 이용해서 연산을 진행할 수 있습니다.
연산을 진행하기 위해서는 꼭 동일한 단위가 입력되어야 하며 만약 50% - 20px과 같이 한 부분에는 %단위를 한 부분에는 픽셀 단위를 기입하게 되면 단위 모순 에러가 발생하게됩니다.

또한 나누기 연산자는 `/` 기호가 사용되는데 이는 위에 연산자에서 설명했듯이 문자들을 연결할때도 사용되는 연산자로 사용하는데 몇 가지 주의사항이 있습니다.

다른 연산자들과 다르게 그냥 `30px / 2`와 같이 사용하면 작동하지 않으며 아래 세 가지 방법 중 하나의 방법을 택하여 선언해 줘야 합니다.

1. 값 또는 그 일부가 변수로 선언되어 저장되거나 함수 호출을 통해 반환되는 경우
   ex) width: $x / 2;
2. 값이 ()소괄호로 묶여져서 선언되는 경우
   ex) width: (30px / 2);
3. 값이 다른 산술자와 함께 사용되는 경우
   ex) 10px + 15px / 3;

- 문자 (Strings)

문자 연산은 기본적으로 `+`, `-`, `/` 기호들을 이용하여 생성이 가능합니다.
문자 연산에서는 첫번째 피연산자의 `quote`여부가 중요하며 첫번째 피연산자가 `quote`를 포함하고 있다면 결과도 이를 포함하고 만약 포함하고 있지 않다면 결과도 이를 포함하지 않고 계산됩니다.

```scss
div::after {
  content: "Fast " + Campus;
  flex-flow: row + "-reverse" + " " + wrap;
}
```

```css
div::after {
  content: "Fast Campus";
  flex-flow: row-reverse wrap;
}
```

- 논리 (Boolean)

Sass의 논리 연산자에는 기본적으로 `and`, `or`, `not`가 사용됩니다.
이는 각각 `그리고`, `또는`, `부정`으로 해석할 수 있으며 파이썬에서 사용되는 논리 연산자와 동일한 역할들을 합니다.
자바스크립트 언어로 생각하면 각각 `&&`, `||`, `!`로 생각하면 쉽게 이해를 할 수 있습니다.

각각의 논리 연산자의 예시는 아래와 같습니다.

    not true --> false
    not false --> true

    true and true --> true
    true and false --> false
    false and false --> false

    true or true --> true
    true or false --> true
    false or false --> false

Truthy and Falsy

참과 거짓을 사용할 수 있는 공간이면 다른 값들도 입력이 가능합니다.
이때 truthy and falsy라고 불리는 조건으로 false와 null값은 falsy를 의미하고 그 두 값들을 제외한 모든 값들에 대해서는 truthy를 의미하게 됩니다.

다른 일반적인 언어들에서는 보통 0, 빈 배열, 빈 문자등도 함께 falsy를 나타내지만 Sass에서는 오직 두 값만 falsy를 나타낸다는 특징이 있습니다.

### 재활용 (Mixins)

Sass에 존재하는 재활용, 즉 Mixins는 재사용 할 css 그룹을 미리 지정해놓고 필요한 경우에 언제든지 편하게 사용할수 있게 만들어주는 효율적인 기능입니다.

`@mixin`과 `@include`는 항상 함께 사용되며 이때 `@mixin`을 사용하면 그룹 단위의 스타일을 변수처럼 적용할 수 있게 됩니다. 즉, 여러개의 스타일을 설정해두었다가 한번에 적용하는 것이 가능해지고 이때 설정에는 @mixin을 그리고 사용할 때는 @include를 활용하여 사용하면 됩니다.

Sass에서는 `=`와 `+` 기호로 `Mixins` 기능을 사용하고 SCSS에서는 `@mixin`과 `@include`로 기능을 사용한다는 차이점이 있습니다.

아래는 Scss와 Sass에서의 mixin 선언을 하는 방법을 나타내는 예시입니다.

```scss
// SCSS
@mixin 믹스인이름 {
  스타일;
}
```

```sass
// Sass
=믹스인이름
  스타일
```

이렇게 선언해준 Mixin을 아래의 방법으로 Scss와 Sass에서 include하여 사용할 수 있습니다.

```scss
// SCSS
@include 믹스인이름;
```

```sass
// Sass
+믹스인이름
```

재밌는 사실로는 Sass에서 `-` 기호와 `_`를 동일한 기호로 이해하기에 Mixin 이름을 만약 reset-list라고 줄 시 reset_list라고 선언해도 똑같은 mixin을 가리키게 됩니다.

- 인수 (Arguments)

Mixin(재활용)은 일반적인 함수처럼 인수를 포함할 수 있습니다.
이를 이용하면 하나의 Mixin을 통해서 다양한 css스타일링을 선언할 수 있게 됩니다.

Mixin 이름 뒤에 괄호를 적고 그 내부에 변수 이름 목록들을 지정해서 사용할 수 있습니다.

```scss
// SCSS
@mixin 믹스인이름($매개변수) {
  스타일;
}
@include 믹스인이름(인수);
```

- 기본값 설정

인수를 선언할때 `@include`시 별도의 인수가 입력되지 않으면 기본적으로 설정해놓은 값을 적용시킬 수도 있습니다.
즉, 매개변수에 이미 기본 값을 적어주고 선언해줄때 해당 변수에 어떠한 값도 지정해주지 않으면 기본 값이 적용하게 됩니다.

아래의 예시 코드를 보면 기본값으로 너비와 높이에 100px씩을 선언해줘서 아무런 변수도 지정해주지 않은 box1 클래스에 대해서는 너비, 높이가 100px로 적용이 된 모습을 확인할 수 있고 따로 너비와 높이를 설정해준 box2 클래스는 해당 크기만큼 적용이된 모습을 확인할 수 있습니다.

```scss
@mixin size($w: 100px, $h: 100px) {
  // 기본값으로 100px을 선언
  width: $w;
  height: $h;
}

.box1 {
  @include size;
}

.box2 {
  @include size(200px, 400px);
}
```

```css
.box1 {
  width: 100px;
  height: 100px;
}

.box2 {
  width: 200px;
  height: 100px;
}
```

- 키워드 인수

Mixin이 포함된 경우 인수 목록에서 인수를 순서대로 전달하는 것 외에도 이름으로 인수를 전달할 수 있습니다.
이는 여러 선택적 인수가 존재하는 Mixin이나 이름 없이 의미가 분명하지 않은 Boolean인수와 함께 사용할 때 특히 유용하며 키워드 인수는 변수 선언 및 선택적 인수와 동일한 구문을 사용해서 활용할 수 있습니다.

아래의 예시를 참고하면 첫번째 인수는 기본값으로 설정하고 싶기에 두번째 인수인 radius만 선언이 필요한 경우 $radius처럼 명시적으로 이름을 선언해서 적용시켜 주는 모습을 확인할 수 있습니다.

```scss
@mixin square($size: 100px, $radius: 0) {
  width: $size;
  height: $size;

  @if $radius != 0 {
    border-radius: $radius;
  }
}

.avatar {
  @include square($radius: 4px);
}
```

- 가변 인수 (Variable Arguments)

간혹 입력할 매개변수의 크기가 가변하는 경우가 발생하는 일이 있을수도 있습니다.
이때는 가변 인수를 활용하여 해결할 수 있습니다.

예를들어 background-image 속성의 경우 여러가지 이미지 파일들을 한번에 선언해서 사용할수 있는데 이때 가변형으로 background-image를 선언해두면 개수에 상관없이 인수를 입력할 수 있게됩니다.

아래의 예시 코드처럼 가변 인수로 사용할 변수 뒤에는 `...`을 함께 붙여줌으로 선언해 줄 수 있으며 이렇게 선언된 변수에는 아래의 예시처럼 원하는만큼 인수를 선언해줄 수 있습니다.

```scss
@mixin bg($width: 100px, $height: 200px, $bg-values...) {
  width: $width;
  height: $height;
  background: $bg-values;
}

div {
  @include bg(
    url("/images/a.png") no-repeat 10px 20px,
    url("/images/b.png") no-repeat,
    url("/images/c.png")
  );
```

### extend

extend 는 일반적인 상속과 비슷한 개념입니다. 특정 선택자의 속성을 모두 가져와야 되는 경우 extend를 사용합니다.

하지만 extend를 사용하는 경우 컴파일 과정에서 원치 않는 결과가 도출될 수가 있습니다.

extend를 사용할 경우 모든 속성이 복사되는 것이 아니라, 현재 extend를 요청한 클래스를 요청 당한 클래스의 내부 클래스로 만들기 때문에, 예상과 다른 결과를 낼 수 있다. 때문에 조심해서 사용해야 합니다.

### Functions

function 과 mixin의 차이는 mixin은 스타일을 반환하지만 function 은 값을 리턴하는게 차이입니다.

또한 function의 경우 함수를 즉시 이름만 써서 사용하지만 mixin의 경우 @include 를 사용합니다.

function 을 통해 css에서는 불가능했던 로직의 재사용을 가능하게 합니다.

함수는 scss 의 내장함수와 이름이 겹칠 경우, 문제가 생길 수 있기 때문에 특별한 명칭을 붙여주어서 구분하는 게 좋습니다.

### 조건문

조건문은 삼항 연산자 같은 사용과, 지시어를 통해 사용하는 방법 두가지가 있습니다.

#### if

일반 언어의 삼항연산자 처럼 사용되며

```scss
$width: 555px;
div {
  width: if($width > 300px, $width, null);
}
```

이렇게 스타일 태그 내부에 즉시 사용합니다.

#### @if

@if, @else if, @else 세 가지 지시어를 사용할 수 있으며, 해당 조건문 내부에 스타일 속성을 넣어서 해당 조건일 경우에만 스타일이 실행되도록 만들 수 있습니다.

### 반복문

여러 스타일을 반복 사용하는 데 사용됩니다.

#### @for

```scss
@for $변수 from through 종료 {
}
```

위 처럼 사용되며, through 대신 to를 사용할 수 있습니다. 둘의 차이는 through 는 종료 조건을 포함하고, to는 종료 조건을 포함하지 않는 것입니다.

#### @each

list와 map 에 반복문을 적용시킬 때 사용합니다. 특히 map의 경우는 key:value 형태로 만들어져 있기 때문에, 두 개의 변수를 선언해야 사용할 수 있습니다.

#### @while

scss는 언어적 활용보다는 스타일링을 지원하기 위해 사용하기 위해 무한루프에 빠질 수 있는 while문은 권장되지 않습니다.

### 내장 함수

scss 는 css 전처리기이기 때문에, 다양한 디자인 스타일링을 위한 내장 함수를 지원합니다.

### extend

extend 는 일반적인 상속과 비슷한 개념입니다. 특정 선택자의 속성을 모두 가져와야 되는 경우 extend를 사용합니다.

하지만 extend를 사용하는 경우 컴파일 과정에서 원치 않는 결과가 도출될 수가 있습니다.

extend를 사용할 경우 모든 속성이 복사되는 것이 아니라, 현재 extend를 요청한 클래스를 요청 당한 클래스의 내부 클래스로 만들기 때문에, 예상과 다른 결과를 낼 수 있다. 때문에 조심해서 사용해야 합니다.

### Functions

function 과 mixin의 차이는 mixin은 스타일을 반환하지만 function 은 값을 리턴하는게 차이입니다.

또한 function의 경우 함수를 즉시 이름만 써서 사용하지만 mixin의 경우 @include 를 사용합니다.

function 을 통해 css에서는 불가능했던 로직의 재사용을 가능하게 합니다.

함수는 scss 의 내장함수와 이름이 겹칠 경우, 문제가 생길 수 있기 때문에 특별한 명칭을 붙여주어서 구분하는 게 좋습니다.

### 조건문

조건문은 삼항 연산자 같은 사용과, 지시어를 통해 사용하는 방법 두가지가 있습니다.

#### if

일반 언어의 삼항연산자 처럼 사용되며

```scss
$width: 555px;
div {
  width: if($width > 300px, $width, null);
}
```

이렇게 스타일 태그 내부에 즉시 사용합니다.

#### @if

@if, @else if, @else 세 가지 지시어를 사용할 수 있으며, 해당 조건문 내부에 스타일 속성을 넣어서 해당 조건일 경우에만 스타일이 실행되도록 만들 수 있습니다.

### 반복문

여러 스타일을 반복 사용하는 데 사용됩니다.

#### @for

```scss
@for $변수 from through 종료 {
}
```

위 처럼 사용되며, through 대신 to를 사용할 수 있습니다. 둘의 차이는 through 는 종료 조건을 포함하고, to는 종료 조건을 포함하지 않는 것입니다.

#### @each

list와 map 에 반복문을 적용시킬 때 사용합니다. 특히 map의 경우는 key:value 형태로 만들어져 있기 때문에, 두 개의 변수를 선언해야 사용할 수 있습니다.

#### @while

scss는 언어적 활용보다는 스타일링을 지원하기 위해 사용하기 위해 무한루프에 빠질 수 있는 while문은 권장되지 않습니다.

### 내장 함수

scss 는 css 전처리기이기 때문에, 다양한 디자인 스타일링을 위한 내장 함수를 지원합니다.

<table>
    <thead>
        <tr>
            <th scope="col">구분</th>
            <th scope="col">함수</th>
            <th scope="col">기능</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th rowspan="9">색상</th>
            <th>mix($color1, $color2) </th>
            <td>두 개의 색을 섞습니다.</td>
        </tr>
        <tr>
            <th>lighten($color, $amount) </th>
            <td>더 밝은색을 만듭니다.</td>
        </tr>
        <tr>
            <th>darken($color, $amount) </th>
            <td>더 어두운색을 만듭니다.</td>
        </tr>
        <tr>
            <th>saturate($color, $amount) </th>
            <td>색상의 채도를 올립니다.</td>
        </tr>
        <tr>
            <th>desaturate($color, $amount) </th>
            <td>색상의 채도를 낮춥니다.</td>
        </tr>
        <tr>
            <th>grayscale($color) </th>
            <td>색상을 회색으로 변환합니다.</td>
        </tr>
        <tr>
            <th>invert($color) </th>
            <td>색상을 반전시킵니다.</td>
        </tr>
        <tr>
            <th>opacify($color, $amount) / fade-in($color, $amount) </th>
            <td>색상을 더 불투명하게 만듭니다.</td>
        </tr>
        <tr>
            <th>transparentize($color, $amount) / fade-out($color, $amount) </th>
            <td>색상을 더 투명하게 만듭니다.</td>
        </tr>
        <tr>
            <th rowspan="7">문자</th>
            <th>unquote($string) </th>
            <td>문자에서 따옴표를 제거합니다.</td>
        </tr>
        <tr>
            <th>str-insert($string, $insert, $index) </th>
            <td>문자의 index번째에 특정 문자를 삽입합니다.</td>
        </tr>
        <tr>
            <th>quote($string) </th>
            <td>문자에 따옴표를 추가합니다.</td>
        </tr>
        <tr>
            <th>str-index($string, $substring) </th>
            <td> 문자에서 특정 문자의 첫 index를 반환합니다.</td>
        </tr>
        <tr>
            <th>str-slice($string, $start-at, [$end-at]) </th>
            <td>문자에서 특정 문자(몇 번째 글자부터 몇 번째 글자까지)를 추출합니다.</td>
        </tr>
        <tr>
            <th>to-upper-case($string) </th>
            <td>문자를 대문자를 변환합니다.</td>
        </tr>
        <tr>
            <th>to-lower-case($string) </th>
            <td>문자를 소문자로 변환합니다.</td>
        </tr>
        <tr>
            <th rowspan="7">숫자</th>
            <th>round($number) </th>
            <td>정수로 반올림합니다.</td>
        </tr>
        <tr>
            <th>ceil($number) </th>
            <td>정수로 올림합니다.</td>
        </tr>
        <tr>
            <th>floor($number)</th>
            <td>정수로 내림(버림)합니다.</td>
        </tr>
        <tr>
            <th>abs($number) </th>
            <td>숫자의 절대 값을 반환합니다. </td>
        </tr>
        <tr>
            <th>min($numbers…) </th>
            <td>숫자 중 최소 값을 찾습니다.</td>
        </tr>
        <tr>
            <th>max($numbers…) </th>
            <td>숫자 중 최대 값을 찾습니다.</td>
        </tr>
        <tr>
            <th>random()</th>
            <td>0 부터 1 사이의 난수를 반환합니다.</td>
        </tr>
        <tr>
            <th rowspan="6">리스트</th>
            <th>length($list) </th>
            <td>List의 개수를 반환합니다.</td>
        </tr>
        <tr>
            <th>nth($list, $n)</th>
            <td>List에서 n번째 값을 반환합니다.</td>
        </tr>
        <tr>
            <th>set-nth($list, $n, $value)</th>
            <td> List에서 n번째 값을 다른 값으로 변경합니다.</td>
        </tr>
        <tr>
            <th>join($list1, $list2, [$separator])</th>
            <td>두 개의 List를 하나로 결합합니다.</td>
        </tr>
        <tr>
            <th>zip($lists…)</th>
            <td>여러 List들을 하나의 다차원 List로 결합합니다.</td>
        </tr>
        <tr>
            <th>index($list, $value)</th>
            <td>List에서 특정 값의 index를 반환합니다.</td>
        </tr>
        <tr>
            <th rowspan="4">map</th>
            <th>map-get($map, $key) </th>
            <td> Map에서 특정 key의 value를 반환합니다.</td>
        </tr>
        <tr>
            <th>map-merge($map1, $map2)</th>
            <td>두 개의 Map을 병합하여 새로운 Map를 만듭니다.</td>
        </tr>
        <tr>
            <th>map-keys($map)</th>
            <td>Map에서 모든 key를 List로 반환합니다.</td>
        </tr>
        <tr>
            <th>map-values($map)</th>
            <td> Map에서 모든 value를 List로 반환합니다.</td>
        </tr>
        <tr>
            <th rowspan="4">관리함수</th>
            <th> variable-exists(name)</th>
            <td> 변수가 현재 범위에 존재하는지 여부를 반환합니다.(인수는 $없이 변수의 이름만 사용합니다.) </td>
        </tr>
        <tr>
            <th>unit($number)</th>
            <td>숫자의 단위를 반환합니다.</td>
        </tr>
        <tr>
            <th>unitless($number)</th>
            <td>숫자에 단위가 있는지 여부를 반환합니다.</td>
        </tr>
        <tr>
            <th>comparable($number1, $number2)</th>
            <td>두 개의 숫자가 연산 가능한지 여부를 반환합니다.</td>
        </tr>
    </tbody>

</table>

<details>
<summary>참고자료</summary>
<a href="https://heropy.blog/2018/01/31/sass/">HEROPY Blog</a>
<br />
<a href="https://sass-lang.com/documentation">Sass 공식문서
<br />
</details>
