---
title: "Create a C# function using Visual Studio Code - Azure Functions"
description: "Learn how to create a C# function, then publish the local project to serverless hosting in Azure Functions using the Azure Functions extension in Visual Studio Code. "
ms.topic: quickstart
ms.date: 01/05/2023
ms.devlang: csharp
ms.custom: devx-track-csharp, mode-ui, vscode-azure-extension-update-complete
---

# Quickstart: Create a C# function in Azure using Visual Studio Code

This article creates an HTTP triggered function that runs on .NET. For information about .NET versions supported for C# functions, see [Supported versions](dotnet-isolated-process-guide.md#supported-versions).

There's also a [CLI-based version](create-first-function-cli-csharp.md) of this article.

Completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

## Configure your environment

Before you get started, make sure you have the following requirements in place:

[!INCLUDE [functions-requirements-visual-studio-code-csharp](../../includes/functions-requirements-visual-studio-code-csharp.md)]

## <a name="create-an-azure-functions-project"></a>Create your local project

In this section, you use Visual Studio Code to create a local Azure Functions project in C#. Later in this article, you'll publish your function code to Azure.

1. Choose the Azure icon in the Activity bar, then in the **Workspace (local)** area, select the **+** button, choose **Create Function** in the dropdown. When prompted, choose **Create new project**.

    :::image type="content" source="./media/functions-create-first-function-vs-code/create-new-project.png" alt-text="Screenshot of create a new project window.":::

1. Select the directory location for your project workspace and choose **Select**. You should either create a new folder or choose an empty folder for the project workspace. Don't choose a project folder that is already part of a workspace.
 
1. For **Select a language**, choose `C#`.
 
1. For **Select a .NET runtime**, choose from one of the following options: 

    | Option | .NET version | Process model | Description |
    | --- | --- | --- |  --- |
    | **.NET 6.0 (LTS)** | .NET 6 | [In-process](functions-dotnet-class-library.md) | _In-process_ C# functions are only supported on [Long Term Support (LTS)](https://dotnet.microsoft.com/en-us/platform/support/policy/dotnet-core) .NET versions. Function code runs in the same process as the Functions host.  |
    | **.NET 6.0 Isolated (LTS)** | .NET 6 | [Isolated worker process](dotnet-isolated-process-guide.md) | Functions run on .NET 6, but in a separate process from the Functions host. |
    | **.NET 7.0 Isolated** | .NET 7 | [Isolated worker process](dotnet-isolated-process-guide.md) | Because .NET 7 isn't an LTS version of .NET, your functions must run in an isolated process on .NET 7. |
    | **.NET Framework Isolated** | .NET 7 | [Isolated worker process](dotnet-isolated-process-guide.md) | Choose this option when your functions need to use libraries only supported on the .NET Framework. |

    The two process models use different APIs, and each process model uses a different template when generating the function project code. If you don't see these options, press F1 and type `Preferences: Open user settings`, then search for `Azure Functions: Project Runtime` and make sure that the default runtime version is set to `~4`.

1. Provide the remaining information at the prompts:

    |Prompt|Selection|
    |--|--|
    |**Select a template for your project's first function**|Choose `HTTP trigger`.|
    |**Provide a function name**|Type `HttpExample`.|
    |**Provide a namespace** | Type `My.Functions`. |
    |**Authorization level**|Choose `Anonymous`, which enables anyone to call your function endpoint. To learn about authorization level, see [Authorization keys](functions-bindings-http-webhook-trigger.md#authorization-keys).|
    |**Select how you would like to open your project**|Select `Add to workspace`.|

1. Visual Studio Code uses the provided information and generates an Azure Functions project with an HTTP trigger. You can view the local project files in the Explorer. For more information about the files that are created, see [Generated project files](functions-develop-vs-code.md?tabs=csharp#generated-project-files).

[!INCLUDE [functions-run-function-test-local-vs-code-csharp](../../includes/functions-run-function-test-local-vs-code-csharp.md)]

After checking that the function runs correctly on your local computer, it's time to use Visual Studio Code to publish the project directly to Azure.

[!INCLUDE [functions-sign-in-vs-code](../../includes/functions-sign-in-vs-code.md)]

[!INCLUDE [functions-publish-project-vscode](../../includes/functions-publish-project-vscode.md)]

[!INCLUDE [functions-vs-code-run-remote](../../includes/functions-vs-code-run-remote.md)]

[!INCLUDE [functions-cleanup-resources-vs-code.md](../../includes/functions-cleanup-resources-vs-code.md)]

## Next steps

You have used [Visual Studio Code](functions-develop-vs-code.md?tabs=csharp) to create a function app with a simple HTTP-triggered function. In the next article, you expand that function by connecting to either Azure Cosmos DB or Azure Queue Storage. To learn more about connecting to other Azure services, see [Add bindings to an existing function in Azure Functions](add-bindings-existing-function.md?tabs=csharp). 

The next article depends on your chosen process model.

# [In-process](#tab/in-process) 

> [!div class="nextstepaction"]
> [Connect to Azure Cosmos DB](functions-add-output-binding-cosmos-db-vs-code.md?pivots=programming-language-csharp&tabs=in-process)
> [Connect to Azure Queue Storage](functions-add-output-binding-storage-queue-vs-code.md?pivots=programming-language-csharp&tabs=in-process)

# [Isolated process](#tab/isolated-process)

> [!div class="nextstepaction"]
> [Connect to Azure Cosmos DB](functions-add-output-binding-cosmos-db-vs-code.md?pivots=programming-language-csharp&tabs=isolated-process)
> [Connect to Azure Queue Storage](functions-add-output-binding-storage-queue-vs-code.md?pivots=programming-language-csharp&tabs=isolated-process)

---

[Azure Functions Core Tools]: functions-run-local.md
[Azure Functions extension for Visual Studio Code]: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions
