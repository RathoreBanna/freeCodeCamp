---
title: Pattern Matching
localeTitle: 模式匹配
---
## 模式匹配

模式匹配是Elixir从Erlang继承的技术。这是一种非常强大的技术，它允许我们从复杂的数据结构中提取更简单的子结构，如列表，元组，映射等。

比赛有2个主要部分，左侧和右侧。右侧是任何类型的数据结构。左侧尝试匹配右侧的数据结构，并将左侧的任何变量绑定到右侧的相应子结构。如果未找到匹配项，则操作员会引发错误。

最简单的匹配是左侧的单个变量和右侧的任何数据结构。这个变量将匹配任何东西。例如：  
`x = 12`  
`x = "Hello"`  
`IO.puts(x)`

您可以将变量放在结构中，以便捕获子结构。例如：  
`[var_1, _unused_var, var_2] = [{"First variable"}, 25, "Second variable" ]`  
`IO.puts(var_1)`  
`IO.puts(var_2)`

这将在var _1中_存储值`{"First variable"}`在var _2中存储`"Second variable"`_ 。还有一个特殊的\_变量（或带有'\_'前缀的变量），它与其他变量完全一样但是告诉elixir， “确保有些东西在这里，但我并不在乎它到底是什么。”在前面的例子中，\_unused\_var就是这样一个变量。

我们可以使用这种技术匹配更复杂的模式。例如，如果要打开并在列表中的元组中获取数字，该列表本身位于列表中，则可以使用以下命令：  
`[_, [_, {a}]] = ["Random string", [:an_atom, {24}]]`  
`IO.puts(a)`

上述程序产生以下结果 -  
`24`

这将绑定到24.其他值被忽略，因为我们使用'\_'。

在模式匹配中，如果我们在右侧使用变量，则使用其值。如果要使用左侧变量的值，则需要使用pin运算符。

例如，如果您的变量“a”的值为25，并且您希望将其与另一个值为25的变量“b”匹配，那么您需要输入 -  
`a = 25`  
`b = 25`  
`^a = b`

最后一行匹配a的当前值，而不是将其赋值给b的值。如果我们有一组不匹配的左侧和右侧，匹配运算符会引发错误。例如，如果我们尝试将元组与列表或大小为2的列表与大小为3的列表进行匹配，则会显示错误。