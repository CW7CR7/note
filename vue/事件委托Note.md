

```html
<html xmlns="http://www.w3.org/1999/xhtml">

<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>当前点击要素样式</title>

    <style type="text/css">
        body,
        #map {
            border: 0px;
            margin: 0px;
            padding: 0px;
            width: 100%;
            height: 100%;
            font-size: 13px;
        }

        #testUl {
            list-style: none;
        }

        #testUl li {
            float: left;
            padding: 10px;
            background: gray;
            margin: 1px;
        }

        #testUl li:hover {
            cursor: pointer;
        }

        .currentShow {
            color: red;
            border-bottom: 1px solid red;
            background: orange !important;
        }
    </style>

</head>

<body>
    <div id="map">
        <ul id='testUl'>
            <li>1</li>
            <li>2</li>
            <li>3</li>
        </ul>
        <button onclick="addLi()">添加Li</button>
    </div>
    <script src="./js/jquery.min.js"></script>
    <script type="text/javascript">
        document.getElementById('testUl').addEventListener('click', function (e) {
            var e = e || window.event
            let target = e.target;
            // console.log(target);
            let nodeName = target.nodeName.toLowerCase();
            // console.log(nodeName);
            if (nodeName == 'li') {
                target.classList.add('currentShow');
                let brotherNodes = siblings(target);
                brotherNodes.forEach(function (node) {
                    let isExist = node.classList['value'].indexOf('currentShow') > -1;
                    if (isExist) {
                        node.classList.remove('currentShow');
                    }
                })
            }
            function siblings(elm) {
                var a = [];
                var p = elm.parentNode.children;
                for (let i of p) {
                    if (p[i] !== elm) a.push(p[i]);
                }
                // 返回所有的兄弟节点
                return a;
            }
        }, false)
        function addLi() {
            $('#testUl').append('<li></li>')
        }
    </script>
</body>

</html>
```

