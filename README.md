# [![](https://github.com/Jeffreytsai1004/Hermes/raw/main/assets/hermes_icon.png?raw=true)](https://github.com/Jeffreytsai1004/Hermes/blob/main/assets/hermes_icon.png?raw=true)Unreal Engine 的 Hermes URL

[](https://github.com/Jeffreytsai1004/Hermes#-hermes-urls-for-unreal-engine)

Hermes URLs 是虚幻引擎的一个插件，开箱即用，允许您将 URL 复制到项目中的任意资产，并与您的团队共享它们，例如通过 Slack。然后，这些链接将直接打开指向链接资源的虚幻编辑器。

此外，Hermes 还提供了易于使用的 API 来注册您自己的终端节点，以便您可以在编辑器中创建其他直接深度链接。例如，您可以创建运行自动测试的链接，直接链接到设置页面，或者其他任何您喜欢的东西！

非常感谢 Krista A. Leemhuis 的精彩图标！

## 设置

[](https://github.com/Jeffreytsai1004/Hermes#setup)

Hermes 正式支持 UE5，并向后兼容 UE4 4.27 版。欢迎支持旧版本的拉取请求。

1.  将此仓库克隆到项目的文件夹中`Plugins`
2.  启动编辑器 - 编辑器首次启动时会自动注册 URL

默认情况下，Hermes 将注册与项目名称匹配的 URI。如果您需要对这些 URI 使用的方案进行更多控制，您可以使用位于 旁边的插件，它允许您在 URI 方案中包含分支名称。你需要在 .uproject 中启用，然后你可以转到 Edit > Preferences，然后在 Plugins 找到“Hermes URLs - Branch Support”进行配置。`HermesBranchSupport``HermesCore``HermesBranchSupport`

Hermes 依靠 [hermes\_urls](https://github.com/jorgenpt/hermes_urls) 向 OS 注册并调度 URL 请求。这是一个小型的 Rust 项目，为了方便起见，它的二进制文件被签入到这个仓库中（在 [HermesCore/Source/HermesURLHandler](https://github.com/Jeffreytsai1004/Hermes/blob/main/HermesCore/Source/HermesURLHandler) 中），但如果从互联网下载 EXE 文件让你感到（可以理解的）不安，请随时查看源代码并构建你自己的。

## 用

[](https://github.com/Jeffreytsai1004/Hermes#using)

设置 Hermes 后，您应该能够在内容浏览器中右键单击任何资源，并看到一个新的“_Copy URL that reveal asset（显示资源的复制 URL_）”选项：

[![](https://github.com/Jeffreytsai1004/Hermes/raw/main/README_contentbrowser.png?raw=true)](https://github.com/Jeffreytsai1004/Hermes/blob/main/README_contentbrowser.png?raw=true)

同样，当您在资源编辑器中打开任何资源时，您应该会在菜单栏的“资源”选项中看到一个新的“_复制打开资源的 URL_”选项：

[![](https://github.com/Jeffreytsai1004/Hermes/raw/main/README_asseteditor.png?raw=true)](https://github.com/Jeffreytsai1004/Hermes/blob/main/README_asseteditor.png?raw=true)

## 扩展

[](https://github.com/Jeffreytsai1004/Hermes#extending)

Hermes 旨在实现高度可定制和扩展。如果您有任何问题，请随时[与我们联系](mailto:jorgen@tjer.no)，如果您认为您的功能应该成为 Hermes 核心体验的一部分，请发送拉取请求！

### 使用您自己的功能创建自定义 URL

[](https://github.com/Jeffreytsai1004/Hermes#creating-custom-urls-with-your-own-functionality)

要了解如何为自定义 URL 创建自己的处理程序，您可以查看 [HermesContentEndpoint.cpp](https://github.com/Jeffreytsai1004/Hermes/blob/main/HermesCore/Source/HermesContentEndpoint/Private/HermesContentEndpoint.cpp)，即 asset links 的实现。允许您将这些链接复制到剪贴板的编辑器集成位于 [HermesContentEndpointEditorExtension.cpp](https://github.com/Jeffreytsai1004/Hermes/blob/main/HermesCore/Source/HermesContentEndpoint/Private/HermesContentEndpointEditorExtension.cpp) 中。

你可以在自己的项目中创建一个类似的模块，并依赖于你的模块，你应该很高兴。`HermesServer`

### 控制您的链接具有的 URL 方案/协议

[](https://github.com/Jeffreytsai1004/Hermes#controlling-what-url-scheme--protocol-your-links-have)

如果您想对 URL 方案/协议有更多的控制权，而不是 and 为您提供的，您可以创建自己的 .它是一个非常小的 C++ 接口，您可以将其注册为模块化功能 —— 您需要实现的只是一个方法。您可以使用 [HermesBranchSupport.cpp](https://github.com/Jeffreytsai1004/Hermes/blob/main/HermesBranchSupport/Source/HermesBranchSupport/Private/HermesBranchSupport.cpp) 作为开发自己的 URI 方案的起点，以覆盖所使用的 URI 方案。`Hermes``HermesBranchSupport``IHermesUriSchemeProvider``TOptional<FString> GetPreferredScheme()``IHermesUriSchemeProvider`

## 许可证

[](https://github.com/Jeffreytsai1004/Hermes#license)

[该图标](https://github.com/Jeffreytsai1004/Hermes/blob/main/assets/hermes_icon.png)版权归 （c） 2022 [Jørgen P. Tjernø](mailto:jorgen@tjer.no) 所有。保留所有权利。

Hermes URLs 根据以下任一

-   Apache 许可证，版本 2.0 （[许可证 - APACHE](https://github.com/Jeffreytsai1004/Hermes/blob/main/LICENSE-APACHE) 或 [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0))
-   MIT 许可证 （[许可证 - MIT](https://github.com/Jeffreytsai1004/Hermes/blob/main/LICENSE-MIT) 或 [http://opensource.org/licenses/MIT](http://opensource.org/licenses/MIT))

由您选择。

## 贡献

[](https://github.com/Jeffreytsai1004/Hermes#contribution)

除非您另有明确说明，否则任何有意提交的贡献 为了包含在您的作品中，如 Apache-2.0 许可证中所定义，应为 双重许可，无任何其他附加条款或条件。
