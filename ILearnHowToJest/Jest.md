Jest: テストをNode.js上で行うことができるライブラリ。フロントエンドのテスト。
Meta(旧Facebook)社が開発しているJavaScript のフレームワーク。

vue-test-utils
ライブラリ。テストしたいコンポーネントのインスタンスを取得する。(コードのインスタンスを作成しテストする)
つまり、テストするコンポーネントで、扱っているデータを取ってくるのが vue-test-utils


単体テストでは、
テストするコンポーネントをマウントで取得し、
テストしたい値を取得し、
実際の値と期待する値が合っているかを判定する。

・一般的なマッチャー(Matcher)

test('two plus two is four', () => {
  expect(2 + 2).toBe(4);
});

test関数の第一引数には、テストがどのようなものなのか説明する記述が入る。
第二引数には、テスト内容を記述。
この場合、2 + 2 が 4 に正しくなっているかを判定している。
判定するには expect関数を使用し、toBe 関数はMatcher 関数の一つで、値が等しいかどうかを判定している。

今回は test関数を使っているが、it関数でも構わない。
その場合は、
it('two plus two is four', () => {
  expect(2 + 2).toBe(4);
});
となる。


npm run test:unit とするとテストが行われ、PASSと表示されれば、このテストが成功したことを意味する。

例）
：
 PASS  tests/unit/example.spec.js
  ✓ two plus two is four (2ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        1.44s
Ran all test suites.

失敗すると、FAIL が表示される。

マッチャーは他にもあり、
・toHaveBeenCalled()  モック関数が呼ばれたか確認
・toBeTruthy() 真偽値のコンテクストの中で値が真であることを確認
・toEqual() オブジェクトインスタンスの全てのプロパティが正しいかどうか
・toContain() 値が含まれているかどうか
など他にもたくさんある。詳しくは公式のExpect のMatchers 参照。




