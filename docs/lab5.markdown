---
layout: default
title: "Lab 5: TODO App"
permalink: /lab-5/
---
<article
  class="post h-entry"
  itemscope
  itemtype="http://schema.org/BlogPosting"
>
  <header class="post-header">
    <h1 class="post-title p-name" itemprop="name headline">
      {{ page.title | escape }}
    </h1>
  </header>
  <div>
    <!-- create a text input and a submit button below it -->
    <input type="text" id="todo-input" />
    <button id="todo-submit">New Item</button>
    <ul id="todo-list"></ul>
    <button id="todo-clear">Clear Completed</button>
    <button id="todo-clear-all">Clear All</button>
    <script>
        const todoItems = JSON.parse(localStorage.getItem('todoItems')) || {};
        function renderTodoListItem(todoItem) {
            const todoItemElement = document.createElement('li');
            const todoCheckbox = document.createElement('input');
            todoCheckbox.type = 'checkbox';
            todoCheckbox.addEventListener('click', function() {
                if (todoCheckbox.checked) {
                    todoItemElement.style.textDecoration = 'line-through';
                    todoItems[todoItem] = true;
                } else {
                    todoItemElement.style.textDecoration = 'none';
                    todoItems[todoItem] = false;
                }
                localStorage.setItem('todoItems', JSON.stringify(todoItems));
            });
            if (todoItems[todoItem]) {
                todoCheckbox.checked = true;
                todoItemElement.style.textDecoration = 'line-through';
            } else {
                todoCheckbox.checked = false;
                todoItemElement.style.textDecoration = 'none';
            }
            localStorage.setItem('todoItems', JSON.stringify(todoItems));
            const todoDelete = document.createElement('button');
            todoDelete.innerHTML = 'Delete';
            todoDelete.addEventListener('click', function() {
                todoItemElement.remove();
                delete todoItems[todoItem];
                localStorage.setItem('todoItems', JSON.stringify(todoItems));
            });
            todoItemElement.appendChild(todoCheckbox);
            todoItemElement.appendChild(document.createTextNode(todoItem));
            todoItemElement.appendChild(todoDelete);
            document.getElementById('todo-list').appendChild(todoItemElement);
        }
        // Render any existing todo items
        for (const todoItem in todoItems) {
            renderTodoListItem(todoItem);
        }
        // Create a new list item when the button is clicked
        const todoSubmit = document.getElementById('todo-submit');
        const todoInput = document.getElementById('todo-input');
        todoSubmit.addEventListener('click', function() {
            if (todoInput.value === '' || todoInput.value in todoItems) {
                return;
            }
            // add the todoInput to localStorage
            todoItems[todoInput.value] = false;
            renderTodoListItem(todoInput.value);
            todoInput.value = '';
        });
        // Button to clear all checked items
        const todoClear = document.getElementById('todo-clear');
        todoClear.addEventListener('click', function() {
            for (const todoItem in todoItems) {
                if (todoItems[todoItem]) {
                    delete todoItems[todoItem];
                }
            }
            localStorage.setItem('todoItems', JSON.stringify(todoItems));
            document.getElementById('todo-list').innerHTML = '';
            for (const todoItem in todoItems) {
                renderTodoListItem(todoItem);
            }
        });
        // Button to clear all items
        const todoClearAll = document.getElementById('todo-clear-all');
        todoClearAll.addEventListener('click', function() {
            localStorage.setItem('todoItems', JSON.stringify({}));
            document.getElementById('todo-list').innerHTML = '';
        });
    </script>
    <style>
        #todo-input {
            margin-bottom: 10px;
        }
        #todo-list {
            list-style-type: none;
            margin: 0;
            padding: 0;
        }
        #todo-list li {
            margin-bottom: 10px;
            border: 1px solid lightgray;
            border-radius: 5px;
            padding: 10px;
        }
        #todo-list li button {
            float: right;
        }
    </style>
  </div>
</article>