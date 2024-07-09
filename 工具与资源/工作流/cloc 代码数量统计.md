### 安装 `cloc`：

- 通过 brew 安装: `brew install cloc`
- 或者使用系统的包管理器，例如在 Debian/Ubuntu 上：`sudo apt install cloc`
- 对于 macOS 用户，可以使用 Homebrew：`brew install cloc`
- Windows 用户可以通过 Chocolatey 安装：`choco install cloc` 1

### 使用 `cloc` 进行代码统计：

- 统计当前目录下的代码行数：`cloc .`
- 统计指定语言的代码行数：`cloc <path> --language=<language>`
- 按文件统计代码行数：`cloc <path> --by-file`
- 忽略指定目录：`cloc <path> --exclude-dir=<dirname>`
- 输出结果到文件：`cloc . --out=result.txt`
- 如果需要输出 CSV 格式的结果，可以使用：`cloc . --csv` 1

此外，还有 VS Code Counter 这个 VS Code 扩展工具，它用于统计代码行数以及代码量等信息 3。对于其他代码量统计工具，如 SLOCCount、CodeMR、SonarQube 和 GitStats，它们各自具有独特的特点和功能，例如支持多种编程语言、提供代码复杂度分析、集成到 CI/CD 工作流中等 4。