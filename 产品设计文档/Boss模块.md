# Boss模块


##  BOSS属性


*  `Id`  主键
*  `name` 名称
*  `hp ` 血量
*  `type` 类型
*  `intensity`  强度
*  `rewards`   奖励

# BOSS `BossService`

* 描述了获取BOSS，BOSS的当前血量，更新BOSS血量和BOSS的击杀者

##  获取BOSS  

`Boss[] getByBossIds(String ids);`


  * 通过id字符串获取boss数组，ids 若干个id拼成的字符串，用逗号隔开
   
  支持批量获取


## 获取和更新BOOS的血量


* 更新BOOS的血量 

` int attack(int bossId, int damage, String playerId);*`

    
** 描述角色对BOOS的伤害量 ，从而更新BOSS的血量

       
*获取BOOS当前的血量 

` int getCurrentHP(int bossId, String playerId);*`
        
** 通过计算来获取BOOS的血量



##  BOSS最后击杀者 

` SgpPlayer getLastAttackPlayer(int bossId)`
      
* 获取BOSS的血量 如果大于等于0 说明BOOS还存在
* 获取角色，如果角色不存在，提示用户‘击杀角色不存在’，否则当前角色就是boss击杀者 
