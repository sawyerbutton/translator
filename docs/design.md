# 工作方式

1. 在前端的 DOMContentLoad 中进行翻译，并保留英文原文的段落 id。
2. 当用户悬停在段落上时，在段落下方显示翻译助手图标，包括显示原文、纠错、评论、历史等按钮。
3. 当用户点击段落时，展开英文原文。

# 细节处理

## 保留原文中的行为（保留原始DOM节点的引用）

1. 为每个文本节点添加唯一的 ngwt-node-id。
1. 发送给翻译器之前，把 Node 重新包装一下，确保任何文本都被包含在 `font[ngwt-text-node]` 元素中（不存在孤立文本），并且给所有元素都加上 ngwt-node-id
1. 翻译器翻译时会保留这些 ngwt-next-id
1. 解析对照文本，并且根据 ngwt-next-id 的值，逐个写回文本节点中
