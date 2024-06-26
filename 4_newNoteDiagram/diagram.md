```mermaid
sequenceDiagram
    participant browser
    participant server

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note with [note: "A NEW NOTE"]
    activate server

    Note right of browser: The browser sends a new note to the server

    Note left of server: The server creates a new note object {content: "A NEW NOTE", date: "2024-4-30"} <br/> and adds it to the notes array

    server-->>browser: HTTP status code: 302
    deactivate server

    Note left of server: The server sends respond with a URL redirect

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

    Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... , {"content": "A NEW NOTE", "date": "2024-4-30"} ]
    deactivate server

    Note right of browser: The browser executes the callback function that renders the notes
```