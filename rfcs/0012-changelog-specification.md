# 统一的changelog版本号规范

- 提案发起时间：2024-07-25
- 提案拉取请求：https://github.com/deepin-community/rfcs/pull/12

## 概要

当前版本号管理较为混乱，各场景下的规则并未明细，应该提供统一的版本号规范

## 动机

明确版本号规范标记软件包修改信息、来源，方便通过版本号追踪与上游版本差异，提供更合理的rebuild版本机制。

## 详细设计


**changelog版本规范**

`upstreamversion-${ver1}deepin${ver2}`

#### 1. 假设上游项目打包版本号为 x.y.z ，deepin打包版本则为 `x.y.z-${ver1}deepin${ver2}` 
 ver1：ver1为0时表示 deepin自行打包的上游软件，ver1不为0时表示来自上游的quilt软件包自带的-ver版本
 ver2：表示来自deepin社区的patch数量，依次递增，可为空

#### 2. 来自deepin community自行打包的上游软件 以0deepin开头标识，若该项目添加了来自deepin的patch则以deepin1 标识，依次累加, 版本号形式x.y.z-0deepin1 , 若上游已经添加-2这类版本号，版本号则为 x.y.z-2deepin1

#### 3. 集成native软件包
将native软件包直接改成quilt格式存在一些changelog版本格式不兼容问题
因此重新修订native版本规范，形式为 `upstreamversiondeepin${ver2}`
native软件包没有-的连字符，因此直接在上游版本号后deepin${ver2} 标记来自deepin的修改

#### 4.  CI自动构建版本号 `x.y.z-${ver1}deepin${ver2}+u001+rb1`，001为距离上一次修改changelog的commit次数，rb1为rebuild次数，依次累加
> [!WARNING]
> 注：commit版本号使用仅限于开发阶段自测验证，不应流转到集成阶段

#### 5. rebuild版本号规范
上文一二条保持不变，若存在需要rebuild软件包，

##### quilt软件包rebuild规范：

情况1：ver2不为空时直接+rb{ver}后缀，表现形式为`x.y.z-1deepin1+rb1`

情况1：ver2为空时的rebuild版本ver2默认为0，表现形式为
  `x.y.z-1deepin0+rb1`
  
##### native软件包rebuild规范：

情况1：ver2不为空时直接+rb{ver}后缀，表现形式为`x.y.zdeepin1+rb1`

情况1：ver2为空时的rebuild版本ver2默认为0，表现形式为
  `x.y.zdeepin0+rb1`

> [!WARNING]
> 注：rebuild版本号使用仅限于依赖包升级，相关依赖树需要基于新版本构建编译的场景使用

> [!WARNING]
> 注：如无特殊情况所有的rebuild版本应该在构建系统中修改，不应该提交到代码存储库中

> [!TIP]
> 注： deepin0版本的用意是为了方便后续的更新迭代，按照版本号规则 deepin+rb1版本大于deepin1+rb1，所以使用deepin0后缀方便后续维护

#### 6. 安全更新版本规范：

对于相同版本软件包需要在两个以上的版本中做安全更新(例如 v23 and v26)时，为确保版本号正确，必须大于当前软包版本且小于后续发行版中的软件包版本，请示在版本号后缀中添加+deb${version}u${num}形式
对于v23版本 `upstreamversion-${ver1}deepin${ver2}+deb23u1` 对于v26版本 `upstreamversion-${ver1}deepin${ver2}+deb26u1` ，对于后续的更新，$num值都应当累加，由于版本号形式较多建议使用 `dpkg --compare-versions` 验证版本号是否符合要求 

> [!TIP]
> 注： 历史遗留的版本号不在本次讨论范围内，新的提交的软件包构建集成等应遵循新版本规范


