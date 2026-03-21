<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Modern Left-Aligned Custom Select</title>

<style>
  :root {
    --primary: #6366f1;
    --bg: #f8fafc;
    --text: #1e293b;
    --border: #e2e8f0;
    --surface: #ffffff;
    --radius: 12px;
  }

  * { box-sizing: border-box; }

  body {
    font-family: 'Inter', system-ui, -apple-system, sans-serif;
    background-color: var(--bg);
    color: var(--text);
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    margin: 0;
  }

  form {
    width: 100%;
    max-width: 400px;
    padding: 2.5rem;
    background: var(--surface);
    border-radius: var(--radius);
    box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.05);
  }

  p {
    display: flex;
    flex-direction: column;
    gap: 10px;
    margin: 0;
  }

  label {
    font-size: 0.875rem;
    font-weight: 600;
    color: #64748b;
    margin-left: 4px;
  }

  /* --- Base Select Logic --- */
  
  select,
  ::picker(select) {
    appearance: base-select;
  }

  select {
    padding: 14px 18px;
    border: 1px solid var(--border);
    border-radius: var(--radius);
    background: white;
    font-size: 1rem;
    cursor: pointer;
    transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
    box-shadow: 0 1px 2px rgba(0,0,0,0.03);
    color: var(--text);
    display: flex;
    align-items: center;
  }

  select:hover {
    border-color: var(--primary);
    background: #fafafa;
  }

  select:focus {
    outline: 3px solid #6366f122;
    border-color: var(--primary);
  }

  select::picker-icon {
    content: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16' fill='%2364748b' viewBox='0 0 256 256'%3E%3Cpath d='M213.66,101.66l-80,80a8,8,0,0,1-11.32,0l-80-80a8,8,0,0,1,11.32-11.32L128,164.69l74.34-74.35a8,8,0,0,1,11.32,11.32Z'%3E%3C/path%3E%3C/svg%3E");
    transition: transform 0.3s ease;
    margin-left: auto; /* Keeps arrow on the right */
  }

  select:open::picker-icon {
    transform: rotate(180deg);
  }

  /* --- Popover/Dropdown Styling --- */

  ::picker(select) {
    width: anchor-size(width);
    padding: 6px;
    border: 1px solid var(--border);
    border-radius: var(--radius);
    background: rgba(255, 255, 255, 0.95);
    backdrop-filter: blur(12px);
    box-shadow: 0 12px 30px -10px rgba(0, 0, 0, 0.15);
    
    /* Animation Logic */
    opacity: 0;
    transform: translateY(-8px) scale(0.98);
    transition: 
      opacity 0.2s, 
      transform 0.2s, 
      display 0.2s allow-discrete;
  }

  :open::picker(select) {
    opacity: 1;
    transform: translateY(6px) scale(1);
  }

  @starting-style {
    :open::picker(select) {
      opacity: 0;
      transform: translateY(-8px) scale(0.98);
    }
  }

  /* --- Option Alignment --- */

  option {
    display: flex;
    align-items: center;
    justify-content: flex-start; /* Explicitly align contents to the left */
    gap: 12px;
    padding: 10px 14px;
    border-radius: calc(var(--radius) - 6px);
    margin: 2px 0;
    transition: background 0.15s ease;
    color: var(--text);
    cursor: pointer;
  }

  option:hover {
    background: #f1f5f9;
  }

  option:checked {
    background: #eef2ff;
    color: var(--primary);
    font-weight: 500;
  }

  option::checkmark {
    content: "✓";
    margin-left: 8px; /* sits closely to the text */
    font-weight: bold;
    color: var(--primary);
    /* Set display: none; if you want the text strictly alone */
  }

  /* Browser Compatibility Message */
  @supports not (appearance: base-select) {
    .compat-notice {
      padding: 12px;
      background: #fff7ed;
      border: 1px solid #ffedd5;
      border-radius: 8px;
      color: #9a3412;
      font-size: 0.85rem;
      margin-bottom: 20px;
      line-height: 1.4;
    }
  }
</style>
</head>
<body>

<form>

  <p>
    <select id="pet-select">
      <option value="">Choose a pet...</option>
      <option value="cat">Cat</option>
      <option value="dog">Dog</option>
      <option value="hamster">Hamster</option>
      <option value="chicken">Chicken</option>
      <option value="fish">Fish</option>
    </select>
  </p>
</form>

</body>
</html>
