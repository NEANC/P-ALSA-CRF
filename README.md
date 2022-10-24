# Personal ALSA Custom Research Filter

个人的 [ALSA](https://github.com/LmeSzinc/AzurLaneAutoScript) 自定义科研过滤器

## ALAS 科研过滤器说明

文献来源：  
[ALAS WIKI 科研过滤器](https://github.com/LmeSzinc/AzurLaneAutoScript/wiki/filter_string_cn#%E7%A7%91%E7%A0%94%E8%BF%87%E6%BB%A4%E5%99%A8)

### 属性

`{series}-{genre}-{duration}`

### Series - 科研期数

| Series | 描述     |
| ------ | -------- |
| S1     | 一期科研 |
| S2     | 二期科研 |
| S3     | 三期科研 |
| S4     | 四期科研 |
| S5     | 五期科研 |

### Genre - 科研类型/舰船稀有度/定向研发中的舰船名称

#### 科研类型

| Genre | 描述               | 消耗（条件） |
| ----- | ------------------ | ------------ |
| Q     | 舰装解析           | 强化部件     |
| H     | 魔方解析(心智补全) | 心智魔方     |
| D     | 定向研发           | 物资         |
| G     | 资金募集           | 物资         |
| B     | 数据收集           | 通关主线     |
| C     | 基础研究           | 无           |
| E     | 试验品募集         | 分解装备     |
| T     | 研究委托           | 进行委托     |

#### 舰船稀有度

```
DR - 彩船
PRY - 金船
```

#### 定向研发中的舰船名称

[请自行查阅 ALAS WIKI](https://github.com/LmeSzinc/AzurLaneAutoScript/wiki/filter_string_cn#genre)

### Duration - 时间

`0.5 、 1 、 1.5 、 2 、 2.5 、 3 、 4 、 5 、 6 、 8 、 10 、 12`

### 内置名称

- `reset` 刷新科研列表。刷新后 Alas 将重新识别科研项目，并返回过滤器的头部重新查找。如果当天的刷新次数耗尽， Alas 将跳过 `reset`。
- `shortest` 时长最短的科研，相当于 `0.5 > 1 > 1.5 > 2 > 2.5 > 3 > 4 > 5 > 6 > 8 > 10 > 12`
- `cheapest` 消耗最低的科研，相当于 `Q1 > Q2 > T3 > T4 > Q4 > C6 > T6 > C8 > C12 > G1.5 > D2.5 > G2.5 > D5 > Q0.5 > G4 > D8 > H1 > H2 > H0.5 > D0.5 > H4`

注意：shortest 和 cheapest 必然会选择一个科研项目，在它们之后的内容将不会被执行。因此，建议科研过滤器以 `> reset > shortest ` 或 `> reset > cheapest ` 结尾，以保证充分利用刷新和防止空选。

#### ALAS 默认科研方案

```
S5-DR0.5 > S5-PRY0.5 > S5-H0.5 > S5-Q0.5 > S5-DR2.5 > 0.5 > S5-G1.5
> S5-Q1 > S5-DR5 > S5-DR8 > S5-G4 > S5-PRY2.5 > 1 > S5-Q2 > reset
> S5-G2.5 > S5-PRY5 > S5-PRY8 > 1.5 > 2 > S5-Q4 > 2.5 > 3
> Q4 > G4 > 4 > 5 > S5-C6 > C6 > 6 > S5-C8 > 8
> S5-C12 > 12
```

## 基于 碧蓝档案 WIKI 策略规划参考 的模板

**注意**:

- 一图流，只是简单给出三类参考策略，力图涵盖多数需求。**主要应用于四、五期科研。**
  - By.碧蓝航线 WIKI，有修改

在自定义科研过滤器内 **不设置时间** 可能会 **导致选择长时间的科研项目**，因此 **一图流内未标识时间** 项目的会被设置为 **0.5H**，请根据自身需求调整。

**提示**：  
在 ALAS 科研设置内选择

- **不使用魔方**时，会导致 `魔方解析(心智补全) H` 无效；
- **不使用物质**时，会导致 `资金募集 G` 无效；
- **不使用部件**时，会导致 `舰装解析 Q` 无效。

### 快均衡策略

基于 [碧蓝档案 WIKI 科研策略专题攻略 - 一图流 - 快均衡策略](https://wiki.biligame.com/blhx/%E7%A7%91%E7%A0%94%E7%AD%96%E7%95%A5%E4%B8%93%E9%A2%98%E6%94%BB%E7%95%A5#%E4%B8%80%E5%9B%BE%E6%B5%81) 的模板

## ![](https://patchwiki.biligame.com/images/blhx/0/0a/lj0yqsz6h4q0m1ghb3kqc1b39v9ap97.png)

#### 快均衡模板

```
DR-0.5 > Q-0.5 > PRY-0.5 > H-0.5
> DR-2.5 > > H-1 > Q-1
> DR-5 > Q-2 > G-1.5
> reset
> DR-8> > G-4 > H-2 > Q-4
> E-2 > G-2.5 > PRY-2.5
```

---

### 慢均衡策略

基于 [碧蓝档案 WIKI 科研策略专题攻略 - 一图流 - 慢均衡策略](https://wiki.biligame.com/blhx/%E7%A7%91%E7%A0%94%E7%AD%96%E7%95%A5%E4%B8%93%E9%A2%98%E6%94%BB%E7%95%A5#%E4%B8%80%E5%9B%BE%E6%B5%81) 的模板

![](https://patchwiki.biligame.com/images/blhx/0/09/0birkgxyq05hl8xo3w0btfdu7uebhxv.png)

#### 慢均衡模板

```
DR-0.5 > Q-0.5 > H-0.5 > PRY-0.5
> DR-2.5 > DR-8 > DR-5 > PRY-2.5
> G-4 > G-1.5 > G-2.5 > Q-1
> reset
> PRY-5 > Q-2 > PRY-8
```

---

### 重装备策略

基于 [碧蓝档案 WIKI 科研策略专题攻略 - 一图流 - 重装备策略](https://wiki.biligame.com/blhx/%E7%A7%91%E7%A0%94%E7%AD%96%E7%95%A5%E4%B8%93%E9%A2%98%E6%94%BB%E7%95%A5#%E4%B8%80%E5%9B%BE%E6%B5%81) 的模板

![](https://patchwiki.biligame.com/images/blhx/7/74/e2619kak8823p5oo3i6r7ybgqmu8uic.png)

#### 重装备模板

```
Q-0.5 > DR-0.5 > PRY-0.5
> Q-4 > Q-2 > Q-1
> G-4> G-1.5 > E-2
> reset
> DR-2.5> > PRY-2.5 > G-2.5
> H-0.5 > T-3 > H-1
```

**注意**:由于 ALAS 无法确定试验品募集(E)的品阶，因此不将其放在资金募集 1.5H(G-1.5H)前。

---

### 注意

碧蓝航线 WIKI 方案不适用于**单船与单期定向策略**  
如需要请自行修改

---

## 个人方案

这是我个人目前使用的方案  
基于慢均衡策略模板修改的  
我希望在获得图纸的同时，能获取四期科研装备

### ALAS 科研设置

| 设置项             | 选项                                  |
| ------------------ | ------------------------------------- |
| 使用魔方           | 总是使用                              |
| 使用物质           | 总是使用                              |
| 使用部件           | 总是使用/无项目可做时(部件不足时使用) |
| 资源不足时延迟科研 | 勾选                                  |
| 科研过滤器         | 自定义                                |

- 自定义科研过滤器

```
DR-0.5 > S4-Q-0.5 > S4-H-0.5 > PRY-0.5
> DR-2.5 > DR-8 > DR-5 > PRY-2.5
> S4-G-4 > S4-G-1.5 > S4-G-2.5 > S4-Q-1
> PRY-5 > S4-Q-2 > PRY-8
> 12
> reset > cheapest
```

**注意**：
如不想切魔方可在 **ALAS 科研设置** 内设置 **不使用魔方**

## 文献来源

- [碧蓝档案 WIKI 科研策略专题攻略](https://wiki.biligame.com/blhx/%E7%A7%91%E7%A0%94%E7%AD%96%E7%95%A5%E4%B8%93%E9%A2%98%E6%94%BB%E7%95%A5)
- [ALAS WIKI Research Filter String [CN]](https://github.com/LmeSzinc/AzurLaneAutoScript/wiki/filter_string_cn)

## License

[![CC-BY-NC-4.0](https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/by-nc.svg)](https://creativecommons.org/licenses/by-nc/4.0/legalcode)
