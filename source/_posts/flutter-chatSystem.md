---
title: flutter_chatSystem
date: 2019-07-07 22:20:21
tags:
    -Flutter
---

今天复习了一下Flutter的布局，写了一个聊天的小demo。关于布局这一方面，没有什么可以记录的坑，所以直接贴代码看效果图吧

![](flutter-chatSystem/chatListPage.gif)

main.dart:
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
     final titleStyle = TextStyle(color: Colors.black,fontWeight: FontWeight.bold,fontSize: 18.0);
     @override
     Widget build(BuildContext context) {
       return ListView(
             children: <Widget>[
               chatItem("image/avatar.ico", title, "你在哪呢，你妈喊你回家吃饭了", "十分钟前")
             ],
           );
     }
     Widget chatItem(String avatar , String title,String content,String time){
       return GestureDetector(
                 child: Container(
                   margin: const EdgeInsets.all(5),
                   decoration: BoxDecoration(
                     // border: Border.all(color: Colors.black,width: 2)
                   ),
                   child: Row(
                   children: <Widget>[
                     Image.asset(avatar,width: 50,height: 50,),
                     Container(
                         margin: const EdgeInsets.fromLTRB(15, 5, 5, 5),
                         child: Column(
                           crossAxisAlignment: CrossAxisAlignment.start,
                           children: <Widget>[
                             Text(title,style: titleStyle,),
                             Text(content),
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
                           child: Text(time),
                         ),
                       )
                     ],
                   ),
                 ),
                 onTap: (){
                   Navigator.push(
                     context, MaterialPageRoute(
                       builder: (BuildContext context){
                         return ChatPage(title);
                       }
                     )
                   );
                 },
               );
     }
   }
   
   // class MessageData{
   //   String avatar;
   //   String title;
   //   String chatContent;
   //   String time;
   //   MessageData(this.avatar,this.title,this.chatContent,this.time);
   // }
   
   // class Message extends StatefulWidget {
   //   @override
   //   _MessageState createState() => _MessageState();
   // }
   
   // class _MessageState extends State<Message> {
   //   @override
   //   Widget build(BuildContext context) {
   //     return Container(
         
   //     );
   //   }
   // }
   
   // List MessageItem = [
   //   MessageData("dsad","dsad","dsadas","dsad")
   // ]; 
~~~

<!-- more -->
chatPage.dart:
~~~
    import 'package:flutter/material.dart';
    
    class ChatPage extends StatefulWidget {
      final String title;
      ChatPage(this.title);
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
              Text("大家好")
            ],
          ),
        );
      }
    }
~~~

未完待续。。。。
