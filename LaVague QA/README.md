This baseline is from this url:     [Quick tour - LaVague](https://docs.lavague.ai/en/latest/docs/lavague-qa/quick-tour/)

# LaVague QA 使用示例

本文档将介绍 **`LaVague QA`**，我们将其作为一个标准的**基线模型 (Baseline Model)** 。

通过以下示例，我们将展示该模型如何将Gherkin功能描述文件（`.feature`）转换为可执行的Pytest测试代码，并了解其基本配置与用法。

本文档中的所有命令都假定您在项目的根目录下运行。

## 1. 环境配置 (重要)

在运行任何示例之前，您必须先配置您的 OpenAI API 密钥。`LaVague` 使用大语言模型来理解您的指令并生成代码，因此需要这个密钥来进行身份验证。

#### 获取你的 API 密钥

首先，从 OpenAI 官方网站获取您的 API 密钥：[platform.openai.com/account/api-keys](https://platform.openai.com/account/api-keys)

#### 设置环境变量

接下来，在您的终端中设置环境变量。请将 `sk-...` 替换为您自己的真实密钥。

- **Windows (PowerShell):**

  ```powershell
  $env:OPENAI_API_KEY = "sk-..."
  ```

- **Windows (CMD):**

  ```cmd
  set OPENAI_API_KEY=sk-...
  ```

- **macOS / Linux:**

  ```bash
  export OPENAI_API_KEY="sk-..."
  ```

**注意**：此设置为临时有效，仅在当前终端窗口中生效。关闭窗口后需要重新设置。

## 2. 测试示例

下面提供一组**`LaVague QA`**测试示例作为参考，这个样例在流程上可以跑通，但它生成的测试代码存在问题，这也是我们拿它作为测试示例的原因。

### Sauce Labs - 测试购物车功能

- **目的**：测试添加商品到购物车功能是否符合预期。

#### Feature 文件 (`test.feature`)

```gherkin
Feature: Add items to the shopping cart

  As a customer
  I want to add items to my cart
  So that I can purchase them later

  Scenario: Add a single item to the cart
    Given I am on the product page
    When I click a product to view details
    And I add the product to the shopping cart
    Then the product count on the shopping cart icon should increase
```

#### 生成 Pytest 代码

```bash
 lavague-qa --url https://www.saucedemo.com/v1/inventory.html  --feature ./test.feature
```

#### 使用pytest运行测试代码

```bash
 pytest .\generated_tests\test.py 
```

