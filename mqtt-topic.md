## 一、未注册设备 topic
   * hub/company/[companyID]/unbinded/[roomID]/[tx|rx]
   
   unite主机未绑定到一个具体会议室时，通过该主题与server进行通讯，server通过该主题获得已连接到该company，但尚未绑定的unite主机。
   server通过向unite主机发送绑定消息实现unite主机与会议室的绑定，绑定后unite主机【已注册设备topic】与主机进行通讯。
   
### 主机join消息
```    
{
    "company":"companyID", //
    "room":"roomID",      //roomID 由于此时尚未绑定，roomID为uinite主机随机设定
    "type": "join",      //消息类型，join
    ”version":1.0,
}
```  

### server bind消息
    server向主机发布bind消息，实现unite主机与会议室的绑定
    
## 二、已注册设备 mqtt topic
   hub/company/[companyID]/rooms/[roomID]/event/[tx|rx]
   
   * companyID: 公司ID
   * rootmID：房间ID
   * tx：unite主机接收到房间内设备发送的消息时，向该主题发布消息，服务器可订阅该主题，接收该房间内的所有设备的消息。
   * rx：unite主机会订阅该主题，若服务器向该主题发布消息，unite主机会收到消息，并处理消息

## 三、服务器发布的消息类型（mqtt消息内容的类型）
    服务器向hub/company/[companyID]/rooms/[roomID]/event/rx发布的消息，unite主机接收并处理

## 四、unite主机发布的消息类型（mqtt消息内容的类型）
    unite主机向hub/company/[companyID]/rooms/[roomID]/event/tx发布的消息，服务器接收并处理
    
### 1. 主机相关消息
#### 1.1 unite主机online消息, 设备连接到mqtt server时发送online消息
```    
{
    "company":"companyID",
    "room":"roomID",
    "device":"deviceID"  //unite主机本身也视为一个设备，deviceID为"system"
    "type": "online",    //消息类型，online
    ”version":"1.0",
}
```    
#### 1.2 unite主机 heartbeat消息， unite主机连接到mqtt server后， 每分钟发一次心跳消息。
```
{
    "company":"companyID",
    "room":"roomID",
    "device":"deviceID"  //unite主机本身也视为一个设备，deviceID为"system"
    "type": "heartbeat",    //消息类型，heartbeat
    ”version":1.0,
}
```    
    
### 2. 设备相关消息
#### 2.1 人感设备 消息
```
{
     "company":"companyID",
     "room":"roomID",
     "device":"deviceID"  //人感设备ID
     "type": "data",    //消息类型，data
     ”state":"on|off"   //消息内容，on：有人，off：无人
}
```
      
#### 2.2 插座设备 消息
```       
{
     "company":"companyID",
     "room":"roomID",
     "device":"deviceID"  //插座设备ID
     "type": "data",    //消息类型，data
     ”state":"on|off"   //消息内容，on：打开，off：关闭
}
```    
   
