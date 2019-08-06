---
title: flutter_chat_system
date: 2019-08-06 20:56:38
tags:
    -Flutter
---

因为最近在从事FLutter的工作，所以还是有必要去做一些相关笔记的，FLutter的生态有待完善，尤其是集成第三方SDK，目前大多数第三方包都是没有给flutter提供
直接import集成方法的，但是好在flutter可以使用MethodChannel等方法来与底层进行通信，有助于我们更好的去集成，但是在此之前，你需要对flutter的dart和安卓的java有一定的了解，
不然就只能像我这样，黑夜中抓瞎。不多说了，写个聊天的小demo，目前只是实现基础的布局，可以先看一下效果。
![](flutter-chatSystem/chatListPage.gif)
关于布局，其实没什么可以说的了，这是最基本的布局。因为表单这一块还没有思路，并没有展示出来。

整个小demo是分了两个`.dart`文件的。
`main.dart`入口函数
~~~
import 'package:flutter/material.dart';
import 'chatPage.dart';

void main()=> runApp(MyApp());

class MyApp extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text("聊天室"),
          centerTitle: true,

        ),
        body: ChatList()
      ),
    );
  }
}

class ChatList extends StatefulWidget {
  @override
  _ChatListState createState() => _ChatListState();
}

class _ChatListState extends State<ChatList> {
  final title = "花开不败";

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
          itemCount: messageData.length,
          itemBuilder: (BuildContext context , int index){
            return InkWell(
              child: MessageItem(messageData[index]),
              onTap: (){
                print(index);
                Navigator.push(context, MaterialPageRoute(builder: (context) => ChatPage()));
              },
            );
          },
        );
  }
}
 class MessageData{
   String avatar;
   String title;
   String chatContent;
   String time;
   MessageData(this.avatar,this.title,this.chatContent,this.time);
 }
List<MessageData> messageData = [
  MessageData("image/avatar.ico", "花开不败", "哈哈哈，我是你的聊天内容", "17:45")
];
class MessageItem extends StatelessWidget {
  final MessageData message ;
  MessageItem(this.message);
  final titleStyle = TextStyle(color: Colors.black,fontWeight: FontWeight.bold,fontSize: 18.0);
  @override
  Widget build(BuildContext context) {
    return  Container(
      margin: const EdgeInsets.all(5),
      decoration: BoxDecoration(
        // border: Border.all(color: Colors.black,width: 2)
      ),
      child: Row(
        children: <Widget>[
          Image.asset(message.avatar,width: 50,height: 50,),
          Container(
            margin: const EdgeInsets.fromLTRB(15, 5, 5, 5),
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: <Widget>[
                Text(message.title,style: titleStyle,),
                Text(message.chatContent),
              ],
            ),
          ),
          Expanded(
            child: Container(
              margin: const EdgeInsets.fromLTRB(0, 0, 0, 20),
              decoration: BoxDecoration(
                // border: Border.all(color: Colors.red,width: 2.0)
              ),
              alignment: Alignment.topRight,
              child: Text(message.time),
            ),
          )
        ],
      ),
    );
  }
}
~~~

需要注意的是，关于列表这一块，不要盲目的去写，首先你应该知道，列表的数据一般都是服务端以一个对象的形式提供，对象内每一个数组都对应着每一个列表项，
`flutter`也为我们提供了一个ListView.builder的构造方法，让我们去遍历每一个数组的数据，然后生成列表。因为我用的是假数据，如果在真实项目中，大家可以直接拿到对象，并赋值一个新的数组，
定义好与后台对应字段信息的变量，直接传参到封装好的布局组件内就可以了。

然后是关于聊天消息的页面，我这边不确定第三方即时通讯SDK能够给我什么参数，假设了一下聊天消息，和user识别，以及对应user的头像。上一下代码。
~~~
import 'package:flutter/material.dart';

class ChatPage extends StatefulWidget {
  @override
  _ChatPageState createState() => _ChatPageState();
}

class _ChatPageState extends State<ChatPage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("花开不败"),
        centerTitle: true,
        leading: IconButton(
          icon: Icon(Icons.arrow_left),
          onPressed: (){
            Navigator.pop(context);
          },
        ),
      ),
      body: ListView(
        children: <Widget>[
          ListView(
            shrinkWrap: true,
            physics: new NeverScrollableScrollPhysics(),
            children: <Widget>[
              chatMessageItem("image/avatar.ico","hai，你好啊",0),
              chatMessageItem("image/demo2.jpg","嗯嗯，你好呀",1),
              chatMessageItem("image/avatar.ico","嗯嗯，你好呀",0),
              chatMessageItem("image/demo2.jpg","嗯嗯，你好呀",1),
              chatMessageItem("image/avatar.ico","嗯嗯，你好呀",0),
              chatMessageItem("image/demo2.jpg","嗯嗯，你好呀",1),
              chatMessageItem("image/avatar.ico","嗯嗯，你好呀",0),
              chatMessageItem("image/demo2.jpg","咱也不敢说咱也不敢问咱也不敢说咱也不敢问咱也不敢说咱也不敢问咱也不敢说咱也不敢问",1),
              chatMessageItem("image/avatar.ico","嗯嗯，你好呀",0),
              chatMessageItem("image/demo2.jpg","咱也不敢说咱也不敢问咱也不敢说咱也不敢问咱也不敢说咱也不敢问咱也不敢说咱也不敢问",1),
                //这里不知道服务端能给我提供什么数组，所以只能自己伪造一些。
            ],
          )
        ],
      ),
    );
  }

  Widget chatMessageItem(String avatar , String message , int user){
    return Container(
      margin: EdgeInsets.symmetric(horizontal: 10,vertical:10),
      child:Row(
        mainAxisAlignment: user == 0 ? MainAxisAlignment.start: MainAxisAlignment.end,
        children: <Widget>[
          Container(
              child:user == 0 ?  CircleAvatar(
                backgroundImage: AssetImage(user == 0 ? avatar : ""),
              ):null

          ),
          Container(
              margin: EdgeInsets.only(left: 10,right: 10),
              width: MediaQuery.of(context).size.width/2,
              decoration: BoxDecoration(
                color: Colors.yellow,
                borderRadius: BorderRadius.only(
                    topLeft: Radius.circular(user == 0 ? 15 : 5),
                    topRight: Radius.circular(user == 1 ? 15 : 5),
                    bottomLeft: Radius.circular(5),
                    bottomRight: Radius.circular(5)
                ),
              ),
              child: Padding(
                child: Text(message,style: TextStyle(color: Colors.black,fontSize: 15),softWrap: true,maxLines: 50,),
                padding: EdgeInsets.symmetric(horizontal: 10,vertical: 10),
              )
          ),
          Container(
            child:user == 1 ?  CircleAvatar(
              backgroundImage: AssetImage(user == 1 ? avatar : ""),
            ):null
          )
        ],
      ),
    );
  }
}
~~~
聊天消息 这一块布局也是没有什么大问题，问题都在后面的表单提交重新Build view层，以及第三方SDK的集成。

未完待续~~~~~~~~
