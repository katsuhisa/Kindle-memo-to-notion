# Kindle-memo-to-notion
Kindleでハイライトした箇所を箇条書きで抽出し、Notionに移行してメモをknowledgeとして整理しやすくする。

# Kindle Highlights to Markdown with Enhancements

[azuのkindle-highlight-to-markdown](https://github.com/azu/kindle-highlight-to-markdown)に基づき、KindleのハイライトとメモをMarkdownまたはJSON形式に変換するための改良版です。
オリジナルのライブラリではページ番号も取得されますが、この改良版ではページ番号を取得せず、Markdown形式での箇条書き表示に特化しています。

## 改良点

このバージョンでは、次の改良を行っています：

- Kindleのページ番号をMarkdown出力から除外します。
- Markdown形式のテキストを箇条書きに変換し、より読みやすく整理されたフォーマットを提供します。

## 使用方法

1. Kindleの[メモとハイライト](https://read.amazon.co.jp/notebook)ページを開きます。
   1.1 ページの任意の場所を右クリック
   1.2 検証をクリック
   <img width="540" alt="スクリーンショット 2024-03-14 23 05 39" src="https://github.com/katsuhisa/Kindle-memo-to-notion/assets/86588377/73e425de-83ca-43fd-836f-33b3cd6751e4">
3. ブラウザの開発者ツールの"Consle"を開きます。
    <img width="540" alt="スクリーンショット 2024-03-14 23 06 14" src="https://github.com/katsuhisa/Kindle-memo-to-notion/assets/86588377/37b25a2c-547b-4f20-b7f2-262403924f99">

    - Firefox: [ウェブコンソール - 開発ツール | MDN](https://developer.mozilla.org/ja/docs/Tools/Web_Console)
    - Chrome: [Console overview - Chrome Developers](https://developer.chrome.com/docs/devtools/console/)
4. 次のコードをConsoleに貼り付けて実行します：

```javascript
const { parsePage, toMarkdown } = await import('https://cdn.skypack.dev/kindle-highlight-to-markdown');
const result = parsePage(window); // JSONオブジェクト
const markdown = toMarkdown(result); // Markdown形式の文字列

// Markdownからページ番号を含む行を削除し、箇条書きに変換
const lines = markdown.split('\n');
const bulletListMarkdown = lines.reduce((acc, line) => {
  if (line.startsWith('> Location:')) {
    return acc;
  }
  if (line.trim() === '>') {
    acc.push('');
  } else {
    const item = line.replace(/^> /, '- ');
    acc.push(item);
  }
  return acc;
}, []).join('\n');

copy(bulletListMarkdown);
```
## 参照元
このプロジェクトは、azuによるkindle-highlight-to-markdownを基にしています。特定の改良を加えることで、ユーザーにより使いやすい形で情報を提供できるようにしています。

## ライセンス
この改良版コードは、オリジナルのライブラリに準じたライセンスのもとで提供されます。詳細については、オリジナルのリポジトリを参照してください。

このテンプレートは、改良した機能の説明、使用方法、そしてオリジナルのプロジェクトへのリンクと敬意を示しています。また、Markdown形式の特性を活かし、リンクやコードブロックを適切に使用しています。あなたのGitHubページにこの内容を追加することで、他のユーザーが利用しやすいガイドを提供できます。
