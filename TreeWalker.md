# Javascript�����̳�<sup>shine</sup>

## DOM �� TreeWalker ��������

TreeWalker������DOM2���ṩ��һ��ǿ��Ĺ��ߣ��������������ĵ��еĽڵ㣬�Ա��ڲ����Զ���Ľڵ㼯�ϡ���������û��ʲô̫����ô��������������Ҫ�����������DOM������������ʱ���˽�һ��TreeWalker���������ܴ�İ�����������Ѿ�����Ϥ�����Webҳ���в��Ҿ���ĳ��CSS��ʽ���ƵĽڵ㼯�ϣ������XML�ļ��в���ĳ������Ϊ�ض�ֵ�Ľű�д��������TreeWalker�����������Ĺ���Ҳ����������ƹ��ܡ��ڱ����У��ҽ��������TreeWalker������Ҫע����ǣ�TreeWalker�����Ѿ���Firefox/Opera8+��֧�֣�����IE6��IE7�в�֧�֡���ע��Chrome��Safari��Щ����WebKit�ں˵������Ҳ֧��TreeWalker����IE9+Ҳ�Ѿ�֧�֣�

���⣬��TreeWalker��ϵ���ܵ�����һ������NodeIterator��Ҳ���ڱ��ĵ��к��ǡ�TreeWalker��NodeIterator�������档

### document.createTreeWalker()����

����ĳЩ����˵��TreeWalker���������е�����ز��Һܸ��ӡ�ʵ���ϣ�Ҫ��ʹ��TreeWalker����ֻ��һ��������document.createTreeWalker()���˷�����4��������������ɴ󲿷ֵĳ��������������ĵ��в���ĳ�����ͻ��߾���ĳ�����ԵĽڵ㡣���ڴ˷����򵥽������£�
```javascript
    document.createTreeWalker(root, nodesToShow, filter, entityExpandBol);
```

���˽�һ����4��������

    root���ĵ�����������ʼ�ڵ�
    nodesToShow��TreeWalker����Ҫ���ʵĽڵ�����
    filter(or null)���������˷��ؽ�����Զ��庯����null��ʾ��ʹ���Զ���Ĺ��˺���
    entityExpandBol������ֵ����ʾ�Ƿ���Ҫ��չʵ������

����NodeFilter����������������Щ����������ϵ�ȡֵ��

- 1��NodeFilter.SHOW_ALL���������нڵ㣻
- 2��NodeFilter.SHOW_ELEMENT������Ԫ�ؽڵ㣻
- 3��NodeFilter.SHOW_ATRRIBUTE���������Խڵ㣻
- 4��NodeFilter.SHOW_TEXT�������ı��ڵ㣻
- 5��NodeFilter.SHOW_ENTITY_REFERENCE������ʵ�����ýڵ㣻
- 6��NodeFilter.SHOW_ENTITY������ʵ��ڵ㣻
- 7��NodeFilter.SHOW_PROCESSING_INSTRUCTION������PI�ڣ�
- 8��NodeFilter.SHOW_COMMENT������ע�ͽڵ㣻
- 9��NodeFilter.SHOW_DOCUMENT�������ĵ��ڵ㣻
- 10��NodeFilter.SHOW_DOCUMENT_TYPE�������ĵ����ͽڵ㣻
- 11��NodeFilter.SHOW_DOCUMENT_FRAGMENT�������ĵ���Ƭ�ڽڣ�
- 12��NodeFilter.SHOW_NOTATION�������ǺŽڵ㣻

��Ȼ����˶�ĳ���������������TreeWalker���صĽڵ㣬������ʵ��Ӧ���У����ܳ��õ�Ҳ�������е���������������

�����ȴ�һ���������ʾ����ʼ��

```html
    <div id="contentarea">
        <p>Some <span>text</span></p>
        <b>Bold text</b>
    </div>
```
```javascript
    var rootnode = document.getElementById("contentarea");
    var walker = document.createTreeWalker(rootnode, NodeFilter.SHOW_ELEMENT, null, false);
```
�����ʾ���У�createTreeWalker������root����ΪID��contentarea��Ԫ�أ���TreeWalker����������ڵ�Ϊ����ʼ���б������ڶ�����������TreeWalkerֻ�������ڵ��µġ�Ԫ�ء��ڵ㣨��������ı��ڵ��ע�ͽڵ㣩����������������Ϊnull��ʾ����Ҫ�����Զ���Ĺ����������ĸ���������������ʵ�������Ƿ�չ����������������Ϊfalse����δ���ִ�����֮��walker����ָ���˰���DIV�Լ����ڵ��Լ�DIV�µ�������Ԫ�ؽڵ㣨P, SPAN, B����
TreeWalker�ı�������

ʹ��document.createTreeWalker()���������˹��˺�Ľڵ��б�Ȼ�����ʹ��TreeWalker�ı�����������Щ�ڵ���б�����

|����|����|
|:------|:------|
|firstChild() 	|���ص�ǰ�ڵ�ĵ�һ���ӽڵ�|
|lastChild() 	|���ص�ǰ�ڵ�����һ���ӽڵ�|
|nextNode() 	|���ع��˺�Ľڵ��б��е���һ���ڵ�|
|nextSibling() 	|���ص�ǰ�ڵ����һ���ֵܽڵ�|
|parentNode() 	|���ص�ǰ�ڵ�ĸ��ڵ�|
|previousNode() 	|���ع��˺�Ľڵ��б��е���һ���ڵ�|
|previousSibling() 	|���ص�ǰ�ڵ����һ���ֵܽڵ�|

currentNode:����TreeWalker����ĵ�ǰλ�û��ߵ�ǰ�ڵ㡣����һ���ɶ�/д���ԣ�����ͨ�����ô����ԣ���TreeWalkerָ��ĳ���ض��Ľڵ㡣

��Ҫ����������Щ���������Ժͱ�׼DOMԪ�صķ��������Ի��������ϵķ���ֻ����TreeWalker�����У���ʵ�ֱ������˺�Ľڵ㼯�ϵ�������

����ʹ�������ʾ�����룬��Σ����Ǽ���һЩ����������TreeWalker���صĽڵ��б�
```javascript
    //������Ĵ���
    alert(walker.currentNode.tagName); //alerts DIV (with id=contentarea)

    //��������ʾ���е��ӽڵ�
    while (walker.nextNode())
        alert(walker.currentNode.tagName); // P, SPAN, B.

    //����TreeWalker��ָ������ָ����ڵ�
    walker.currentNode = rootnode
    alert(walker.firstChild().tagName); // P
```

����ʹ��TreeWalker�ı�������ʱ��TreeWalker�������η��ع��˺�Ľڵ㣬ͬʱ�����ƶ��˵�ǰָ��ڵ��ָ�룬���ԣ���ʹ��while (walker.nextNode())��ɱ���֮�󣬻�Ҫʹ��walker.currentNode=rootnode�������ĵ�ǰ�ڵ�ָ����ڵ㣬�Ա��ȡ����һ����Ԫ�ء�

����һ��ʾ������һ�¶�TreeWalker��������⣺
```html
    <p id="essay">George<span> loves </span> <b>JavaScript!</b></p>
```
```javascript
    var rootnode = document.getElementById("essay");
    var walker = document.createTreeWalker(rootnode, NodeFilter.SHOW_TEXT, null, false);

    walker.firstChild(); //Walk to first child node (the text "George")
    var paratext = walker.currentNode.nodeValue;

    while (walker.nextSibling()){ //Step through each sibling of "George"
        paratext += walker.currentNode.nodeValue;
    }

    alert(paratext); // "George loves JavaScript!"
```

�����ʾ���У����Ǳ����˸��ڵ������е��ı��ڵ��Ի�ȡ���������ı��ַ�����

�ڱ���TreeWalker�ķ��ؽ��ʱ����Ҳ����ʹ�ñ�׼DOMԪ�ص����Ժͷ�������ΪTreeWalker�ķ���ֵ�����������˹��˺�Ľڵ㣬��������Щ�ڵ��������ĵ��еĹ�ϵ�������������ʾ����

```html
    <ul id="mylist">
        <li>List 1</li>
        <li>List 2</li>
        <li>List 3</li>
    </ul>
```
```javascript
    var rootnode = document.getElementById("mylist");
    var walker = document.createTreeWalker(rootnode, NodeFilter.SHOW_ELEMENT, null, false);

    alert(walker.currentNode.childNodes.length); //alerts 7 (includes text nodes)
    alert(walker.currentNode.getElementsByTagName("*").length); //alerts 3
```

���ʾ���У�ʹ��TreeWalker����UL�ڵ��µ�����Ԫ�ء�����ܻ�����Ϊalert(walker.currentNode.childNodes.length)�᷵��3����ΪULֻ��3��LI��Ԫ�ء�����ʵ���ϼ������ı��ڵ�Ļ���ULԪ�ؾͰ���7����Ԫ���ˣ������Ϊʲô����Ĵ���᷵��7��

�˽�����α���TreeWalker�ķ��ؽڵ��б�֮�����潫��������Զ�������������ǵ�document.createTreeWalker()�����ĵ��������������ǽ��������ָ��һ���Զ���ĺ���������Զ���������Ĺ��ܡ�
��document.createTreeWalker()��ʹ�ù�����

TreeWalker����ı������ṩһ�����ĵ��й��˽ڵ����������ǰ��������У������Ѿ������˿���ʹ��NodeFilter�ĸ��ֳ���������NodeFilter.SHOW_ELEMENT�������������Ĺ��˹��ܡ�������ʵ�ʵĳ����У���Щ�������ܻ�������֧�������������������Ҫ�õ�document.createTreeWalker()�����ĵ�������������������������Զ���һ�����˺���������Զ���Ĺ��ˣ�Ҳ����˵�����ڵڶ���������ָ���ĳ��������Ľ���ٴν��й��ˡ�

    document.createTreeWalker(root, nodesToShow, filter, entityExpandBol)

"filter"����ָ��һ�����������磺
```javascript
    function myfilter(node){
        if (node.tagName == "DIV" || node.tagName == "IMG") //ֻ����DIV��IMGԪ��
            return NodeFilter.FILTER_ACCEPT;
        else
            return NodeFilter.FILTER_SKIP;
    }
    var walker = document.createTreeWalker(document.body, NodeFilter.SHOW_ELEMENT, myfilter, false);
    while (walker.nextNode())
        walker.currentNode.style.display = "none"; //����ҳ�������е�DIV��IMGԪ��
```
�������ʾ�������У����Ƕ�����һ������myfilter�ĺ��������������������DIV��IMGԪ�أ�����������Ԫ���ų����⡣��Ϊ�������ĺ���ֻ����һ������������TreeWalker�ڱ��������ĵ�ʱ��ǰ��ָ��Ľڵ㡣�ڹ����������У������ʹ�ò�ͬ�ķ���ֵ��ʵ�ֽ��ܡ��ܾ�����������ǰ�Ľڵ㣺

    NodeFilter.FILTER_ACCEPT
    NodeFilter.FILTER_REJECT
    NodeFilter.FILTER_SKIP

����������FILTER_ACCEPT���Ǳ�ʾ��������ڵ㣬������������صĽ���С�����FILTER_REJECT��FILTER_SKIP�ĺ�����ܻ���Щ����ô�����ˡ�����FILTER_REJECT��TreeWalker���ܾ���ǰ�ڵ��Լ������еĺ���ڵ㣬Ҳ����˵������Ĺ�������������FILTER_REJECT��ʱ��TreeWalker�����ٱ����ýڵ��µ����к���ڵ㡣�������Ҫ�������˵���ǰ�ڵ㣬����Ҳϣ��TreeWalker���������ýڵ��µ����к���ڵ㣬��ô��ʹ��NodeFilter.FILTER_SKIP�������������������У������ FILTER_SKIP ��Ϊ FILTER_REJECT��

```javascript
    function myfilter(node){
        if (node.tagName=="DIV" || node.tagName=="IMG") //filter out DIV and IMG elements
            return NodeFilter.FILTER_ACCEPT;
        else
            return NodeFilter.FILTER_REJECT;
    }
```

�����Ļᵼ�·��صĽ���п��ܲ�û�а����ĵ���ȫ����DIV��IMGԪ�أ���Ϊ���һ��IMGԪ����Ϊһ��PԪ�ص���Ԫ�صĻ�����ô����PԪ�ر�������FILTER_REJECT����ôPԪ���µ�IMGԪ��Ҳ���ᱻTreeWalker������

���ʹ��NodeFilter����

��ǰ��������������Ѿ��˽⵽NodeFilter�ṩ�˺ܶೣ���������ǻ�ȡĳ�����͵Ľڵ㣬��Щ����Ҳ�������ʹ�ã����磺

    OR ������NodeFilter.SHOW_ELEMENT | NodeFilter.SHOW_TEXT
    AND ������NodeFilter.SHOW_TEXT + NodeFilter.SHOW_COMMENT
    NOT ������~NodeFilter.SHOW_COMMENT (��ȡ���еķ�ע�ͽڵ�)

ֻ�������е�Ԫ�ؽڵ���ı��ڵ㣺
```javascript
    document.createTreeWalker(root, NodeFilter.SHOW_ELEMENT | NodeFilter.SHOW_TEXT, null, entityExpandBol);
```
�����DOM2���ṩ��TreeWalker�������ס�����������е��������֧�ִ˶���