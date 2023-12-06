Jest: テストをNode.js上で行うことができるライブラリ。フロントエンドのテスト。<br>
Meta(旧Facebook)社が開発しているJavaScript のフレームワーク。<br>
<br>
vue-test-utils<br>
ライブラリ。テストしたいコンポーネントのインスタンスを取得する。(コードのインスタンスを作成しテストする)<br>
つまり、テストするコンポーネントで、扱っているデータを取ってくるのが vue-test-utils<br>

<br>
単体テストでは、<br>
テストするコンポーネントをマウントで取得し、<br>
テストしたい値を取得し、<br>
実際の値と期待する値が合っているかを判定する。<br>
<br>
<br>
・一般的なマッチャー(Matcher)

test('two plus two is four', () => {<br>
  expect(2 + 2).toBe(4);<br>
});

test関数の第一引数には、テストがどのようなものなのか説明する記述が入る。<br>
第二引数には、テスト内容を記述。<br>
この場合、2 + 2 が 4 に正しくなっているかを判定している。<br>
判定するには expect関数を使用し、toBe 関数はMatcher 関数の一つで、値が等しいかどうかを判定している。<br>
<br>
今回は test関数を使っているが、it関数でも構わない。<br>
その場合は、<br>
it('two plus two is four', () => {<br>
  expect(2 + 2).toBe(4);<br>
});<br>
となる。

npm run test:unit とするとテストが行われ、PASSと表示されれば、このテストが成功したことを意味する。<br><br>

例）<br>
：<br>
 PASS  tests/unit/example.spec.js<br>
  ✓ two plus two is four (2ms)<br>

Test Suites: 1 passed, 1 total<br>
Tests:       1 passed, 1 total<br>
Snapshots:   0 total<br>
Time:        1.44s<br>
Ran all test suites.<br>

失敗すると、FAIL が表示される。

マッチャーは他にもあり、<br>
・toHaveBeenCalled()  モック関数が呼ばれたか確認<br>
・toBeTruthy() 真偽値のコンテクストの中で値が真であることを確認<br>
・toEqual() オブジェクトインスタンスの全てのプロパティが正しいかどうか<br>
・toContain() 値が含まれているかどうか<br>
など他にもたくさんある。詳しくは公式のExpect のMatchers 参照。<br>
<br>
<br>

・Vue.js のコンポーネントを利用してテストを実地<br>
vue/test-utils から mount 関数を import する。<br>
vue/test-utils は Vue Test Util ライブラリを表している。<br>

import { mount } from '@vue/test-utils'; <br>
これで Vue Test Unit ライブラリから関数をimport。<br>

例）<br>
import { mount } from '@vue/test-utils';

const App = {<br>
  &nbsp;template:`<div>Hello World</div>`<br>
}

test("test App Component",function(){<br>
&nbsp;const wrapper = mount(App);<br>
&nbsp;console.log(wrapper.text())<br>
})

<br>
import した mount関数のなかに Appコンポーネントを指定 することで、<br>
Wrapperオブジェクトを作成できる。
<br>
<br>

上記のコードの場合、<br>
App コンポーネントの情報を持つ Wrapper オブジェクトを<br>
mount 関数によって作成し(wrapper定数に入れる)、
その中の情報をテストできる、ということになる。
*const wrapper としているが、 const hogehoge でもWrapper オブジェクトは作成される。
<br>
<br>

expect 関数による値のチェックは行なっていないが、<br>
この状態でもテストを実施することが可能で、<br>
実行するとテストはPASS(成功)し、実行メッセージの中で要素の中身である Hello World が確認できる。
<br>
<br>
<br>

text メソッドによってコンポーネントのコンテンツが取得できることがわかったので、<br>
expect 関数と toBe関数を使ってテストを実行する。<br>
expect 関数の引数にコンポーネントの要素のコンテンツを取得するwrapper.text() を指定して Hello World と一致するかチェックする。<br><br>

import { mount } from '@vue/test-utils';

const App = {<br>
  template:`
<div>Hello World</div>
  `
}

test("test App Component",function(){<br>
  const wrapper = mount(App);<br>
  expect(wrapper.text()).toBe('Hello World')<br>
})

実行するとテストが通る。PASS(成功)。<br>
シンプルな例ですが、Vueコンポーネントをテストする方法を確認することができた。<br>
toBe関数の引数を Hello World 以外にしてテストが失敗することもきちんと確認する！

<br>
<br>
<br>
・SFC（シングルファイルコンポーネント）でのテスト<br>
次はコンポーネントオブジェクトではなく、SFCを利用してテストを実施してみる。

-App.vue-
```html
<template>
  <div>Hello World</div>
</template>
```

example.spec.js ファイルでは作成した App.vue を import する。<br>
App コンポーネントを import する以外は先ほど実行したテスト内容と同じです。<br>
-example.spec.js-<br>
import { mount } from '@vue/test-utils';<br>// components ディレクトリのApp.vue ファイル<br>
import App from "@/components/App.vue";   を import

test("test App Component",function(){<br>
  const wrapper = mount(App);<br>
  expect(wrapper.text()).toBe('Hello World')<br>
})<br>

テストを実行すると、SFCを使ってテストが実施できる。<br>
テストにPASSできていることが確認できる。
