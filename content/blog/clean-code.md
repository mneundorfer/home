---
title: "Clean Code Summary"
date: 2018-03-27T13:34:15+01:00
draft: true
tags: ["clean code"]
---

*based on the great Clean Code book by Uncle Bob*

Here, I have distilled the rules which seemed most important for *me* to write down - mostly because I felt I am not following them strictly enough. This is *not a complete list* of all the rules and concepts explained in the book.

## Terms / Concepts

* Single Responsibility Principle `SRP`: A class should only have one reason to change
* Open/Closed Principle `OCP`

## Names

| Rule                  | Description       | Example       |
| --------------------- | ----------------- | ------------- |
| Class Names           | Avoid generic terms such as `Handler`, `Manager`, `Processor`, `Data` |  |
| Method Names          | Verbalization. Also, prefix accessors (`Get`), mutators (`Set`) and predicates (`Is`) | `GetTool`, `IsAvailable`, `AttachSomething` |
| Solution Domain Names | Use well-known terms from CS, such as pattern/concept names. Don't draw too much names from the problem domain to avoid "domain-lock-in" | `JobQueue` |
| Problem Domain Names  | Utilize names from the problem domain. The closer the code is to the problem, the more names from the problem domain should be used |

## Functions

| Rule                  | Description       | Example       |
| --------------------- | ----------------- | ------------- |
| Small                 | Keep functions small. *Really* small. This plays nicely together with "Do one Thing". Rule of thumb: 10 lines are the absolute maximum, less is better
| Do *one* Thing        | See "Small" and `SRP`. A function should do exactly one thing, but it should do that well
| One Level of Abstraction | Avoid mixing levels of abstraction, such as low-level string functions (`append`) and higher-level functions of more complex objects, such as `render` |
| Avoid `switch`        | By definition, does more than one thing. If cannot be avoided, try to bury as deep down as possible | 
| Number of Arguments   | Monadic and dyadic functions should be preferred, triads be avoided at all (or only used in very rare occasions). See also: `SRP`. Also bad: boolean arguments (already suggests that `SRP` is violated)
| Don't return `null`   | This results in every caller having to check for `null`. Instead, use e.g. empty collections

## Comments

| Rule                  | Description       | Example       |
| --------------------- | ----------------- | ------------- |


## Objects and Data Structures

## Error Handling

| Rule                  | Description       | Example       |
| --------------------- | ----------------- | ------------- |
| Exceptions > ErrorCodes 