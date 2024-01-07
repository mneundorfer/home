---
title: ".NET ChangerTracker Behavior"
date: 2024-01-07T20:53:53+02:00
---

One key aspect which was not very intuitive for me is that the `ChangeTracker` is *not* cleared when `SaveChanges()` is called. Instead, all tracked entities are kept within the `ChangeTracker`.

While this has been an explicit design decision by the EF Core team, this can result in unexpected behavior when using multiple DB contexts in parallel, like e.g. when running integration tests.

In my test setups, I usually inject an instance of a `DbContext` to set up or validate tests. This `DbContext` then lives during the whole test execution.

```cs
// arrange
_dbContext.Items.Add(new Item(1, "Value"));
_dbContext.SaveChanges();

// act
(Test Execution altering Item 1)

// assert
_dbContext.Items.Single(i => i.Id == 1).Value.ShouldBe("NewValue"); // fails
```

This will fail, as the item is already tracked after the test setup ("arrange"). The production code alters the item in the database (e.g. changes "Value" to "NewValue"), but that will not be reflected in the `_dbContext` instance which is used in the test.

Adding `_dbContext.ChangeTracker.Clear();` *before* the assertions resolves this issue.

Note: There's one exception to the rule: If a tracked item is *deleted* in between, this will be detected by EF)