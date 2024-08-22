# SOLID & Clean Code

> Documentación creada por Alex Dorado durante la realización del curso *‘Principios SOLID y Clean Code’* de Fernando Herrera *-* [https://cursos.devtalles.com/](https://cursos.devtalles.com/)
> 

# La deuda técnica y el Clean Code

## ¿Que es la deuda técnica?

 Falta de calidad en el código que genera costos económicos:

- Tiempo en realizar mantenimiento.
- Tiempo en refactorizar.
- Tiempo en comprender código.
- Tiempo adicional en la transferencia de código.

## Tipos de deuda técnica

- **Imprudente**: No hay tiempo, sólo copia y pega eso de nuevo.
- **Inadvertido**: ¿Qué son patrones de diseño?
- **Prudente**: Tenemos que entregar rápido, ya refactorizaremos.

## ¿Qué es el Clean Code?

Código limpio es aquel escrito con la intención que otra persona (o tu mismo en un futuro) lo entienda.

- Nombres pronunciables y expresivos
- Ausencia de información técnica en nombres
- Ej. 2 - Renombrar clases
    
    ```jsx
    // Ej. 01 - Renombrar clases
    (() => {
    
        // Ejemplo
        // Archivos a evaluar - files to evaluate
        const filesToEvaluate = [
            { id: 1, flagged: false },
            { id: 2, flagged: false },
            { id: 3, flagged: true },
            { id: 4, flagged: false },
            { id: 5, flagged: false },
            { id: 7, flagged: true },
        ]; 
        
        // Archivos marcados para borrar - files to delete
        const filesToDelete = filesToEvaluate.map( file => file.flagged );
    
        // Malos
        class User { };
        class UserMixin { };
        class UserImplementation { };
        interface IUser { };
    
        // Mejor
        class User { };
        interface User { };
    
        // Tarea
            
        // día de hoy - today
        const today = new Date();
        
        // días transcurridos - elapsed time in days
        const elapsedTimeInDays: number = 23;
        
        // número de archivos en un directorio - number of files in directory
        const numberOfFilesInDirectory = 33;
        
        // primer nombre - first name
        const firstName = 'Fernando';
        
        // primer apellido - last name
        const lastName = 'Herrera';
    
        // días desde la última modificación - days since modification
        const daysSinceLastModification = 12;
        
        // cantidad máxima de clases por estudiante - max classes per student
        const maxClassesPerStudent = 6;
    
    })();
    
     
    ```
    

## Nombre según el tipo de dato

- Arrays:

```jsx
// Bueno
const fruits = ['manzana', 'platano', 'fresa'];

// Mejor (Ya que no es ambiguo y defines que son nombres de frutas)
const fruitNames = ['manzana', 'platano', 'fresa'];
```

- Booleanos

```jsx
// Mal (No definen correctamente el contenido de la variable o no son nombres logicos)
const open = true;
const write = true;
const fruit = false;
const notEmpty = true;

// Mejor
const isOpen = true;
const canWrite = true;
const hasFruit = true;
const isEmpty = false;
```

- Numeros

```jsx
// Mal (No se sabe a que se refieren)
const fruits = 3;
const cars = 10;

// Mejor
const maxFruits = 5;
const minFruits = 1;
const totalOfCars = 5;
```

- Funciones
    - Los nombres de las funciones deben representar acciones. Debe expresar lo que hace específicamente pero abstenerse de todo lo que implementa la función.
    - Es recomendable limitar a 3 el numero de parámetros que se envía en la función.
    
    ```jsx
    // Mal
    createUserIfNotExist();
    updateUserIfNotEmpty();
    sendEmailIfFieldsValid();
    
    // Mejor
    createUser();
    updateUser();
    sendEmail();
    ```
    

- Ej. 2 - Name Types
    
    ```jsx
    (() => {
    
        // arreglo de temperaturas celsius
        const temperaturesCelius = [33.6, 12.34];
    
        // Dirección ip del servidor
        const serverIp = '123.123.123.123';
    
        // Listado de usuarios
        const users = [{id: 1, email: 'fernando@google.com'},{ id: 2, email: 'juan@google.com' }, { id: 3, email: 'melissa@google.com' }];
    
        // Listado de emails de los usuarios
        const usersEmails = people.map( user => user.email );
    
        // Variables booleanas de un video juego
        const canJump = false;
        const canRun = true;
        const hasItems = false;
        const isLoading = false;
    
        // Otros ejercicios
        // tiempo inicial
        const startTime = new Date().getTime();
        //....
        // 3 doritos después
        //...
        // Tiempo al final
        const endTime = new Date().getTime() - startTime;
    
        // Funciones
        // Obtiene los libros
        function getBooks() {
            throw new Error('Function not implemented.');
        }
    
        // obtiene libros desde un URL
        function getBooksByUrl( url: string) {
            throw new Error('Function not implemented.');
        }
        
        // obtiene el área de un cuadrado basado en sus lados
        function getSquareArea( lado: number ) {
            throw new Error('Function not implemented.');
        }
    
        // imprime el trabajo
        function printJob() {
            throw new Error('Function not implemented.');
        }
    
    })();
    ```
    

## Consideraciones para las clases

Las clases deben tener nombres formados por un sustantivo o frases de sustantivo. Intentar evitar nombres genéricos.

- ¿Qué hace exactamente la clase?
- ¿Cómo realiza la tarea exactamente la clase?
- ¿Hay algo específico sobre su ubicación?

```jsx
// Malos
class Manager {};
class Data {};
class Info {};
class SpecialMonsterView {};
```

## Detalles adicionales sobre funciones

- Simplicidad es fundamental.
- Funciones de tamaño reducido.
- Funciones de una sola línea sin causar complejidad.
- Menos de 20 líneas de código (recomendación).
- Evitar el uso del “else”.
- Priorizar el uso de la condicional ternaria.
- Ej. 3 - función a mejorar
    
    ```jsx
    // Incorrecta
      const getPayAmount = ({ isDead = false, isSeparated = true, isRetired = false }) => {
            let result;
            if ( isDead ) {
                result = 1500;
            } else {
                if ( isSeparated ) {
                    result = 2500;
                } else {
                    if ( isRetired ) {
                        result = 3000;
                    } else {
                        result = 4000; 
                    }
                }
            }
            
            return result;
        }
    
    // Correcta
      const getPayAmount = ({ isDead = false, isSeparated = true, isRetired = false }) => {
            if ( isDead ) return 1500;       
            if ( isSeparated ) return 2500;	      
    	      return isRetired ? 3000 : 4000;        
      }
    ```
    

## Principio DRY

> DRY: Don’t Repeat Yourself
> 
- Simplemente es evitar tener duplicidad de código.
- Simplifica las pruebas.
- Ayuda a centralizar los procesos.

# Clases y comentarios

## Herencia - Problemática

- 1). Ejemplo **no** aplicando el principio de responsabilidad única
    
    ```jsx
    (()=> {
    	
    	// No aplicando el principio de responsabilidad única
    	
    	type Gender = 'M'|'F';
    	
    	class Person {
    		constructor(
    			public name: string,
    			public gender: Gender,
    			public birthdate: Date
    		){}
    	}
    	
    	class User extends Person {
    	
    		public lastAccess: Date;
    	
    		constructor(
    			public email: string,
    			public role: string,
    			private lastAccess: Date,
    			name: string,
    			gender: Gender,
    			birthdate: Date
    		) {
    			super( name, gender, birthdate );
    			this.lastAccess = newDate();
    		}
    		
    		checkCredentials(){
    			return true;
    		}
    		
    	}
    	
    	class UserSettings extends User {
    		constructor(
    			public workingDirectory: string,
    			public lastOpenFolder: string,
    			email: string,
    			name: string,
    			gender: Gender,
    			birthdate: Date
    		) {
    			super(email, role, name, gender, birthdate);
    		}
    	}
    	
    	const userSettings = new UserSettings(
    		'/usr/home',
    		'/home',
    		'alex@google.com',
    		'Admin',
    		'Alex',
    		'M',
    		new Date('1994-11-07');
    	);
    	
    	console.log({ userSettings });
    })();
    ```
    
- 2). Ejemplo refactorización de código anterior
    
    ```jsx
    (()=> {
    	
    	// 2). Ejemplo refactorización de código anterior
    	
    	type Gender = 'M'|'F';
    	
    	interface PersonProps {
    		name: string;
    		gender: Gender;
    		birthdate: Date;
    	}
    	
    	class Person {
    		public name: string;
    		public gender: Gender;
    		public birthdate: date;
    	
    		constructor({name, gender, birthdate}: PersonProps){
    			this.name = name;
    			this.gender = gender;
    			this.birthdate = birthdate;
    		}
    	}
    	
    	interface UserProps {
    		email: string;
    		role: string;
    		name: string;
    		gender: Gender;
    		
    	}
    	
    	class User extends Person {
    	
    		public lastAccess: Date;
    		public email: string;
    		public role: string;
    			
    		constructor({
    			email,
    			role,
    			lastAccess,
    			name,
    			gender,
    			birthdate
    		}: UserProps) {
    			super( {name, gender, birthdate} );
    			this.lastAccess = newDate();
    			this.email = email;
    			this.role = role;
    		}
    		
    		checkCredentials(){
    			return true;
    		}
    		
    	}
    	
    	interface UserSettingsProps{
    		workingDirectory: string;
    		lastOpenFolder: string;
    		email: string;
    		name: string;
    		gender: Gender;
    		birthdate: Date;
    	}
    	
    	class UserSettings extends User {
    		public wokringDirectory: string;
    		public lastOpenFoder: string;
    	
    		constructor({
    			workingDirectory,
    			lastOpenFolder,
    			email,
    			name,
    			gender,
    			birthdate 
    		}: UserSettingsProps) {
    			super(email, role, name, gender, birthdate);
    			this.workingDirectory = workingDirectory;
    			this.lastOpenFolder = lastOpenFolder;
    		}
    	}
    	
    	const userSettings = new UserSettings(
    		workingDirectory: '/usr/home',
    		lastOpenFolder: '/home',
    		email: 'alex@google.com',
    		role: 'Admin',
    		name: 'Alex',
    		gender: 'M',
    		birthdate: new Date('1994-11-07');
    	);
    	
    	console.log({ userSettings });
    })();
    ```
    
- 3). Ejemplo aplicando principio de responsabilidad única aplicado
    
    ```jsx
    (() => {
    
        // Aplicando el principio de responsabilidad única
    		// Priorizar la composición frente a la herencia
    
        type Gender = 'M'|'F';
    
        interface PersonProps {
            birthdate : Date;
            gender    : Gender;
            name      : string;
        }
    
        class Person {
            public birthdate: Date;
            public gender   : Gender;
            public name     : string;
    
            constructor({ name, gender, birthdate }: PersonProps ){
                this.name      = name;
                this.gender    = gender;
                this.birthdate = birthdate;
            }
        }
    
        interface UserProps {
            email     : string;
            role      : string;
        }
    
        class User {
            
            public email: string;
            public role : string;
            public lastAccess: Date;
    
            constructor({
                email,
                role,
            }: UserProps ) {            
                this.lastAccess = new Date();
                this.email = email;
                this.role  = role;
            }
    
            checkCredentials() {
                return true;
            }
        }
    
        interface SettingsProps {
            lastOpenFolder   : string;
            workingDirectory : string;
        }
    
        class Settings {
    
            public workingDirectory: string;
            public lastOpenFolder  : string;
    
            constructor({
                workingDirectory,
                lastOpenFolder,
            }: SettingsProps ) {
                this.workingDirectory = workingDirectory;
                this.lastOpenFolder   = lastOpenFolder;
            }
        }
        
    		interface UserSettingsProps{
    			workingDirectory: string;
    			lastOpenFolder: string;
    			email: string;
    			name: string;
    			gender: Gender;
    			birthdate: Date;
    		}    
    
    		class UserSettings {
    			public person: Person;
    			public user: User;
    			public settings: Settings
    			
    			constructor({
    				name, gender, birthdate,
    				email, role,
    				lastOpenFolder, workingDirectory
    			}: UserSettingsProps){
    				this.person = new Person({ name, gender, birthdate });
    				this.user = new User({ email, role });
    				this.settings = new Settings({ lastOpenFolder, workingDirectory  })
    			}
    		}
    
        const userSettings = new UserSettings({
            birthdate: new Date('1985-10-21'),
            email: 'fernando@google.com',
            gender: 'M',
            lastOpenFolder: '/home',
            name: 'Fernando',
            role: 'Admin',
            workingDirectory: '/usr/home',
        });
    
        console.log({ userSettings });
    
    })();
    ```
    

## Estructura recomendada para una clase

1. Propiedades estáticas.
2. Propiedades públicas.
3. Métodos
    1. Empezando por los constructores estáticos.
    2. Luego el constructor.
    3. Seguidamente métodos estáticos.
    4. Métodos privados después.
    5. Resto de métodos de instancia ordenados de mayor a menor importancia.
    6. Getters y Setters al final.

## Comentarios en el código

Cuando usamos librerías de terceros, APIS, frameworks, etc. nos encontraremos ante situaciones en las que escribir un comentario será mejor que dejar una solución compleja o un hack sin explicación.

Los comentarios deberían de ser la excepción, no la regla.

El código debe ser suficientemente auto explicativo. Buscar el ¿por qué? en lugar de ¿qué? o ¿cómo?

# Acrónimo STUPID & CodeSmells

> Todo lo que **no se debería hacer**. Anti-patrones. Code smells (Huele mal, se ve raro).
> 

6 Code Smells que debemos evitar.

- **S**ingleton: Patrón singleton.
- **T**ight Coupling: Alto acoplamiento.
- **U**ntestability: Código no probable (Unit test).
- **P**remature optimization: Optimizaciones prematuras.
- **I**ndescriptive Naming: Nombres poco descriptivos.
- **D**uplication: Duplicidad de código, no aplicar el principio DRY.

## Patrón Singleton

Pros:

- Garantiza una única instancia de la clase a lo largo de toda la aplicación

Const:

- Vive en el contexto global.
- Puede ser modificado por cualquiera.
- No es rastreable.
- Difícil de testear debido a su ubicación.
- Ejemplo:
    
    ```jsx
    const Singleton = (function () {
        
        let instance;
    
        function createInstance() {
            return new Object('I am the instance');
        }
    
        return {
            getInstance() {
                if (!instance) {
                    instance = createInstance();
                }
                return instance;
            }
        };
    })();
    
    function main() {
    
        const instance1 = Singleton.getInstance();
        const instance2 = Singleton.getInstance();
    
        console.log('Misma instancia? ', (instance1 === instance2));
    }
    
    main();
    ```
    

## Acoplamiento y cohesión

Lo ideal es tener bajo acoplamiento y buena cohesión.

Acoplamiento se refiere a cuán relacionadas o dependientes son dos clases o módulos entre sí

- **En bajo acoplamiento** cambiar algo importante en una clase no debería afectar a la otra.
- **En alto acoplamiento** dificultaría el cambio y el mantenimiento de su código, dado que las clases están muy unidas, hacer un cambio podría requerir una renovación completa del sistema.

### Alto Acoplamiento

- Desventajas
    - Un cambio en un módulo por lo general provoca un efecto dominó de los cambios en otros módulos.
    - El ensamblaje de módulos puede requerir más esfuerzo y/o tiempo debido a la mayor dependencia entre módulos.
    - Un módulo en particular puede ser más difícil de reutilizar y/o probar porque deben incluir módulos dependientes.
- Posibles soluciones
    - “A” tiene un atributo que se refiere a “B”.
    - “A” llama a los servicios de un objeto “B”.
    - “A” tiene un método que hace referencia a “B” (a través del tipo de retorno o parámetro).
    - “A” es una subclase de la clase “B”.

### Cohesión

- La cohesión se refiere a lo que la clase o módulo puede hacer.
- La baja cohesión significaría que la clase realiza una gran variedad de acciones: es amplia, no se enfoca en lo que debe hacer.
- Alta cohesión significa que la clase se enfoca en lo que debería estar haciendo, es decir, solo métodos relacionados con la intención de la clase.

### Ejemplo de alto acoplamiento y bajo acoplamiento

- Alto acoplamiento
    
    ```jsx
    (()=>{
        // No aplicando el principio de responsabilidad única
        type Gender = 'M'|'F';
    
        // Alto Acoplamiento
    
        class Person {
            constructor(
                public firstName: string,
                public lastName: string,
                public gender: Gender,
                public birthdate: Date,
            ){}
        }
    
        class User extends Person {
            constructor(
                public email: string,
                public role: string,
                private lastAccess: Date,
                firstName: string,
                lastName: string,
                gender: Gender,
                birthdate: Date,
            ){
                super(firstName, lastName, gender, birthdate);
                this.lastAccess = new Date();
            }
    
            checkCredentials() {
                return true;
            }
        }
    
    class UserSettings extends User {
        constructor(
            public workingDirectory: string,
            public lastFolderOpen: string,
            email     : string,
            role      : string,
            firstName      : string,
            lastName: string,
            gender    : Gender,
            birthdate : Date,
        ){
            super(
                email,
                role,
                new Date(),
                firstName,
                lastName,
                gender,
                birthdate
            )
        }
    }
        
        const userSettings = new UserSettings(
            '/urs/home',
            '/development',
            'fernando@google.com',
            'F',
            'Fernando',
            'Dorado',
            'M',
            new Date('1985-10-21')
        );
    
        console.log({ userSettings, credentials: userSettings.checkCredentials() });
        
    })()
    ```
    
- Bajo acoplamiento
    
    ```jsx
    (()=>{
        // Aplicando el principio de responsabilidad única
        // Prioriza la composición frente a la herencia
    
        type Gender = 'M'|'F';
    
        interface PersonProps {
            firstName     : string;
            lastName: string;
            gender   : Gender;
            birthdate: Date;
        }
    
        class Person {
            public firstName     : string;
            public lastName: string;
            public gender   : Gender;
            public birthdate: Date;
    
            constructor({ firstName, lastName, gender, birthdate }: PersonProps ){
                this.firstName = firstName;
                this.lastName = lastName;
                this.gender = gender;
                this.birthdate = birthdate;
            }
        }
    
        interface UserProps {
            email     : string;
            role      : string;
        }
        class User {
    
            public email       : string;
            public role        : string;
            private lastAccess : Date;
    
            constructor({ email, role }: UserProps ){
                this.lastAccess = new Date();
                this.email = email;
                this.role = role;
            }
    
            checkCredentials() {
                return true;
            }
        }
    
        interface SettingsProps {
            lastFolderOpen  : string;
            workingDirectory: string;
        }
    
        class Settings {
            public workingDirectory: string; 
            public lastFolderOpen  : string; 
    
            constructor({ workingDirectory, lastFolderOpen }: SettingsProps ){
                this.workingDirectory = workingDirectory;
                this.lastFolderOpen = lastFolderOpen;
            }
        }
        
        
        // Nuevo User Settings
        interface UserSettingsProps {
            birthdate       : Date;
            email           : string;
            gender          : Gender;
            lastFolderOpen  : string;
            firstName            : string;
            lastName: string;
            role            : string;
            workingDirectory: string;
        }
    
        class UserSettings {
            // constructor(
            //     public person: Person,
            //     public user  : User,
            //     public settings: Settings,
            // ){}
            public person  : Person;
            public user    : User; 
            public settings: Settings;
    
            constructor({ 
                firstName, lastName, gender, birthdate,
                email, role,
                workingDirectory, lastFolderOpen,
            }: UserSettingsProps) {
                this.person = new Person({ firstName, lastName, gender, birthdate });
                this.user = new User({ email, role });
                this.settings = new Settings({ workingDirectory, lastFolderOpen })
            }
        }
        
    
        const userSettings = new UserSettings({
            birthdate: new Date('1985-10-21'),
            email: 'fernando@google.com',
            gender: 'M',
            lastFolderOpen: '/home',
            firstName: 'Fernando',
            lastName: 'Dorado',
            role: 'Admin',
            workingDirectory: '/usr/home'
        });
    
        console.log({ userSettings, credentials: userSettings.user.checkCredentials() });
        
    })()
    ```
    

## CodeSmells adicionales

Código dificilmente testeable.

### Código no probable

- Código con alto acoplamiento.
- Código con muchas dependencias no inyectadas.
- Dependencias en el contexto global (Tipo Singleton).

Debemos tener en mente las pruebas desde la creación del código.

### Optimizaciones prematuras

- Mantener abiertas las opciones retrasando la toma de decisiones permite darle darle mayor relevancia a lo que es más importante en una aplicación
- No debemos anticiparnos a los requisitos y desarrollar abstracciones innecesarias que puedan añadir complejidad accidental.
    - Complejidad accidental: Cuando implementamos una solución compleja a la mínima indispensable.
    - Complejidad esencial: Es inherente al problema. Necesaria.

### Nombres poco descriptivos

- Nombres de variables mal nombradas.
- Nombres de clases genéricas.
- Nombres de funciones mal nombradas.
- Ser muy especifico o demasiado genérico.

### Duplicidad de código

No aplicar el principio DRY

## Principios SOLID
