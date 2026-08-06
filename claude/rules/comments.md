## コメント

関数の中は「何のための処理か」を書いたコメントと、それに紐づく処理をひと塊にする。塊の間は1行空ける。

```ts
// 本文はfetchへ渡す前にcloneしておく。渡した後では読めなくなる
const requestBody = readBody(request.clone());
const startedAt = Date.now();
const startedTick = performance.now();
const response = original.call(window, request);

void report(request, requestBody, response, startedAt, startedTick);
return response;
```

- コメントは塊の先頭に置き、その下に関係する処理を続けて書く
- 1行ごとにコメントを付けない。説明が要る塊にだけ書く
- 日本語で簡潔に。「なぜ」を優先し、コードを読めば分かるWhatを繰り返さない
- 文末に句点「。」は付けない
