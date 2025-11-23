---
layout: post
title: "DOMイベント操作～要素取得編"
date: 2025-11-23
categories: [JavaScript / DOM]  
permalink: /JavaScript-DOM/  
---

# document.getElementsByClassName()  
そのクラス名を持つ要素を取得するために使用  
document.getElementsByClassName('クラス名');  

document.getElementsByClassName('highlight-target');  

# HTML要素.textContent  
HTML要素の中のテキストを取得したり、変更したりするために使う  
textContentはHTMLタグを無視して、テキストだけを取得  
```
<p id="myElement">デフォルトのテキスト</p>
<button id="myButton">クリックするとテキストが変更する！</button>

<script>
 const text = document.getElementById("myElement");
 const button = document.getElementById('myButton');
 button.addEventListener('click', function() {
     text.textContent = '新しいテキスト'; 
 });
</script>
```

# document.getElementsByTagName()  
そのタグ名を持つ要素を取得するために使用  
document.getElementsByTagName(`タグ名`)  

---
---
# ここからページ下部まで、CSSセレクタの書き方で探せる
querySelector / querySelectorAll は“CSS と同じセレクタの書き方” で探すことができる  
CSS と同じ記述方法 → .box, #title, ul li, div > p
実際に探している対象 → HTML の DOM（CSS は一切参照しない）

---
---

# document.querySelector()  
ウェブページの中から特定の要素を一番最初の一つだけ探し出す
例えば、ウェブページの中にあるボタンやテキストボックスなどを探すときなど  
document.querySelector("要素の名前");

# document.querySelectorAll()  
特定の条件に合う要素をすべて取得する  
document.querySelectorAll(`タグ名、クラス名など`);  

# forEach  
配列の各要素に対して順番に処理を行う  
これを使うと、1つ1つの要素に同じ操作を簡単に実行することができる  
配列.forEach(関数)  
```
const names = ['Alice', 'Bob', 'Charlie'];
names.forEach(function(name) {
  console.log(name);
})
```

# parentElement  
特定の要素の親要素を取得  
element.parentElement  
```
<div class="parent">親要素です
  <p class="child">子要素です</p>
</div>

<script>
  document.addEventListener("DOMContentLoaded", function() {
    const parent = document.querySelector('p.child').parentElement;
    parent.style.width = '100px';
    parent.style.height = '100px';
    parent.style.backgroundColor = 'red';
  });
</script>
```

# createElement(tag)  
新しいHTML要素（タグ）を作ることができる  
例えば、createElement('div')と書くと、新しいdiv要素が作られる  

# element.appendChild(element)  
新しい子要素を既存の要素の最後に追加する  
ウェブページに新しい内容を追加したり、既存の内容を変更したりすることができる  

# children  
要素の子要素を取得  
親要素.children  
```
<div class="parent">
  親要素です
  <p class="child">子要素です</p>
  <p class="child">子要素です</p>
</div>

<script>
  const child = document.querySelector('div.parent').children;
  for (let i = 0; i < child.length; i++) {
    child[i].style.color = "red";
  }
</script>
```  

# nextElementSibling  
指定した要素の次にあたる要素を取得  
```
<div id="firstDiv">これは1番目の要素です</div>
<div id="secondDiv">これは2番目の要素です</div>

<script>
const firstDiv = document.getElementById('firstDiv');
const secondDiv = firstDiv.nextElementSibling;

// 2番目の<div>要素を取得し、背景色を変更
secondDiv.style.backgroundColor = "red"; 
</script>  
```  

# previousElementSibling  
指定した要素の前にある要素を取得  
```  
<div id="firstDiv">これは1番目の要素です</div>
<div id="secondDiv">これは2番目の要素です</div>

<script>
const secondDiv = document.getElementById('secondDiv');
const firstDiv = secondDiv.previousElementSibling;

// 1番目の<div>要素を取得し、背景色を変更
firstDiv.style.backgroundColor = "red"; 
</script>
```  
---
練習問題
``` 
// li要素の次のテキストを変更
const list = document.querySelector('.list')👈🏻①
const nextList = list.nextElementSibling

nextList.textContent = '変更'

// p要素の前の文字色を赤色に変更
const paragraph = document.querySelector('.paragraph')👈🏻②
const prevParagraph = paragraph.previousElementSibling

prevParagraph.style.color = '#ff0000'
``` 
①　なぜ getElementsByClassName ではなく、querySelector('.list') を使うのか？  
- querySelector() は CSS と同じ書き方 で要素を1つ取得できる  
-  document.querySelector() は 最初の1つだけ を返す  
   HTMLCollection（複数のセット） を返す  
-  要素の前後を取るときにも相性が良い 
   querySelector は最初から 単体の要素 を返すので使いやすい  

②　(.list) や (.paragraph) の “.ドット”は、CSS セレクタの書き方  
class名を指定する場合は、CSS セレクタのルールで「.」が必須  
querySelector() ではCSS の指定方法をそのまま使う  
```
.xxx → class 名
#xxx → id 名
xxx → タグ名

document.querySelector('list') // ❌ ただの <list> というタグを探す  
document.querySelector('.list') // ✔ listクラスを持つ要素  
```
---

# firstElementChild  
指定された要素の子要素の中で、最初の要素を取得  
親要素.firstElementChild  
```
<ul id="parent">
  <li>これは最初の子要素です。</li>
  <li>これは2番目の子要素です。</li>
</ul>

<script>
const parent = document.getElementById('parent');
const firstChild = parent.firstElementChild;

// 文字色を変更
firstChild.style.color = "red";
</script>
```

# lastElementChild  
指定された要素の子要素の中で、最後の要素を取得  
親要素.lastElementChild  

