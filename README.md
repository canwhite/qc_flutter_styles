# qc_flutter_styles
styles


## style

```

----------------------------------------------------------
1）widget
顶层当然就是Widget，Flutter中一切都是
它是一个容器概念



我们常见的一个组件：

class UILayout extends StatelessWidget {
  //首先这部分是一定要重写的  
  @override
  Widget build(BuildContext context) {
    //todo  
    return return Scaffold()
  }
}  

--当然还有StatefulWidget


----------------------------------------------------------
2）html
除了最最外层有个root容器，MaterialApp，我们常见的html就是scaffold


class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      //直接在这里定义路由表
      routes: {
        //key和value
        "ListPage": (context) => ListPage(),
        "UIWg": (context) => UIWg(),
        "UILayout": (context) => UILayout(),
        "UIAnimation": (context) => UIAnimation(),
        "DetailPage": (context) => DetailPage(), //增加详情页的路由配置
      },
      home: MyHomePage(),
    );
  }
}

-scaffold 类似于html，可以当作html理解
return  scaffold(
    appBar: AppBar(
        title: const Text("List Page"),
    ),
    /** Row Column Center */
    body: Column()
)

----------------------------------------------------------
3）layout: row和column


首先row和column只接收children
Column(
  children: [
    // 子组件
    Text('Child 1'),
    Text('Child 2'),
    Text('Child 3'),
  ],
)

Row(
  children: [
    // 子组件
    Text('Child 1'),
    Text('Child 2'),
    Text('Child 3'),
  ],
)

另外还有listView和GridView也是只能加children，这个后续再讲

----------------------------------------------------------
4）flex和fixed

这两个和上边一样，不过一般出现在它们内部，主要是
一个是flex弹性布局
一个是fixed相对定位

/**
    * Flex/Expanded
    * 弹性布局
    */
Flex(
    direction: Axis.horizontal,
    children: <Widget>[
    Container(
        width: 30,
        height: 100,
        color: Colors.blue,
    ),
    Expanded(
        flex: 1,
        child: Container(
        height: 100.0,
        color: Colors.red,
        ),
    ),
    Expanded(
        flex: 1,
        child: Container(
        height: 100.0,
        color: Colors.green,
        ),
    ),
    ],
),

/**
* 相对定位
* Stack: 支持元素堆叠
* Positioned：支持绝对定位
*/
    
Stack(
    children: <Widget>[
        Image(
            //注意image对应value是 NetworkImage
            image: NetworkImage(
                "https://mat1.gtimg.com/pingjs/ext2020/qqindex2018/dist/img/qq_logo_2x.png"),
            width: 200.0,
        ),
        Positioned(
            top: 20,
            right: 10,
            child: Image(
                //注意Image对应value是AssetImage
                image: AssetImage("web/icons/Icon-192.png"),
                height: 30,
                width: 200.0)),
    ],
),



----------------------------------------------------------
5）div和padding、margin以及border

Container 类似于html中div，是个逻辑块儿
它是和另外几个一样可以设置border和padding的

Container(
    color: Colors.blue,
    width: 300,
    height: 200,
    decoration: BoxDecoration(
        border: Border.all(color: Colors.black, width: 2.0),
    ),
    margin: EdgeInsets.all(10),
    //从左边开始，顺时针进行
    padding: EdgeInsets.only(left: 10),
    //用Align包着
    child: const Align(
        //Align角定位布局
        alignment: Alignment.bottomRight,
        child: const Text("Hello Align ",
            style: TextStyle(fontSize: 20, color: Colors.white)),
    )),
这里有个区分，几乎所有的组件都支持padding和margin
但是支持border的主要是以下几个小的组件：Container、Card、TextField、Button 、Image
Container：Container 组件可以通过设置 decoration 属性来添加边框。
Card：Card 组件可以通过设置 shape 属性来添加边框。
TextField：文本输入框组件 TextField 可以通过设置 decoration 属性中的 border 来添加边框。
Button 组件：一些按钮组件，如 ElevatedButton、TextButton、OutlinedButton 等可以通过设置样式来实现边框。
Image：图像组件 Image 也可以通过放置在带有边框的容器中来实现边框效果。

----------------------------------------------------------
6）两种List
ListView(
  children: [
    // 子组件
    ListTile(title: Text('Item 1')),
    ListTile(title: Text('Item 2')),
    ListTile(title: Text('Item 3')),
  ],
)


GridView.count(
  crossAxisCount: 2, // 每行显示的列数
  children: [
    // 子组件
    Container(color: Colors.red),
    Container(color: Colors.blue),
    Container(color: Colors.green),
    Container(color: Colors.yellow),
  ],
)

两种list的区别主要就和上边一致了

点击的话是常用GestureDetector包装列表类
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('ListView and GridView Example'),
        ),
        body: ListView.builder(
          itemCount: 10, // 假设有10个列表项
          itemBuilder: (context, index) {
            return GestureDetector(
              onTap: () {
                // 处理点击事件
                print('Item $index tapped');
              },
              child: ListTile(
                title: Text('Item $index'),
              ),
            );
          },
        ),
      ),
    );
  }
}

只需将ListView.builder替换为GridView.builder，并在itemBuilder回调中创建适当的网格项。


----------------------------------------------------------
7）动态添加样式
List<Widget> generateChildren() {
  List<Widget> children = [];

  // 根据条件生成子组件
  if (condition1) {
    children.add(Text('Child 1'));
  }

  if (condition2) {
    children.add(Text('Child 2'));
  }

  // 使用循环生成子组件
  for (int i = 0; i < count; i++) {
    children.add(Text('Child ${i + 3}'));
  }

  return children;
}

// 在组件的 build 方法中使用动态生成的 children
Widget build(BuildContext context) {
  return Column(
    children: generateChildren(),
  );
}





```