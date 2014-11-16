# OVIRT MANAGER用户界面插件的引导

一个典型的插件引导程式包括如下步骤：

获得插件的 pluginApi 实例

获得运行时插件配置对象

注册有关的事件处理函数

通知用户界面插件框架继续对插件进行初始化过程

下面的代码片段展示了实际运行过程中上面的步骤的实现：


    // Access plugin API using 'parent' due to this code being evaluated within the context of an iframe element.
    // As 'parent.pluginApi' is subject to Same-Origin Policy, this will only work when WebAdmin HTML page and plugin
    // host page are served from same origin. WebAdmin HTML page and plugin host page will always be on same origin
    // when using UI plugin infrastructure support to serve plugin resource files.
    var api = parent.pluginApi('MyPlugin');
    // Runtime configuration object associated with the plugin (or an empty object).
    var config = api.configObject();
    // Register event handler function(s) for later invocation by UI plugin infrastructure.
    api.register({
        // UiInit event handler function.
        UiInit: function() {
        // Handle UiInit event.
            window.alert('Favorite music band is ' + config.band);
        }
    });
    // Notify UI plugin infrastructure to proceed with plugin initialization.
    api.ready();



