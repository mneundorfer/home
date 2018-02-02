---
title: ".NET Core Microservice Template"
date: 2018-01-04T11:42:00+01:00
draft: true
tags: ["netcore", "ddd"]
---

After using .NET Core since right away after it was announced at work, I was just starting my first private project with it. And: surprise, I had to learn again lots of the basic stuff that in our project just has been done (felt) decades ago.

## The Setup

The infrastructure behind this exercise is the following

[x] [(ASP).NET Core 2.0](https://github.com/dotnet/core/blob/master/release-notes/download-archives/2.0.0-download.md) application
[x] [PostgreSQL](http://www.postgresql.org/) as database layer
[ ] Running behind [nginx](https://nginx.org/) as reverse proxy
[ ] Automated deployment to [Docker](https://www.docker.com/)
[x] [VisualStudio Code](https://code.visualstudio.com/) as IDE

As a matter of fact, I was kind of rusty when taking my first steps. So first of all, I had to install .NET Core 2.0. This is pretty straightforward and can be done via a simple installer available for all OS.

### Wiring Up a PostgreSQL Docker Container

All of that can be pretty much taken from he official Postgres image on [Dockerhub](https://hub.docker.com/_/postgres/). The only (important) difference is that the container should be bound to localhost in order to be able to be reached from your app.

```bash
docker run --name postgres -p 5432:5432 -e POSTGRES_PASSWORD=mysecretpassword -d postgres
```

### Scaffolding the Migrations

The migrations are generated based on the database provider - which is actually (usually) defined in the ASP.NET project. So you have to call

```bash
dotnet ef migrations add Initial -s ..\Service\Service.csproj
```

from your Persistence project by passing the actual entry point (i.e. startup project) via the `-s [--startup-project]` parameter.