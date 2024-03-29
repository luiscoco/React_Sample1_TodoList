# Start learning React.js: Sample_1 TodoList application

## 0. Prerequisites

Install Node.js

![image](https://github.com/luiscoco/React_Sample1_TodoList/assets/32194879/3e9ec707-26c4-4c2e-a218-466c5fa727d0)



## 1. Application main features

**Components**: Demonstrates the use of functional components for items and classes for lists

**State & Props**: Shows how to manage and pass data within components

**Hooks**: Uses useState and useEffect for state management and side effects

**Event Handling**: Implements form submissions and button clicks to add or remove items

## 2. Application explantaion

### 2.1. Functions

**addTodo**: Adds a new item to the todos array if there's text in the input

**toggleComplete**: Finds the correct todo item by its id and toggles its completed status

**deleteTodo**: Filters out the todo item with the matching id from the todos array

### 2.2. Functionality

**Adding Items**: Type task text into the input field

Clicking "Add" calls the addTodo function, adding a new item to the todos array

**Listing Items**: The TodoList component's render method maps over the todos array

For each item, it creates a <TodoItem /> component, passing the necessary data

**Marking Complete**: Clicking the checkbox next to a todo calls onToggleComplete, which in turn calls the toggleComplete function in TodoList to update the item's status

**Deleting Items**: Clicking "Delete" calls onDelete, triggering deleteTodo in TodoList, removing the item

### 2.3. How It Works Together

The App component acts as the overall container

The TodoList manages the list's state and the logic for adding, updating, and removing tasks

Individual TodoItem components visually represent each todo task

### 2.4. Key Concepts

**React Components**: The app is built as modular components (functional and class-based)

**State Management**: Todo data lives in the TodoList component's state

**Props**: Data is passed down from TodoList to TodoItem components

**Event Handling**: User interactions with checkboxes and buttons trigger functions

**React Hooks**: The provided code uses the useState hook for state management

## 3. Project Setup

**Create React App**: Assuming you haven't already, use this command in your terminal

```
npx create-react-app todo-list-app
cd todo-list-app
```

**File Structure**

![image](https://github.com/luiscoco/React_Sample1_TodoList/assets/32194879/3190d490-ee24-4f4a-a12b-335c102de20b)

## 4. Application source code

### 4.1. TodoItem.js

Defines a simple functional component representing a single todo task

**Props**: It receives properties (todo, onToggleComplete, onDelete) that tell it

The content and completion status of the task (todo)

What functions to call when the task is marked complete/incomplete (onToggleComplete) or deleted (onDelete)

**Rendering**: It displays the task text, a checkbox to mark it as done (with line-through styling if completed), and a "Delete" button

```javascript
import React from 'react';

function TodoItem({ todo, onToggleComplete, onDelete }) {
  return (
    <li style={{ textDecoration: todo.completed ? 'line-through' : 'none' }}>
      <input
        type="checkbox"
        checked={todo.completed}
        onChange={() => onToggleComplete(todo.id)}
      />
      {todo.text}
      <button onClick={() => onDelete(todo.id)}>Delete</button>
    </li>
  );
}

export default TodoItem; 
```

### 4.2. TodoList.js

A class-based component that is the core of the todo list

**State**: Manages these pieces of data:

**todos**: An array of todo items. Each todo item is an object with id, text, and completed properties

**newTodoText**: The text currently entered in the input field for adding tasks

```javascript
import React, { useState } from 'react';
import TodoItem from './TodoItem';

class TodoList extends React.Component {
  state = {
    todos: [],
    newTodoText: ''
  };

  addTodo = () => {
    if (this.state.newTodoText.trim()) { // Prevent empty todos
      this.setState({
        todos: [
          ...this.state.todos, 
          { id: Date.now(), text: this.state.newTodoText, completed: false }
        ],
        newTodoText: ''
      });
    }
  };

  toggleComplete = (id) => {
    this.setState({
      todos: this.state.todos.map(todo => 
        todo.id === id ? { ...todo, completed: !todo.completed } : todo
      )
    });
  };

  deleteTodo = (id) => {
    this.setState({
      todos: this.state.todos.filter(todo => todo.id !== id)
    });
  };

  render() {
    return (
      <div>
        <input 
          type="text" 
          value={this.state.newTodoText}
          onChange={(e) => this.setState({ newTodoText: e.target.value })}
        />
        <button onClick={this.addTodo}>Add</button>
        <ul>
          {this.state.todos.map(todo => (
            <TodoItem 
              key={todo.id} 
              todo={todo} 
              onToggleComplete={this.toggleComplete}
              onDelete={this.deleteTodo}
            />
          ))}
        </ul>
      </div>
    );
  }
}

export default TodoList;
```

### 4.3. App.js

The highest-level component

Renders the "Todo List" title and includes the <TodoList /> component

```javascript
import TodoList from './TodoList';

function App() {
  return (
    <div>
      <h1>Todo List</h1>
      <TodoList />
    </div>
  );
}

export default App;
```

### 4.4. Index.js

#### 4.4.1. Imports

**React**: Imports the core React library, needed to create components and work with React's JSX syntax

**ReactDOM**: Specifically imports the createRoot function from the 'react-dom/client' module. This is needed for rendering React components into the real web page's DOM

**App**: Imports your main App component, which represents the root of your Todo List application

#### 4.4.2. Code

**document.getElementById('root')**: This line finds a DOM element (usually a div) with the ID of "root" in your HTML file. This is your target container

**ReactDOM.createRoot(...)**: This creates a "root" object from ReactDOM, which is the starting point for attaching your React application to the actual webpage

**root.render(...)**: This is the key action that tells React to take control of the content inside the "root" container

**React.StrictMode...**: This optional component helps identify potential problems in your React code during development

**App**: This is where your main App component, containing the rest of your Todo List structure, is placed and rendered into the page

#### 4.4.3. Simplified Explanation

**Find an Anchor**: The code locates the "root" element in your HTML

**Prepare React**: It sets up a connection point between your React code and the webpage

**Display the App**: It tells React to render your Todo List application (the <App /> component and all its components) directly within the "root" element

```javascript
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

## 5. How to run and test the application

### 5.1. Run the application

We load the  libraries/dependences running this command

```
npm install
```

or 

```
npm i
```

If you get errors try to run the command

```
npm audit fix --force
```

If you continue getting errors then run the command

```
npm cache clean --force
```

To run the application run the command

```
npm start
```

### 5.2. Test the application

![image](https://github.com/luiscoco/React_Sample1_TodoList/assets/32194879/4828d663-8cb8-42a6-a4e1-f6617c908d61)

![image](https://github.com/luiscoco/React_Sample1_TodoList/assets/32194879/ec0b314d-293c-45d9-b0ae-6bcb71d7b771)

![image](https://github.com/luiscoco/React_Sample1_TodoList/assets/32194879/f13af9a3-0905-4438-962f-9b6a1b838203)

![image](https://github.com/luiscoco/React_Sample1_TodoList/assets/32194879/395c3f1c-2f88-4139-8db3-654b77352afa)

![image](https://github.com/luiscoco/React_Sample1_TodoList/assets/32194879/1f029a6e-6f64-4ee0-ba16-b4d740f06200)
