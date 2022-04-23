# Vue 3 + Typescript + Vite 模板搭建

### 初步 Vite +Vue 项目搭建

参考[vite 官方文档教程](https://cn.vitejs.dev/guide/#scaffolding-your-first-vite-project)

```
# npm 6.x
npm create vite@latest my-vue-app --template vue

# npm 7+, extra double-dash is needed:
npm create vite@latest my-vue-app -- --template vue

# yarn
yarn create vite my-vue-app --template vue

# pnpm
pnpm create vite my-vue-app -- --template vue
```

这里我选用yarn命令创建，用npm创建的话不会有相应库可供选择安装，在可选项中我选择vue-ts

cd 到 相应的目录文件夹

```
# 进入项目文件夹
cd 你自己命名的文件夹
# 安装依赖
yarn
# 启动
yarn dev
```

项目中引入ts后在.vue文件中导入vues时可能会出现无法识别vue的错误（也可能不出现）

解决方案：添加类型声明， 在shims-vue.d.ts`同级新增一个xx.d.ts文件（文件名随意，后缀一定是.d.ts） 加如以下配置

```
import Vue from 'vue'
import VueRouter from 'vue-router'
import { Route } from 'vue-router'
import { Store } from 'vuex'
import t from '@/i18n'
// 扩充
declare module 'vue/types/vue' {
    interface Vue {
        $router: VueRouter
        $route: Route
        $store: Store<any>
        $t: t
    }
}
```



### 加入Eslint支持

#### eslint 安装

[eslint官方文档](https://eslint.org/docs/user-guide/getting-started)

[typeScript插件](https://github.com/typescript-eslint/typescript-eslint/tree/main/packages/eslint-plugin)  

```
# eslint 安装
yarn add eslint --dev

# eslint 插件相关安装
yarn add eslint-plugin-vue --dev
yarn add @typescript-eslint/eslint-plugin --dev
yarn add eslint-plugin-prettier --dev

# typescript parser
yarn add @typescript-eslint/parser --dev

```

 注意: 如果 `eslint` 安装报错:如下

```
error @eslint/eslintrc@1.2.2: The engine "node" is incompatible with this module. Expected version "^12.22.0 || ^14.17.0 || >=16.0.0". Got "14.15.3"
error Found incompatible module.
```

[解决方案参考链接](https://blog.csdn.net/qq_42144899/article/details/88574761)

执行以下命令

```
yarn config set ignore-engines true
再执行安装eslint的命令 
yarn add eslint --dev 
```

#### 项目下新建 .eslintrc.js

更多配置规则见[官方文档](http://eslint.cn/docs/rules/)

```
module.exports = {
  root: true,
  env: {
    browser: true,
    node: true,
    es2021: true,
  },
  parser: 'vue-eslint-parser',
  extends: [
    'eslint:recommended',
    'plugin:vue/vue3-recommended',
    'plugin:@typescript-eslint/recommended',
    'plugin:prettier/recommended',
    // eslint-config-prettier 的缩写
    'prettier',
  ],
  parserOptions: {
    ecmaVersion: 12,
    parser: '@typescript-eslint/parser',
    sourceType: 'module',
    ecmaFeatures: {
      jsx: true,
    },
  },
  // eslint-plugin-vue @typescript-eslint/eslint-plugin eslint-plugin-prettier的缩写
  plugins: ['vue', '@typescript-eslint', 'prettier'],
  rules: {
    '@typescript-eslint/ban-ts-ignore': 'off',
    '@typescript-eslint/no-unused-vars': 'off',
    '@typescript-eslint/explicit-function-return-type': 'off',
    '@typescript-eslint/no-explicit-any': 'off',
    '@typescript-eslint/no-var-requires': 'off',
    '@typescript-eslint/no-empty-function': 'off',
    '@typescript-eslint/no-use-before-define': 'off',
    '@typescript-eslint/ban-ts-comment': 'off',
    '@typescript-eslint/ban-types': 'off',
    '@typescript-eslint/no-non-null-assertion': 'off',
    '@typescript-eslint/explicit-module-boundary-types': 'off',
    'no-var': 'error',
    'prettier/prettier': 'error',
    // 禁止出现console
    'no-console': 'warn',
    // 禁用debugger
    'no-debugger': 'warn',
    // 禁止出现重复的 case 标签
    'no-duplicate-case': 'warn',
    // 禁止出现空语句块
    'no-empty': 'warn',
    // 禁止不必要的括号
    'no-extra-parens': 'off',
    // 禁止对 function 声明重新赋值
    'no-func-assign': 'warn',
    // 禁止在 return、throw、continue 和 break 语句之后出现不可达代码
    'no-unreachable': 'warn',
    // 强制所有控制语句使用一致的括号风格
    curly: 'warn',
    // 要求 switch 语句中有 default 分支
    'default-case': 'warn',
    // 强制尽可能地使用点号
    'dot-notation': 'warn',
    // 要求使用 === 和 !==
    eqeqeq: 'warn',
    // 禁止 if 语句中 return 语句之后有 else 块
    'no-else-return': 'warn',
    // 禁止出现空函数
    'no-empty-function': 'warn',
    // 禁用不必要的嵌套块
    'no-lone-blocks': 'warn',
    // 禁止使用多个空格
    'no-multi-spaces': 'warn',
    // 禁止多次声明同一变量
    'no-redeclare': 'warn',
    // 禁止在 return 语句中使用赋值语句
    'no-return-assign': 'warn',
    // 禁用不必要的 return await
    'no-return-await': 'warn',
    // 禁止自我赋值
    'no-self-assign': 'warn',
    // 禁止自身比较
    'no-self-compare': 'warn',
    // 禁止不必要的 catch 子句
    'no-useless-catch': 'warn',
    // 禁止多余的 return 语句
    'no-useless-return': 'warn',
    // 禁止变量声明与外层作用域的变量同名
    'no-shadow': 'off',
    // 允许delete变量
    'no-delete-var': 'off',
    // 强制数组方括号中使用一致的空格
    'array-bracket-spacing': 'warn',
    // 强制在代码块中使用一致的大括号风格
    'brace-style': 'warn',
    // 强制使用骆驼拼写法命名约定
    camelcase: 'warn',
    // 强制使用一致的缩进
    indent: 'off',
    // 强制在 JSX 属性中一致地使用双引号或单引号
    // 'jsx-quotes': 'warn',
    // 强制可嵌套的块的最大深度4
    'max-depth': 'warn',
    // 强制最大行数 300
    // "max-lines": ["warn", { "max": 1200 }],
    // 强制函数最大代码行数 50
    // 'max-lines-per-function': ['warn', { max: 70 }],
    // 强制函数块最多允许的的语句数量20
    'max-statements': ['warn', 100],
    // 强制回调函数最大嵌套深度
    'max-nested-callbacks': ['warn', 3],
    // 强制函数定义中最多允许的参数数量
    'max-params': ['warn', 3],
    // 强制每一行中所允许的最大语句数量
    'max-statements-per-line': ['warn', { max: 1 }],
    // 要求方法链中每个调用都有一个换行符
    'newline-per-chained-call': ['warn', { ignoreChainWithDepth: 3 }],
    // 禁止 if 作为唯一的语句出现在 else 语句中
    'no-lonely-if': 'warn',
    // 禁止空格和 tab 的混合缩进
    'no-mixed-spaces-and-tabs': 'warn',
    // 禁止出现多行空行
    'no-multiple-empty-lines': 'warn',
    // 禁止出现;
    semi: ['warn', 'never'],
    // 强制在块之前使用一致的空格
    'space-before-blocks': 'warn',
    // 强制在 function的左括号之前使用一致的空格
    // 'space-before-function-paren': ['warn', 'never'],
    // 强制在圆括号内使用一致的空格
    'space-in-parens': 'warn',
    // 要求操作符周围有空格
    'space-infix-ops': 'warn',
    // 强制在一元操作符前后使用一致的空格
    'space-unary-ops': 'warn',
    // 强制在注释中 // 或 /* 使用一致的空格
    // "spaced-comment": "warn",
    // 强制在 switch 的冒号左右有空格
    'switch-colon-spacing': 'warn',
    // 强制箭头函数的箭头前后使用一致的空格
    'arrow-spacing': 'warn',
    'no-var': 'warn',
    'prefer-const': 'warn',
    'prefer-rest-params': 'warn',
    'no-useless-escape': 'warn',
    'no-irregular-whitespace': 'warn',
    'no-prototype-builtins': 'warn',
    'no-fallthrough': 'warn',
    'no-extra-boolean-cast': 'warn',
    'no-case-declarations': 'warn',
    'no-async-promise-executor': 'warn',
  },
  globals: {
    defineProps: 'readonly',
    defineEmits: 'readonly',
    defineExpose: 'readonly',
    withDefaults: 'readonly',
  },
}
```

#### 项目下新建 .eslintignore

 eslint 忽略检查 (根据项目需要自行添加)

```
node_modules
dist
```

### 加入prettier 支持

```
# 安装 prettier
yarn add prettier --dev
```



#### 解决 eslint 和 prettier 冲突

 解决 `ESLint` 中的样式规范和 `prettier` 中样式规范的`冲突`，以 `prettier` 的样式规范`为准`，使 ESLint 中的样式规范自动失效 

```
# 安装插件 eslint-config-prettier
yarn add eslint-config-prettier --dev
```

#### 项目下新建  .prettierrc.js 

Prettier 的配置文件可以用 4 种文件格式编写，随便喜欢哪一种，文件名不要写错就行

1. JavaScript `.prettierrc.js`或`prettier.config.js`
2. JSON `.prettierrc.json`
3. YAML `.prettierrc.yaml`或`.prettierrc.yml`
4. TOML `.prettierrc.toml`

 配置 `prettier` 格式化规则 

更多配置详看[配置文档](https://prettier.io/docs/en/configuration.html)

```
module.exports = {
  tabWidth: 2,
  jsxSingleQuote: true,
  jsxBracketSameLine: true,
  printWidth: 100,
  singleQuote: true,
  semi: false,
  overrides: [
    {
      files: '*.json',
      options: {
        printWidth: 200,
      },
    },
  ],
  arrowParens: 'always',
}
```



#### 项目下新建 .prettierignore

```
# 忽略格式化文件 (根据项目需要自行添加)
node_modules
dist
!.prettierignore
```

在.prettierrc.js文件中可能会出现以下警告，可以在 .prettierignore中添加 !.prettierignore

```
 warning  File ignored by default.  Use a negated ignore pattern (like "--ignore-pattern '!<relative/path/to/filename>'") to override

```

#### package.json 文件的*scripts"*选项加入以下配置

```
 "script": {
    "lint": "eslint src --fix --ext .ts,.tsx,.vue,.js,.jsx",
    "prettier": "prettier --write ."
  }
```

 上面配置完成后,可以运行以下`命令`测试下代码检查个`格式化`效果: 

```
 # eslint 检查
 yarn lint 
 
 # prettier 自动格式化
 yarn prettier 
```
