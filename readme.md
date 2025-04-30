# Sistema de Comentarios en React

Este proyecto implementa un sistema simple de comentarios utilizando React con CDN (sin build tools). El sistema permite a los usuarios añadir comentarios a través de un formulario y ver una lista actualizada de todos los comentarios enviados.

## Características

- Creación de componentes React funcionales
- Uso de JSX con Babel standalone
- Manejo de estado con React Hooks (useState)
- Comunicación entre componentes padre-hijo mediante props
- Renderizado dinámico de listas
- Manejo de formularios y eventos de usuario
- Todo en un único archivo HTML sin dependencias externas

## Estructura de Componentes

### Componente App (Componente Principal)

Responsabilidades:

- Mantiene el estado global de la aplicación (lista de comentarios)
- Renderiza el título principal
- Renderiza el componente CommentForm
- Renderiza la lista de comentarios
- Proporciona la función para añadir nuevos comentarios

Código relevante:

```jsx
function App() {
  // Estado para almacenar la lista de comentarios
  const [comments, setComments] = React.useState([]);

  // Función para añadir un nuevo comentario
  const addComment = (newComment) => {
    setComments([...comments, newComment]);
  };

  return (
    <div>
      <h1>¡Hola, bienvenido a React!</h1>
      <CommentForm onAddComment={addComment} />
      <div className="comment-list">
        <h2>Comentarios ({comments.length})</h2>
        {comments.length === 0 && (
          <p>No hay comentarios. ¡Sé el primero en comentar!</p>
        )}
        {comments.map((comment, index) => (
          <CommentItem key={index} text={comment} index={index} />
        ))}
      </div>
    </div>
  );
}
```

### Componente CommentForm (Hijo)

Responsabilidades:

- Maneja el estado local del texto del comentario
- Captura la entrada del usuario
- Valida que el comentario no esté vacío
- Envía el comentario al componente padre
- Limpia el campo de entrada después del envío

Código relevante:

```jsx
function CommentForm({ onAddComment }) {
  // Estado para el campo de entrada
  const [commentText, setCommentText] = React.useState("");

  // Función para manejar cambios en el input
  const handleInputChange = (e) => {
    setCommentText(e.target.value);
  };

  // Función para manejar el envío del formulario
  const handleSubmit = (e) => {
    e.preventDefault();

    if (commentText.trim() !== "") {
      // Enviar el comentario al componente padre
      onAddComment(commentText);

      // Limpiar el campo después del envío
      setCommentText("");
    }
  };

  return (
    <div className="comment-form">
      <h2>Añadir nuevo comentario</h2>
      <form onSubmit={handleSubmit}>
        <input
          type="text"
          value={commentText}
          onChange={handleInputChange}
          placeholder="Escribe tu comentario aquí..."
        />
        <button type="submit">Enviar comentario</button>
      </form>
    </div>
  );
}
```

### Componente CommentItem (Hijo)

Responsabilidades:

- Renderiza un comentario individual
- Muestra el número y texto del comentario

Código relevante:

```jsx
function CommentItem({ text, index }) {
  return (
    <div className="comment-item">
      <strong>Comentario #{index + 1}:</strong> {text}
    </div>
  );
}
```

## Flujo de Datos

1. **Inicialización**:

   - El componente `App` crea un estado vacío para los comentarios: `const [comments, setComments] = React.useState([])`.
   - Pasa la función `addComment` como prop al componente `CommentForm`.

2. **Entrada de Usuario**:

   - El usuario escribe un comentario en el campo de texto.
   - El estado local en `CommentForm` se actualiza con cada pulsación de tecla mediante `handleInputChange`.

3. **Envío del Comentario**:

   - El usuario hace clic en "Enviar comentario".
   - Se ejecuta `handleSubmit` que previene la recarga de la página con `e.preventDefault()`.
   - Se valida que el comentario no esté vacío.
   - Se llama a la función `onAddComment` pasando el texto del comentario al componente padre.
   - Se limpia el campo de entrada.

4. **Actualización del Estado**:

   - En `App`, la función `addComment` actualiza el estado `comments` añadiendo el nuevo comentario al array existente.
   - React detecta el cambio de estado y re-renderiza los componentes afectados.

5. **Renderizado de la Lista**:
   - La lista de comentarios se renderiza utilizando el método `map()` para transformar cada comentario en un componente `CommentItem`.
   - Si no hay comentarios, se muestra un mensaje indicándolo.

## Tecnologías Utilizadas

- **React 18**: Biblioteca JavaScript para construir interfaces de usuario.
- **ReactDOM 18**: Renderizador de React para el DOM.
- **Babel**: Transpilador que permite utilizar JSX sin necesidad de un entorno de construcción.
- **HTML5 / CSS3**: Para la estructura y estilos básicos.

## Cómo Ejecutar el Proyecto

1. Simplemente abre el archivo `index.html` en un navegador web moderno.
