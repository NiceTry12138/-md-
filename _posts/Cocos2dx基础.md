---
title: Cocos2dx基础
date: 2018-11-04 19:43:40
tags:
---

# Cocos2dx-网络通信
1. Socket通讯
2. http协议
3. WebSocket协议	 

- Cocos2d-x封装了3个类来处理HTTP请求
	- HttpRequest
	- HttpClient
	- HttpResponse
- 他们在命名空间cocos2d::network中定义
- WebSocket protocol是HTML5一种新的协议
	- 实现了浏览器和服务器全双工通信
	- 实现浏览器和服务器的即时通讯

## 使用Http协议进行网络通信
1. HttpRequest
2. HttpClient
3. HttpRespose

- 在使用上述三个类的时候，必须遵守一定的流程
	1. 创建HttpRequest实例
	2. 设置请求方式-Get/Post等
	3. 设置请求地址和发送数据
	4. 设置响应回调函数，在回调函数中处理获取的数据
	5. 创建HttpClient实例，发送请求
	6. 释放连接

### HttpRequest
- 是一种数据类型
- 提供了一些定义或获取HTTP请求的参数的方法

- 常用方法
	- 设置请求连接
		- void setUrl(const char *url)
	- 设置请求类型
		- void setRequestType(Type type)
		- Type是一个枚举类型
		- enum class Type{
			- GET,
			- POST,
			- PUT,
			- DELETE,
			- UNKOW,
		- };
	- 设置回调函数
		- void setResponseCallback(Ref *pTarget, SEL_HttpResponse pSelector)
	- 设置请求的数据，参数buffer是提交的数据，len是请求数据的长度
		- void serRequestData(const char *buffer, unsigned int len)


### HttpClient

- 在创建完HttpRequest之后，就需要创建HttpClient对象
- HttpClient对象控制请求相关的参数
	- 发送请求
	- 设置请求超时时间
	- ……
- 使用单例模式，是唯一实例
- 常用方法
	- 发送请求
		- send(Http Request* request)
	- 设置连接超时时间
		- setTimeoutForConnect(int value)

### HttpRespose

- 包含服务器返回的数据等信息
- 使用HTTPResponse提供的方法可获取这些数据
	- 获取请求返回的数据
		- std::vector<char>* getResponseData();
	- 获取返回状态（200,300,404,500...）
		- getResponseState()
	- 判断是否返回成功
		- issucced()


```cpp
// 引入头文件
#include "network/HttpRequest.h"
#include "network/HttpClient.h"
#include "network/HttpResponse.h"
// 引入名空间
using namespace cocos2d::network;

// 获取HttpRequest对象
auto request = new HttpRequest();
// 设置请求连接
request->setUrl("http://httpbin.org/ip");
// 设置请求方式
request->setRequestType(HttpRequest::Type::GET);
// 设置发送数据
char data[50] = "data";
request->setRequestData(data, strlen(data));

// 设置回调函数
request->setResponseCallback(CC_CALLBACK_2(HelloWorld::ConnetIntnet,this));

// 获取唯一的clien实例
auto client = HttpClient::getInstance();
// 设置超时时间
client->setTimeoutForConnect(60);
// 设置读取时间
client->setTimeoutForRead(100);
// 发送请求
client->send(request);


void HelloWorld::ConnetIntnet(HttpClient * client, HttpResponse * response)
{
	CCLOG("response code = %d", response->getResponseCode());
	if (response->isSucceed()){

		std::vector<char> *data = response->getResponseData();
		std::stringstream oss;
		for (int i = 0; i < data->size(); i++) {
			oss << (*data)[i];
		}
		CCLOG(" response data is %s", oss.str().c_str());
	}else{
		CCLOG("error msg is : %s", response->getErrorBuffer());
	}
}

```

### 发送POST请求

- 很简单
- 修改上述的部分代码即可

```cpp

request->setUrl("http://httpbin.org/post");
// 设置请求方式
request->setRequestType(HttpRequest::Type::POST);
// 设置发送数据
char data[50] = "controller=cocos2d&username=test";
request->setRequestData(data, strlen(data));

// 最后加上
request->release();
```
- 观察输出结构
	- form 表单中 controller 就是 cocos2d，username 是 test

```xml

response code = 200
 response data is {
  "args": {}, 
  "data": "", 
  "files": {}, 
  "form": {
    "controller": "cocos2d", 
    "username": "test"
  }, 
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "identity", 
    "Connection": "close", 
    "Content-Length": "32", 
    "Content-Type": "application/x-www-form-urlencoded", 
    "Host": "httpbin.org"
  }, 
  "json": null, 
  "origin": "61.136.151.254", 
  "url": "http://httpbin.org/post"
}

```

#### 设置Content-Type
- POST请求需要设置 Content-type的格式
	- application/html 或者 xml 或 json
	- 默认为text/html

- 一般来说 Content-Type:application/html;charset=uft-8

#### 设置请求头信息

```cpp

set::vector<std::string> header;
header.push_back("Content-Type:application/html;charset=utf-8");
request->setHeaders(header);
// 具体情况具体分析吧，有的服务器使用的是XML，有的是HTML，有的是Json

```

## 使用WebSocket发送请求

### WebSocket
- WebSocket类了跟websocket相关操作的方法。他的作用包括
	1. 创建socket对象
		- new 方法
	2. 向服务器发送数据，可以是文本数据，也可以是二进制数据
		- send方法
	3. 半段连接状态
	4. 等等

```cpp

enum class ErrorCode{
	TIME_OUT,// 连接超时
	CONNECTION_FAILURE, // 连接失败
	UNKNOW, // 为止错误
}

```

```cpp

cocos2d::network::WebSocket* wsSendText = new network::WebSocket();
// 创建对象

wsSendText->init(*this, "ws://echo.websocket.org");
// 初始化请求地址

weSendText->send("hello WebSocket, I'm a text message");
// 发送数据

```

### WebSocket::Delegete
- 类似Socket
- WebSocket::Delegete提供了四个纯虚函数
- 在使用WebSocket时，要先继承Delegete类，实现四个纯虚函数

```cpp

virtual void onOpen(WebSocket* ws);
// 当打开websocket连接时调用
// 即WebSocket new 出来的时候调用的函数

virtual void onMessage(WebSocket* ws, const Data& data);
// 当接收到数据时调用

virtual void onClose(WebSocket* ws);
// 当关闭连接时调用

voirtual void onError(WebSocket* ws, const ErrorCode& error);
// 当发送数据但没有建立连接，或者收到断开连接信号时调用

```

```cpp

wstest = new WebSocket();
wstest->init(*this,	"ws://echo.websocket.org");
wstest->send("hello world");
wstest->close();
	
```

# Box2D物理引擎在Cocos的应用

- 为了能够使用BOX2D，所以需要在vs中配置
  - 右键工程名，选择属性
  - 在常规中 设置 附加包含目录（第一个）
    - 修改 $(EngineRoot)external\chipmunk\include\chipmunk 
    - 为 $(EngineRoot)external\Box2D\include\
  - 在 预处理 器中 设置 预处理器定义
    - 修改 CC_ENABLE_CHIPMUNK_INTEGRATION= 1
    - 为 CC_ENABLE_BOX2D_INTEGRATION= 1



## 创建世界，设置边界

- HelloWorld.cpp文件

```cpp
#include "HelloWorldScene.h"
#include "SimpleAudioEngine.h"

USING_NS_CC;

Scene* HelloWorld::createScene()
{
	return HelloWorld::create();
}

HelloWorld::~HelloWorld()
{
	CC_SAFE_DELETE(world);//删除对象 并指向一个NULL
}

static void problemLoading(const char* filename)
{
    printf("Error while loading: %s\n", filename);
    printf("Depending on how you compiled you might have to add 'Resources/' in front of filenames in HelloWorldScene.cpp\n");
}

bool HelloWorld::init()
{
    if ( !Scene::init() )
    {
        return false;
    }

	this->initpjysics();

	this->scheduleUpdate();

	EventListenerTouchOneByOne *listener = EventListenerTouchOneByOne::create();
	listener->onTouchBegan = CC_CALLBACK_2(HelloWorld::onTouchBegan, this);
	_eventDispatcher->addEventListenerWithSceneGraphPriority(listener, this);

    auto visibleSize = Director::getInstance()->getVisibleSize();
    Vec2 origin = Director::getInstance()->getVisibleOrigin();

	
    
    return true;
}

void HelloWorld::update(float dt)
{
	// 同步精灵与物体
	float timeStep = 0.03f;
	int32 velocityIterations = 8;
	int32 positionIterations = 1;
	// 设置刷新时间
	world->Step(timeStep, velocityIterations, positionIterations);
	for (b2Body *b = world->GetBodyList(); b; b = b->GetNext()) {
		if (b->GetUserData() != nullptr) {
			// 运动只有两种运动 一个旋转 一个位移，因此只需要将物体角度，位置与精灵角度，位置同步
			Sprite* sprite = (Sprite *)b->GetUserData();
			// 物体的单位是 m ， 精灵的单位是 像素
			sprite->setPosition(Vec2(b->GetPosition().x * PTM_PATIO, b->GetPosition().y * PTM_PATIO));
			sprite->setRotation(-1 * CC_RADIANS_TO_DEGREES(b->GetAngle()));
		}
	}
}


void HelloWorld::menuCloseCallback(Ref* pSender)
{
    Director::getInstance()->end();

    #if (CC_TARGET_PLATFORM == CC_PLATFORM_IOS)
    exit(0);
#endif

}
// 创建世界，引入世界边界
void HelloWorld::initpjysics()
{
	auto visibleSize = Director::getInstance()->getVisibleSize();
	Vec2 origin = Director::getInstance()->getVisibleOrigin();

	//设置重力
	b2Vec2 gravity;
	gravity.Set(0.0f, -10.0f);

	//创建世界
	world = new b2World(gravity);

	// 允许物体休眠
	world->SetAllowSleeping(true);
	// 开启连续物理测试
	// 防止 物体 间 出现 物体穿透
	world->SetContinuousPhysics(true);

	// 物理世界的边界
	b2BodyDef groundBody;
	groundBody.position.Set(0,0);//左下角

	b2Body *ground = world->CreateBody(&groundBody);

	b2EdgeShape groundBox;
	
	// 定义底部
	groundBox.Set(b2Vec2(0,0), b2Vec2(visibleSize.width/PTM_PATIO,0)); // / PTM_PATIO 是 把像素换成 米

	// 使用夹具 固定 形状到物体
	// 参数是 形状指针， 密度
	ground->CreateFixture(&groundBox, 0);
	
	// 定义顶部
	groundBox.Set(b2Vec2(0, visibleSize.height/PTM_PATIO), b2Vec2(visibleSize.width / PTM_PATIO, visibleSize.height/PTM_PATIO)); // / PTM_PATIO 是 把像素换成 米
	ground->CreateFixture(&groundBox, 0);

	// 定义左侧
	groundBox.Set(b2Vec2(0, 0), b2Vec2(0, visibleSize.height/PTM_PATIO)); // / PTM_PATIO 是 把像素换成 米
	ground->CreateFixture(&groundBox, 0);

	
	// 定义右侧
	groundBox.Set(b2Vec2(visibleSize.width/PTM_PATIO, 0), b2Vec2(visibleSize.width / PTM_PATIO, visibleSize.height/PTM_PATIO)); // / PTM_PATIO 是 把像素换成 米
	ground->CreateFixture(&groundBox, 0);


}

void HelloWorld::addNewSprite(Touch * touch, Event * unused_event)
{
	auto p = touch->getLocation();

	// 创建物理相关精灵
	auto sprite = Sprite::create("");
	sprite->setPosition(touch->getLocation());
	this->addChild(sprite);

	// 定义物体
	b2BodyDef bodyDef;
	bodyDef.type = b2_dynamicBody;//动态物体
	bodyDef.position.Set(p.x/PTM_PATIO, p.y/PTM_PATIO);

	b2Body *body = world->CreateBody(&bodyDef);//从物理世界创建body

	body->SetUserData(sprite); //将 物体 与 body 关联

	//定义形状
    auto contenSize = sprite.getContentSize();
	b2PolygonShape dynamicBox;//这是个结构体
	dynamicBox.SetAsBox(contenSize.width/PTM_RATIO/2,contenSeiz.width/PTM_PATIO/2); //设置形状大小，中心点到左边距，右边距
    // 这里自动适配图片大小，又因为 是 中心点到左右两边的距离，所以要 除以 2

	// 定义夹具
	b2FixtureDef fixtrue;
	fixtrue.shape = &dynamicBox;
	fixtrue.density = 1.0f;//密度
	fixtrue.friction = 0.3f;// 摩擦系数

	// 将夹具 与 body 连接
	body->CreateFixture(&fixtrue);
	
	// 但是物体并不会动，需要在update函数中设置
}

bool HelloWorld::onTouchBegan(Touch * touch, Event * event)
{
	addNewSprite(touch, event);
	return false;
}

```

- HelloWorld.h文件

```cpp

#ifndef __HELLOWORLD_SCENE_H__
#define __HELLOWORLD_SCENE_H__

#include "cocos2d.h"
#include "Box2D\Box2D.h"
#include "ContactListener.h"
USING_NS_CC;

#define PTM_PATIO 32

class HelloWorld : public cocos2d::Scene
{
public:
    static cocos2d::Scene* createScene();
	~HelloWorld();
	
    virtual bool init();
	virtual void update(float dt);
    // a selector callback
    void menuCloseCallback(cocos2d::Ref* pSender);
	void initpjysics();//初始化物理引擎
	void addNewSprite(Touch* touch, Event* unused_event);
	b2World *world;
	ContactListener* contactListener;
    
	bool onTouchBegan(Touch* touch, Event *event);

    // implement the "static create()" method manually
    CREATE_FUNC(HelloWorld);
};

#endif // __HELLOWORLD_SCENE_H__

```





## 碰撞检测

- ContactListener.h


```cpp
#pragma once
#include "cocos2d.h"
#include "Box2D\Box2D.h"
using namespace std;
USING_NS_CC;

class ContactListener : public b2ContactListener {
private:
	virtual void BeginContact(b2Contact* contact);
	virtual void EndContact(b2Contact* contact);
	virtual void PreSolve(b2Contact* contact, const b2Manifold* oldManifold);
	virtual void PostSolve(b2Contact* contact, const b2ContactImpulse* impulse);

};

```
- ContactListener.cpp 文件


```cpp
#include "ContactListener.h"
USING_NS_CC;

void ContactListener::BeginContact(b2Contact * contact)
{
	CCLOG("begin");
	b2Body* bodyA = contact->GetFixtureA()->GetBody();// 通过夹具获得物体A的body
	b2Body* bodyB = contact->GetFixtureB()->GetBody();// 通过夹具获得物体A的body
	auto spriteA = (Sprite *)bodyA->GetUserData(); // 通过body获取精灵，强转一下
	auto spriteB = (Sprite *)bodyB->GetUserData(); // 通过body获取精灵，强转一下

	if (spriteA != nullptr && spriteB != nullptr) {
		spriteA->setColor(Color3B::YELLOW);
		spriteB->setColor(Color3B::YELLOW);
	}
}

void ContactListener::EndContact(b2Contact * contact)
{
	CCLOG("end");
	b2Body* bodyA = contact->GetFixtureA()->GetBody();// 通过夹具获得物体A的body
	b2Body* bodyB = contact->GetFixtureB()->GetBody();// 通过夹具获得物体A的body
	auto spriteA = (Sprite *)bodyA->GetUserData(); // 通过body获取精灵，强转一下
	auto spriteB = (Sprite *)bodyB->GetUserData(); // 通过body获取精灵，强转一下

	if (spriteA != nullptr && spriteB != nullptr) {
		spriteA->setColor(Color3B::WHITE);
		spriteB->setColor(Color3B::WHITE);
	}
}

void ContactListener::PreSolve(b2Contact * contact, const b2Manifold * oldManifold)
{
	CCLOG("PreSolve");
}

void ContactListener::PostSolve(b2Contact * contact, const b2ContactImpulse * impulse)
{
	CCLOG("PostSolve");
}


```


## 关节

1. 距离关节
   - 两个物体之间保持固定的距离，每个物体上的点称为锚点。
   - 关节定义是b2DistanceJoinDef
2. 旋转关节
   - 允许物体围绕公共点旋转。
   - 关节定义是 b2RevoluteJoiDef
3. 平移关节
   - 两个物体之间的相对旋转是固定的，他们可以沿着一个坐标轴进行平移。
   - 关节定义是 b2PrismaticJointDef
4. 焊接关节
   - 可以吧物体固定在相同方向上。
   - 关节定义是 b2WeldJointDef
5. 轮滑关节
   - 轮滑关节用于创建理想的轮滑，两个物体唯一绳子两端，绳子通过某个固定点（轮滑的位置）将两个物体连接起来
   - 当一个物体升起，另一个物体就会下降
   - 关节定义是 b2PulleyJointDef
6. 摩擦关节
   - 降低两个物体之间的相对运动
   - 关节定义是 b2FrictionJointDef
7. 齿轮关节
   - 控制其他两个关节（旋转关节或者平移关节），其中一个的愚弄的那个会影响另一个
   - 关节定义是 b2GearJointDef
8. 鼠标关节
   - 点击物体上任意一个点可以在世界范围内进行拖动
   - 关节定义是 b2MouseJointDef



# 动作

```cpp

Sprite * sp= Sprite::create("Icon.png");
sp->setPosition(Vec2(150, 150));
addChild(sp,0,922);

//    Action动作

// MoveBy  创建一个移动的动作   参数1：移动到目标坐标所需的时间 参数2：目标坐标    
// 支持reverse 可以获取其反向动作
//     MoveTo  一样的
ActionInterval * moveBy = MoveBy::create(5,Vec2(300, 100));
ActionInterval * actionmoveback= moveBy->reverse();
sp->runAction(actionmoveback);

//     ScaleTo   作用：创建一个缩放的动作
//    参数1：达到缩放大小所需的时间
//    参数2 ：缩放的比例
ActionInterval * scaleto = ScaleTo ::create(2, 2);
sp->runAction(scaleto);

//     ScaleBy  作用:创建一个缩放的动作
//    参数1：达到缩放大小的所需时间  参数2：缩放比例
ActionInterval * scaleby = ScaleBy::create(2, 2);
ActionInterval * actionbyback = scaleby->reverse();
sp->runAction(actionbyback);

//     RotateTo
//    作用创建一个旋转的动作
//    参数1：旋转的时间  参数2：旋转饿角度  0 - 360
ActionInterval * rotateto = RotateTo::create(2, 90);
sp->runAction(rotateto);

//   SkewTo
//   作用创建一个倾斜的动作
//    参数1：倾斜到特定角度所需的时间
//    参数2：x轴的倾斜角度
//    参数3：y轴的倾斜角度
ActionInterval * skewto = SkewTo::create(2, 10, 10);
sp->runAction(skewto);

//     JumpTo
//    作用：创建一个跳的动作
//    参数1：跳到目标动作位子的所需时间
//    参数2：目标位置
//    参数3：跳的高度
//    参数4跳到目标位置的次数
ActionInterval* jumpto = JumpTo ::create(2, Vec2(300, 200), 50, 4 );
sp->runAction(jumpto);

//     JumpBy
//    作用：创建一个跳的动作
//    参数1：跳到目标动作位子的所需时间
//    参数2：目标位置
//    参数3：跳的高度
//    参数4跳到目标位置的次数
//    这个支持方向动作reverse
ActionInterval * jumpby = JumpBy ::create(3, Vec2(300, 200), 50, 4);
ActionInterval * ac= jumpby->reverse();
sp->runAction(ac);



//         Bezier
//     BezierConfig结构体
 BezierConfig bezierCon;
bezierCon.controlPoint_1=Vec2(200, 150);//控制点1
bezierCon.controlPoint_2=Vec2(200, 160);//控制点2
bezierCon.endPosition =Vec2(340, 100);// 结束位置
//BezierTo
//        创建一个贝塞尔曲线运动的动作
//        参数1：贝塞尔曲线运动的时间
//        参数2 ： BezierConfig结构体
ActionInterval * action = BezierTo::create(2, bezierCon);
ActionInterval * action1 = BezierBy::create(3, bezierCon);//支持反向
ActionInterval * action2 = action->reverse();
sp->runAction(action1);


//FadeIn
//作用：创建一个渐变出现的动作
//参数是时间
ActionInterval * fadein = FadeIn::create(2);
sp->runAction(fadein);


//     FadeOut
//    作用：创建一个渐变消失的动作
//    参数是时间
ActionInterval * fadeout = FadeOut::create(2);
sp->runAction(fadeout);


// TintTo
//    作用：创建一个色彩变化的消失动作
//    参数1：色彩变化的动作
//    参数2 ：红色分量
//    参数3：蓝色分量
ActionInterval * tinto = TintTo ::create(3, 255, 255, 0);
sp->runAction(tinto);


//     TintBy
//    作用：创建一个色彩变化的出现动作
//    参数1：色彩变化的动作
//    参数2 ：红色分量
//    参数3：蓝色分量   但是家了reverse就是 反向的
ActionInterval * tintby = TintBy::create(3, 0, 255, 255);
ActionInterval * tintby1 = tintby->reverse();
sp->runAction(tintby1);

//     Blink
//    作用 :创建一额闪烁的动作
//    参数1：闪烁完成的时间
//    参数2:闪烁的次数

ActionInterval * blink = Blink ::create(3, 10);
sp->runAction(blink);



//     DelayTime
//    创建一个延迟的动作
//    参数  延迟的时间
ActionInterval * delaytime = DelayTime::create(3);
sp->runAction(delaytime);

//     OrbitCamera
//    作用：创建一个球面坐标轨迹进行旋转的动作
//    参数1 ： 旋转轨迹的时间
//    参数2 ：起始半径
//    参数3：半径差
//    参数4：起始z角
//    参数5：旋转z角的差
//    参数6：起始x角
//    参数7：旋转x角的差
ActionInterval * orbitcameraa = OrbitCamera::create(3, 10, 0, 45, 180, 90, 0);
sp->runAction(orbitcameraa);


//     CardinalSpline
//    作用：创建数组  点的数组
PointArray * array = PointArray::create(20);
array->addControlPoint(Vec2(0,0));
array->addControlPoint(Vec2(210,0));
array->addControlPoint(Vec2(210,240));
array->addControlPoint(Vec2(0,160));
array->addControlPoint(Vec2(0,0));
//    CardinalSplineTo
//    作用：创建一个样条曲线轨迹的动作
//    参数1：完成轨迹所需的时间
//    参数2：控制点的坐标数组
//    拟合度  其值= 0 路径最柔和
ActionInterval  * CardinalSplineTo=CardinalSplineTo::create(3, array, 0);
sp->runAction(CardinalSplineTo);


//    CardinalSplineBy
//    作用：创建一个样条曲线轨迹的动作
//    参数1：完成轨迹所需的时间
//    参数2：控制点的坐标数组
//    拟合度  其值= 0 路径最柔和
ActionInterval * CardinalSplineBy = CardinalSplineBy::create(3, array, 0);
sp->runAction(CardinalSplineBy);

//    CatmullRomTo   CatmullRomBY
//    作用：创建一个样条插值轨迹
//    参数1：完成轨迹的时间
//    参数2：控制点的数组坐标
ActionInterval * catmullRomTo = CatmullRomTo::create(3, array);
sp->runAction(catmullRomTo);

//    Follow
//    作用：创建一个跟随动作
//    参数1：跟随的目标对象
//    跟随范围，离开范围就不再跟随
//创建一个参照物spT
Sprite * spt = Sprite::create("Icon.png");
spt->setPosition(Vec2(420,40));
addChild(spt);
sp->runAction(MoveTo::create(3, Vec2(940,sp->getPositionY())));

Follow * follow = Follow::create(sp,Rect(0, 0, 960, 320));
this-> runAction(follow);

//     EaseBounceIn
//    目标动作
ActionInterval* move = MoveTo::create(3, Vec2(300, sp->getPositionY()));
////    让目标动作缓慢开始
////    参数：目标动作
ActionInterval * EaseBounceIn = EaseBounceIn::create(move);
sp->runAction(EaseBounceIn);

//    EaseBounceOut
//    作用：让目标动作赋予反弹力，且以目标动作结束位子开始反弹
//    参数目标动作
ActionInterval * easeBounceOut = EaseBounceOut ::create(move);
sp->runAction(easeBounceOut);

//    EaseBounceInOut
//    作用：让目标动作赋予反弹力，且以目标动作起始与结束位子开始反弹
ActionInterval * easeBounceInOut= EaseBounceInOut::create(move);
sp->runAction(easeBounceInOut);

//   EaseBackIn
//    作用：让目标动作赋予回力 ， 且以目标动作起点位置作为回力点
//    参数：目标动作
ActionInterval * easeBackIn = EaseBackIn::create(move);
sp->runAction(easeBackIn);

//    EaseBackOut
//    作用：让目标动作赋予回力 ， 且以目标动作终点位置作为回力点
//    参数：目标动作
ActionInterval *easeBackOut = EaseBackOut::create(move);
sp->runAction(easeBackOut);

//     EaseBackInOut
//    作用：让目标动作赋予回力 ， 且以目标动作起点和终点位置作为回力点
//    参数：目标动作
 ActionInterval * easeBackInOut =  EaseBackInOut::create(move);
sp->runAction(easeBackInOut);

//     EaseElasticIn
//    作用：让目标动作赋予弹性 ，且以目标动作起点位子赋予弹性
//     参数：目标动作
 ActionInterval * easeElasticIn=  EaseElasticIn::create(move);
sp->runAction(easeElasticIn);

//      EaseElasticOut
//    作用：让目标动作赋予弹性 ，且以目标动作终点位子赋予弹性
//     参数：目标动作
 ActionInterval *easeElasticOut =  EaseElasticOut::create(move);
sp->runAction(easeElasticOut);

//     EaseElasticInOut
//    作用：让目标动作赋予弹性 ，且以目标动作起点和终点位子赋予弹性
//     参数：目标动作
 ActionInterval *easeElasticInOut =  EaseElasticOut::create(move);
sp->runAction(easeElasticInOut);


//     EaseExponentialIn
//    让目标动作缓慢开始
//    参数：目标动作
 ActionInterval * easeExponentialIn=  EaseExponentialIn::create(move);
sp->runAction(easeExponentialIn);

//     EaseExponentialOut
//    让目标动作缓慢中止
//    参数：目标动作
ActionInterval * easeExponentialInt=  EaseExponentialOut::create(move);
sp->runAction(easeExponentialInt);

//     EaseExponentialInOut
//    让目标动作缓慢开始和中止
//    参数：目标动作
 ActionInterval * easeExponentialInOut=  EaseExponentialInOut::create(move);
sp->runAction(easeExponentialInOut);

//     EaseRateAction
//    作用 ： 让目标动作设置速率
//    参数1:目标动作
//    参数2：速率
 ActionInterval * moveto =  MoveTo::create(5,  p(300,sp->getPositionY()));
 ActionInterval * easeRateAction =  EaseRateAction::create(move, 3);
sp->runAction(easeRateAction);

//     EaseSineIn
//    作用：动作由慢到快
//      参数：目标动作
 ActionInterval * easeSineIn =  EaseSineIn::create(move);
sp->runAction(easeSineIn);

//     EaseSineOut
//    作用：动作由快到慢
//      参数：目标动作
 ActionInterval * easeSineOut =  EaseSineOut::create(move);
sp->runAction(easeSineOut);

//     EaseSineInOut
//    作用：动作由慢到快再快到慢
//      参数：目标动作
 ActionInterval * easeSineInOut =  EaseSineInOut::create(move);
sp->runAction(easeSineInOut);



//     Speed
//    作用：让目标动作运行速度加倍
//    参数1：目标动作
//    参数2:倍速
 ActionInterval * move =  MoveTo::create(10,  p(300,sp->getPositionY()));
 Speed * speed = Speed::create(move, 100);
sp->runAction(speed);

//     Spawn
//  作用：让多个动作同时执行
//    参数：目标动作的可变参数
 ActionInterval * move1 =  MoveTo::create(10,  p(300,sp->getPositionY()));
 ActionInterval * scale =  ScaleTo::create(2, 3);
 ActionInterval * rotate =  RotateTo::create(4, 190);
 FiniteTimeAction * spawn = Spawn::create(move1,scale,rotate,NULL);
sp->runAction(spawn);

//     Sequence
//    作用：让多个动作按照前后顺序逐一执行
//    参数：目标动作的可变参数
 ActionInterval * move2 =  MoveTo::create(2,  p(300, sp->getPositionY()));
 ActionInterval * scalet =  ScaleTo::create(2, 3);
 FiniteTimeAction * seq=  Sequence::create(move2,scalet,NULL);
sp->runAction(seq);


    //    扩展如果要对目标动作全部进行方向运动，可以使用如下形式操作
 FiniteTimeAction *seqe= Sequence::create(moveby,scaleby,...NULL);
 FiniteTimeAction * reverseseq =  Sequence::create(seqe,seq->reverse(),NULL)



//注意 Sequence中的所有动作都必须支持reverse函数，否则会出现异常
 ActionInterval * move =  MoveBy::create(2,  p(300, sp->getPositionY()));
 ActionInterval * scale =  ScaleBy::create(2, 3);
 FiniteTimeAction * seq=  Sequence::create(move,scale,NULL);
 FiniteTimeAction * reveseseq =  Sequence::create(seq,seq->reverse(),NULL);
sp->runAction(reveseseq);




//     Repeat
//    作用：对目标动作进行重复运动（目标动作可以是 Sequence ， Spawn）
//    参数1：目标动作
//    参数2：重复次数
 ActionInterval * move =  MoveTo::create(2,  p(300, sp->getPositionY()));
 ActionInterval * move2 =  MoveTo::create(2,  p(100,100));
 FiniteTimeAction*seq = Sequence::create(move,move2,NULL);
 FiniteTimeAction *repeat =  Repeat::create(seq, 3);
sp->runAction(repeat);


//     RepeatForever
//    作用：对目标动作进行永久性的重复运动（目标动作可以是 Sequence ， Spawn）
//    参数：目标动作
 ActionInterval * move =  MoveTo::create(1,  p(300, sp->getPositionY()));
 ActionInterval * move1 =  MoveTo::create(1,  p(100,100));
 FiniteTimeAction* seq =  Sequence::create(move,move1,NULL);
 ActionInterval * repeatForever = RepeatForever::create(( ActionInterval* )seq);
sp->runAction(repeatForever);

//     CallFunc
//    作用：创建一个回调动作（调用不带参数的回调方法）；
//    参数1：目标动作
//    参数2：目标回调函数
 ActionInterval * move =  MoveTo::create(1,  p(300, sp->getPositionY()));
 CallFunc * funcall=  CallFunc::create(this, callfunc_selector(HelloWorld::callbackC));
 FiniteTimeAction * seq =  Sequence::create(move,funcall,NULL);
sp->runAction(seq);

//     CallFuncN
//    作用：创建一个回调动作（调用 带一个参数的回调方法）；
//    参数1：目标动作
//    参数2：目标回调函数
 ActionInterval * move =  MoveTo::create(1,  p(300, sp->getPositionY()));
 CallFuncN * funcall=  CallFuncN::create(this, callfuncN_selector(HelloWorld::callbackN));
 FiniteTimeAction * seq =  Sequence::create(move,funcall,NULL);
sp->runAction(seq);

//     CallFuncND
//    作用：创建一个回调动作（调用 带两个参数的回调方法）；
//    参数1：目标动作
//    参数2：目标回调函数
 ActionInterval * move =  MoveTo::create(1,  p(300, sp->getPositionY()));
 CallFuncND * funcall=  CallFuncND::create(this, callfuncND_selector(HelloWorld::callbackND)  ,(void*)0xbebabeba);
 FiniteTimeAction * seq =  Sequence::create(move,funcall,NULL);
sp->runAction(seq);
```

# 内存管理机制

## 常用算法

### 引用计数算法
- 每个对象都有一个引用，一个数来跟踪它被引用的次数
- 每增加一次 引用计数+1 ，每减少一次 应用计数-1
- 垃圾回收时 引用计数 为0 时就要被回收
- `最为致命`的问题是无法解决循环引用

### 标记清除算法
- 根可达的集合，cocos中的所有对象都有一个同一个父节点
- 第一个阶段从应用节点开始标记所有被引用的对象
- 第二个阶段遍历整个堆，把未标记的对象清除
- `最为致命`的问题是这个算法需要暂停整个应用，并且会产生内存碎片

### 复制算法
- 将内存分为连个区域，每次只使用其中一个区域。
- 垃圾回收时，遍历整个区域，将正在使用的对象复制到另一个区域中
- 复制成本较小，而且可以进行内存管理，不会出现内存碎片
- `最为致命`的问题是这个算法需要两倍的内存空间

### 标记-整理算法
- 集合了标记清除和复制算法
- 第一阶段，从根节点开始标记所有的被应用的节点
- 第二阶段，清除未被标记的节点，同时将被标记的节点压缩到一起，按顺序排放

## delete和new
### new运算符使用的一般格式为 　　
	new 类型 [初值] 　　用new分配数组空间时不能指定初值。
	如果由于内存不足等原因而无法正常分配空间，则new会返回一个空指针NULL，用户可以根据该指针的值判断分配空间是否成功。
	new int;//开辟一个存放整数的存储空间，返回一个指向该存储空间的地址(即指针) 　　
	new int(100);//开辟一个存放整数的空间，并指定该整数的初值为100，返回一个指向该存储空间的地址　　
	new char[10];//开辟一个存放字符数组(包括10个元素)的空间，返回首元素的地址 　　
	new int[5][4];//开辟一个存放二维整型数组(大小为5*4)的空间，返回首元素的地址
	float *p=new float (3.14159);//开辟一个存放单精度数的空间，并指定该实数的初值为//3.14159，将返回的该空间的地址赋给指针变量p 　　
### delete运算符使用的一般格式为 　　
	delete [ ]指针变量 　　
	例如要撤销上面用new开辟的存放单精度数的空间(上面第5个例子)，应该用 　　delete p；　　
	前面用“new char[10];”开辟的字符数组空间，如果把new返回的指针赋给了指针变量pt，则应该用以下形式的delete运算符撤销该空间： 　　
	  delete [] pt；//在指针变量前面加一对方括号，表示是对数组空间的操作 　　

## Cocos2dx 的内存管理
- 使用的是 引用计数方法
- 所有的自动释放的对象都`继承`于`Ref`类
	- Node基类也继承与`Ref`类
- Ref类用于管理引用计数

### Ref的方法
- retain() 增加引用计数
- release() 减少引用计数
- autorelease() 生成自动释放对象
- getReferanceCount() 获取对象的引用计数

### 创建流程
- 创建一个对象的时候
- 首先调用对象的父类的构造函数
- 最终会调用到`Ref`这个基类
- 在`Ref`这基类中会初始化引用计数`ReferanceCount`为1

**在release函数中，有判断引用计数的值，如果为0会自动释放对象**

## CREATE_FUNC()函数
### 源码分析

```cpp
/** 
 * define a create function for a specific type, such as CCLayer 
 * @__TYPE__ class type to add create(), such as CCLayer 
 */  
#define CREATE_FUNC(__TYPE__) \  
static __TYPE__* create() \  
{ \  
    __TYPE__ *pRet = new __TYPE__(); \
	 //创建传过来的东西
    if (pRet && pRet->init()) \  
    { \  
        pRet->autorelease(); \  
        return pRet; \  
    } \  
    else \  
    { \  
        delete pRet; \  
        pRet = NULL; \  
        return NULL; \  
    } \  
}
```
**很明显上面的pRet 使用了 autorelease() 方法**
**先使用C++的new方法创建一个对象，如果创建成功，则添加自动清除**rc

### 什么是CREATE_FUNC()
	为类似CCLayer类的特定类增加一个create函数，我们也可以看到在宏的下面定义了一个create()函数返回到类型就是宏带入的参数"__TYPE__"指针类型
### create（）函数做了什么？
	他执行了类的构造函数，执行了init()初始化函数，最后又设置创建出的对象为自动释放内存，这样其他人在使用这个类的时候，只要是用create（）函数创建出来的对象就是不用费心区管理释放内存
## 引用计数
### 什么时候引用计数
	每一个对象都有一个关联的引用计数 —— 对该对象的活跃引用的数量。
	如果对象的引用计数是零，那么它就是垃圾（用户程序不可到达它），并可以回收。

## Cocos2dx内存管理分为两块
	1. 通过加入 `autorelease` 来自动释放那些创建后未使用的对象
	2. 通过`节点管理`来保证对象在弃用后及时的删除

### 及时释放弃用的对象
`使用条件`：该对象是Node的子类对象
`使用方法`：addChild，removeChild
#### 内存管理过程：
	addChild  添加对象后，对象可以被使用
	removeChild 删除对象后，对象被立刻删除（通过 delete）
### 及时释放未使用的对象
#### 简述
	新创建的对象如果 一帧 内不使用，就会被自动释放。（所谓一针，即是一个gameloop）
#### 使用条件
	对象通过CREAT_FUNC()宏创建或者对象使用autorelease加入了自动释放池
#### 使用方法
	自动实现
#### 管理过程
##### 对象不使用的情况
	对象创建		引用+1
	对象自动释放 	引用-1
##### 对象使用的情况
	对象创建		引用+1
	对象使用		引用+1//通过 addchild 使用对象
	对象自动释放	引用-1
引用的初始值为0，如果一阵结束后对象的引用值还是0，那就会被delete掉

## 内存管理的实现原理

### 第一部分
`Red`类：进行引用计数，提供加入自动释放池的接口。
`AutoreleasePool`类：管理一个`vector`数组来存放自动释放池的对象。提供对释放池的清空操作
`PoolManager`类：管理一个`vector`数组来存放自动释放池。默认情况下引擎只创建一个自动释放池，因此这个类是提供给开发者使用的，例如处于性能考虑添加自己的自动释放池
`DisplayLinkDirector`类：只是一个导演类，提供游戏的主循环，实现每一帧的资源释放。这个类继承自`Director`类，也是唯一一个继承了`Director`的类，也就是说完全可以合并为一个类。

#### Ref源码

```cpp
// 引用计数变量
unsigned int _referenceCount;

// 对象被构造后，引用计数值为 1
Ref::Ref()
: _referenceCount(1) //当Ref对象被创建时，引用计数的值为 1
{
#if CC_ENABLE_SCRIPT_BINDING
	static unsigned int uObjectCount = 0;
	_luaID = 0;
	_ID = ++uObjectCount;
	_scriptObject = nullptr;
#endif
	
#if CC_USE_MEM_LEAK_DETECTION
	trackRef(this);
#endif
}

// 引用+1
void Ref::retain()
{
	CCASSERT(_referenceCount > 0, "reference count should greater than 0");
	++_referenceCount;
}

// 引用-1 。如果引用为0则释放对象
void Ref::release()
{
	CCASSERT(_referenceCount > 0, "reference count should greater than 0");
	--_referenceCount;

	if (_referenceCount == 0)
	{

#if CC_USE_MEM_LEAK_DETECTION
		untrackRef(this);
#endif
		delete this; // 注意这里 把对象 delete 了
	}
}

// 提供加入自动释放池的接口。对象调用此函数即可加入自动释放池的管理。
Ref* Ref::autorelease()
{
	PoolManager::getInstance()->getCurrentPool()->addObject(this);
	return this;
}

//获取引用计数值
unsigned int Ref::getReferenceCount() const
{
	return _referenceCount;
}
```

#### AutoreleasePool源码

```cpp

// 存放释放池对象的数组
std::vector<Ref*> _managedObjectArray;

// 往释放池添加对象
void AutoreleasePool::addObject(Ref* object)
{
	_managedObjectArray.push_back(object);
}

// 清空释放池，将其中的所有对象都 delete
void AutoreleasePool::clear()
{
	// 释放所有对象
	for (const auto &obj : _managedObjectArray)
	{
		obj->release();
	}
	// 清空vector数组
	_managedObjectArray.clear();
}

// 查看某个对象是否在释放池中
bool AutoreleasePool::contains(Ref* object) const
{
	for (const auto& obj : _managedObjectArray)
	{
		if (obj == object)
			return true;
	}
	return false;
}
```

#### PoolManager源码

```cpp
// 释放池管理器单例对象
static PoolManager* s_singleInstance;

// 释放池数组
std::vector<AutoreleasePool*> _releasePoolStack;

// 获取 释放池管理器的单例
PoolManager* PoolManager::getInstance()
{
	if (s_singleInstance == nullptr)
	{
		// 新建一个管理器对象
		s_singleInstance = new PoolManager(); 
		
		// 添加一个自动释放池
		new AutoreleasePool("cocos2d autorelease pool");// 内部使用了释放池管理器的push，这里的调用很微妙，读者可以动手看一看
	}
	return s_singleInstance;
}

// 获取当前的释放池
AutoreleasePool* PoolManager::getCurrentPool() const
{
	return _releasePoolStack.back();
}

// 查看对象是否在某个释放池内
bool PoolManager::isObjectInPools(Ref* obj) const
{
	for (const auto& pool : _releasePoolStack)
	{
		if (pool->contains(obj))
			return true;
	}
	return false;
}

// 添加释放池对象
void PoolManager::push(AutoreleasePool *pool)
{
	_releasePoolStack.push_back(pool);
}

// 释放池对象出栈
void PoolManager::pop()
{
	CC_ASSERT(!_releasePoolStack.empty());
	_releasePoolStack.pop_back();
}
```

#### DisplayLinkDirector源码

```cpp

void DisplayLinkDirector::mainLoop()
{
	//第一次当导演
	if (_purgeDirectorInNextLoop)
	{
		_purgeDirectorInNextLoop = false;
		purgeDirector();//进行清理工作
	}
	else if (! _invalid)
	{
		// 绘制场景，游戏主要工作都在这里完成
		drawScene();
		
		// 清空资源池
		PoolManager::getInstance()->getCurrentPool()->clear();
	}
}
```

### 过程分析
	首先，创建了一个 Node 对象A，Node 继承Ref，因此 Ref 的引用计数为1；
	然后，A通过 autorelease 将自己放入自动释放池；drawScene() 完成后，
	一帧结束，Director 通过释放池将池中的对象 clear()，即对 Node 对象A进行 release() 操作。
	A的引用计数变为0，执行 delete 释放A对象。


# Cocos2dx 文件读写

## 简介
- 在Pc端，程序是可以读写任意电脑的文件夹的
- 在 IOC/安卓 端，程序可以安装在任意文件夹下，但是只能访问安装文件夹里的文件
- 这是一个安全机制

**cocos2dx 中的resouce资源文件夹 在打包安装到 IOS/安卓 上的时候是写死的不能更改的**

## 使用
- 使用到的类 `FileUtils::getInstance()`
- getWritablePath() 返回一个字符串string，获取一个可以写的文件路径

```cpp

string filePath = FileUtils::getInstance()->getWritablePath() + "user,txt"; 
// 这里的getWriteablePath() 是获取可以写的路径
string userData = FileUtils::getInstance()->getStringFromFile(filePath);
FileUtils::getInstance()->writeStringToFile(userData, filePath); 
// 保存文本的文件信息

```
**如果是获取安装路径的文件信息，则可以直接使用路径信息**
**例如，在resouce资源文件夹下有个Data文件夹，里面有个user.txt文件，则直接使用FileUtils::getInstance()->getStringFromFile("Data/user.txt");就可以，而不需要使用可写路径**

## 反蓄序列化
- 通过一个JSON文件，给一个类赋值

- 保存为UTF-8无dom格式

```json
[
	{"name":"tom",	"age":12,	"address":"******"}
	{"name":"lucy",	"age":13,	"address":"******"}
	{"name":"jack",	"age":14,	"address":"******"}
	{"name":"拉拉",	"age":15,	"address":"******"}
	{"name":"波",	"age":16,	"address":"******"}
	{"name":"树莓",	"age":17,	"address":"******"}
]
```

```cpp

class Student{
public:
	Student(string _name, int _age, string _address);
	~Student();

private:
	string name, address;
	int age;
}

Student::Student(string _name, int _age, string _address){
	this.name = _name;
	this.address = _address;
	this.age = _age;
}


```

**如果是在代码中用new的方法写死这个Student类，很明显是很2的**

- 在Cocos2dx 的代码中使用 `#include "spine/Json.h"`

```cpp

// 需要注意的是，这里并没有使用 上面的 可写路径
std::string strRoles = FileUtils::getInstance()->getStringFromFile("Data/User.txt");
// 反序列化，将字符串转为json格式
Json* data = Json_create(strRoles.c_str());
// 由于上述的json是一个数组，所以这里的data是一个数组
Json* stu = js->child;
// json数组的第一个元素
while(stu){
	// 这里就是一个获取的过程
	int id = Json_getItem(stu, "age");
	// 由于返回的是一个string类型，所以使用valueString, 同理还有 valuefloat 等
	std::string name = Json_getItem(stu, "name")->valueString;
	std::string address = Json_getItem(stu, "name")->valueString;

	Studen stu1 = new Student(name, age, address);

	// 往下走
	stu = stu->next;
}

```
