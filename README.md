# calculator-app
from flask import Flask, request, render_template_string

app = Flask(__name__)

html = """
<!DOCTYPE html>
<html>
<head><title>Calculator</title></head>
<body>
<h2>Simple Calculator</h2>
<form method="post" action="/">
<input type="number" name="num1" required>
<select name="op">
<option value="+">+</option>
<option value="-">-</option>
<option value="*">*</option>
<option value="/">/</option>
</select>
<input type="number" name="num2" required>
<button type="submit">Calculate</button>
</form>
{% if result is not none %}
<h3>Result: {{ result }}</h3>
{% endif %}
</body>
</html>
"""

@app.route("/", methods=["GET", "POST"])
def calculator():
    result = None
    if request.method == "POST":
        num1 = float(request.form["num1"])
        num2 = float(request.form["num2"])
        op = request.form["op"]
        if op == "+": result = num1 + num2
        elif op == "-": result = num1 - num2
        elif op == "*": result = num1 * num2
        elif op == "/": result = num1 / num2 if num2 != 0 else "Error"
    return render_template_string(html, result=result)

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
