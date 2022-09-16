# yanglegeyang
羊了个羊在线版

## 功能

1. 去广告  
[george-jiang-wow](https://github.com/george-jiang-wow/yanglegeyang)实现的
2. 快速通关  
[george-jiang-wow](https://github.com/george-jiang-wow/yanglegeyang)实现的
3. 直接下一关  
[george-jiang-wow](https://github.com/george-jiang-wow/yanglegeyang)实现的
4. 初始100道具  
我实现的

## 体验
访问 https://hwhaocool.github.io/yanglegeyang-magic/ 

## 教你怎么修改

### 道具-初始化数量

文件`index.0df91.js` 搜索 `e.prototype.initGameUi`

在这里我设置了三个道具每个数量都是100

```
this.userData.prop_cancel = 100;
this.userData.prop_random = 100;
this.userData.prop_remove = 100;
```

### 道具-使用判断逻辑
以随机道具举例说明


文件`index.0df91.js` 搜索 `randomEndFunc`

```js
// 获取道具
if (!this.isMoving) {
    if (this.randomMask.activeInHierarchy) {
        cc.game.emit(s.EMITKEY.SHOWMAINTIPS, "每关只能使用一次哦");
    } else {
        if (this.userData.prop_random >= 1) {
        var t = this.chessboardNode.getComponent(h.default).updateBlockArea();
    
        if (console.log("isOk ###### ", t), t) {
            {
            l.default.playAudioMusic("audio/sound/random.mp3", !1);
            this.userData.prop_random--;
            d.default.getInstance().reportProperty.random_use++;
            d.default.getInstance().sheepMark.propRandomCount++;
            0 == d.default.getInstance().reportProperty.random_ad && console.log("使用初始道具 ###### propRandom");
            }
            var e = N.default.getTAUserInfo();
            {
            e.item_name = "洗牌道具";
            v.default.reportTACommon("prop_initial", e);
            c.default.saveUserData(this.userData);
            this.setGameLayerUiData();
            d.default.getInstance().levelWinDict.random += 1;
            }

            //这里扣减道具数量，
            //注释掉就是道具数量不减少
            // 改为+1 就是越用越多
            var o = this.userData.prop_random - 1;
            o < 0 && (o = 0);
        }
        } else {
        // 没有看广告之前会进入这里
        console.log("洗牌道具不足");
        this.showPropPop(3, 10);
        }
    }
    }
```