[Using change detection hooks](guide/lifecycle-hooks#using-change-detection-hooks)

[使用变更检测钩子](guide/lifecycle-hooks#using-change-detection-hooks)

[Defining custom change detection](guide/lifecycle-hooks#defining-custom-change-detection)

[定义自定义变更检测](guide/lifecycle-hooks#defining-custom-change-detection)

The following examples demonstrate how to modify default change-detection behavior
to perform explicit detection when needed.

下面的例子演示了如何修改默认的变更检测行为，以便在需要时执行显式变更检测。

Use `markForCheck()` with `CheckOnce` strategy

使用 `markForCheck()` 和 `CheckOnce` 策略

The following example sets the `OnPush` change-detection strategy for a component
\(`CheckOnce`, rather than the default `CheckAlways`\), then forces a second check
after an interval.

下面的例子为组件设置了 `OnPush` 变更检测策略（`CheckOnce` 而不是默认的
`CheckAlways`），然后每隔一段时间强制进行第二轮检测。
参见[在线例子](http://plnkr.co/edit/GC512b?p=preview)。

Detach change detector to limit how often check occurs

分离开变更检测器以限制变更检测的发生频度

The following example defines a component with a large list of read-only data
that is expected to change constantly, many times per second.
To improve performance, we want to check and update the list
less often than the changes actually occur. To do that, we detach
the component's change detector and perform an explicit local check every five seconds.

下面的例子定义了一个带有只读数据的大型列表，这些数据预计每秒会变化很多次。
为了提高性能，我们检测和更新列表的频率就应该比实际发生的变化少得多。
要解决这个问题，就要分离开变更检测器，并每隔五秒钟显式执行一次变更检查。

Reattaching a detached component

重新附加一个已分离的组件

The following example creates a component displaying live data.
The component detaches its change detector from the main change detector tree
when the `live` property is set to false, and reattaches it when the property
becomes true.

下面的例子创建了一个用来显示活动数据的组件。
当 `live` 属性为 `false` 时，该组件就把它的变更检测器从主变更检测器树中分离出来，当该属性变为
`true` 时，则重新附加上它。

Base class that provides change detection functionality.
A change-detection tree collects all views that are to be checked for changes.
Use the methods to add and remove views from the tree, initiate change-detection,
and explicitly mark views as _dirty_, meaning that they have changed and need to be re-rendered.

Angular 各种视图的基础类，提供变更检测功能。
变更检测树会收集要检查的所有视图。
使用这些方法从树中添加或移除视图、初始化变更检测并显式地把这些视图标记为*脏的*，意思是它们变了、需要重新渲染。

When a view uses the {&commat;link ChangeDetectionStrategy#OnPush OnPush} \(checkOnce\)
change detection strategy, explicitly marks the view as changed so that
it can be checked again.

当视图使用 {&commat;link ChangeDetectionStrategy#OnPush
OnPush}（`checkOnce`）变更检测策略时，把该视图显式标记为已更改，以便它再次进行检查。

Components are normally marked as dirty \(in need of rerendering\) when inputs
have changed or events have fired in the view. Call this method to ensure that
a component is checked even if these triggers have not occurred.

当输入已更改或视图中发生了事件时，组件通常会标记为脏的（需要重新渲染）。调用此方法会确保即使那些触发器没有被触发，也仍然检查该组件。

Detaches this view from the change-detection tree.
A detached view is  not checked until it is reattached.
Use in combination with `detectChanges()` to implement local change detection checks.

从变更检测树中分离开视图。
已分离的视图在重新附加上去之前不会被检查。
与 `detectChanges()` 结合使用，可以实现局部变更检测。

Detached views are not checked during change detection runs until they are
re-attached, even if they are marked as dirty.

即使已分离的视图已标记为脏的，它们在重新附加上去之前也不会被检查。

Checks this view and its children. Use in combination with {&commat;link ChangeDetectorRef#detach
detach}
to implement local change detection checks.

检查该视图及其子视图。与 {&commat;link ChangeDetectorRef#detach detach} 结合使用可以实现局部变更检测。

Checks the change detector and its children, and throws if any changes are detected.

检查变更检测器及其子检测器，如果检测到任何更改，则抛出异常。

Use in development mode to verify that running change detection doesn't introduce
other changes. Calling it in production mode is a noop.

在开发模式下可用来验证正在运行的变更检测器是否引入了其它变更。在生产模式下调用它时没有任何效果。

Re-attaches the previously detached view to the change detection tree.
Views are attached to the tree by default.

把以前分离开的视图重新附加到变更检测树上。
视图会被默认附加到这棵树上。

Returns a ChangeDetectorRef \(a.k.a. a ViewRef\)

返回 ChangeDetectorRef（又名 ViewRef）

The node that is requesting a ChangeDetectorRef

请求 ChangeDetectorRef 的节点

The view to which the node belongs

节点所属的视图

Whether the view is being injected into a pipe.

视图是否正在注入管道。

The ChangeDetectorRef to use

要使用的 ChangeDetectorRef

Creates a ViewRef and stores it on the injector as ChangeDetectorRef \(public alias\).

创建一个 ViewRef 并将其作为 ChangeDetectorRef（公共别名）存储在注入器中。