# fullstackopenPart0

#0.4: Nuevo diagrama de nota

sequenceDiagram
    participant browser
    participant server
    
    Note right of browser: Usuario escribe en el campo de texto y hace clic en "Save"
    
    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
    activate server
    Note right of browser: El navegador envía los datos del formulario como el cuerpo de la solicitud POST
    server-->>browser: HTTP 302 (redirección a /exampleapp/notes)
    deactivate server
    
    Note right of browser: El servidor guarda la nueva nota y responde con una redirección
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the css file
    deactivate server
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server
    
    Note right of browser: El navegador comienza a ejecutar el código JavaScript que obtiene el JSON del servidor
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server
    
    Note right of browser: El navegador ejecuta la función callback que renderiza las notas (incluyendo la nueva)


#0.5: Diagrama de aplicación de una sola página

sequenceDiagram
    participant browser
    participant server
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate server
    server-->>browser: HTML document
    deactivate server
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the css file
    deactivate server
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
    activate server
    server-->>browser: the SPA JavaScript file
    deactivate server
    
    Note right of browser: El navegador comienza a ejecutar el código JavaScript
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server
    
    Note right of browser: El navegador ejecuta la función callback que renderiza las notas usando DOM-API

#0.6: Nueva nota en diagrama de aplicación de una sola pagina

sequenceDiagram
    participant browser
    participant server
    
    Note right of browser: Usuario escribe en el campo de texto y hace clic en "Save"
    
    Note right of browser: El código JavaScript del SPA maneja el evento del formulario
    Note right of browser: Agrega la nueva nota a la lista de notas
    Note right of browser: Vuelve a renderizar la lista de notas en la página
    
    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
    activate server
    Note right of browser: POST contiene la nueva nota como JSON: {"content": "nueva nota", "date": "2023-1-1"}
    server-->>browser: HTTP 201 Created {"message":"note created"}
    deactivate server
    
    Note right of browser: El navegador permanece en la misma página y no se realizan solicitudes adicionales