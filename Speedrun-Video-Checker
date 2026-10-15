
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Speedrun Video Checker</title>

<style>
:root {
  --bg: #ffffff;
  --panel: #f7f7f7;
  --text: #171717;
  --muted: #707070;
  --border: #dedede;
  --button: #171717;
  --button-text: #ffffff;
}

body.dark {
  --bg: #111111;
  --panel: #1b1b1b;
  --text: #f5f5f5;
  --muted: #a0a0a0;
  --border: #333333;
  --button: #ffffff;
  --button-text: #111111;
}

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background: var(--bg);
  color: var(--text);
  font-family: Arial, Helvetica, sans-serif;
  transition: background 0.2s, color 0.2s;
}

header {
  height: 68px;
  border-bottom: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 7%;
}

.logo {
  font-size: 17px;
  font-weight: 700;
  letter-spacing: -0.5px;
}

.theme-button {
  background: var(--panel);
  color: var(--text);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 9px 13px;
  cursor: pointer;
}

main {
  max-width: 620px;
  margin: 70px auto;
  padding: 0 22px;
}

h1 {
  font-size: 32px;
  letter-spacing: -1px;
  margin-bottom: 10px;
}

.subtitle {
  color: var(--muted);
  line-height: 1.6;
  margin-bottom: 32px;
}

.panel {
  background: var(--panel);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 24px;
}

label {
  display: block;
  font-size: 14px;
  font-weight: 600;
  margin-bottom: 9px;
}

input, textarea {
  width: 100%;
  background: var(--bg);
  color: var(--text);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 12px;
  font: inherit;
  outline: none;
  margin-bottom: 22px;
}

input:focus, textarea:focus {
  border-color: var(--muted);
}

textarea {
  min-height: 100px;
  resize: vertical;
  line-height: 1.5;
}

.hint {
  color: var(--muted);
  font-size: 12px;
  margin-top: -14px;
  margin-bottom: 22px;
}

.analyze-button {
  width: 100%;
  padding: 13px;
  background: var(--button);
  color: var(--button-text);
  border: none;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 700;
  cursor: pointer;
}

.analyze-button:hover {
  opacity: 0.85;
}

#status {
  display: none;
  margin-top: 18px;
  padding: 14px;
  border: 1px solid var(--border);
  border-radius: 8px;
  font-size: 13px;
  line-height: 1.6;
}

footer {
  text-align: center;
  color: var(--muted);
  font-size: 12px;
  padding: 20px;
}

@media (max-width: 500px) {
  header {
    padding: 0 20px;
  }

  main {
    margin-top: 42px;
  }

  h1 {
    font-size: 27px;
  }

  .panel {
    padding: 18px;
  }
}
</style>
</head>

<body>

<header>
  <div class="logo">SV Checker</div>
  <button class="theme-button" id="themeToggle">
    ☾ Dark Mode
  </button>
</header>

<main>
  <h1>Video Integrity Checker</h1>
  <p class="subtitle">
    Check gameplay footage for potential matches with other
    speedrun recordings.
  </p>

  <section class="panel">
    <form id="checkerForm">

      <label for="videoUrl">Submission Video URL</label>
      <input
        type="url"
        id="videoUrl"
        placeholder="https://www.youtube.com/watch?v=..."
        required
      >

      <label for="referenceUrls">Reference Video URLs</label>
      <textarea
        id="referenceUrls"
        placeholder="Paste reference URLs, one per line..."
        required
      ></textarea>

      <p class="hint">
        Add known recordings to compare against the submission.
      </p>

      <button class="analyze-button" type="submit">
        Analyze Video
      </button>

      <div id="status" role="status" aria-live="polite"></div>

    </form>
  </section>
</main>

<footer>
  Open-source tool for speedrun video review.
</footer>

<script>
const themeToggle = document.getElementById("themeToggle");

themeToggle.addEventListener("click", () => {
  document.body.classList.toggle("dark");

  const isDark = document.body.classList.contains("dark");

  themeToggle.textContent = isDark
    ? "☀ Light Mode"
    : "☾ Dark Mode";
});

document.getElementById("checkerForm").addEventListener(
  "submit",
  (event) => {
    event.preventDefault();

    const videoUrl = document.getElementById("videoUrl").value.trim();
    const references = document.getElementById("referenceUrls")
      .value.trim()
      .split("\n")
      .map(url => url.trim())
      .filter(Boolean);

    const status = document.getElementById("status");
    status.style.display = "block";

    const validUrl = (value) => {
      try {
        const url = new URL(value);
        return url.protocol === "https:" &&
          ["youtube.com", "www.youtube.com", "youtu.be",
           "m.youtube.com"].includes(url.hostname);
      } catch {
        return false;
      }
    };

    if (!validUrl(videoUrl)) {
      status.textContent =
        "Enter a valid YouTube submission URL.";
      return;
    }

    if (references.length === 0 ||
        !references.every(validUrl)) {
      status.textContent =
        "Enter valid YouTube reference URLs, one per line.";
      return;
    }

    status.textContent =
      "Links validated. The video comparison engine is not connected yet.";
  }
);
</script>

</body>
</html>
