## MOCK-KAKIN (honkai kakin-emulator)
这是一个基于angular5的崩坏3rd蛋池模拟器。

## 特性
1. 标配补给、装备补给和精准补给  
2. 自定义蛋池配置（任意物品及概率）  
3. 批量抽取配置（可用于验证）  
4. 几乎和游戏一致的界面风格，拥有保底机制并且默认开启。

## 应用地址
BAE:  
http://mockkakin.duapp.com  

Github Pages (备用) :  
https://dyingsunlight.github.io/mock-kakin/  

可配置的物品名称全部都可以在
[这里的目录找到](https://github.com/dyingsunlight/mock-kakin/tree/master/src/app/gacha/resources)  

## 部署流程
Mock-Kakin 可部署于静态服务器, 不需要动态的处理支持。
1. ``clone`` 或者 下载本项目源代码
2. ``npm install``  安装依赖项。
3. ``npm run start`` 启动开发者模式，可以直接开发并预览。
4. ``npm run build`` 执行默认发布，输出文件夹为 ``default``，应用入口为
``app-index.html``。如需部署在特定路径或者遇见资源路径错误的问题，请参见 ``package.json`` 中的 ``build-for-github`` 构建设置，配置好基础链接就可以。
5. ``可选``关于启用 preloader ，复制 ``preloader`` 文件夹内的所有文件到 ``app-index.html`` 同目录中
，使用``index.html``作为应用入口即可。  

**如果有部署疑问，或者遭遇问题，可以请提交issue**

## 优化
1. 所有的图片资源已经进行过有损的高压处理，无需再进行压缩。
2. 由于使用的图片资源较多，访问时会产生大量的请求数。
推荐在可能的情况时，为所有图片的Cache-Control设置尽可能长的max-age(图片资源几乎不会变动)。
能够有效的减少请求数量。
3. 推荐启用Preloader，能够有效提升加载时的用户体验。

## 概率算法：

1. **保底基础出货概率** 由于保底机制的存在，十连必定出货。因此设定为 10%",
2. **保底出货概率** = A级角色卡 + S级角色卡 或者是 4星武器 + 4星圣痕
3. **单抽出货概率** = **保底出货概率** - **保底基础出货概率**
4. 根据原始 **保底出货概率** 的比例，分配 **单抽出货概率**
到补给配置作为基础配置来源
5. 多次模拟器测试，不断修正补给配置，修改概率因子逼近游戏内的公示概率
6. 统计单抽不保底概率

### 标配补给
| 类别      | 单次抽取概率 | 保底概率(公示概率) |
|:-----------:|:--------------:|:--------------------:|
| S级女武神 | **0.94%**    | **1.5%**           |
| A级女武神 | **8.52%**    | **13.5%**          |

### 精准补给
| 类别      | 单次抽取概率 | 保底概率(公示概率) |
|:-----------:|:--------------:|:--------------------:|
| UP 武器   | **0.53%**    | **2.479%**         |
| 非UP 武器 | **0.53%**    | **2.479%**         |
| UP 圣痕   | **0.8%**     | **3.719%**         |
| 非UP圣痕  | **0.8%**     | **3.719%**         |

### 装备补给
| 类别      | 单次抽取概率 | 保底概率(公示概率) |
|:-----------:|:--------------:|:--------------------:|
| 武器      | **3.25%**    | **5.704%**         |
| 圣痕      | **4.83%**    | **8.556%**         |

### 扩充补给
| 类别      | 单次抽取概率 | 保底概率(公示概率) |
|:-----------:|:--------------:|:--------------------:|
| S级女武神 | **0.94%**    | **1.5%**           |
| A级德丽莎 | **2.77%**    | **4.5%**           |
| 其它      | **1.395%**   | **2.25%**          |
