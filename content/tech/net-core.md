---
title: "Net Core"
date: 2018-01-04T11:42:00+01:00
draft: true
---

# Getting Started with .NET Core

After using .NET Core since right away after it was announced at work, I was just starting my first private project with it. And: surprise, I had to learn again lots of the basic stuff that in our project just has been done (felt) decades ago.

## The Setup

The infrastructure behind this exercise is the following

* [.NET Core 2.0]()
* [PostgreSQL]() as database layer
* Running behind [nginx]() as reverse proxy
* Automated deployment to [Docker]()
* [VisualStudio Code]() as IDE

## The First Steps

As a matter of fact, I was kind of rusty when taking my first steps. So first of all, I had to install .NET Core 2.0. This is pretty straightforward and can be done via a simple installer available for all OS.

## Wiring Up a PostgreSQL Docker Container

All of that can be pretty much taken from he official Postgres image on [Dockerhub](https://hub.docker.com/_/postgres/). The only (important) difference is that the container should be bound to localhost in order to be able to be reached from your app.

```shell
docker run --name postgres -p 5432:5432 -e POSTGRES_PASSWORD=mysecretpassword -d postgres
```

## Scaffolding the Migrations

```bash
dotnet ef migrations add Initial -s ..\StaticPagesComments.Service\StaticPagesComments.Service.csproj
```

```cs
public CommentController (ILogger<CommentController> logger, ICommentModel model) {
    _logger = logger;
    _model = model;
}
```