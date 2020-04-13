# JavaScript事件

##### 事件传播的三个阶段

- 第一阶段：从window对象传导到目标节点，称为“捕获阶段”（capture phase）。
- 第二阶段：在目标节点上触发，称为“目标阶段”（target phase）。
- 第三阶段：从目标节点传导回window对象，称为“冒泡阶段”（bubbling phase）。

这种三阶段的传播模型，会使得一个事件在多个节点上触发。比如，假设div节点之中嵌套一个p节点。
