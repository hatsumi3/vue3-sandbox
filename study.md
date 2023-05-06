# vue + typescript メモ

## defineprops への default 値設定

typescript を使用して型のみ宣言して使用する場合は defipeProps にてデフォルト値を指定できない。その場合 withDefaults コンパイラーマクロを使用する

- [link 公式](https://ja.vuejs.org/api/sfc-script-setup.html#default-props-values-when-using-type-declaration)

上記以外はそのまま記載できる

```js
type Props = {
  message: string,
};

export default defineComponent({
  props: {
    message: {
      type: String,
      default: "default Value",
    },
  },
  setup(props: Props) {
    props.message; //string型として型推論される
  },
});
```

- [参考](https://qiita.com/ryo2132/items/f055679e9974dbc3f977)

## git commit message

semantic commit message が無難？

- [公式](https://gist.github.com/joshbuchea/6f47e86d2510bce28f8e7f42ae84c716)
- [emoji,Issue Number 付き](https://zenn.dev/itosho/articles/git-commit-message-2023#%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%83%E3%83%88)
