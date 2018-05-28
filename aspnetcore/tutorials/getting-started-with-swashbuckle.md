---
title: Swashbuckle 和 ASP.NET Core 入门
author: zuckerthoben
description: 了解如何将 Swashbuckle 添加到 ASP.NET Core web API 项目中以集成 Swagger UI。
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 05/08/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: tutorials/get-started-with-swashbuckle
ms.openlocfilehash: 0eb9aa12419cc09899af6bc85dd32a85687dab62
ms.sourcegitcommit: 9bc34b8269d2a150b844c3b8646dcb30278a95ea
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2018
---
# <a name="get-started-with-swashbuckle-and-aspnet-core"></a><span data-ttu-id="5910d-103">Swashbuckle 和 ASP.NET Core 入门</span><span class="sxs-lookup"><span data-stu-id="5910d-103">Get started with Swashbuckle and ASP.NET Core</span></span>

<span data-ttu-id="5910d-104">作者：[Shayne Boyer](https://twitter.com/spboyer) 和 [Scott Addie](https://twitter.com/Scott_Addie)</span><span class="sxs-lookup"><span data-stu-id="5910d-104">By [Shayne Boyer](https://twitter.com/spboyer) and [Scott Addie](https://twitter.com/Scott_Addie)</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="5910d-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="5910d-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="5910d-106">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="5910d-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>
::: moniker-end

<span data-ttu-id="5910d-107">Swashbuckle 有三个主要组成部分：</span><span class="sxs-lookup"><span data-stu-id="5910d-107">There are three main components to Swashbuckle:</span></span>

* <span data-ttu-id="5910d-108">[Swashbuckle.AspNetCore.Swagger](https://www.nuget.org/packages/Swashbuckle.AspNetCore.Swagger/)：将 `SwaggerDocument` 对象公开为 JSON 终结点的 Swagger 对象模型和中间件。</span><span class="sxs-lookup"><span data-stu-id="5910d-108">[Swashbuckle.AspNetCore.Swagger](https://www.nuget.org/packages/Swashbuckle.AspNetCore.Swagger/): a Swagger object model and middleware to expose `SwaggerDocument` objects as JSON endpoints.</span></span>

* <span data-ttu-id="5910d-109">[Swashbuckle.AspNetCore.SwaggerGen](https://www.nuget.org/packages/Swashbuckle.AspNetCore.SwaggerGen/)：从路由、控制器和模型直接生成 `SwaggerDocument` 对象的 Swagger 生成器。</span><span class="sxs-lookup"><span data-stu-id="5910d-109">[Swashbuckle.AspNetCore.SwaggerGen](https://www.nuget.org/packages/Swashbuckle.AspNetCore.SwaggerGen/): a Swagger generator that builds `SwaggerDocument` objects directly from your routes, controllers, and models.</span></span> <span data-ttu-id="5910d-110">它通常与 Swagger 终结点中间件结合，以自动公开 Swagger JSON。</span><span class="sxs-lookup"><span data-stu-id="5910d-110">It's typically combined with the Swagger endpoint middleware to automatically expose Swagger JSON.</span></span>

* <span data-ttu-id="5910d-111">[Swashbuckle.AspNetCore.SwaggerUI](https://www.nuget.org/packages/Swashbuckle.AspNetCore.SwaggerUI/)：Swagger UI 工具的嵌入式版本。</span><span class="sxs-lookup"><span data-stu-id="5910d-111">[Swashbuckle.AspNetCore.SwaggerUI](https://www.nuget.org/packages/Swashbuckle.AspNetCore.SwaggerUI/): an embedded version of the Swagger UI tool.</span></span> <span data-ttu-id="5910d-112">它解释 Swagger JSON 以构建描述 Web API 功能的可自定义的丰富体验。</span><span class="sxs-lookup"><span data-stu-id="5910d-112">It interprets Swagger JSON to build a rich, customizable experience for describing the Web API functionality.</span></span> <span data-ttu-id="5910d-113">它包括针对公共方法的内置测试工具。</span><span class="sxs-lookup"><span data-stu-id="5910d-113">It includes built-in test harnesses for the public methods.</span></span>

## <a name="package-installation"></a><span data-ttu-id="5910d-114">包安装</span><span class="sxs-lookup"><span data-stu-id="5910d-114">Package installation</span></span>

<span data-ttu-id="5910d-115">可以使用以下方法来添加 Swashbuckle：</span><span class="sxs-lookup"><span data-stu-id="5910d-115">Swashbuckle can be added with the following approaches:</span></span>

### <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="5910d-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5910d-116">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="5910d-117">从“程序包管理器控制台”窗口：</span><span class="sxs-lookup"><span data-stu-id="5910d-117">From the **Package Manager Console** window:</span></span>
  * <span data-ttu-id="5910d-118">转到“视图” > “其他窗口” > “程序包管理器控制台”</span><span class="sxs-lookup"><span data-stu-id="5910d-118">Go to **View** > **Other Windows** > **Package Manager Console**</span></span>
  * <span data-ttu-id="5910d-119">导航到包含 TodoApi.csproj 文件的目录</span><span class="sxs-lookup"><span data-stu-id="5910d-119">Navigate to the directory in which the *TodoApi.csproj* file exists</span></span>
  * <span data-ttu-id="5910d-120">请执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="5910d-120">Execute the following command:</span></span>

    ```powershell
    Install-Package Swashbuckle.AspNetCore
    ```

* <span data-ttu-id="5910d-121">从“管理 NuGet 程序包”对话框中：</span><span class="sxs-lookup"><span data-stu-id="5910d-121">From the **Manage NuGet Packages** dialog:</span></span>
  * <span data-ttu-id="5910d-122">右键单击“解决方案资源管理器” > “管理 NuGet 包”中的项目</span><span class="sxs-lookup"><span data-stu-id="5910d-122">Right-click the project in **Solution Explorer** > **Manage NuGet Packages**</span></span>
  * <span data-ttu-id="5910d-123">将“包源”设置为“nuget.org”</span><span class="sxs-lookup"><span data-stu-id="5910d-123">Set the **Package source** to "nuget.org"</span></span>
  * <span data-ttu-id="5910d-124">在搜索框中输入“Swashbuckle.AspNetCore”</span><span class="sxs-lookup"><span data-stu-id="5910d-124">Enter "Swashbuckle.AspNetCore" in the search box</span></span>
  * <span data-ttu-id="5910d-125">从“浏览”选项卡中选择“Swashbuckle.AspNetCore”包，然后单击“安装”</span><span class="sxs-lookup"><span data-stu-id="5910d-125">Select the "Swashbuckle.AspNetCore" package from the **Browse** tab and click **Install**</span></span>

### <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="5910d-126">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="5910d-126">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="5910d-127">右键单击“Solution Pad” > “添加包...”中的“包”文件夹</span><span class="sxs-lookup"><span data-stu-id="5910d-127">Right-click the *Packages* folder in **Solution Pad** > **Add Packages...**</span></span>
* <span data-ttu-id="5910d-128">将“添加包”窗口的“源”下拉列表设置为“nuget.org”</span><span class="sxs-lookup"><span data-stu-id="5910d-128">Set the **Add Packages** window's **Source** drop-down to "nuget.org"</span></span>
* <span data-ttu-id="5910d-129">在搜索框中输入“Swashbuckle.AspNetCore”</span><span class="sxs-lookup"><span data-stu-id="5910d-129">Enter "Swashbuckle.AspNetCore" in the search box</span></span>
* <span data-ttu-id="5910d-130">从结果窗格中选择“Swashbuckle.AspNetCore”包，然后单击“添加包”</span><span class="sxs-lookup"><span data-stu-id="5910d-130">Select the "Swashbuckle.AspNetCore" package from the results pane and click **Add Package**</span></span>

### <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="5910d-131">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5910d-131">Visual Studio Code</span></span>](#tab/visual-studio-code)

<span data-ttu-id="5910d-132">从“集成终端”中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="5910d-132">Run the following command from the **Integrated Terminal**:</span></span>

```console
dotnet add TodoApi.csproj package Swashbuckle.AspNetCore
```

### <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="5910d-133">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="5910d-133">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="5910d-134">运行下面的命令：</span><span class="sxs-lookup"><span data-stu-id="5910d-134">Run the following command:</span></span>

```console
dotnet add TodoApi.csproj package Swashbuckle.AspNetCore
```

---

## <a name="add-and-configure-swagger-middleware"></a><span data-ttu-id="5910d-135">添加并配置 Swagger 中间件</span><span class="sxs-lookup"><span data-stu-id="5910d-135">Add and configure Swagger middleware</span></span>

<span data-ttu-id="5910d-136">将 Swagger 生成器添加到 `Startup.ConfigureServices` 方法中的服务集合中：</span><span class="sxs-lookup"><span data-stu-id="5910d-136">Add the Swagger generator to the services collection in the `Startup.ConfigureServices` method:</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="5910d-137">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup2.cs?name=snippet_ConfigureServices&highlight=8-11)]</span><span class="sxs-lookup"><span data-stu-id="5910d-137">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup2.cs?name=snippet_ConfigureServices&highlight=8-11)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="5910d-138">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Startup2.cs?name=snippet_ConfigureServices&highlight=9-12)]</span><span class="sxs-lookup"><span data-stu-id="5910d-138">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Startup2.cs?name=snippet_ConfigureServices&highlight=9-12)]</span></span>
::: moniker-end

<span data-ttu-id="5910d-139">导入以下命名空间以使用 `Info` 类：</span><span class="sxs-lookup"><span data-stu-id="5910d-139">Import the following namespace to use the `Info` class:</span></span>

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup2.cs?name=snippet_InfoClassNamespace)]

<span data-ttu-id="5910d-140">在 `Startup.Configure` 方法中，启用中间件为生成的 JSON 文档和 Swagger UI 提供服务：</span><span class="sxs-lookup"><span data-stu-id="5910d-140">In the `Startup.Configure` method, enable the middleware for serving the generated JSON document and the Swagger UI:</span></span>

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup2.cs?name=snippet_Configure&highlight=4,8-11)]

<span data-ttu-id="5910d-141">启动应用，并导航到 `http://localhost:<port>/swagger/v1/swagger.json`。</span><span class="sxs-lookup"><span data-stu-id="5910d-141">Launch the app, and navigate to `http://localhost:<port>/swagger/v1/swagger.json`.</span></span> <span data-ttu-id="5910d-142">生成的描述终结点的文档显示在 [Swagger 规范 (swagger.json)](xref:tutorials/web-api-help-pages-using-swagger#swagger-specification-swaggerjson) 中。</span><span class="sxs-lookup"><span data-stu-id="5910d-142">The generated document describing the endpoints appears as shown in [Swagger specification (swagger.json)](xref:tutorials/web-api-help-pages-using-swagger#swagger-specification-swaggerjson).</span></span>

<span data-ttu-id="5910d-143">可在 `http://localhost:<port>/swagger` 找到 Swagger UI。</span><span class="sxs-lookup"><span data-stu-id="5910d-143">The Swagger UI can be found at `http://localhost:<port>/swagger`.</span></span> <span data-ttu-id="5910d-144">通过 Swagger UI 浏览 API，并将其合并其他计划中。</span><span class="sxs-lookup"><span data-stu-id="5910d-144">Explore the API via Swagger UI and incorporate it in other programs.</span></span>

> [!TIP]
> <span data-ttu-id="5910d-145">要在应用的根 (`http://localhost:<port>/`) 处提供 Swagger UI，请将 `RoutePrefix` 属性设置为空字符串：</span><span class="sxs-lookup"><span data-stu-id="5910d-145">To serve the Swagger UI at the app's root (`http://localhost:<port>/`), set the `RoutePrefix` property to an empty string:</span></span>
>
> [!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup3.cs?name=snippet_UseSwaggerUI&highlight=4)]

## <a name="customize--extend"></a><span data-ttu-id="5910d-146">自定义和扩展</span><span class="sxs-lookup"><span data-stu-id="5910d-146">Customize & extend</span></span>

<span data-ttu-id="5910d-147">Swagger 提供了为对象模型进行归档和自定义 UI 以匹配你的主题的选项。</span><span class="sxs-lookup"><span data-stu-id="5910d-147">Swagger provides options for documenting the object model and customizing the UI to match your theme.</span></span>

### <a name="api-info-and-description"></a><span data-ttu-id="5910d-148">API 信息和说明</span><span class="sxs-lookup"><span data-stu-id="5910d-148">API info and description</span></span>

<span data-ttu-id="5910d-149">传递给 `AddSwaggerGen` 方法的配置操作会添加诸如作者、许可证和说明的信息：</span><span class="sxs-lookup"><span data-stu-id="5910d-149">The configuration action passed to the `AddSwaggerGen` method adds information such as the author, license, and description:</span></span>

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup4.cs?name=snippet_AddSwaggerGen)]

<span data-ttu-id="5910d-150">Swagger UI 显示版本的信息：</span><span class="sxs-lookup"><span data-stu-id="5910d-150">The Swagger UI displays the version's information:</span></span>

![包含版本信息的 Swagger UI：说明、作者以及查看更多链接](web-api-help-pages-using-swagger/_static/custom-info.png)

### <a name="xml-comments"></a><span data-ttu-id="5910d-152">XML 注释</span><span class="sxs-lookup"><span data-stu-id="5910d-152">XML comments</span></span>

<span data-ttu-id="5910d-153">可使用以下方法启用 XML 注释：</span><span class="sxs-lookup"><span data-stu-id="5910d-153">XML comments can be enabled with the following approaches:</span></span>

# <a name="visual-studiotabvisual-studio-xml"></a>[<span data-ttu-id="5910d-154">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5910d-154">Visual Studio</span></span>](#tab/visual-studio-xml/)

* <span data-ttu-id="5910d-155">右键单击“解决方案资源管理器”中的项目，然后选择“属性”</span><span class="sxs-lookup"><span data-stu-id="5910d-155">Right-click the project in **Solution Explorer** and select **Properties**</span></span>
* <span data-ttu-id="5910d-156">查看“生成”选项卡的“输出”部分下的“XML 文档文件”框</span><span class="sxs-lookup"><span data-stu-id="5910d-156">Check the **XML documentation file** box under the **Output** section of the **Build** tab</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac-xml"></a>[<span data-ttu-id="5910d-157">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="5910d-157">Visual Studio for Mac</span></span>](#tab/visual-studio-mac-xml/)

* <span data-ttu-id="5910d-158">打开“项目选项”对话框 >“生成” > “编译器”</span><span class="sxs-lookup"><span data-stu-id="5910d-158">Open the **Project Options** dialog > **Build** > **Compiler**</span></span>
* <span data-ttu-id="5910d-159">查看“常规选项”部分下的“生成 xml 文档”框</span><span class="sxs-lookup"><span data-stu-id="5910d-159">Check the **Generate xml documentation** box under the **General Options** section</span></span>

# <a name="visual-studio-codetabvisual-studio-code-xml"></a>[<span data-ttu-id="5910d-160">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5910d-160">Visual Studio Code</span></span>](#tab/visual-studio-code-xml/)

<span data-ttu-id="5910d-161">将以下代码片段手动添加到 .csproj 文件：</span><span class="sxs-lookup"><span data-stu-id="5910d-161">Manually add the following snippet to the *.csproj* file:</span></span>

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/TodoApi.csproj?name=snippet_SuppressWarnings&highlight=2)]

---

<span data-ttu-id="5910d-162">启用 XML 注释，为未记录的公共类型和成员提供调试信息。</span><span class="sxs-lookup"><span data-stu-id="5910d-162">Enabling XML comments provides debug information for undocumented public types and members.</span></span> <span data-ttu-id="5910d-163">警告消息指示未记录的类型和成员。</span><span class="sxs-lookup"><span data-stu-id="5910d-163">Undocumented types and members are indicated by the warning message.</span></span> <span data-ttu-id="5910d-164">例如，以下消息指示违反警告代码 1591：</span><span class="sxs-lookup"><span data-stu-id="5910d-164">For example, the following message indicates a violation of warning code 1591:</span></span>

```text
warning CS1591: Missing XML comment for publicly visible type or member 'TodoController.GetAll()'
```

<span data-ttu-id="5910d-165">定义要在 .csproj 文件中忽略的以分号分隔的警告代码列表，以取消警告：</span><span class="sxs-lookup"><span data-stu-id="5910d-165">Suppress warnings by defining a semicolon-delimited list of warning codes to ignore in the *.csproj* file:</span></span>

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/TodoApi.csproj?name=snippet_SuppressWarnings&highlight=3)]

<span data-ttu-id="5910d-166">配置 Swagger 以使用生成的 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="5910d-166">Configure Swagger to use the generated XML file.</span></span> <span data-ttu-id="5910d-167">对于 Linux 或非 Windows 操作系统，文件名和路径区分大小写。</span><span class="sxs-lookup"><span data-stu-id="5910d-167">For Linux or non-Windows operating systems, file names and paths can be case-sensitive.</span></span> <span data-ttu-id="5910d-168">例如，“TodoApi.XML”文件在 Windows 上有效，但在 CentOS 上无效。</span><span class="sxs-lookup"><span data-stu-id="5910d-168">For example, a *TodoApi.XML* file is valid on Windows but not CentOS.</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="5910d-169">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup.cs?name=snippet_ConfigureServices&highlight=30-32)]</span><span class="sxs-lookup"><span data-stu-id="5910d-169">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup.cs?name=snippet_ConfigureServices&highlight=30-32)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="5910d-170">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Startup.cs?name=snippet_ConfigureServices&highlight=31-33)]</span><span class="sxs-lookup"><span data-stu-id="5910d-170">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Startup.cs?name=snippet_ConfigureServices&highlight=31-33)]</span></span>
::: moniker-end

<span data-ttu-id="5910d-171">在上述代码中，[反射](/dotnet/csharp/programming-guide/concepts/reflection)用于生成与 Web API 项目相匹配的 XML 文件名。</span><span class="sxs-lookup"><span data-stu-id="5910d-171">In the preceding code, [Reflection](/dotnet/csharp/programming-guide/concepts/reflection) is used to build an XML file name matching that of the Web API project.</span></span> <span data-ttu-id="5910d-172">此方法可确保生成的 XML 文件名与项目名称匹配。</span><span class="sxs-lookup"><span data-stu-id="5910d-172">This approach ensures that the generated XML file name matches the project name.</span></span> <span data-ttu-id="5910d-173">[AppContext.BaseDirectory](/dotnet/api/system.appcontext.basedirectory#System_AppContext_BaseDirectory)属性用于构造 XML 文件的路径。</span><span class="sxs-lookup"><span data-stu-id="5910d-173">The [AppContext.BaseDirectory](/dotnet/api/system.appcontext.basedirectory#System_AppContext_BaseDirectory) property is used to construct a path to the XML file.</span></span>

<span data-ttu-id="5910d-174">通过向节标题添加说明，将三斜杠注释添加到操作增强了 Swagger UI。</span><span class="sxs-lookup"><span data-stu-id="5910d-174">Adding triple-slash comments to an action enhances the Swagger UI by adding the description to the section header.</span></span> <span data-ttu-id="5910d-175">执行 `Delete` 操作前添加 [\<summary>](/dotnet/csharp/programming-guide/xmldoc/summary) 元素：</span><span class="sxs-lookup"><span data-stu-id="5910d-175">Add a [\<summary>](/dotnet/csharp/programming-guide/xmldoc/summary) element above the `Delete` action:</span></span>

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_Delete&highlight=1-3)]

<span data-ttu-id="5910d-176">Swagger UI 显示上述代码的 `<summary>` 元素的内部文本：</span><span class="sxs-lookup"><span data-stu-id="5910d-176">The Swagger UI displays the inner text of the preceding code's `<summary>` element:</span></span>

![显示 DELETE 方法的 XML 注释“删除特定 TodoItem”](web-api-help-pages-using-swagger/_static/triple-slash-comments.png)

<span data-ttu-id="5910d-179">生成的 JSON 架构驱动 UI：</span><span class="sxs-lookup"><span data-stu-id="5910d-179">The UI is driven by the generated JSON schema:</span></span>

```json
"delete": {
    "tags": [
        "Todo"
    ],
    "summary": "Deletes a specific TodoItem.",
    "operationId": "ApiTodoByIdDelete",
    "consumes": [],
    "produces": [],
    "parameters": [
        {
            "name": "id",
            "in": "path",
            "description": "",
            "required": true,
            "type": "integer",
            "format": "int64"
        }
    ],
    "responses": {
        "200": {
            "description": "Success"
        }
    }
}
```

<span data-ttu-id="5910d-180">将 [\<remarks>](/dotnet/csharp/programming-guide/xmldoc/remarks) 元素添加到 `Create` 操作方法文档。</span><span class="sxs-lookup"><span data-stu-id="5910d-180">Add a [\<remarks>](/dotnet/csharp/programming-guide/xmldoc/remarks) element to the `Create` action method documentation.</span></span> <span data-ttu-id="5910d-181">它可以补充 `<summary>` 元素中指定的信息，并提供更可靠的 Swagger UI。</span><span class="sxs-lookup"><span data-stu-id="5910d-181">It supplements information specified in the `<summary>` element and provides a more robust Swagger UI.</span></span> <span data-ttu-id="5910d-182">`<remarks>` 元素内容可包含文本、JSON 或 XML。</span><span class="sxs-lookup"><span data-stu-id="5910d-182">The `<remarks>` element content can consist of text, JSON, or XML.</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="5910d-183">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_Create&highlight=4-14)]</span><span class="sxs-lookup"><span data-stu-id="5910d-183">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_Create&highlight=4-14)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="5910d-184">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_Create&highlight=4-14)]</span><span class="sxs-lookup"><span data-stu-id="5910d-184">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_Create&highlight=4-14)]</span></span>
::: moniker-end

<span data-ttu-id="5910d-185">请注意带这些附加注释的 UI 增强功能：</span><span class="sxs-lookup"><span data-stu-id="5910d-185">Notice the UI enhancements with these additional comments:</span></span>

![显示包含其他注释的 Swagger UI](web-api-help-pages-using-swagger/_static/xml-comments-extended.png)

### <a name="data-annotations"></a><span data-ttu-id="5910d-187">数据注释</span><span class="sxs-lookup"><span data-stu-id="5910d-187">Data annotations</span></span>

<span data-ttu-id="5910d-188">使用 [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) 命名空间中的属性来修饰模型，以帮助驱动 Swagger UI 组件。</span><span class="sxs-lookup"><span data-stu-id="5910d-188">Decorate the model with attributes, found in the [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) namespace, to help drive the Swagger UI components.</span></span>

<span data-ttu-id="5910d-189">将 `[Required]` 属性添加到 `TodoItem` 类的 `Name` 属性：</span><span class="sxs-lookup"><span data-stu-id="5910d-189">Add the `[Required]` attribute to the `Name` property of the `TodoItem` class:</span></span>

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Models/TodoItem.cs?highlight=10)]

<span data-ttu-id="5910d-190">此属性的状态更改 UI 行为并更改基础 JSON 架构：</span><span class="sxs-lookup"><span data-stu-id="5910d-190">The presence of this attribute changes the UI behavior and alters the underlying JSON schema:</span></span>

```json
"definitions": {
    "TodoItem": {
        "required": [
            "name"
        ],
        "type": "object",
        "properties": {
            "id": {
                "format": "int64",
                "type": "integer"
            },
            "name": {
                "type": "string"
            },
            "isComplete": {
                "default": false,
                "type": "boolean"
            }
        }
    }
},
```

<span data-ttu-id="5910d-191">将 `[Produces("application/json")]` 属性添加到 API 控制器。</span><span class="sxs-lookup"><span data-stu-id="5910d-191">Add the `[Produces("application/json")]` attribute to the API controller.</span></span> <span data-ttu-id="5910d-192">这样做的目的是声明控制器的操作支持 application/json 的响应内容类型：</span><span class="sxs-lookup"><span data-stu-id="5910d-192">Its purpose is to declare that the controller's actions support a response content type of *application/json*:</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="5910d-193">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_TodoController&highlight=1)]</span><span class="sxs-lookup"><span data-stu-id="5910d-193">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_TodoController&highlight=1)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="5910d-194">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_TodoController&highlight=1)]</span><span class="sxs-lookup"><span data-stu-id="5910d-194">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_TodoController&highlight=1)]</span></span>
::: moniker-end

<span data-ttu-id="5910d-195">“响应内容类型”下拉列表选此内容类型作为控制器的默认 GET 操作：</span><span class="sxs-lookup"><span data-stu-id="5910d-195">The **Response Content Type** drop-down selects this content type as the default for the controller's GET actions:</span></span>

![包含默认响应内容类型的 Swagger UI](web-api-help-pages-using-swagger/_static/json-response-content-type.png)

<span data-ttu-id="5910d-197">随着 Web API 中的数据注释的使用越来越多，UI 和 API 帮助页变得更具说明性和更为有用。</span><span class="sxs-lookup"><span data-stu-id="5910d-197">As the usage of data annotations in the Web API increases, the UI and API help pages become more descriptive and useful.</span></span>

### <a name="describe-response-types"></a><span data-ttu-id="5910d-198">描述响应类型</span><span class="sxs-lookup"><span data-stu-id="5910d-198">Describe response types</span></span>

<span data-ttu-id="5910d-199">消费应用程序开发人员最关心的问题是返回的内容 &mdash; 具体的响应类型和错误代码（如果不标准）。</span><span class="sxs-lookup"><span data-stu-id="5910d-199">Consuming developers are most concerned with what's returned&mdash;specifically response types and error codes (if not standard).</span></span> <span data-ttu-id="5910d-200">在 XML 注释和数据注释中表示响应类型和错误代码。</span><span class="sxs-lookup"><span data-stu-id="5910d-200">The response types and error codes are denoted in the XML comments and data annotations.</span></span>

<span data-ttu-id="5910d-201">`Create` 操作成功后返回 HTTP 201 状态代码。</span><span class="sxs-lookup"><span data-stu-id="5910d-201">The `Create` action returns an HTTP 201 status code on success.</span></span> <span data-ttu-id="5910d-202">发布的请求正文为 NULL 时，将返回 HTTP 400 状态代码。</span><span class="sxs-lookup"><span data-stu-id="5910d-202">An HTTP 400 status code is returned when the posted request body is null.</span></span> <span data-ttu-id="5910d-203">如果 Swagger UI 中没有提供合适的文档，那么使用者会缺少对这些预期结果的了解。</span><span class="sxs-lookup"><span data-stu-id="5910d-203">Without proper documentation in the Swagger UI, the consumer lacks knowledge of these expected outcomes.</span></span> <span data-ttu-id="5910d-204">在以下示例中，通过添加突出显示的行解决此问题：</span><span class="sxs-lookup"><span data-stu-id="5910d-204">Fix that problem by adding the highlighted lines in the following example:</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="5910d-205">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_Create&highlight=17,18,20,21)]</span><span class="sxs-lookup"><span data-stu-id="5910d-205">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_Create&highlight=17,18,20,21)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="5910d-206">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_Create&highlight=17,18,20,21)]</span><span class="sxs-lookup"><span data-stu-id="5910d-206">[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_Create&highlight=17,18,20,21)]</span></span>
::: moniker-end

<span data-ttu-id="5910d-207">Swagger UI 现在清楚地记录预期的 HTTP 响应代码：</span><span class="sxs-lookup"><span data-stu-id="5910d-207">The Swagger UI now clearly documents the expected HTTP response codes:</span></span>

![Swagger UI 针对“响应消息”下的状态代码和原因显示 POST 响应类描述“返回新建的待办事项”和“400 - 如果该项为 null”](web-api-help-pages-using-swagger/_static/data-annotations-response-types.png)

### <a name="customize-the-ui"></a><span data-ttu-id="5910d-209">自定义 UI</span><span class="sxs-lookup"><span data-stu-id="5910d-209">Customize the UI</span></span>

<span data-ttu-id="5910d-210">股票 UI 既实用又可呈现。</span><span class="sxs-lookup"><span data-stu-id="5910d-210">The stock UI is both functional and presentable.</span></span> <span data-ttu-id="5910d-211">但是，API 文档页应代表品牌或主题。</span><span class="sxs-lookup"><span data-stu-id="5910d-211">However, API documentation pages should represent your brand or theme.</span></span> <span data-ttu-id="5910d-212">将 Swashbuckle 组件标记为需要添加资源以提供静态文件，并构建文件夹结构以托管这些文件。</span><span class="sxs-lookup"><span data-stu-id="5910d-212">Branding the Swashbuckle components requires adding the resources to serve static files and building the folder structure to host those files.</span></span>

<span data-ttu-id="5910d-213">如果以 .NET Framework 或 .NET Core 1.x 为目标，请将 [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles) NuGet 包添加到项目：</span><span class="sxs-lookup"><span data-stu-id="5910d-213">If targeting .NET Framework or .NET Core 1.x, add the [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles) NuGet package to the project:</span></span>

```xml
<PackageReference Include="Microsoft.AspNetCore.StaticFiles" Version="2.0.0" />
```

<span data-ttu-id="5910d-214">如果以 .NET Core 2.x 为目标并使用[元包](xref:fundamentals/metapackage)，则已安装上述 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="5910d-214">The preceding NuGet package is already installed if targeting .NET Core 2.x and using the [metapackage](xref:fundamentals/metapackage).</span></span>

<span data-ttu-id="5910d-215">启用静态文件中间件：</span><span class="sxs-lookup"><span data-stu-id="5910d-215">Enable the static files middleware:</span></span>

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup.cs?name=snippet_Configure&highlight=3)]

<span data-ttu-id="5910d-216">从 [Swagger UI GitHub 存储库](https://github.com/swagger-api/swagger-ui/tree/master/dist)中获取 dist 文件夹的内容。</span><span class="sxs-lookup"><span data-stu-id="5910d-216">Acquire the contents of the *dist* folder from the [Swagger UI GitHub repository](https://github.com/swagger-api/swagger-ui/tree/master/dist).</span></span> <span data-ttu-id="5910d-217">此文件夹包含 Swagger UI 页必需的资产。</span><span class="sxs-lookup"><span data-stu-id="5910d-217">This folder contains the necessary assets for the Swagger UI page.</span></span>

<span data-ttu-id="5910d-218">创建 wwwroot/swagger/ui 文件夹，然后将 dist 文件夹的内容复制到其中。</span><span class="sxs-lookup"><span data-stu-id="5910d-218">Create a *wwwroot/swagger/ui* folder, and copy into it the contents of the *dist* folder.</span></span>

<span data-ttu-id="5910d-219">使用以下 CSS 在 wwwroot/swagger/ui 中创建 custom.css 文件，以自定义页面标题：</span><span class="sxs-lookup"><span data-stu-id="5910d-219">Create a *custom.css* file, in *wwwroot/swagger/ui*, with the following CSS to customize the page header:</span></span>

[!code-css[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/wwwroot/swagger/ui/custom.css)]

<span data-ttu-id="5910d-220">引用其他 CSS 文件后，引用 index.html 文件中的“custom.css”：</span><span class="sxs-lookup"><span data-stu-id="5910d-220">Reference *custom.css* in the *index.html* file, after any other CSS files:</span></span>

[!code-html[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/wwwroot/swagger/ui/index.html?name=snippet_SwaggerUiCss&highlight=3)]

<span data-ttu-id="5910d-221">浏览到 `http://localhost:<port>/swagger/ui/index.html` 中的 index.html 页。</span><span class="sxs-lookup"><span data-stu-id="5910d-221">Browse to the *index.html* page at `http://localhost:<port>/swagger/ui/index.html`.</span></span> <span data-ttu-id="5910d-222">在标题文本框中输入 `http://localhost:<port>/swagger/v1/swagger.json`，然后单击“浏览”按钮。</span><span class="sxs-lookup"><span data-stu-id="5910d-222">Enter `http://localhost:<port>/swagger/v1/swagger.json` in the header's textbox, and click the **Explore** button.</span></span> <span data-ttu-id="5910d-223">生成的页面如下所示：</span><span class="sxs-lookup"><span data-stu-id="5910d-223">The resulting page looks as follows:</span></span>

![使用自定义标题的 Swagger UI](web-api-help-pages-using-swagger/_static/custom-header.png)

<span data-ttu-id="5910d-225">还可以对页面执行更多操作。</span><span class="sxs-lookup"><span data-stu-id="5910d-225">There's much more you can do with the page.</span></span> <span data-ttu-id="5910d-226">在 [Swagger UI GitHub 存储库](https://github.com/swagger-api/swagger-ui)中查看 UI 资源的完整功能。</span><span class="sxs-lookup"><span data-stu-id="5910d-226">See the full capabilities for the UI resources at the [Swagger UI GitHub repository](https://github.com/swagger-api/swagger-ui).</span></span>