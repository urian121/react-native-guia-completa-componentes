# 📖 Guía Completa de Componentes en React Native

Guía completa de componentes en React Native 📱. Aprende a usar y personalizar los principales componentes con ejemplos prácticos y buenas prácticas. 🚀

## 1️⃣ Instalación y Configuración

Si aún no tienes un entorno de desarrollo configurado, puedes instalar **React Native CLI** o usar **Expo** (***recomendado por React***):

### Instalación con Expo

```bash
npx create-expo-app MiApp
cd MiApp
npx expo start
```

### Instalación con React Native CLI

```bash
npx react-native init MiApp
cd MiApp
npx react-native start
```

## 2️⃣ Primer Componente

Un componente funcional básico en **React Native** se define así:

```jsx
import React from 'react';
import { Text, View } from 'react-native';

const MiComponente = () => {
  return (
    <View>
      <Text>¡Hola, React Native!</Text>
    </View>
  );
};

export default MiComponente;
```

📌 **Explicación:**
- `<View>`: Similar a un `<div>` en HTML.
- `<Text>`: Se usa para mostrar texto.

## 3️⃣ Componentes Básicos

### 🟢 View (Contenedor)
**`View`**: Es el componente más básico sobre el que heredan la mayoría de los demás componentes. Lo podríamos comparar como un `<div>` de HTML.

```jsx
<View style={{ backgroundColor: 'lightgray', padding: 20, borderRadius: 5 }}>
  <Text>Este es un contenedor</Text>
</View>
```

### 📌 Importante  
> [!IMPORTANT]  
> En **React** y **React Native**, las dobles llaves (`{{ }}`) indican que estás pasando un **objeto** en **JSX**.  
> - La primera `{ }` permite escribir una expresión de **JavaScript** dentro de **JSX**.  
> - La segunda `{ }` contiene el objeto con los estilos en formato **clave-valor**.  
>
> 📌 Esto es necesario porque los estilos en React se definen como objetos de JavaScript en lugar de cadenas CSS.  


#### Crear un contenedor fácilmente usando `View`
Este código define un componente `Container` que usa `View` para envolver y aplicar estilos a sus hijos.
En `App`, el `Container` se reutiliza para mostrar un `Text` dentro de un fondo estilizado.

```jsx
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

const Container = ({ children }) => {
  return <View style={styles.container}>{children}</View>;
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: '#f5f5f5',
  },
});

export default function App() {
  return (
    <Container>
      <Text>Hola, esto está dentro del contenedor</Text>
    </Container>
  );
}
```

### 🔤 Text (Texto)
**`Text`**: Componente para mostrar textos.

```jsx
<Text style={{ fontSize: 20, fontWeight: 'bold', color: '#333' }}>
  Texto en React Native
</Text>
```

### 🔘 Button (Botón)
**`Button`**: Sirve para crear botones interactivos básicos con una apariencia estándar según la plataforma (iOS o Android).

```jsx
import { Button } from 'react-native';

<Button 
  title="Presionar" 
  onPress={() => alert('¡Clic!')} 
  color="#841584" 
/>
```

### 🎛️ TextInput (Caja de Texto)
**`TextInput`**: Componente que proporciona un espacio al usuario para que pueda ingresar texto por medio del teclado de su dispositivo.

```jsx
import React, { useState } from 'react';
import { TextInput } from 'react-native';

const InputExample = () => {
  const [texto, setTexto] = useState('');
  
  return (
    <TextInput
      placeholder="Escribe aquí"
      value={texto}
      onChangeText={setTexto}
      style={{ 
        borderWidth: 1, 
        borderColor: '#ccc', 
        borderRadius: 5,
        padding: 10 
      }}
    />
  );
};
```

### 📸 Image (Imagen)
**`Image`**: Componente que sirve para mostrar imágenes

```jsx
import React, { useState } from 'react';
import { Image } from 'react-native';

// Imagen desde URL
<Image 
  source={{ uri: 'https://reactnative.dev/img/tiny_logo.png' }} 
  style={{ width: 100, height: 100 }} 
/>

// Imagen local
<Image 
  source={require('./assets/logo.png')} 
  style={{ width: 100, height: 100 }} 
/>
```
### 📱 Componente SafeAreaView
Se usa para asegurarse de que el contenido de la pantalla no se superponga con áreas seguras del dispositivo, como el **`notch`** en iPhones o la barra de navegación en **`Android**`.

#### Cómo funciona

- `SafeAreaView` ajusta automáticamente su padding para evitar que el contenido quede oculto detrás de áreas no seguras.
Funciona mejor en **iOS**, pero en **Android** no tiene efecto a menos que uses SafeAreaProvider de la librería `react-native-safe-area-context`.

```jsx
import React from 'react';
import { SafeAreaView, Text, StyleSheet } from 'react-native';

export default function App() {
  return (
    <SafeAreaView style={styles.container}>
      <Text>Hola, esto está dentro de SafeAreaView</Text>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f5f5f5',
  },
});
```

#### Mejor soporte en Android
En **Android**, para un mejor comportamiento, usa `SafeAreaProvider` de `react-native-safe-area-context`:

1. Instala la librería
`npm install react-native-safe-area-context`

2. Implementación con SafeAreaProvider

```jsx
import React from 'react';
import { SafeAreaView, Text, StyleSheet } from 'react-native';
import { SafeAreaProvider } from 'react-native-safe-area-context';

export default function App() {
  return (
    <SafeAreaProvider>
      <SafeAreaView style={styles.container}>
        <Text>Contenido seguro en iOS y Android</Text>
      </SafeAreaView>
    </SafeAreaProvider>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f5f5f5',
  },
});
```
✅ Con esta configuración, el `SafeAreaView` funciona bien en **iOS** y **Android**.

### 📜 ScrollView (Vista Desplazable)
**`ScrollView`**: Componente permite establecer un contenedor en el que se podrán almacenar varios componentes que se pueden ir desplazando en la pantalla.

```jsx
import React, { useState } from 'react';
import { ScrollView, View, Text, StyleSheet } from 'react-native';

const ScrollViewExample = () => {
  return (
    <ScrollView style={{ flex: 1 }}>
      {/* Contenido que puede desplazarse verticalmente */}
      <View style={{ height: 200, backgroundColor: 'pink', margin: 10 }}>
        <Text>Sección 1</Text>
      </View>
      <View style={{ height: 200, backgroundColor: 'skyblue', margin: 10 }}>
        <Text>Sección 2</Text>
      </View>
      <View style={{ height: 200, backgroundColor: 'lightgreen', margin: 10 }}>
        <Text>Sección 3</Text>
      </View>
    </ScrollView>
  );
};

// ScrollView horizontal
const HorizontalScrollExample = () => {
  return (
    <ScrollView 
      horizontal={true} 
      showsHorizontalScrollIndicator={false}
      style={{ height: 200 }}
    >
      <View style={{ width: 150, height: 150, backgroundColor: 'red', margin: 10 }} />
      <View style={{ width: 150, height: 150, backgroundColor: 'blue', margin: 10 }} />
      <View style={{ width: 150, height: 150, backgroundColor: 'green', margin: 10 }} />
    </ScrollView>
  );
};
```

### 🔄 ActivityIndicator (Indicador de Carga)
**`ActivityIndicator`**: Muestra un indicador de carga circular animado.
Se utiliza para indicar a los usuarios que una operación está en proceso, como cuando se están cargando datos de una `API`, procesando información o realizando cualquier tarea que requiera tiempo.

```jsx
import React, { useState } from 'react';
import { ActivityIndicator, View } from 'react-native';

const LoadingIndicator = () => {
  return (
    <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
      <ActivityIndicator size="large" color="#0000ff" />
    </View>
  );
};
```

### 📱 TouchableOpacity (Área Táctil)
**`TouchableOpacity`**: Crea áreas táctiles que responden al toque del usuario con un efecto de opacidad. 
Cuando el usuario presiona el elemento, este se vuelve ligeramente transparente (reduce su opacidad) para proporcionar retroalimentación visual.

```jsx
import React, { useState } from 'react';
import { TouchableOpacity, Text } from 'react-native';

const TouchableExample = () => {
  return (
    <TouchableOpacity 
      style={{ 
        backgroundColor: '#2196F3', 
        padding: 10, 
        borderRadius: 5,
        alignItems: 'center' 
      }}
      onPress={() => alert('Tocado!')}
    >
      <Text style={{ color: 'white' }}>Botón Personalizado</Text>
    </TouchableOpacity>
  );
};
```

## 4️⃣ Componentes con Estado (`useState`)
Para manejar datos dentro de un componente usamos `useState`:

```jsx
import React, { useState } from 'react';
import { View, Text, Button, StyleSheet } from 'react-native';

const Contador = () => {
  const [contador, setContador] = useState(0);
  
  return (
    <View style={styles.container}>
      <Text style={styles.contador}>Contador: {contador}</Text>
      <View style={styles.buttonRow}>
        <Button title="Incrementar" onPress={() => setContador(contador + 1)} />
        <Button title="Decrementar" onPress={() => setContador(contador - 1)} />
      </View>
      <Button title="Reiniciar" onPress={() => setContador(0)} />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    padding: 20,
    alignItems: 'center',
  },
  contador: {
    fontSize: 24,
    marginBottom: 20,
  },
  buttonRow: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    width: '100%',
    marginBottom: 10,
  },
});

export default Contador;
```

📌 **Explicación:**
- `useState(0)`: Crea una variable de estado (contador) con valor inicial `0`.
- `setContador(contador + 1)`: Actualiza el estado al hacer clic.

## 5️⃣ Estilos en React Native
Se pueden definir estilos de dos maneras:

### 1️⃣ Estilos en línea

```jsx
<Text style={{ color: 'blue', fontSize: 20, fontWeight: 'bold' }}>
  Texto Azul
</Text>
```

### 2️⃣ Estilos con StyleSheet (Recomendado)
**`StyleSheet`**: Componente en el que añadiremos los estilos del componente.

```jsx
import React, { useState } from 'react';
import { StyleSheet, View, Text } from 'react-native';

const MiComponente = () => {
  return (
    <View style={styles.container}>
      <Text style={styles.titulo}>Título Principal</Text>
      <Text style={styles.subtitulo}>Subtítulo</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: '#f5f5f5',
  },
  titulo: { 
    color: 'red', 
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 10,
  },
  subtitulo: {
    color: '#333',
    fontSize: 18,
  }
});

export default MiComponente;
```

### 3️⃣ Combinando estilos

```jsx
<Text style={[styles.texto, { color: 'green' }]}>
  Este texto combina estilos
</Text>
```

## 6️⃣ Diseño con Flexbox
**React Native** utiliza Flexbox para el diseño:

```jsx
import React, { useState } from 'react';
import { View, StyleSheet } from 'react-native';

const FlexboxExample = () => {
  return (
    <View style={styles.container}>
      <View style={styles.box1} />
      <View style={styles.box2} />
      <View style={styles.box3} />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: 'row', // 'column', 'row', 'column-reverse', 'row-reverse'
    justifyContent: 'space-between', // 'flex-start', 'flex-end', 'center', 'space-around'
    alignItems: 'center', // 'flex-start', 'flex-end', 'stretch'
    padding: 20,
  },
  box1: { width: 50, height: 50, backgroundColor: 'red' },
  box2: { width: 50, height: 50, backgroundColor: 'green' },
  box3: { width: 50, height: 50, backgroundColor: 'blue' },
});
```

## 7️⃣ Listas y Scroll

### FlatList (Para listas largas)
Renderiza listas de datos extensas de forma eficiente, cargando solo los elementos visibles en pantalla. Es ideal para mostrar grandes colecciones de datos con buen rendimiento.

```jsx
import React, { useState } from 'react';
import { FlatList, Text, View, StyleSheet } from 'react-native';

const datos = [
  { id: '1', nombre: 'Juan' },
  { id: '2', nombre: 'Ana' },
  { id: '3', nombre: 'Carlos' },
  { id: '4', nombre: 'María' },
  // ... más datos
];

const Lista = () => (
  <FlatList
    data={datos}
    keyExtractor={(item) => item.id}
    renderItem={({ item }) => (
      <View style={styles.item}>
        <Text style={styles.nombre}>{item.nombre}</Text>
      </View>
    )}
    ItemSeparatorComponent={() => <View style={styles.separator} />}
  />
);

const styles = StyleSheet.create({
  item: {
    padding: 15,
    backgroundColor: 'white',
  },
  nombre: {
    fontSize: 16,
  },
  separator: {
    height: 1,
    backgroundColor: '#eeeeee',
  },
});

export default Lista;
```

### SectionList (Para listas con secciones)
Muestra datos organizados en secciones con encabezados. Es similar a FlatList pero permite agrupar elementos relacionados bajo títulos de sección, ideal para datos categorizados como contactos por inicial, productos por categoría o ajustes agrupados por función.

```jsx
import React, { useState } from 'react';
import { SectionList, Text, View, StyleSheet } from 'react-native';

const datos = [
  {
    title: 'Frutas',
    data: ['Manzana', 'Banana', 'Naranja'],
  },
  {
    title: 'Verduras',
    data: ['Zanahoria', 'Brócoli', 'Espinaca'],
  },
];

const SectionListExample = () => (
  <SectionList
    sections={datos}
    keyExtractor={(item, index) => item + index}
    renderItem={({ item }) => (
      <View style={styles.item}>
        <Text style={styles.itemText}>{item}</Text>
      </View>
    )}
    renderSectionHeader={({ section: { title } }) => (
      <View style={styles.sectionHeader}>
        <Text style={styles.sectionTitle}>{title}</Text>
      </View>
    )}
  />
);

const styles = StyleSheet.create({
  item: {
    padding: 10,
    backgroundColor: 'white',
  },
  itemText: {
    fontSize: 16,
  },
  sectionHeader: {
    padding: 10,
    backgroundColor: '#f0f0f0',
  },
  sectionTitle: {
    fontSize: 18,
    fontWeight: 'bold',
  },
});
```

## 8️⃣ Uso de API con `fetch`
Para obtener datos de una API usamos `fetch`:

```jsx
import React, { useEffect, useState } from 'react';
import { View, Text, FlatList, StyleSheet, ActivityIndicator } from 'react-native';

const ApiExample = () => {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/users');
        if (!response.ok) {
          throw new Error('La respuesta de la red no fue satisfactoria');
        }
        const json = await response.json();
        setData(json);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, []);

  if (loading) {
    return (
      <View style={styles.centered}>
        <ActivityIndicator size="large" color="#0000ff" />
      </View>
    );
  }

  if (error) {
    return (
      <View style={styles.centered}>
        <Text style={styles.error}>Error: {error}</Text>
      </View>
    );
  }

  return (
    <FlatList
      data={data}
      keyExtractor={(item) => item.id.toString()}
      renderItem={({ item }) => (
        <View style={styles.userItem}>
          <Text style={styles.userName}>{item.name}</Text>
          <Text style={styles.userEmail}>{item.email}</Text>
        </View>
      )}
    />
  );
};

const styles = StyleSheet.create({
  centered: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  error: {
    color: 'red',
    fontSize: 18,
  },
  userItem: {
    padding: 15,
    borderBottomWidth: 1,
    borderBottomColor: '#eee',
  },
  userName: {
    fontSize: 18,
    fontWeight: 'bold',
  },
  userEmail: {
    fontSize: 14,
    color: '#666',
  },
});

export default ApiExample;
```

## 9️⃣ Navegación entre Pantallas
Para la navegación, instala `React Navigation`:

```bash
npm install @react-navigation/native
npx expo install react-native-screens react-native-safe-area-context
npm install @react-navigation/native-stack
```

### Ejemplo de Navegación Básica

```jsx
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
import { Button, Text, View } from 'react-native';

// Pantalla de Inicio
const HomeScreen = ({ navigation }) => {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text style={{ fontSize: 24, marginBottom: 20 }}>Pantalla de Inicio</Text>
      <Button
        title="Ir a Detalles"
        onPress={() => navigation.navigate('Details', { itemId: 86, title: 'Mi Título' })}
      />
    </View>
  );
};

// Pantalla de Detalles
const DetailsScreen = ({ route, navigation }) => {
  const { itemId, title } = route.params;
  
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text style={{ fontSize: 24, marginBottom: 10 }}>Pantalla de Detalles</Text>
      <Text>itemId: {itemId}</Text>
      <Text>title: {title}</Text>
      <Button title="Regresar" onPress={() => navigation.goBack()} />
    </View>
  );
};

const Stack = createNativeStackNavigator();

const App = () => {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Home">
        <Stack.Screen 
          name="Home" 
          component={HomeScreen} 
          options={{ title: 'Inicio' }}
        />
        <Stack.Screen 
          name="Details" 
          component={DetailsScreen}
          options={({ route }) => ({ title: route.params.title })}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
};

export default App;
```

## 🔟 Hooks Comunes

### `useEffect` (Efectos Secundarios)
**`useEffect`** es un hook de efectos secundarios que permite ejecutar código en diferentes momentos del ciclo de vida de un componente.
Se usa comúnmente para **cargar datos, suscribirse a eventos, manipular el DOM, o ejecutar lógica después de renderizar**.

```jsx
import React, { useState, useEffect } from 'react';
import { Text, View } from 'react-native';

const Timer = () => {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds(prevSeconds => prevSeconds + 1);
    }, 1000);
    
    // Función de limpieza
    return () => clearInterval(interval);
  }, []); // Array vacío = ejecutar solo al montar

  return (
    <View>
      <Text>Segundos: {seconds}</Text>
    </View>
  );
};
```

### `useContext` (Contexto Global)
**`useContext`**: permite acceder a un contexto global en cualquier parte de la aplicación sin necesidad de pasar props manualmente.
Es útil para manejar estados globales como autenticación, temas, idiomas, etc.

```jsx
import React, { createContext, useContext, useState } from 'react';
import { View, Text, Button } from 'react-native';

// Crear el contexto
const TemaContext = createContext();

// Proveedor de contexto
const TemaProvider = ({ children }) => {
  const [tema, setTema] = useState('claro');
  
  const cambiarTema = () => {
    setTema(temaActual => temaActual === 'claro' ? 'oscuro' : 'claro');
  };
  
  return (
    <TemaContext.Provider value={{ tema, cambiarTema }}>
      {children}
    </TemaContext.Provider>
  );
};

// Componente que consume el contexto
const ComponenteTematizado = () => {
  const { tema, cambiarTema } = useContext(TemaContext);
  
  return (
    <View style={{ 
      backgroundColor: tema === 'claro' ? '#fff' : '#333',
      padding: 20 
    }}>
      <Text style={{ 
        color: tema === 'claro' ? '#000' : '#fff' 
      }}>
        Tema actual: {tema}
      </Text>
      <Button title="Cambiar Tema" onPress={cambiarTema} />
    </View>
  );
};

// Uso en la app
const App = () => {
  return (
    <TemaProvider>
      <ComponenteTematizado />
    </TemaProvider>
  );
};
```

## 1️⃣1️⃣ Manejo de Formularios

```jsx
import React, { useState } from 'react';
import { View, TextInput, Button, Text, StyleSheet, Alert } from 'react-native';

const FormularioExample = () => {
  const [formState, setFormState] = useState({
    nombre: '',
    email: '',
    password: ''
  });
  
  const [errors, setErrors] = useState({});
  
  const handleChange = (field, value) => {
    setFormState({
      ...formState,
      [field]: value
    });
  };
  
  const validarFormulario = () => {
    let tempErrors = {};
    
    if (!formState.nombre) tempErrors.nombre = "El nombre es obligatorio";
    if (!formState.email) tempErrors.email = "El email es obligatorio";
    else if (!/\S+@\S+\.\S+/.test(formState.email)) {
      tempErrors.email = "Email inválido";
    }
    if (!formState.password) tempErrors.password = "La contraseña es obligatoria";
    else if (formState.password.length < 6) {
      tempErrors.password = "La contraseña debe tener al menos 6 caracteres";
    }
    
    setErrors(tempErrors);
    return Object.keys(tempErrors).length === 0;
  };
  
  const handleSubmit = () => {
    if (validarFormulario()) {
      // Aquí enviarías los datos al servidor
      Alert.alert("Éxito", "Formulario enviado correctamente");
      console.log("Datos del formulario:", formState);
    }
  };
  
  return (
    <View style={styles.form}>
      <Text style={styles.label}>Nombre:</Text>
      <TextInput
        style={[styles.input, errors.nombre && styles.errorInput]}
        value={formState.nombre}
        onChangeText={(text) => handleChange('nombre', text)}
        placeholder="Escribe tu nombre"
      />
      {errors.nombre && <Text style={styles.errorText}>{errors.nombre}</Text>}
      
      <Text style={styles.label}>Email:</Text>
      <TextInput
        style={[styles.input, errors.email && styles.errorInput]}
        value={formState.email}
        onChangeText={(text) => handleChange('email', text)}
        placeholder="tu@email.com"
        keyboardType="email-address"
        autoCapitalize="none"
      />
      {errors.email && <Text style={styles.errorText}>{errors.email}</Text>}
      
      <Text style={styles.label}>Contraseña:</Text>
      <TextInput
        style={[styles.input, errors.password && styles.errorInput]}
        value={formState.password}
        onChangeText={(text) => handleChange('password', text)}
        placeholder="********"
        secureTextEntry
      />
      {errors.password && <Text style={styles.errorText}>{errors.password}</Text>}
      
      <Button title="Enviar" onPress={handleSubmit} />
    </View>
  );
};

const styles = StyleSheet.create({
  form: {
    padding: 20,
  },
  label: {
    fontSize: 16,
    marginBottom: 5,
    fontWeight: 'bold',
  },
  input: {
    borderWidth: 1,
    borderColor: '#ddd',
    padding: 10,
    borderRadius: 5,
    marginBottom: 15,
  },
  errorInput: {
    borderColor: 'red',
  },
  errorText: {
    color: 'red',
    fontSize: 12,
    marginTop: -10,
    marginBottom: 10,
  }
});

export default FormularioExample;
```

## 1️⃣2️⃣ Mejores Prácticas

### Separar Lógica y Presentación

```jsx
// Component/UserProfile/index.js (Componente contenedor - lógica)
import React, { useState, useEffect } from 'react';
import UserProfileView from './UserProfileView';

const UserProfile = ({ userId }) => {
  const [userData, setUserData] = useState(null);
  const [loading, setLoading] = useState(true);
  
  useEffect(() => {
    // Obtener datos del usuario
    fetch(`https://api.example.com/users/${userId}`)
      .then(response => response.json())
      .then(data => {
        setUserData(data);
        setLoading(false);
      });
  }, [userId]);
  
  const handleUpdateName = (newName) => {
    // Lógica para actualizar nombre
  };
  
  return (
    <UserProfileView
      userData={userData}
      loading={loading}
      onUpdateName={handleUpdateName}
    />
  );
};

// Component/UserProfile/UserProfileView.js (Componente de presentación)
import React from 'react';
import { View, Text, ActivityIndicator, Button, TextInput } from 'react-native';

const UserProfileView = ({ userData, loading, onUpdateName }) => {
  if (loading) {
    return <ActivityIndicator size="large" />;
  }
  
  return (
    <View>
      <Text>Nombre: {userData.name}</Text>
      <Text>Email: {userData.email}</Text>
      {/* Resto del UI */}
    </View>
  );
};
```

### Personalizar Componentes Reutilizables

```jsx
// Components/CustomButton.js
import React from 'react';
import { TouchableOpacity, Text, StyleSheet } from 'react-native';

const CustomButton = ({ 
  title, 
  onPress, 
  type = 'primary', // 'primary', 'secondary', 'outline'
  size = 'medium', // 'small', 'medium', 'large'
  disabled = false,
  style = {}
}) => {
  return (
    <TouchableOpacity
      onPress={onPress}
      disabled={disabled}
      style={[
        styles.button,
        styles[type],
        styles[size],
        disabled && styles.disabled,
        style
      ]}
    >
      <Text style={[
        styles.text,
        styles[`${type}Text`],
        disabled && styles.disabledText
      ]}>
        {title}
      </Text>
    </TouchableOpacity>
  );
};

const styles = StyleSheet.create({
  button: {
    borderRadius: 8,
    justifyContent: 'center',
    alignItems: 'center',
  },
  primary: {
    backgroundColor: '#2196F3',
  },
  secondary: {
    backgroundColor: '#FF9800',
  },
  outline: {
    backgroundColor: 'transparent',
    borderWidth: 1,
    borderColor: '#2196F3',
  },
  small: {
    paddingVertical: 6,
    paddingHorizontal: 12,
  },
  medium: {
    paddingVertical: 10,
    paddingHorizontal: 16,
  },
  large: {
    paddingVertical: 14,
    paddingHorizontal: 24,
  },
  disabled: {
    backgroundColor: '#CCCCCC',
    borderColor: '#CCCCCC',
  },
  text: {
    fontWeight: 'bold',
  },
  primaryText: {
    color: 'white',
  },
  secondaryText: {
    color: 'white',
  },
  outlineText: {
    color: '#2196F3',
  },
  disabledText: {
    color: '#888888',
  },
});

export default CustomButton;

// Uso del componente personalizado
import CustomButton from './Components/CustomButton';

const Screen = () => {
  return (
    <View>
      <CustomButton 
        title="Botón Primario" 
        onPress={() => alert('Primario!')} 
      />
      <CustomButton 
        title="Botón Secundario" 
        type="secondary" 
        size="large" 
        onPress={() => alert('Secundario!')} 
      />
      <CustomButton 
        title="Botón Outline" 
        type="outline" 
        size="small" 
        onPress={() => alert('Outline!')} 
      />
      <CustomButton 
        title="Botón Deshabilitado" 
        disabled={true} 
        onPress={() => alert('No se ejecutará')} 
      />
    </View>
  );
};
```

## 1️⃣3️⃣ Depuración y Herramientas

### Console.log para debugging:

```jsx
const MiComponente = () => {
  const datos = { nombre: 'Juan', edad: 30 };
  
  console.log('Datos actuales:', datos);
  console.warn('Advertencia importante');
  console.error('Error crítico');
  
  return <View>...</View>;
};
```

### Uso de React DevTools:

1. Instala React DevTools:
```bash
npm install -g react-devtools
```

2. Ejecuta en otra terminal:
```bash
react-devtools
```

3. Conecta tu aplicación (sigue las instrucciones en pantalla)

## 1️⃣4️⃣ Optimizaciones de Rendimiento

### Uso de `React.memo` para componentes puros:

```jsx
import React, { memo } from 'react';
import { Text } from 'react-native';

const MiComponente = memo(({ texto }) => {
  console.log('Renderizando MiComponente');
  return <Text>{texto}</Text>;
});

export default MiComponente;
```

### `useMemo` para cálculos costosos:
**`useMemo`**: memoriza valores computados para evitar cálculos innecesarios en cada render.
Se usa cuando tienes funciones costosas o cálculos que no deberían ejecutarse si sus dependencias no han cambiado.

```jsx
import React, { useMemo } from 'react';
import { View, Text } from 'react-native';

const ListaFiltrada = ({ items, filtro }) => {
  const itemsFiltrados = useMemo(() => {
    console.log('Calculando filtro...');
    return items.filter(item => item.includes(filtro));
  }, [items, filtro]); // Solo recalcula si items o filtro cambian
  
  return (
    <View>
      {itemsFiltrados.map(item => (
        <Text key={item}>{item}</Text>
      ))}
    </View>
  );
};
```

### `useCallback` para funciones:
Sirve para memorizar funciones, evitando que se vuelvan a crear en cada render. Esto mejora el rendimiento al evitar que componentes hijos innecesariamente se vuelvan a renderizar.

```jsx
import React, { useState, useCallback } from 'react';
import { View, Button } from 'react-native';

const Contador = () => {
  const [contador, setContador] = useState(0);
  
  // useCallback evita recrear la función en cada renderizado
  const incrementar = useCallback(() => {
    setContador(c => c + 1);
  }, []); // Array vacío = no depende de ningún valor
  
  return (
    <View>
      <Button title={`Contador: ${contador}`} onPress={incrementar} />
    </View>
  );
};
```
