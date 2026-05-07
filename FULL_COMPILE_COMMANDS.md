# LaTeX 完整编译命令

当你修改了下面这些内容时，建议进行完整编译，而不是只跑一次 `xelatex`：

- 文献条目 `.bib`
- `\cite{}` 引用
- 图表、公式、章节引用 `\ref{}` / `\eqref{}`
- 目录页码
- 会影响分页的设置
  例如：`\raggedbottom`、`library`、图片大小、表格大小、段落内容增减

## 为什么要完整编译

LaTeX 的交叉引用、参考文献编号、目录页码和分页结果，往往需要多轮编译才能稳定。

尤其像 `\raggedbottom` 这种会影响页面垂直分配的设置，虽然不是文献改动，但它会改变分页，因此也建议完整编译一次。

## PowerShell 下的完整编译命令

在项目根目录执行：

```powershell
& 'C:\Users\chenz\AppData\Local\Programs\MiKTeX\miktex\bin\x64\xelatex.exe' -interaction=nonstopmode -file-line-error demo.tex
& 'C:\Users\chenz\AppData\Local\Programs\MiKTeX\miktex\bin\x64\bibtex.exe' demo
& 'C:\Users\chenz\AppData\Local\Programs\MiKTeX\miktex\bin\x64\xelatex.exe' -interaction=nonstopmode -file-line-error demo.tex
& 'C:\Users\chenz\AppData\Local\Programs\MiKTeX\miktex\bin\x64\xelatex.exe' -interaction=nonstopmode -file-line-error demo.tex
```

## 简化理解

- 只改正文、没改文献时：通常至少编译 2 次
- 改了文献或引用时：建议完整跑 4 步

## 可选：只快速刷新分页

如果你只是改了排版设置，例如 `\raggedbottom`，没有改文献，也可以先试：

```powershell
& 'C:\Users\chenz\AppData\Local\Programs\MiKTeX\miktex\bin\x64\xelatex.exe' -interaction=nonstopmode -file-line-error demo.tex
& 'C:\Users\chenz\AppData\Local\Programs\MiKTeX\miktex\bin\x64\xelatex.exe' -interaction=nonstopmode -file-line-error demo.tex
```

如果页码、引用、目录还有变化，再执行上面的完整编译流程。
