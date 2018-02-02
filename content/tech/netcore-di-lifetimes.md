---
title: "Service Lifecycles in .NET Core"
date: 2018-01-24T21:01:00+01:00
draft: false
tags: ["dotnet-core", "dependency-injection", "lifecycle"]
---

# Intro

The [official documentation](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection#service-lifetimes-and-registration-options) only has a brief overview of the available lifetimes of services when using the DI mechanism of .NET Core. An additional great explanation of the lifetimes themselves can be found in this extensive [answer on SO](https://stackoverflow.com/a/38139500).

Although it seems trivial at first, I had to find out the hard way what it actually means when programming a real-life application. 

First of all, a short sum-up of the two resources given above: Services in .NET Core can be configured with three different lifetimes: `Transient`, `Scoped` and `Singleton`.

# The Setup

Now, lets assume the following situation: We have three classes in place:

* `DataListener`: This class contains a callback which is invoked from outside the HTTP pipeline. In my current project, that's a ZeroMQ message bus.
* `DataHandler`: The actual user of the data in the `DataCache`.

```cs

public class DataListener : IDataListener {

    private readonly IDataHandler _dataHandler;

    public DataListener(IDataHandler dataHandler) {
        _dataHandler = dataHandler;
    }

    private void Callback(Data newData) {
        _dataHandler.DoSomethingWhenDataHasChanged(newData);
    }

}

public class DataHandler : IDataHandler {

    public DataHandler() {

    }

    public void DoSomethingWhenDataHasChanged(Data newData) {
        // Now do something fancy...
    }

}
```

It is pretty obvious that the scope of the `DataListener` has to be `Singleton`, as the callback is registered once on the startup of the application. The `DataHandler` can actually use a `Transient` scope - which should always be the scope to look for, if possible.

```cs
# Startup.cs
public void ConfigureServices(...) {
    services.AddSingleton<IDataListener>(DataListener);
    services.AddTransient<IDataHandler>(DataHandler);
}
```

So far, so good. The important part to recognize here is the following: Although explicitly marked with a `Transient` scope, during the whole lifecycle of the application there will *only be exactly one instance* of the `DataHandler`. This part is crucial. And also if, when you think about it for just a second, it makes perfect sense - it cost me enough time that I thought writing some lines about it so I will never forget it is worth it.

# The Secret

Well, honestly - there is no secret. Again, think about it. This is the dependency graph:

```bash
DataHandler <-- DataListener
 ```

So here is what happens: During startup of the application, the `DateListener` is instantiated. It is instantiated exactly *once*, because we told him this exact thing. When this happens, the dependency to `DataHandler` is resolved - `DataHandler` is also instantiated and injected in the constructor. And therefore, the `DataHandler` also will behave like a `Singleton` - at least as long as it is not used by other `Transient` classes...