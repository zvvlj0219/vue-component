<template>
  <div>
    <slot name="hello"></slot>
  </div>
</template>

<!-- v-slot（名前付きスロット）の使い方-->

<!-- 
①以下を親コンポーネントに追記
- コンポーネント名は任意に指定できる VslotComponentのところ
- v-slotのプロパティに任意のスロット名をわたす helloのところ
- v-slot を使うときは絶対templateタグを使う 
- v-slot を書くところはtemplateタグであってコンポーネントタグではない

<VslotComponent >
  <template v-slot:hello>
    <p>HelloWorld</p>
  </template>
</VslotComponent>

-->
<!--
②VslotComponent内
コンポーネントのテンプレートの中に<slot></slot>を追記
name="hello" をslotタグに追加 

slotのところが親コンポーネント内の子コンポーネントタグ（VslotComponent）内に書いたhtmlに置換される

<template>
  <div>
   <slot name="hello"></slot>
  </div>
</template>

-->