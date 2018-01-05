# ctags for JavaScript

```
/
|
|-- ctags_for_javascript/
|   |-- .ctags
```

<a href="https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Regular_Expressions">正規表現 - JavaScript | MDN</a>

## .ctags
```:l1,l2
--langdef=js
--langmap=js:.js
```

```:l3
--regex-js=/(,|(;|^|=)[ \t]*(var|let|([A-Za-z_$][A-Za-z0-9_$.]+\.)*))[ \t]*([A-Za-z0-9_$]+)[ \t]*=[ \t]*\{/\5/,object/
```

```:l3'
/
    (
        ,
        |
        (;|^|=)
        [ \t]*
        (
            var
            |
            let
            |
            ([A-Za-z_$][A-Za-z0-9_$.]+\.)*
        )
    )
    [ \t]*
    ([A-Za-z0-9_$]+)            <--(1)５番目であるこの中身がタグとして認識される。つまり、検索結果に上がるものはここのタグが同じ奴
    [ \t]*
    =
    [ \t]*
    \{
/
\5                              <--(1)
/
    ,object
/
```

```:l3'
(;|^|=)：
    js文の終わりを表す';'、文の先頭を表す'^'、イコールを表す'='のいずれかの次に
[ \t]*：
    スペース' 'またはタブ'\t'を任意個、挟むかもしれないし挟まないかもしれないが、
(var|let|([A-Za-z_$][A-Za-z0-9_$.]+\.)*)：
    'var', 'let', のいずれか、または'[A-Za-z_$][A-Za-z0-9_$.]+\.'（これはプロパティの定義をチェックしている。）が含まれている。
[ \t]*
([A-Za-z0-9_$]+)
[ \t]*
=：
    イコールが含まれている。
[ \t]*
/(,| ... \{/
\5：
    それぞれ「(」と「) で囲まれた部分に先行してマッチした5番目の文字列と同じ文字列パターンにマッチする。この機能は理論的には、言うならば非正規で（正規言語の記述力を超える）、POSIX拡張正規表現では採用されていない。(ref:wiki)
/,object/：
```

イコール'='を入れた理由は以下のようなソースコードが書かれていたか（THREEx.ArToolkitSourceを検索したかったが、イコール'='を入れなければタグ認識されなかった。
```js
ARjs.Source = THREEx.ArToolkitSource = function(parameters){	
	var _this = this
```



```l4
--regex-js=/(,|(;|^|=)[ \t]*(var|let|([A-Za-z_$][A-Za-z0-9_$.]+\.)*))[ \t]*([A-Za-z0-9_$]+)[ \t]*=[ \t]*function[ \t]*\(/\5/,function/
```


```
--regex-js=/(,|(;|^|=)[ \t]*(var|let|([A-Za-z_$][A-Za-z0-9_$.]+\.)*))[ \t]*([A-Za-z0-9_$]+)[ \t]*=[ \t]*\[/\5/,array/
--regex-js=/(,|(;|^|=)[ \t]*(var|let|([A-Za-z_$][A-Za-z0-9_$.]+\.)*))[ \t]*([A-Za-z0-9_$]+)[ \t]*=[ \t]*[^"]'[^']*/\5/,string/
--regex-js=/(,|(;|^|=)[ \t]*(var|let|([A-Za-z_$][A-Za-z0-9_$.]+\.)*))[ \t]*([A-Za-z0-9_$]+)[ \t]*=[ \t]*(true|false)/\5/,boolean/
--regex-js=/(,|(;|^|=)[ \t]*(var|let|([A-Za-z_$][A-Za-z0-9_$.]+\.)*))[ \t]*([A-Za-z0-9_$]+)[ \t]*=[ \t]*[0-9]+/\5/,number/
--regex-js=/(,|(;|^|=)[ \t]*(var|let|([A-Za-z_$][A-Za-z0-9_$.]+\.)*))[ \t]*([A-Za-z0-9_$]+)[ \t]*=[ \t]*.+([,;=]|$)/\5/,variable/
--regex-js=/(,|(;|^|=)[ \t]*(var|let|([A-Za-z_$][A-Za-z0-9_$.]+\.)*))[ \t]*([A-Za-z0-9_$]+)[ \t]*[ \t]*([,;]|$)/\5/,variable/
--regex-js=/function[ \t]+([A-Za-z0-9_$]+)[ \t]*\([^)]*\)/\1/,function/

--regex-js=/(,|^|=)[ \t]*([A-Za-z_$][A-Za-z0-9_$]+)[ \t]*:[ \t]*\{/\2/,object/
--regex-js=/(,|^|=)[ \t]*([A-Za-z_$][A-Za-z0-9_$]+)[ \t]*:[ \t]*function[ \t]*\(/\2/,function/
--regex-js=/(,|^|=)[ \t]*([A-Za-z_$][A-Za-z0-9_$]+)[ \t]*:[ \t]*\[/\2/,array/
--regex-js=/(,|^|=)[ \t]*([A-Za-z_$][A-Za-z0-9_$]+)[ \t]*:[ \t]*[^"]'[^']*/\2/,string/
--regex-js=/(,|^|=)[ \t]*([A-Za-z_$][A-Za-z0-9_$]+)[ \t]*:[ \t]*(true|false)/\2/,boolean/
--regex-js=/(,|^|=)[ \t]*([A-Za-z_$][A-Za-z0-9_$]+)[ \t]*:[ \t]*[0-9]+/\2/,number/
--regex-js=/(,|^|=)[ \t]*([A-Za-z_$][A-Za-z0-9_$]+)[ \t]*:[ \t]*[^=]+([,;]|$)/\2/,variable/
```

