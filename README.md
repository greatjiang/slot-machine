# slot-machine
1. h5老虎机抽奖小游戏
2. 代码没有优化，目前只是实现了抽奖滚动的功能（动态、可配）
3. 配置项speed circle 还有其它可根据实际情况随意配置
4. 接口配置项推荐
中奖接口
```
  {
    code:xxx,
    data:{
      result:[1,2,3],   //返回中奖礼物下标
      gift:{}           //对应中奖结果
    }
  }
```
5. 摇奖机礼物可根据接口动态配置
  目前礼物位置暂时用数字占位可根据实际情况更改
6. 代码中有注释