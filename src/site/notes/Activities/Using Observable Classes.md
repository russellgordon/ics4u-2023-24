---
{"dg-publish":true,"permalink":"/activities/using-observable-classes/","dgHomeLink":true,"dgShowToc":true}
---

# Using Observable Classes

## Introduction

In this tutorial you will learn how easy the `Observation` framework makes it to share data among views within a SwiftUI app.

We will extend an app first written in last year's course.

Building the initial app will move quickly so that we can focus on learning how to use the `Observation` framework in this lesson.

When complete, you will have an app that looks like this:

![Screenshot 2024-01-18 at 7.42.33 AM.png|400](/img/user/Media/Screenshot%202024-01-18%20at%207.42.33%E2%80%AFAM.png)

In tomorow's lesson, you will learn how to use the new `SwiftData` framework makes it to persist the data to a database – much more easily than with the `Blackbird` framework we used last year.

Let's get started.

## Project organization

Create a [[Tutorials/Creating a New iOS Project\|new iOS project]] named **EnhancedTodoList**.

In order:

- Delete `ContentView`
- Create two new groups named:
	- `Views`
	- `Model`
- Create a new view named:
	- `LandingView`
- Make the app entry point open `LandingView`
- Create a remote
- Commit and push your work

Some screenshots to help – creating the project:

![Screenshot 2024-01-18 at 9.34.26 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%209.34.26%E2%80%AFAM.png)

After the project has been organized:

![Screenshot 2024-01-18 at 9.37.13 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%209.37.13%E2%80%AFAM.png)

Creating the remote:

![Screenshot 2024-01-18 at 9.37.44 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%209.37.44%E2%80%AFAM.png)

Committing and pushing these changes:

![Screenshot 2024-01-18 at 9.38.35 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%209.38.35%E2%80%AFAM.png)

When complete, your local list of commits should look something like this:

![Screenshot 2024-01-18 at 9.39.06 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%209.39.06%E2%80%AFAM.png)

## Create tab view

`LandingView` will serve as a tab view for navigating between the to-do list and the statistics view.

Begin by creating two more views.

The first named `StatisticsView`:

![Screenshot 2024-01-18 at 9.41.52 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%209.41.52%E2%80%AFAM.png)

The second named  `TodoListView`:

![Screenshot 2024-01-18 at 9.42.23 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%209.42.23%E2%80%AFAM.png)

Then add the following code to `LandingView`:

```swift
import SwiftUI

struct LandingView: View {
    var body: some View {
        TabView {
            TodoListView()
                .tabItem {
                    Text("Tasks")
                    Image(systemName: "checklist")
                }
            
            StatisticsView()
                .tabItem {
                    Text("Stats")
                    Image(systemName: "chart.line.uptrend.xyaxis")
                }
        }
    }
}

#Preview {
    LandingView()
}
```

When on `LandingView` you should see the following:

![Screenshot 2024-01-18 at 9.42.56 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%209.42.56%E2%80%AFAM.png)

Commit and push your work with this message:

```
Added tab view.
```

## Create the model

Make a new Swift file named `TodoItem` with the following code inside:

```swift
import Foundation

struct TodoItem: Identifiable {
    
    let id = UUID()
    var details: String
    let createdOn: Date
    var isCompleted: Bool
    var completedOn: Date?
    
    init(
        details: String,
        createdOn: Date = Date(),
        isCompleted: Bool = false,
        completedOn: Date? = nil
    ) {
        self.details = details
        self.createdOn = createdOn
        self.isCompleted = isCompleted
        self.completedOn = completedOn
    }

}

let exampleData = [
    
    TodoItem(details: "Go for a walk"),
    TodoItem(details: "Study for Physics"),
    TodoItem(details: "Call mom"),
    
]
```

That will look like this:

![Screenshot 2024-01-18 at 9.50.29 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%209.50.29%E2%80%AFAM.png)

Although we do not strictly need to add an initializer when creating a structure, it's helpful here to make it clear that we are assigning default values for certain properties.

- `createdOn` is of type `Date` and assigning it an instance of the `Date()` type sets the value to the current date and time
- `isCompleted` will of course be `false` for a newly created to-do item
- `completedOn` will be set to `nil` since the date the to-do item is completed is not known until it is completed

> [!NOTE]
> We make the `TodoItem` structure conform to the `Identifiable` protocol so that we can use an array of instances of this structure in a scrollable `List` structure in our user interface.

Commit and push your work with this note:

```
Added the initial data model.
```

## Show a scrollable list of data

In `TodoListView` change the preview so that it shows LandingView instead:

![Screenshot 2024-01-18 at 9.59.49 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%209.59.49%E2%80%AFAM.png)

This gives a more realistic preview of what we will see when running the app on a device.

Replace the contents of the `TodoListView` structure with this code instead:

```swift
struct TodoListView: View {
    
    // MARK: Stored properties
    
    // Our list of items to complete
    @State private var items: [TodoItem] = []
    
    // MARK: Computed properties
    var body: some View {
        NavigationStack {
            VStack {
                
                List(items) { currentItem in
                    Label {
                        Text(currentItem.details)
                    } icon: {
                        Image(systemName: currentItem.isCompleted ? "checkmark.circle" : "circle")
                    }
                }
            }
            .navigationTitle("Tasks")
        }
        .onAppear {
            // Populate with example data
            if items.isEmpty {
                items.append(contentsOf: exampleData)
            }
        }
    }
    
}
```

That will look like this:

![Screenshot 2024-01-18 at 10.04.46 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%2010.04.46%E2%80%AFAM.png)

We use the `.onAppear` closure attached to the `NavigationStack` to append our example data from the model to the `items` array.

This will save us from repeatedly having to enter data to test out the interface.

Commit and push your work with this message:

```
Added a scrollable list to show to-do items.
```

## Create placeholder content

If we comment out the line of code that pre-populates the list of to-do items:

![Screenshot 2024-01-18 at 10.06.43 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%2010.06.43%E2%80%AFAM.png)

... the intial interface looks quite bare.

This is what the app would look like on first launch right now.

Apple's [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/) suggest that interfaces give a suggestion of how to get started with using an app.

We can do this by adding an `if-else` statement to the `TodoListView` structure and using the `ContentUnavailableView` that is provided by Apple as part of the SwiftUI framework:

![Screenshot 2024-01-18 at 10.15.36 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%2010.15.36%E2%80%AFAM.png)

Make the same change in your own code by highlighting all the code contained within the `VStack` and replacing it with this code:

```swift
VStack {
	
	if items.isEmpty {
		
		ContentUnavailableView(label: {
			Label(
				"Nothing to do",
				systemImage: "powersleep"
			)
			.foregroundStyle(.green)
		}, description: {
			Text("To-do items will appear here once you add some.")
		})
		
	} else {
		
		List(items) { currentItem in
			Label {
				Text(currentItem.details)
			} icon: {
				Image(systemName: currentItem.isCompleted ? "checkmark.circle" : "circle")
			}
		}
		
	}
}
```

After making that change, try removing the comment on line 51 so that example data is added back in:

![Screenshot 2024-01-18 at 10.17.41 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%2010.17.41%E2%80%AFAM.png)

In this case, we see the list.

Now comment out the code on line 51 again:

![Screenshot 2024-01-18 at 10.17.59 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%2010.17.59%E2%80%AFAM.png)

You see the `ContentUnavailableView` show up.

Commit and push your work with this message:

```
Added a view to tell the user what to do when the app first launches without any data existing yet.
```

## Allow tasks to be added

It follows that we need a way for users to add a task.

Add the following stored property:

```swift
// The item currently being created
@State private var newItemDetails = ""
```

...like this:

![Screenshot 2024-01-18 at 10.21.38 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%2010.21.38%E2%80%AFAM.png)

That will hold the text of the new to-do item being entered by a user.

Next, use code folding to hide the contents of the `body` property that builds the user interface:

![Screenshot 2024-01-18 at 10.22.40 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%2010.22.40%E2%80%AFAM.png)

Now, add the following code after the `body` property, taking care to place it before the closing `}` of the `TodoListView` structure:

```swift
// MARK: Functions
func addItem() {
	let newToDoItem = TodoItem(details: newItemDetails)
	items.insert(newToDoItem, at: 0)
	newItemDetails = ""
}
```

... like this:

![Screenshot 2024-01-18 at 10.29.35 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%2010.29.35%E2%80%AFAM.png)

Finally, unfold the `body` property again, and add this code just before `if-else` statement:

```swift
HStack {
	
	TextField("Enter a to-do item", text: $newItemDetails)
	
	Button("Add") {
		addItem()
	}

}
.padding(20)
```

... like this:

![Screenshot 2024-01-18 at 10.25.45 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%2010.25.45%E2%80%AFAM.png)

You should now be able to add new items to your list.

> [!IMPORTANT]
>
> If the keyboard appears to be frozen, quit Xcode using **Command-Q**, then re-open your project. 
>  
>  Another option is to  run the app in the full Simulator to test the addition of new entries:
> 
> ![Screenshot 2024-01-18 at 10.35.04 AM.png|325](/img/user/Media/Screenshot%202024-01-18%20at%2010.35.04%E2%80%AFAM.png)
> ![Screenshot 2024-01-18 at 10.36.11 AM.png|325](/img/user/Media/Screenshot%202024-01-18%20at%2010.36.11%E2%80%AFAM.png)

Commit and push your work with this message:

```
Made it possible to add new items to the list.
```

## Begin using the Observation framework

If you've added a few items, you probably tried out marking them as complete.

You will note that this does not work.

First, we need to add code to make this happen.

Below the `addItem` function, but before the closing `}` of the `TodoListView` structure, add this code:

```swift
func toggle(item: TodoItem) {
	if item.isCompleted {
		item.completedOn = nil
		item.isCompleted = false
	} else {
		item.completedOn = Date()
		item.isCompleted = true
	}
	
}
```

... like this:

![Screenshot 2024-01-18 at 10.45.56 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%2010.45.56%E2%80%AFAM.png)

You will immediately see error messages.

That is because our model for each instance of a to-do item is a structure:

![Screenshot 2024-01-18 at 10.41.18 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%2010.41.18%E2%80%AFAM.png)

SwiftUI handles instances of structures as *immutable* by default, for performance reasons.

Because of this, individual *properties* of a structure instance within the `items` array cannot be modified. So we cannot change the `isCompleted` property value from `false` to `true`, for example.

SwiftUI *can* see changes in the `items` array itself that holds the list of to-do items:

![Screenshot 2024-01-18 at 10.41.55 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%2010.41.55%E2%80%AFAM.png)

... and that is why the interface updates when we add a new item.

To fix this situation, we need to make  `TodoListItem` into a *class*, rather than having it be a structure.

We must also use the `Observation` framework.

SwiftUI will take care of the remaining details for us – automatically updating the user interface when properties of an instance of `TodoListItem` are changed.

So, next, make these edits on lines 8, 10, and 11, to the `TodoListItem` model file:

![Screenshot 2024-01-18 at 10.57.17 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%2010.57.17%E2%80%AFAM.png)

Then, back on `TodoListView`, add the following code as a view modifier on the `Image` structure that shows the circle for a to-do item:

```swift
.onTapGesture {
	toggle(item: currentItem)
}
```

... like this:

![Screenshot 2024-01-18 at 10.59.34 AM.png](/img/user/Media/Screenshot%202024-01-18%20at%2010.59.34%E2%80%AFAM.png)

You should now find that you can mark to-do items as completed or incomplete.

