Event-Recommendation分析建模
==

## 1.data set 介绍 ##

 - users.csv
 - event.csv
 - user_friends.csv
 - event_attendees.csv
 - train.csv
 - test.csv

字段详情：
**train.csv**
 - user_id：用户的ID号
 - event_id：活动的ID号
 - invited：是否受邀请
 - timestamp：这一条活动信息被用户看到的时间点
 - interested/not_interested：用户是否反馈了感兴趣与否

**users.csv**

 - user_id：用户的ID号
 - locale：地理信息
 - birthday：用户生日
 - gender：性别
 - joinedAt：用户第一次使用这个APP的时间
 - location：地理信息

**user_friends.csv**

 - user_is:用户ID
 - user friends id:用户朋友的id,为一个list

**events.csv**

 - event_id:活动ID
 - user_id:用户ID
 - start_time:活动预计开始时间
 - city:活动举办城市
 - state:活动举办的洲
 - zip:邮编
 - country:活动举办的国家
 - lat:经度
 - Ing:纬度
 - count_1 ---count_N：对活动描述的单词去掉时态语态后，统计词频后，取前N（前100个）个词的词频
 - count_other:后100个

**event_attendees.csv**

 - event_id:活动ID
 - yes:是否参加活动
 - maybe:
 - invited:
**解决思路分析**
我们有这几类数据：
 - 用户的历史数据
 - event相关数据
 - 用户社交数据

协同过滤是基于用户-event 历史交互数据，我们把社交数据和event相关信息作为影响最后结果的因素纳入考量。
我们把推荐问题转化成每一个人对每一个event是否感兴趣，感兴趣/不感兴趣 ，是一个target，其他影响结果作为feature。
同时feature里面也包含由协同过滤产生的推荐度。
**工业界标准做法：**
构建如下特征，我们构造的是有监督学习的问题，用机器学习的方法去建模。
 - user-baseed协同过滤对event推荐度
 - item-based协同过滤对event推荐度
 - 活动的热度
 - 用户社交活跃度
 - 朋友对用户的影响度
 - 等等.......

最后得出每个用户对每个event感兴趣的概率。
从而构建一个推荐模型。
