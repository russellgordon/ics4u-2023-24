---
{"dg-publish":true,"permalink":"/activities/using-observable-classes-part-2/","dgHomeLink":true,"dgShowToc":true}
---

# Using Observable Classes, Part 2

## Introduction

In [[Activities/Using Observable Classes\|part 1 of this tutorial]] you learned how to re-build most of the to-do list we built over *four* classes last year.

In part 2 of this tutorial we will finish the job, using the `Observation` and `SwiftData` frameworks.

Let's get started.

## Deleting items

To delete items, we must add the `.onDelete` view modifier.

However, the `onDelete` view modifier only works on a `ForEach` structure – it does not work when attached to a `List` structure.

> [!NOTE]
> Why does `.onDelete` not work when attached to a `List` structure?
> 
> Well, a `List` can include static values that are *not* contained in an array:
> 
> ![Screenshot 2024-01-18 at 5.22.49 PM.png|500](/img/user/Media/Screenshot%202024-01-18%20at%205.22.49%E2%80%AFPM.png)
> 
> Of course, static values such as this cannot be deleted.
> 
> A `ForEach` structure only works on arrays of data.
> 
> Of course, arrays of data are dynamic, and so long as an array contains elements, those elements can be deleted.
> 
> This is why `.onDelete` only works on a `ForEach` structure.

Locate the `List` structure in your `TodoListView` file:

![Screenshot 2024-01-18 at 5.24.17 PM.png](/img/user/Media/Screenshot%202024-01-18%20at%205.24.17%E2%80%AFPM.png)

Now change that into a `ForEach`:

![Screenshot 2024-01-18 at 5.25.09 PM.png](/img/user/Media/Screenshot%202024-01-18%20at%205.25.09%E2%80%AFPM.png)

Your view will look odd momentarily, until you enclose the entire `ForEach` structure in a new `List` structure, like this:

![ForEach Into List.gif](/img/user/Media/ForEach%20Into%20List.gif)

Scroll down below the `toggle` function and add the following code, take care to add the function before the closing `}` of the `TodoListView` structure:

```swift
func delete(at offsets: IndexSet) {
	items.remove(atOffsets: offsets)
}
```

... like this:

![Screenshot 2024-01-18 at 5.30.40 PM.png](/img/user/Media/Screenshot%202024-01-18%20at%205.30.40%E2%80%AFPM.png)

Finally, move back up to the `ForEach` structure. Attach this code:

```swift
.onDelete(perform: delete)
```

... to the bottom of the `ForEach` structure, like this:

![Screenshot 2024-01-18 at 5.32.21 PM.png](/img/user/Media/Screenshot%202024-01-18%20at%205.32.21%E2%80%AFPM.png)

You can now swipe to delete items from your to-do list.

Please commit and push your work with this message:

```
Can now delete items from the list.
```

## Add search

To begin adding search capability to the app, first add a stored property to hold the text the user will be using to conduct a search:

```swift
// The search text provided by the user
@State var searchText = ""
```

... like this:

![Screenshot 2024-01-18 at 5.41.38 PM.png](/img/user/Media/Screenshot%202024-01-18%20at%205.41.38%E2%80%AFPM.png)

Next, scroll down to the `List` stucture and add the following view modifier:

```swift
.searchable(text: $searchText)
```

...like this:

![Screenshot 2024-01-18 at 5.43.08 PM.png](/img/user/Media/Screenshot%202024-01-18%20at%205.43.08%E2%80%AFPM.png)

SwiftUI takes care of adding the user interface elements. You can now type in the search field, and what you type will be placed in the `searchText` stored property. However, nothing happens. To fix that, we need to make two more small edits.

First, we need to add a computed property that will take care of filtering our list of to-do items.

Place this code:

```swift
// Provide list of to-do items filtered based on the search text
var filteredItems: [TodoItem] {
	if searchText.isEmpty {
		return items
	} else {
		return items.filter { item in
			item.details.lowercased().contains(searchText.lowercased())
		}
	}
}
```

... above the `body` property but after the stored properties, like this:
