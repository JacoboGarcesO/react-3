# CLASE: Hooks (useState, useEffect) y React Router (2 horas)

---

## ESPACIO INICIAL: Discusión de Proyecto (20 min)

### Objetivos de esta sesión:
- Revisar el progreso del proyecto en curso
- Discutir dudas y desafíos encontrados
- Compartir avances individuales o de equipo
- Alinear próximos pasos y entregables

### Temas a abordar:
1. **Estado actual del proyecto** (5 min)
   - ¿En qué fase estamos?
   - ¿Qué se ha completado?
   - ¿Qué está pendiente?

2. **Desafíos y soluciones** (8 min)
   - Problemas técnicos encontrados
   - Dificultades de implementación
   - Compartir soluciones entre el equipo

3. **Próximos pasos** (5 min)
   - Definir tareas para la semana
   - Establecer prioridades
   - Asignar responsabilidades

4. **Conexión con el tema de hoy** (2 min)
   - ¿Cómo aplican los hooks al proyecto?
   - ¿Necesitaremos routing en nuestro proyecto?

---

## HORA 1: Hooks - useState y useEffect (60 min)

### 1.1 Introducción a los Hooks (5 min)

**¿Qué son los Hooks?**
- Funciones especiales de React que "enganchan" funcionalidades a componentes
- Permiten usar estado y otras características sin clases
- Siempre empiezan con "use" (useState, useEffect, useContext, etc.)

**Reglas de los Hooks:**
1. ✅ Solo llamarlos en el nivel superior (NO dentro de loops, condicionales o funciones anidadas)
2. ✅ Solo llamarlos en componentes de React o custom hooks
3. ❌ NO llamarlos en funciones JavaScript normales

**Hoy veremos los 2 hooks más importantes:**
- `useState`: para manejar estado
- `useEffect`: para efectos secundarios

---

### 1.2 useState - Estado en Componentes (25 min)

**¿Qué es el estado?**
- Datos que pueden cambiar en el tiempo
- Cuando el estado cambia, React re-renderiza el componente
- Permite que la UI sea dinámica e interactiva

**Sintaxis básica:**

```jsx
const [variable, setVariable] = useState(valorInicial)
```

- `variable`: el valor actual del estado
- `setVariable`: función para actualizar el estado
- `valorInicial`: valor inicial del estado

---

**Ejemplo 1: Contador Simple**

**Crear `src/components/Contador.jsx`:**

```jsx
import { useState } from 'react'
import './Contador.css'

function Contador() {
  // Declarar estado
  const [contador, setContador] = useState(0)
  
  // Funciones para modificar el estado
  const incrementar = () => {
    setContador(contador + 1)
  }
  
  const decrementar = () => {
    setContador(contador - 1)
  }
  
  const reiniciar = () => {
    setContador(0)
  }
  
  return (
    <div className="contador">
      <h2>Contador: {contador}</h2>
      <div className="botones">
        <button onClick={decrementar}>-</button>
        <button onClick={reiniciar}>Reset</button>
        <button onClick={incrementar}>+</button>
      </div>
    </div>
  )
}

export default Contador
```

**Crear `src/components/Contador.css`:**

```css
.contador {
  text-align: center;
  padding: 30px;
  background-color: white;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  max-width: 400px;
  margin: 20px auto;
}

.contador h2 {
  font-size: 2.5rem;
  color: #667eea;
  margin-bottom: 20px;
}

.botones {
  display: flex;
  gap: 15px;
  justify-content: center;
}

.botones button {
  padding: 12px 30px;
  font-size: 1.2rem;
  font-weight: 600;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  background-color: #667eea;
  color: white;
  transition: all 0.3s;
}

.botones button:hover {
  background-color: #5568d3;
  transform: translateY(-2px);
}
```

**Usar en App.jsx:**

```jsx
import Contador from './components/Contador'

function App() {
  return (
    <div style={{ padding: '20px' }}>
      <h1 style={{ textAlign: 'center' }}>Demo de useState</h1>
      <Contador />
    </div>
  )
}

export default App
```

---

**Ejemplo 2: Toggle de Visibilidad**

**Crear `src/components/Toggle.jsx`:**

```jsx
import { useState } from 'react'
import './Toggle.css'

function Toggle() {
  const [visible, setVisible] = useState(true)
  
  const toggleVisibilidad = () => {
    setVisible(!visible)  // Invierte el valor booleano
  }
  
  return (
    <div className="toggle-container">
      <button onClick={toggleVisibilidad}>
        {visible ? 'Ocultar' : 'Mostrar'} Contenido
      </button>
      
      {visible && (
        <div className="contenido">
          <h3>¡Contenido Visible! 👀</h3>
          <p>Este contenido se muestra y oculta con useState</p>
        </div>
      )}
    </div>
  )
}

export default Toggle
```

**Crear `src/components/Toggle.css`:**

```css
.toggle-container {
  padding: 30px;
  text-align: center;
  max-width: 500px;
  margin: 20px auto;
}

.toggle-container button {
  padding: 12px 30px;
  font-size: 1rem;
  font-weight: 600;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s;
}

.toggle-container button:hover {
  background-color: #218838;
}

.contenido {
  margin-top: 20px;
  padding: 20px;
  background-color: #e7f3ff;
  border-radius: 8px;
  border: 2px solid #667eea;
}

.contenido h3 {
  color: #667eea;
  margin-bottom: 10px;
}
```

---

**Ejemplo 3: Input Controlado**

**Crear `src/components/FormularioNombre.jsx`:**

```jsx
import { useState } from 'react'
import './FormularioNombre.css'

function FormularioNombre() {
  const [nombre, setNombre] = useState('')
  
  const manejarCambio = (e) => {
    setNombre(e.target.value)
  }
  
  return (
    <div className="formulario-nombre">
      <h2>Hola, {nombre || 'Invitado'}! 👋</h2>
      
      <input
        type="text"
        placeholder="Escribe tu nombre..."
        value={nombre}
        onChange={manejarCambio}
      />
      
      <p className="info">Caracteres: {nombre.length}</p>
    </div>
  )
}

export default FormularioNombre
```

**Crear `src/components/FormularioNombre.css`:**

```css
.formulario-nombre {
  text-align: center;
  padding: 30px;
  background-color: white;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  max-width: 500px;
  margin: 20px auto;
}

.formulario-nombre h2 {
  color: #667eea;
  margin-bottom: 20px;
}

.formulario-nombre input {
  width: 100%;
  padding: 12px;
  font-size: 1rem;
  border: 2px solid #ddd;
  border-radius: 8px;
  transition: border-color 0.3s;
}

.formulario-nombre input:focus {
  outline: none;
  border-color: #667eea;
}

.info {
  margin-top: 10px;
  color: #666;
  font-size: 0.9rem;
}
```

---

**Puntos clave de useState:**
- ✅ Siempre usar la función `set` para actualizar el estado
- ❌ NUNCA modificar el estado directamente: `contador = 5` ❌
- ✅ React re-renderiza automáticamente cuando el estado cambia
- ✅ Puedes tener múltiples `useState` en un componente

---

### 1.3 useEffect - Efectos Secundarios (30 min)

**¿Qué son los efectos secundarios?**
- Operaciones que afectan cosas fuera del componente
- Ejemplos: fetch de datos, timers, suscripciones, manipulación del DOM

**Sintaxis básica:**

```jsx
useEffect(() => {
  // Código del efecto
  
  return () => {
    // Función de limpieza (opcional)
  }
}, [dependencias])
```

**Array de dependencias:**
- `[]` vacío: se ejecuta una sola vez (al montar el componente)
- `[variable]`: se ejecuta cada vez que `variable` cambia
- Sin array: se ejecuta en cada render (rara vez usado)

---

**Ejemplo 1: Título del Documento**

**Crear `src/components/CambiadorTitulo.jsx`:**

```jsx
import { useState, useEffect } from 'react'
import './CambiadorTitulo.css'

function CambiadorTitulo() {
  const [contador, setContador] = useState(0)
  
  // useEffect se ejecuta cada vez que contador cambia
  useEffect(() => {
    document.title = `Contador: ${contador}`
    
    // Función de limpieza (opcional aquí)
    return () => {
      document.title = 'React App'
    }
  }, [contador])  // 👈 Dependencia: se ejecuta cuando contador cambia
  
  return (
    <div className="cambiador-titulo">
      <h2>Mira el título de la pestaña del navegador 👆</h2>
      <p>Contador: {contador}</p>
      <button onClick={() => setContador(contador + 1)}>
        Incrementar
      </button>
    </div>
  )
}

export default CambiadorTitulo
```

---

**Ejemplo 2: Fetch de Datos (API)**

**Crear `src/components/ListaUsuarios.jsx`:**

```jsx
import { useState, useEffect } from 'react'
import './ListaUsuarios.css'

function ListaUsuarios() {
  const [usuarios, setUsuarios] = useState([])
  const [cargando, setCargando] = useState(true)
  const [error, setError] = useState(null)
  
  useEffect(() => {
    // Fetch de datos al montar el componente
    fetch('https://jsonplaceholder.typicode.com/users')
      .then(response => response.json())
      .then(data => {
        setUsuarios(data)
        setCargando(false)
      })
      .catch(err => {
        setError(err.message)
        setCargando(false)
      })
  }, [])  // 👈 Array vacío: se ejecuta solo una vez
  
  if (cargando) {
    return <div className="lista-usuarios">Cargando usuarios...</div>
  }
  
  if (error) {
    return <div className="lista-usuarios error">Error: {error}</div>
  }
  
  return (
    <div className="lista-usuarios">
      <h2>Lista de Usuarios</h2>
      <div className="usuarios-grid">
        {usuarios.map(usuario => (
          <div key={usuario.id} className="usuario-card">
            <h3>{usuario.name}</h3>
            <p>📧 {usuario.email}</p>
            <p>🏢 {usuario.company.name}</p>
          </div>
        ))}
      </div>
    </div>
  )
}

export default ListaUsuarios
```

**Crear `src/components/ListaUsuarios.css`:**

```css
.lista-usuarios {
  padding: 30px;
  max-width: 1200px;
  margin: 0 auto;
}

.lista-usuarios h2 {
  text-align: center;
  color: #2c3e50;
  margin-bottom: 30px;
}

.usuarios-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
}

.usuario-card {
  background-color: white;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s;
}

.usuario-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.usuario-card h3 {
  color: #667eea;
  margin-bottom: 10px;
}

.usuario-card p {
  color: #666;
  margin: 5px 0;
}

.error {
  color: red;
  text-align: center;
  padding: 20px;
}
```

---

**Ejemplo 3: Timer con Limpieza**

**Crear `src/components/Temporizador.jsx`:**

```jsx
import { useState, useEffect } from 'react'
import './Temporizador.css'

function Temporizador() {
  const [segundos, setSegundos] = useState(0)
  const [activo, setActivo] = useState(false)
  
  useEffect(() => {
    let intervalo = null
    
    if (activo) {
      intervalo = setInterval(() => {
        setSegundos(seg => seg + 1)
      }, 1000)
    }
    
    // 👇 Función de limpieza: detiene el intervalo
    return () => {
      if (intervalo) {
        clearInterval(intervalo)
      }
    }
  }, [activo])  // Se ejecuta cuando 'activo' cambia
  
  const toggleTimer = () => {
    setActivo(!activo)
  }
  
  const reiniciar = () => {
    setSegundos(0)
    setActivo(false)
  }
  
  return (
    <div className="temporizador">
      <h2>⏱️ Temporizador</h2>
      <div className="tiempo">{segundos}s</div>
      <div className="controles">
        <button onClick={toggleTimer}>
          {activo ? 'Pausar' : 'Iniciar'}
        </button>
        <button onClick={reiniciar}>Reiniciar</button>
      </div>
    </div>
  )
}

export default Temporizador
```

**Crear `src/components/Temporizador.css`:**

```css
.temporizador {
  text-align: center;
  padding: 40px;
  background-color: white;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  max-width: 400px;
  margin: 20px auto;
}

.temporizador h2 {
  color: #2c3e50;
  margin-bottom: 20px;
}

.tiempo {
  font-size: 4rem;
  font-weight: 700;
  color: #667eea;
  margin: 30px 0;
}

.controles {
  display: flex;
  gap: 15px;
  justify-content: center;
}

.controles button {
  padding: 12px 30px;
  font-size: 1rem;
  font-weight: 600;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  background-color: #667eea;
  color: white;
  transition: all 0.3s;
}

.controles button:hover {
  background-color: #5568d3;
}
```

---

**Puntos clave de useEffect:**
- ✅ Ideal para fetch de datos, suscripciones, timers
- ✅ Array de dependencias controla cuándo se ejecuta
- ✅ Función de limpieza previene memory leaks
- ❌ No usar para lógica que debería estar en event handlers

---

## HORA 2: React Router (60 min)

### 2.1 ¿Qué es React Router? (5 min)

**React Router** es una librería para manejar navegación en aplicaciones React.

**¿Por qué lo necesitamos?**
- React es SPA (Single Page Application)
- Necesitamos múltiples "páginas" sin recargar
- Queremos URLs limpias y navegación fluida
- Necesitamos navegación programática

**Instalación:**
```bash
npm install react-router-dom
```

---

### 2.2 Conceptos Básicos (10 min)

**Componentes principales:**

1. **`<BrowserRouter>`**: Envuelve toda la app
2. **`<Routes>`**: Contenedor de rutas
3. **`<Route>`**: Define una ruta
4. **`<Link>`**: Navegación sin recargar
5. **`useNavigate`**: Navegación programática

**Ejemplo simple de estructura:**

```jsx
<BrowserRouter>
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="/about" element={<About />} />
  </Routes>
</BrowserRouter>
```

---

### 2.3 Crear Páginas (20 min)

**Crear carpeta `src/pages/`**

**Crear `src/pages/Home.jsx`:**

```jsx
import './Page.css'

function Home() {
  return (
    <div className="page home-page">
      <h1>🏠 Bienvenido a Mi App</h1>
      <p className="intro">
        Esta es una aplicación de demostración de React con Hooks y React Router.
      </p>
      
      <div className="features">
        <div className="feature-card">
          <h3>⚡ Rápido</h3>
          <p>Navegación sin recargas de página</p>
        </div>
        <div className="feature-card">
          <h3>🎨 Moderno</h3>
          <p>Diseño limpio y responsive</p>
        </div>
        <div className="feature-card">
          <h3>🚀 Potente</h3>
          <p>Construido con React y Hooks</p>
        </div>
      </div>
    </div>
  )
}

export default Home
```

**Crear `src/pages/Home.css`:**

```css
.home-page {
  text-align: center;
}

.intro {
  font-size: 1.2rem;
  color: #666;
  max-width: 600px;
  margin: 20px auto 50px;
}

.features {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 30px;
  max-width: 900px;
  margin: 0 auto;
}

.feature-card {
  background-color: white;
  padding: 40px 30px;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s;
}

.feature-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 8px 12px rgba(0, 0, 0, 0.15);
}

.feature-card h3 {
  color: #667eea;
  font-size: 1.5rem;
  margin-bottom: 15px;
}

.feature-card p {
  color: #666;
  font-size: 1rem;
}
```

---

**Crear `src/pages/About.jsx`:**

```jsx
import './Page.css'

function About() {
  return (
    <div className="page about-page">
      <h1>📖 Sobre Nosotros</h1>
      
      <div className="about-content">
        <section className="about-section">
          <h2>Nuestra Historia</h2>
          <p>
            Somos un equipo apasionado por crear experiencias web increíbles 
            usando las últimas tecnologías de React.
          </p>
        </section>
        
        <section className="about-section">
          <h2>Nuestra Misión</h2>
          <p>
            Proporcionar aplicaciones web rápidas, accesibles y hermosas 
            que mejoren la vida de nuestros usuarios.
          </p>
        </section>
        
        <section className="about-section">
          <h2>Tecnologías</h2>
          <div className="tech-list">
            <span className="tech-badge">⚛️ React</span>
            <span className="tech-badge">🎣 Hooks</span>
            <span className="tech-badge">🛣️ React Router</span>
            <span className="tech-badge">🎨 CSS3</span>
          </div>
        </section>
      </div>
    </div>
  )
}

export default About
```

**Crear `src/pages/About.css`:**

```css
.about-page {
  max-width: 800px;
  margin: 0 auto;
}

.about-content {
  background-color: white;
  padding: 40px;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.about-section {
  margin-bottom: 40px;
}

.about-section:last-child {
  margin-bottom: 0;
}

.about-section h2 {
  color: #667eea;
  margin-bottom: 15px;
}

.about-section p {
  color: #555;
  line-height: 1.6;
  font-size: 1.1rem;
}

.tech-list {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
  margin-top: 20px;
}

.tech-badge {
  background-color: #667eea;
  color: white;
  padding: 10px 20px;
  border-radius: 20px;
  font-weight: 600;
}
```

---

**Crear `src/pages/Contact.jsx`:**

```jsx
import { useState } from 'react'
import './Contact.css'

function Contact() {
  const [formData, setFormData] = useState({
    nombre: '',
    email: '',
    mensaje: ''
  })
  
  const [enviado, setEnviado] = useState(false)
  
  const manejarCambio = (e) => {
    setFormData({
      ...formData,
      [e.target.name]: e.target.value
    })
  }
  
  const manejarEnvio = (e) => {
    e.preventDefault()
    console.log('Datos del formulario:', formData)
    setEnviado(true)
    
    // Reiniciar después de 3 segundos
    setTimeout(() => {
      setEnviado(false)
      setFormData({ nombre: '', email: '', mensaje: '' })
    }, 3000)
  }
  
  return (
    <div className="page contact-page">
      <h1>📬 Contáctanos</h1>
      
      {enviado ? (
        <div className="mensaje-exito">
          <h2>✅ ¡Mensaje enviado con éxito!</h2>
          <p>Nos pondremos en contacto pronto.</p>
        </div>
      ) : (
        <form className="contact-form" onSubmit={manejarEnvio}>
          <div className="form-group">
            <label>Nombre:</label>
            <input
              type="text"
              name="nombre"
              value={formData.nombre}
              onChange={manejarCambio}
              required
            />
          </div>
          
          <div className="form-group">
            <label>Email:</label>
            <input
              type="email"
              name="email"
              value={formData.email}
              onChange={manejarCambio}
              required
            />
          </div>
          
          <div className="form-group">
            <label>Mensaje:</label>
            <textarea
              name="mensaje"
              value={formData.mensaje}
              onChange={manejarCambio}
              rows="5"
              required
            />
          </div>
          
          <button type="submit">Enviar Mensaje</button>
        </form>
      )}
    </div>
  )
}

export default Contact
```

**Crear `src/pages/Contact.css`:**

```css
.contact-page {
  max-width: 600px;
  margin: 0 auto;
}

.contact-form {
  background-color: white;
  padding: 40px;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.form-group {
  margin-bottom: 20px;
}

.form-group label {
  display: block;
  margin-bottom: 8px;
  color: #333;
  font-weight: 600;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 12px;
  border: 2px solid #ddd;
  border-radius: 8px;
  font-size: 1rem;
  font-family: inherit;
  transition: border-color 0.3s;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #667eea;
}

.contact-form button {
  width: 100%;
  padding: 15px;
  background-color: #667eea;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 1.1rem;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.3s;
}

.contact-form button:hover {
  background-color: #5568d3;
}

.mensaje-exito {
  background-color: white;
  padding: 60px 40px;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  text-align: center;
}

.mensaje-exito h2 {
  color: #28a745;
  margin-bottom: 15px;
}
```

---

**Crear estilos globales para todas las páginas `src/pages/Page.css`:**

```css
.page {
  padding: 40px 20px;
  min-height: calc(100vh - 200px);
}

.page h1 {
  color: #2c3e50;
  margin-bottom: 30px;
  font-size: 2.5rem;
}
```

**Importar en cada página:**
```jsx
import './Page.css'
```

---

### 2.4 Configurar React Router (15 min)

**Actualizar `src/App.jsx`:**

```jsx
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom'
import Home from './pages/Home'
import About from './pages/About'
import Contact from './pages/Contact'
import './App.css'

function App() {
  return (
    <BrowserRouter>
      <div className="app">
        {/* Navbar de navegación */}
        <nav className="navbar">
          <div className="nav-brand">Mi App</div>
          <div className="nav-links">
            <Link to="/">Inicio</Link>
            <Link to="/about">Nosotros</Link>
            <Link to="/contact">Contacto</Link>
          </div>
        </nav>
        
        {/* Contenido que cambia según la ruta */}
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
          <Route path="/contact" element={<Contact />} />
        </Routes>
        
        {/* Footer */}
        <footer className="footer">
          <p>© 2025 Mi App React - Todos los derechos reservados</p>
        </footer>
      </div>
    </BrowserRouter>
  )
}

export default App
```

**Actualizar `src/App.css`:**

```css
.app {
  min-height: 100vh;
  background-color: #f8f9fa;
}

/* Navbar */
.navbar {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  padding: 20px 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.nav-brand {
  color: white;
  font-size: 1.5rem;
  font-weight: 700;
}

.nav-links {
  display: flex;
  gap: 30px;
}

.nav-links a {
  color: white;
  text-decoration: none;
  font-weight: 600;
  font-size: 1.1rem;
  transition: opacity 0.3s;
}

.nav-links a:hover {
  opacity: 0.8;
}

/* Footer */
.footer {
  background-color: #2c3e50;
  color: white;
  text-align: center;
  padding: 30px;
  margin-top: 60px;
}

.footer p {
  margin: 0;
}
```

---

**Explicar los componentes de React Router:**

1. **`<BrowserRouter>`**: Envuelve toda la app para habilitar el routing
2. **`<Routes>`**: Contenedor para todas las rutas
3. **`<Route>`**: Define una ruta específica
   - `path`: la URL (ej: "/about")
   - `element`: el componente a mostrar
4. **`<Link>`**: Enlace para navegar (reemplaza `<a>`)
   - `to`: la ruta de destino

**¡Guardar y probar en el navegador!**

Ahora deberían poder navegar entre páginas sin recargar.

---

### 2.5 Navegación Programática (10 min)

**A veces necesitamos navegar mediante código (no con clicks)**

**Ejemplo: Redirigir después de enviar un formulario**

**Actualizar `src/pages/Contact.jsx`:**

```jsx
import { useState } from 'react'
import { useNavigate } from 'react-router-dom'  // 👈 Importar hook
import './Contact.css'

function Contact() {
  const navigate = useNavigate()  // 👈 Obtener función de navegación
  const [formData, setFormData] = useState({
    nombre: '',
    email: '',
    mensaje: ''
  })
  
  const manejarCambio = (e) => {
    setFormData({
      ...formData,
      [e.target.name]: e.target.value
    })
  }
  
  const manejarEnvio = (e) => {
    e.preventDefault()
    console.log('Datos del formulario:', formData)
    
    // Simular envío
    alert('¡Mensaje enviado! Redirigiendo a inicio...')
    
    // Navegar programáticamente
    navigate('/')  // 👈 Redirige a Home
  }
  
  return (
    <div className="page contact-page">
      <h1>📬 Contáctanos</h1>
      
      <form className="contact-form" onSubmit={manejarEnvio}>
        <div className="form-group">
          <label>Nombre:</label>
          <input
            type="text"
            name="nombre"
            value={formData.nombre}
            onChange={manejarCambio}
            required
          />
        </div>
        
        <div className="form-group">
          <label>Email:</label>
          <input
            type="email"
            name="email"
            value={formData.email}
            onChange={manejarCambio}
            required
          />
        </div>
        
        <div className="form-group">
          <label>Mensaje:</label>
          <textarea
            name="mensaje"
            value={formData.mensaje}
            onChange={manejarCambio}
            rows="5"
            required
          />
        </div>
        
        <button type="submit">Enviar Mensaje</button>
      </form>
    </div>
  )
}

export default Contact
```

**Hook `useNavigate`:**
- `navigate('/')`: ir a una ruta
- `navigate(-1)`: ir atrás
- `navigate(1)`: ir adelante

---

## RESUMEN Y CIERRE (5 min)

### 3 en línea para praticar con los chicos: https://github.com/JacoboGarcesO/3-inline

---

**¡Excelente trabajo! 🎉**
