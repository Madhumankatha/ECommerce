<p>
INSTALL PACKAGE

$ pip install -r requirements.txt

RUN PROJECT

$ uvicorn main:app

APP RUNNING URL

http://127.0.0.1:8000/

SWAGGER UI

http://127.0.0.1:8000/docs

</p>

<p>TEMPLATE</p>

<pre>
{% extends "base.html" %}
{% block title %}Title{% endblock %}

{% block content  %}
<div class="container">
    <!-- Added your content -->
</div>
{% endblock %}

{% block javascript %}
<script type="text/javascript">
    <!-- Added your Javascript code -->
</script>
{% endblock %}

</pre>

<p>ADMIN TEMPLATE</p>

<pre>

{% extends "/admin/base.html" %}
{% block title %}Title{% endblock %}

{% block content  %}
<div class="container">
    <!-- Added your content -->
</div>
{% endblock %}

{% block javascript %}
<script type="text/javascript">
    <!-- Added your Javascript code -->
</script>
{% endblock %}

</pre>

<p>cart query<p>
<pre>
SELECT * from USERS u,carts c, plants p where u.id=c.uid and c.pid=p.id
</pre>

<p>
Declaring URLs

GET METHOD
</p>

<pre>
@app.get("/", response_class=HTMLResponse)
def index(request: Request):
    return templates.TemplateResponse("index.html", {"request": request})
</pre>

POST METHOD

<pre>
@app.post("/", response_class=HTMLResponse)
def index(request: Request):
    return RedirectResponse("/index", status_code=status.HTTP_302_FOUND)
</pre>

Database Connection

READ DATA FROM TABLE

<pre>
con = sqlite3.connect("app.db")
    con.row_factory = sqlite3.Row
    cur = con.cursor()
    cur.execute("select * from products where id =?", [pid])
    description = cur.fetchall()
    con.close
</pre>

INSERT DATA INTO TABLE

<pre>
    with sqlite3.connect("app.db") as con:
        cur = con.cursor()
        cur.execute("INSERT into users(username, password, email, address, phone) values(?,?,?,?,?)",
                    (username, password, email, address, phone))
        con.commit()
</pre>

SESSION HANDLING

<pre>
# adding the Session Middleware
from starlette.middleware.sessions import SessionMiddleware

app.add_middleware(SessionMiddleware, secret_key='MyApp')

#SETTING A SESSION
request.session.setdefault("isLogin", True)

#GETTING A SESSION
request.session.get("isLogin")
</pre>
