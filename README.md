# Quiz App — README

Brief description

This is a small web-based quiz app consisting of a single HTML page with a few JavaScript and CSS files. It is designed to be run from a static server or opened in a browser for local testing.

Files

- `index.html`: App entry point. Loads styles and scripts and contains the markup for the quiz UI.
- `app.css`: General styles for the site.
- `game.css`: Styles specific to the quiz/game screen.
- `canvas.js`: Optional canvas-based helper (used for drawing/animations or visual progress indicators).
- `fake.js`: Provides mock data or helper functions to simulate an API during development.
- `game.js`: Main application logic — quiz flow, event handlers, rendering, and network calls.

How the Fetch API is used

The app uses the Fetch API to retrieve quiz data (questions) and to submit results/scores when available. Fetch runs in the browser and returns a Promise that resolves to a Response object.

Common patterns used in this project:

- GET requests (load questions):

```
fetch('/path/to/questions.json')
  .then(response => {
    if (!response.ok) throw new Error(response.statusText);
    return response.json();
  })
  .then(data => {
    // initialize or start the quiz with `data`
  })
  .catch(err => console.error('Failed to load questions:', err));
```

- POST requests (submit score):

```
fetch('/api/score', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ name: 'Player', score: 12 })
})
  .then(r => r.json())
  .then(result => console.log('Score saved', result))
  .catch(err => console.error('Failed to submit score:', err));
```

Notes and troubleshooting

- If you open `index.html` directly from the filesystem (file://) some browsers block Fetch requests for local files. To avoid this, serve the project over HTTP using a simple static server.

  Example (from the project root):

  ```bash
  python -m http.server 8000
  ```

  Or using `http-server` (Node):

  ```bash
  npx http-server -p 8000
  ```

- CORS: If fetching from a remote API, ensure the API allows cross-origin requests or run a local proxy.
- Where to look: check `game.js` and `fake.js` for the exact fetch calls used by this project.

Customizing the API endpoint

If you want the app to use a different API endpoint, look for a URL constant or the `fetch` calls inside `game.js` and replace the path with your endpoint. If `fake.js` is used, you can swap it out or modify its exported data to test different question sets.

Next steps

- Open `index.html` in a browser or run a local server with the commands above.
- If you want, I can run a quick local server command for you, or update the project to fetch from a configurable URL.

---

Created to explain project files and the Fetch API usage for local testing and small deployments.
