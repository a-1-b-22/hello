## 一、mqtt topic 格式
   app/[companyID]/rooms/[roomID]/event/[tx|rx]
   
   companyID: 公司ID
   rootmID：房间ID
   tx：unite主机接收到房间内设备发送的消息时，向该主题发布消息，服务器可订阅该主题，接收该房间内的所有设备的消息。
   rx：unite主机会订阅该主题，若服务器向该主题发布消息，unite主机会收到消息，并处理消息

## 二、服务器发布的消息类型（mqtt消息内容的类型）
    服务器向app/[companyID]/rooms/[roomID]/event/rx发布的消息，unite主机接收并处理

## 三、unite主机发布的消息类型（mqtt消息内容的类型）
    unite主机向app/[companyID]/rooms/[roomID]/event/tx发布的消息，服务器接收并处理
    
###1. 主机相关消息
####1.1 unite主机online消息, 设备连接到mqtt server时发送online消息
```    
{
    "company":"companyID",
    "room":"roomID",
    "device":"deviceID"  //unite主机本身也视为一个设备，deviceID为"system"
    "type": "online",    //消息类型，online
    ”version":1.0,
}
```    
####1.2 unite主机 heartbeat消息， unite主机连接到mqtt server后， 每分钟发一次心跳消息。
```
{
    "company":"companyID",
    "room":"roomID",
    "device":"deviceID"  //unite主机本身也视为一个设备，deviceID为"system"
    "type": "heartbeat",    //消息类型，heartbeat
    ”version":1.0,
}
```    
    
###2. 设备相关消息
####2.1 人感设备 消息
```
{
     "company":"companyID",
     "room":"roomID",
     "device":"deviceID"  //人感设备ID
     "type": "data",    //消息类型，data
     ”state":"on|off"   //消息内容，on：有人，off：无人
}
```
      
####2.2 插座设备 消息
```       
{
     "company":"companyID",
     "room":"roomID",
     "device":"deviceID"  //插座设备ID
     "type": "data",    //消息类型，data
     ”state":"on|off"   //消息内容，on：打开，off：关闭
}
```    
   
