# 为 deepin 提供第一方 AppStream 支持

- 提案发起时间：2024-05-27
- 提案拉取请求：https://github.com/deepin-community/rfcs/pull/11

## 概要

AppStream 是当前被广泛支持的 FreeDesktop 规范，旨在通过标准化的元数据集来使得发行版更好的对用户呈现应用程序的对应信息。deepin 应当主动提供 AppStream 元信息的多个方面的支持。

## 动机

AppStream 目前已经被包括 [Flatpak](https://docs.flatpak.org/en/latest/conventions.html#metainfo-files)、[Snapcraft](https://snapcraft.io/docs/using-external-metadata#heading--appstream)、[AppImage](https://docs.appimage.org/packaging-guide/optional/appstream.html) 在内的项目所直接支持，且被包括 [Arch Linux](https://archlinux.org/packages/extra/any/archlinux-appstream-data/)、[Debian](https://wiki.debian.org/AppStream#How_to_obtain_the_data.3F)、[Fedora](https://src.fedoraproject.org/rpms/appstream-data) 在内的各大发行版支持。一些社区项目也提供了基于 AppStream 的应用信息展示服务与在线应用（注：不同于软件包）检索服务（如 [KDE](https://apps.kde.org/) 与 [PureOS](https://software.pureos.net/sw/deepin-voice-recorder.desktop)）。

尽管 AppStream 的初衷在于供应用商店类的应用展示其所需要的应用元信息，但其也可以用于诸多用于“实现应用商店类应用”之外的场景的需求。主动支持 AppStream 对 deepin 项目有诸多益处，包括：

1. 主动声明应用与组件自身的信息，在第三方移植与收录我们的应用时，可以呈现我们主动提供的描述文字、截图、应用组件 ID、变更日志、官网等各种信息
2. 主动声明组件的必要性，例如声明文管为 DDE 的必要组件，来避免用户从应用商店卸载应用时导致 DDE 环境被破坏（同时，我们也可以规避硬编码此类信息）
3. 对于描述类文字，可以更方便的进行本地化，由社区一同进行文本翻译
4. 便于我们自动化生成第一方应用的介绍页面（替代 <https://www.deepin.org/original/> 与 <https://www.deepin.org/acknowledgments/>）
5. 便于我们自身收录与展示第三方应用的元信息（[Linyaps（玲珑）商店](https://store.linglong.dev/) 目前只有图标和名称）
6. 便于第三方应用商店（例如 [dde-store](https://github.com/UbuntuDDE/dde-store)）移植到 deepin
7. 规避由于[通过主动覆盖 desktop 文件的方式干预应用行为](https://github.com/linuxdeepin/deepin-deb-fix)影响 `dpkg -S` 导致的卸载行为的[主动特判](https://github.com/linuxdeepin/dde-application-wizard/pull/21)
8. 便于第三方应用商店展示 Linyaps 应用并提供进一步相关集成

## 详细设计

AppStream 的支持需要从多个方面分别进行：

### 确立基本 Guideline 并编写指南文档

- desktop 文件名称应当为 [reverse-DNS 命名形式](https://en.wikipedia.org/wiki/Reverse_domain_name_notation)，应用可为 `org.deepin.music.desktop`，桌面组件可为 `org.deepin.dde.controlcenter.desktop`。
- component ID 一般与主 desktop 文件保持一致，并提供对应元信息文件，例如 `org.deepin.dde.controlcenter.appdata.xml`。
- `<developer>` 标签填写 `id="org.deepin"`，名称使用 `deepin Community`。
- 不应被卸载的桌面核心组件应当主动声明 `<compulsory_for_desktop>DDE</compulsory_for_desktop>`。
- 截图（可选）由 `linuxdeepin/product-screenshots` 项目进行管理，目录结构使用 `<组件ID>/<大版本号>/纯英文文件名.格式` 结构，可通过 `https://www.deepin.org/index/docs/product-screenshots/<对应路径>` 访问（注：此 URL 要求上线后不可变化）。
- 元信息文件应当通过 `appstreamcli validate` 检测。

其它社区可供参考的指南文档：[KDE: Guidelines and HOWTOs/AppStream](https://community.kde.org/Guidelines_and_HOWTOs/AppStream)

### 第一方应用程序/组件主动提供 AppStream 元信息文件（Upstream Metadata）

deepin 第一方项目与桌面组件应当主动提供 AppStream 元信息文件，文件内容规则参见上一个段落。

第一方 AppStream 元信息应当至少包括使 `appstreamcli validate` 通过检测的必要字段。其余字段为选填，但建议填写。应用的概要介绍、描述信息、截图由运营小组提供。

### deepin 发行版

1. 提供 AppStream 相关软件包（高于 1.0 版本）
2. 生成并以软件包（和/或在线）的形式提供 Catalog Metadata
3. 提供“深度原创应用”清单（置于 `/usr/share/swcatalog/xml/`）

### 官网 deepin 原创应用、致谢页面

改由 Catalog Metadata 与 Upstream Metadata 生成。

### Linyaps 主动支持 AppStream 规范

1. 第三方应用提交时，接受并使用应用自身附带的 AppStream 信息
2. Linyaps 第一方在 `/var/lib/linglong/appstream/` 下提供 Catalog Metadata（且 [bundle](https://freedesktop.org/software/appstream/docs/chap-CatalogData.html#tag-ct-bundle) 使用 `linglong` 名称）
3. （可选，建议）向 appstreamcli 上游提供与 Linyaps 相关的集成，例如提供 `AS_POOL_FLAG_LOAD_LINGLONG`、`as_pool_register_linglong_dir()`、`exec_linglong_action()` 等支持

## 提案弊端

暂无

## 遗留问题

暂无

## 替代方案

### “深度原创应用”清单

上述提到了多个方面，其中，“深度原创应用”清单本身不一定需要以 AppStream 形式提供。关于此点，上述提案所述方案与 GNOME 采取的方案近似。GNOME 由 gnome-software 软件包在 `/usr/share/swcatalog/xml/` 下提供了 org.gnome.Software.Featured.xml 与 org.gnome.Software.Curated.xml 文件，为相关软件追加 `GnomeSoftware::FeatureTile` 自定义属性以及 `GnomeSoftware::popular` “荣誉”标签，旨在允许供应商对应用商店展示的对应类型应用的推荐列表进行定制化。若我们不需要此类定制化内容，也可单纯的固定提供一个列表来表示需要在官网展示的深度原创应用清单，而应用的介绍内容仍保持通过 AppStream 获取。
