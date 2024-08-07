
# Codepen-Like React App

This project is a simple Codepen-like application built using React, Codemirror, and react-codemirror2. The app allows users to write HTML, CSS, and JavaScript code and see the output in real-time.

## Features

- Three separate editors for HTML, CSS, and JavaScript.
- Real-time output preview in an iFrame.
- State management for the editor contents using React's useState hook.

## Dependencies

The project uses the following dependencies:

- `codemirror`
- `react-codemirror2`

You can install them using:

```bash
npm install codemirror react-codemirror2
```

## Project Structure

The project structure is as follows:

```
src/
  ├── components/
  │   └── Editor.js
  ├── App.js
  ├── App.css
  └── index.js
```

## Usage

### Editor Component

The `Editor` component is responsible for rendering the individual code editors. It uses `codemirror` and `react-codemirror2` for the editor functionality.

```jsx
// src/components/Editor.js

import React from 'react';
import { Controlled as CodeMirror } from 'react-codemirror2';
import 'codemirror/lib/codemirror.css';
import 'codemirror/theme/material.css';
import 'codemirror/mode/xml/xml';
import 'codemirror/mode/css/css';
import 'codemirror/mode/javascript/javascript';

const Editor = ({ language, value, onChange }) => {
  return (
    <CodeMirror
      value={value}
      options={{
        mode: language,
        theme: 'material',
        lineNumbers: true
      }}
      onBeforeChange={(editor, data, value) => {
        onChange(value);
      }}
    />
  );
};

export default Editor;
```

### App Component

The `App` component manages the state of the editor contents and renders the `Editor` components and the output iFrame.

```jsx
// src/App.js

import React, { useState } from 'react';
import Editor from './components/Editor';
import './App.css';

function App() {
  const [html, setHtml] = useState('');
  const [css, setCss] = useState('');
  const [js, setJs] = useState('');

  const srcDoc = `
    <html>
      <body>${html}</body>
      <style>${css}</style>
      <script>${js}</script>
    </html>
  `;

  return (
    <div className="App">
      <div className="pane top-pane">
        <Editor language="xml" value={html} onChange={setHtml} />
        <Editor language="css" value={css} onChange={setCss} />
        <Editor language="javascript" value={js} onChange={setJs} />
      </div>
      <div className="pane">
        <iframe
          srcDoc={srcDoc}
          title="output"
          sandbox="allow-scripts"
          frameBorder="0"
          width="100%"
          height="100%"
        />
      </div>
    </div>
  );
}

export default App;
```

### CSS

Add some basic styling in `App.css` to make the application look better:

```css
/* src/App.css */

.App {
  display: flex;
  height: 100vh;
  flex-direction: column;
}

.pane {
  display: flex;
  flex: 1;
}

.top-pane {
  display: flex;
  flex: 1;
}

.CodeMirror {
  flex: 1;
  height: 100%;
}
```

## Running the App

To run the app, use:

```bash
npm start
```

This will start the development server and open the app in your default web browser.


Feel free to customize this README as needed.
