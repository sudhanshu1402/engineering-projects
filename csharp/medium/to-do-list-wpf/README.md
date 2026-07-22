# ToDo List (WPF)

The XAML layout for a minimal to-do window: a text box, an "Add Task" button, and a list of tasks.

## What this is

A single WPF window definition. It lays out three controls in a vertical `StackPanel`:

- `TaskInput` — a `TextBox` for typing a task
- an "Add Task" `Button` wired to a `AddTask_Click` handler
- `TasksList` — a `ListBox` that shows the tasks

That's the whole file. This is a learning exercise in WPF XAML markup, not a finished app.

## Heads up: this won't run on its own

`main-window.xaml` is only the view. To actually build and run it you'd need the parts that aren't in this folder:

- The code-behind (`MainWindow.xaml.cs`) with the `AddTask_Click` method the button points at, and the `TodoList.MainWindow` class the XAML declares.
- A WPF project file (`.csproj`) targeting `net-windowsX.X` with `<UseWPF>true</UseWPF>`.
- An `App.xaml` / entry point.

The intended behavior is obvious from the markup: type into `TaskInput`, click the button, and the text gets added to `TasksList`. A matching handler would be roughly:

```csharp
private void AddTask_Click(object sender, RoutedEventArgs e)
{
    if (!string.IsNullOrWhiteSpace(TaskInput.Text))
    {
        TasksList.Items.Add(TaskInput.Text);
        TaskInput.Clear();
    }
}
```

But no `.cs` file exists here — that snippet is the missing piece, not something in the repo.

## The markup

```xml
<Window x:Class="TodoList.MainWindow" ...
        Title="ToDo List" Height="300" Width="300">
    <StackPanel>
        <TextBox Name="TaskInput" />
        <Button Content="Add Task" Click="AddTask_Click"/>
        <ListBox Name="TasksList" />
    </StackPanel>
</Window>
```

## Scope

Practice snippet. It captures the layout half of a classic WPF to-do example; the logic and project scaffolding are left out.
