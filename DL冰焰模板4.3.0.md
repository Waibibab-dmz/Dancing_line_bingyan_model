# 1.线的基础设置

**Player**

* LevelData是当前关卡的核心文件
* Scene Camera当前关卡的摄像机（跟随线的摄像机）
* Scene Light当前关卡的定向光
* Character Material角色材质
* Start Position（以及后面的两个参数）分别为线的开始位置、刚开始的朝向和点击后的朝向
* Pool Size和线的长短有关
* Played Animators/Played Timelines线开始移动时播的帧动画/时间线
* allow turn点击后转弯
* no death碰到障碍会不会死
* draw direction四面转弯

**Scene Data（Level Data）**

* level title关卡标题
* sound track关卡音乐
* speed速度
* time scale 关卡倍速
* gravity重力
* color对线、地面等材质进行修改

# 2.铺引导线/铺路

**LevelHolder铺引导线**

* step1.Guidance Controller中有一个create boxes勾上
* step2.点击开始走几步后暂停，复制GuidanceBoxHolder，点击结束粘贴上去
* step3.勾上autoplay后线可以自动走

**LevelHolder铺路**

* step1.勾上Road Paver
* step2.同上面的step2

# 3.收集物

在Assets/Template文件夹中拖出Gem到地图中，关卡开始之后如果吃到再死亡就会显示当前吃了多少个钻石

**参数**

* fake：勾上之后会变成假钻石，吃不到



# 4.checkpoint

**RevivePosition**

* 线的复活位置
* 不要随便放，可能导致音画不同步

**CheckpointTrigger**

* 检查点的触发器



# 5.FallPredicter

**参数**

* Speed：速度（要和线的速度同步）
* Width：宽度
* Count：个数

在开始后想播放轨迹，可以把Line Renderer勾上



# 6.Pyramid

**OpenPyramid**

* 当线穿过此trigger，金字塔打开

**FinalTurn**

* 最终转向
* 如果直接进金字塔，可以隐藏掉

**WaitforWin**

* 进金字塔后多久会显示胜利界面

**StopPlayer**

* 进金字塔多久后线停止



# 7.事件

在player上添加gameevents脚本

* ongameawake在游戏启动时触发，比如添加directional light光强度
* onplayerstart在线移动的时候触发
* onchangedirection在线转弯的时候触发，可以做一些粒子（如滑雪特效）
* onleaveground在线离开地面的时候
* ontouchground在线基础地面的时候
* ongameover在线死亡的时候调用
* ongetgem在线吃到钻石的时候触发
* onplayerjump在线跳跃的时候触发

> 怎么让线跳跃？拖出来一个trigger，加上jump脚本



# 8.摄像机

也可以拖出来一个trigger，放在线的前面，加上camera trigger脚本

* offset：摄像机偏移
* rotation：摄像机朝向
* scale：离线的距离
* field of view：视场大小
* follow：是否跟随线
* duration：做这个动画所需时间
* ease：动画曲线
* mode：fast or fast beyond360



# 9.动画

可以先放一个obstacle，加上localposanimator脚本

**localposanimator**

* on animator start：动画启动事件
* on animator finished：动画结束事件
* transform type：new（默认）：从原位置移动到给出的位置，add：从原位置加上给出的位置
* trigger time：线开始移动后多少时间触发这个动画
* duration：所需要的时间
* offset time：勾上后表示达到trigger time的时候这个动画刚好做完
* don't revive：复活的时候不要恢复这个动画

**localrotanimator**

* 跟上面一样，只不过是针对旋转

**localscaleanimator**

* 跟上面一样，只不过是针对缩放

**触发器触发动画**

* 添加触发器
* 添加eventtrigger代码
  * invoke on awake：启动的时候触发事件
  * invoke on click:进入trigger还要点击才会触发
* 可以做一个obstacle动画设置好之后（要取消勾选triggered by time）然后在eventtrigger中拖进去obstacle选择localposanimator-->tirgger()



# 10.假线

**fakeplayer（记得获取线的初始位置）**

* is wall：碰到真线会死
* create turn trigger：用于记录假线何时转向
* sychronism player：跟真线同步转弯，不勾上的话是按p（key）转弯
* 加trigger：（让假线启动）在trigger中加fake player trigger选择刚才的假线，type的turn让线转向，set state是更改线的状态，如选moving就是开始移动
* 运行之后对于留下的假线，可以把fakeplayertriggerholder复制到主页面



# 11.触发器代码

**change direction**

* 更改线的移动方向

**gravity trigger**

* 改变重力

**jump**

* 跳跃
* power：跳跃力度
* add predict：线轨迹预测

**kill player**

* 杀死线

**play Animator**

* 播放帧动画

**play audio clip**

* 播放音频

**set active**

* active on awake：启动执行，比如对于ground可以显现出来/不显现出来

**set anbient**

* 更改环境光

**set fog**

* 是否使用雾气

**set image color**

* 可以先创建一个image：gameobject-->ui-->image
* 在image中stretch选择最右下角的，可以把top和bottom都改成0，就会把整个屏幕盖上，也可以该下颜色，要把raycast target关掉
* 在set image color中选择image，color就是颜色

**set light**

* 可以把rotation调成000

**set material color**

* 更改材质球的颜色
* 要让开始的时候变正常，可以在scenedata中设置初始颜色

**speed**

* 改速度，摄像机跟随速度也变快
* 不想让摄像机跟随变快？把set..speed关掉

**teleport**

* 传送（传送到一个位置or传送到一个空物体处）



# 12.补充

运行之后：

* 按d：隐藏/显示左上角信息
* 按k：自杀
* 按s：在线当前的位置生成触发器
* 按c：在控制台输出当前音乐时间，可以做相关动画





















































