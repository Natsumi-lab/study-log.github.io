---
layout: post
title: "DOMイベント操作～eventListener編"
date: 2025-11-23
categories: [JavaScript / DOM]  
permalink: /JavaScript-DOM/  
---

# document.addEventListener()  
ウェブページ上の特定の要素に対して何か特定の事象（イベント）が起こったときに、
何か特定の動作（関数）を行うように指示する  
対象要素.addEventListener( 種類, 関数, false )  

# clickイベント  
clickイベントを使用すると、ユーザーがボタンをクリックしたときの処理を登録する　

```  
<script>
  const button = document.getElementById('demo-button');
  button.addEventListener('click', () => {  
    // ここにクリックしたときに行う処理を書く  
});  
</script>  
```  

# mouseoverイベント  
マウスを要素の上に置いたときに発生するイベント  　
ボタンの色を変えたり、情報を表示したりすることができる  

```  
<script>
const button = document.getElementById('demo-button');
button.addEventListener('mouseover', function() {
  // ここにマウスオーバー時に行いたい処理を書く
});
</script>  
```  

# DOMContentLoaded
ウェブページが読み込まれた後に発生するイベント  
```  
<script>
 document.addEventListener("DOMContentLoaded", function() {
    // ここにウェブページが読み込まれた後に実行したいコードを書く
  const title = document.getElementById('demo');
......
  });
</script>  
```  

# 無名関数（匿名関数）  
```  
通常の関数には名前がある 
function 名前(){
  //処理 
}
``` 

``` 
無名関数の場合は、名前の通り名前がない   
function () {  
  //処理 
}
```  
名前がないので そのままでは使えません  
だから　　
``` 
🟢変数に代入する
const greet = function() {
  console.log("こんにちは");
};

greet(); // 実行される

無名関数を変数に入れることで
「その変数名で関数を呼べる」ようになる。
``` 

``` 
🟢イベント処理  
button.addEventListener("click", function() {
  console.log("クリックされました！");
});
ここで addEventListener に渡している関数は 名前がない
``` 

``` 
🟢アロー関数
button.addEventListener("click", () => {
  console.log("クリック！");
});
``` 
## 無名関数を使う理由
- 一回きりの関数に 名前をつける必要がない  
- 変数に入れて後から呼びたい場合に便利(例：const add = (a, b) => a + b;)  
- 関数式として扱える(関数を値として扱えるのが JavaScript の特徴)  

# this 　
function と アロー関数で this が変わる　　
| 書き方                  | this は何？                       |
| -------------------- | ------------------------------ |
| **function() { … }** | イベントが起きた要素（クリックされた要素）          |
| **() => { … }**      | 外側の this をそのまま使う（イベント要素にはならない） |

function の中の this → その要素の情報やプロパティにアクセスできる  
クリックされた要素を this で使いたいとき　

アロー関数の中の this → 要素ではなく外側に束縛された this  
this を使う必要がないとき  

# changeイベント  
フォーム要素（テキストボックスやセレクトボックスなど）の値を変更して、その要素からフォーカスが外れたときに発生  
``` 
<input type="text" id="myTextbox">

<script>
const textbox = document.getElementById('demoTextbox');
// ここに値を変更した後の処理を書く
textbox.addEventListener('change', function() {
  alert('テキストを変更しました : ' + this.value);
});
</script>
```

# checked  
チェックボックスやラジオボタンが選択されているかどうかを調べたり、選択状態を変更したりする  
checkedの値がtrueなら選択されている、falseなら選択されていない

# submitイベント  
``` 
フォームが送信されたときに発生  
document.getElementById("demo").addEventListener("submit", function(){
     // ここに、フォームが送信されたときに行いたい動作を書く  
```  

# value  
ユーザーが入力したテキストを取得したりテキストボックスの値を変更するときに使う  
使い方　
- 入力された文字を取得する  
const text = document.getElementById("input").value;  
console.log(text);  

- 入力欄に文字をセットする  
document.getElementById("input").value = "初期値です";  

- ボタンをクリックしたら入力内容を表示する  
button.addEventListener("click", () => {  
  const v = input.value;  
  console.log(v);  
});  

# e.preventDefault()  
ブラウザが元々持っている特定のイベントの動作を止めるための命令  
eはイベント  
preventDefault()はそのイベントのデフォルトの動作を止める  
```
 // リンクをクリックしても新しいページに移動しないようにする  
document.querySelector('a').addEventListener('click', function(e) {
  e.preventDefault();
});
```  

# HTMLFormElement.reset()  
フォームの入力フィールドを初期状態に戻す  
フォーム要素.reset();  

# disabled  
フォーム要素（ボタンやテキストボックスなど）を無効化する  
例えばボタンがクリックできなくなる、入力欄に文字を打てなくなる、選択できなくなる等  
disabled = true → 無効  
disabled = false → 有効  

# mouseoverイベント  
マウスを要素の上に置いたときに発生するイベント  
element.addEventListener('mouseover', function() {
  // ここにマウスオーバー時に行いたい処理を書く
});

# mouseoutイベント  
マウスカーソルが特定の要素から離れたときに発生  
element.addEventListener('mouseout', function() {  
  // ここに、マウスが要素から離れたときに行う処理を書く  
});  

# document.removeEventListener()  
特定のイベントを削除する  

# scrollイベント  
ユーザーがページをスクロールしたときに発生  
document.addEventListener('scroll', function() {
  // ここにスクロールしたときに行う処理を書く

# scroll  
ウェブページ上でのスクロール位置を取得したり、特定の位置にスクロールするために使われる  
- window.scrollXは、ウェブページの左端から現在の水平（横）スクロール位置までの距離をピクセルで取得する
- window.scrollYは、ウェブページの上端から現在の垂直（縦）スクロール位置までの距離をピクセルで取得する
- window.scrollToは、指定した水平（横）と垂直（縦）の位置にウェブページをスクロールする
```
// 現在の水平（横）スクロール位置をピクセルで表示
console.log('水平スクロール位置: ' + window.scrollX + 'px'); 

// 現在の垂直（縦）スクロール位置をピクセルで表示  
console.log(window.scrollY); 

// ページの一番上にスクロール
window.scrollTo(0, 0); 

// ページの垂直（縦）位置500pxにスクロール
window.scrollTo(0, 500); 
```