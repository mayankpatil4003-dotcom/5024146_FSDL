import { useState, useEffect } from 'react'
import './App.css'

function App() {
  // Load todos from localStorage or start with empty array
  const [todos, setTodos] = useState(() => {
    const savedTodos = localStorage.getItem('todos')
    return savedTodos ? JSON.parse(savedTodos) : []
  })
  
  const [input, setInput] = useState('')
  const [filter, setFilter] = useState('all') // 'all', 'active', 'completed'
  const [editingId, setEditingId] = useState(null)
  const [editText, setEditText] = useState('')

  // Save todos to localStorage whenever they change
  useEffect(() => {
    localStorage.setItem('todos', JSON.stringify(todos))
  }, [todos])

  const addTodo = () => {
    if (input.trim()) {
      setTodos([
        ...todos,
        {
          id: Date.now(),
          text: input,
          completed: false,
          createdAt: new Date().toISOString()
        }
      ])
      setInput('')
    }
  }

  const toggleTodo = (id) => {
    setTodos(todos.map(todo =>
      todo.id === id ? { ...todo, completed: !todo.completed } : todo
    ))
  }

  const deleteTodo = (id) => {
    setTodos(todos.filter(todo => todo.id !== id))
  }

  const startEditing = (todo) => {
    setEditingId(todo.id)
    setEditText(todo.text)
  }

  const saveEdit = (id) => {
    if (editText.trim()) {
      setTodos(todos.map(todo =>
        todo.id === id ? { ...todo, text: editText } : todo
      ))
      setEditingId(null)
      setEditText('')
    }
  }

  const cancelEdit = () => {
    setEditingId(null)
    setEditText('')
  }

  const clearCompleted = () => {
    setTodos(todos.filter(todo => !todo.completed))
  }

  const getFilteredTodos = () => {
    switch(filter) {
      case 'active':
        return todos.filter(todo => !todo.completed)
      case 'completed':
        return todos.filter(todo => todo.completed)
      default:
        return todos
    }
  }

  const filteredTodos = getFilteredTodos()
  const activeCount = todos.filter(todo => !todo.completed).length
  const completedCount = todos.filter(todo => todo.completed).length

  return (
    <div className="app">
      <h1>📝 Todo App</h1>
      
      {/* Add Todo Form */}
      <div className="add-todo">
        <input
          type="text"
          value={input}
          onChange={(e) => setInput(e.target.value)}
          onKeyPress={(e) => e.key === 'Enter' && addTodo()}
          placeholder="What needs to be done?"
          className="todo-input"
        />
        <button onClick={addTodo} className="add-btn">Add Todo</button>
      </div>

      {/* Filter Buttons */}
      <div className="filters">
        <button 
          onClick={() => setFilter('all')}
          className={filter === 'all' ? 'active' : ''}
        >
          All ({todos.length})
        </button>
        <button 
          onClick={() => setFilter('active')}
          className={filter === 'active' ? 'active' : ''}
        >
          Active ({activeCount})
        </button>
        <button 
          onClick={() => setFilter('completed')}
          className={filter === 'completed' ? 'active' : ''}
        >
          Completed ({completedCount})
        </button>
      </div>

      {/* Todo List */}
      <ul className="todo-list">
        {filteredTodos.map(todo => (
          <li key={todo.id} className={`todo-item ${todo.completed ? 'completed' : ''}`}>
            {editingId === todo.id ? (
              // Edit Mode
              <div className="edit-mode">
                <input
                  type="text"
                  value={editText}
                  onChange={(e) => setEditText(e.target.value)}
                  onKeyPress={(e) => e.key === 'Enter' && saveEdit(todo.id)}
                  autoFocus
                />
                <div className="edit-actions">
                  <button onClick={() => saveEdit(todo.id)} className="save-btn">💾</button>
                  <button onClick={cancelEdit} className="cancel-btn">❌</button>
                </div>
              </div>
            ) : (
              // View Mode
              <>
                <div className="todo-content">
                  <input
                    type="checkbox"
                    checked={todo.completed}
                    onChange={() => toggleTodo(todo.id)}
                    className="todo-checkbox"
                  />
                  <span 
                    className="todo-text"
                    onDoubleClick={() => startEditing(todo)}
                  >
                    {todo.text}
                  </span>
                </div>
                <div className="todo-actions">
                  <button 
                    onClick={() => startEditing(todo)}
                    className="edit-btn"
                    title="Edit (double-click text)"
                  >
                    ✏️
                  </button>
                  <button 
                    onClick={() => deleteTodo(todo.id)}
                    className="delete-btn"
                    title="Delete"
                  >
                    🗑️
                  </button>
                </div>
              </>
            )}
          </li>
        ))}
      </ul>

      {/* Footer with Stats */}
      {todos.length > 0 && (
        <div className="todo-footer">
          <div className="stats">
            <span>📊 {activeCount} active, {completedCount} completed</span>
          </div>
          {completedCount > 0 && (
            <button onClick={clearCompleted} className="clear-btn">
              Clear Completed
            </button>
          )}
        </div>
      )}

      {/* Empty State */}
      {todos.length === 0 && (
        <div className="empty-state">
          <p>🎉 No todos! Add one above to get started.</p>
        </div>
      )}
    </div>
  )
}

export default App