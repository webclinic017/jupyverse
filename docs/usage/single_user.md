The single user mode is usually meant to run e.g. JupyterLab as a desktop application. Under the hood, a server and a web front-end are launched, but it should be transparent to the user, who just interacts with a "web app".

Even though Jupyverse most often runs on a personal computer in this mode, it is not limited to this use case. For instance, if it runs on a network, it could be accessed by other people. It is thus important to limit access to the server, especially considering that Jupyter users can run potentially harmful code.

This is why Jupyverse comes with built-in authentication. Please refer to the [auth plugins](../../plugins/auth) section for more details. The authentication mechanisms below make use of the [fps-auth](../../plugins/auth/#fps-auth) plugin.

## Token authentication

This is the default mode when launching Jupyverse, just enter in a terminal:
```bash
jupyverse
# same as: jupyverse --auth.mode=token
```
This should open a new window in a browser, and load JupyterLab or RetroLab, depending on the front-end you chose to install (see [Install](../../install)).

If you look at the terminal, you should see among other things:
```
[I 2022-08-30 09:37:55 auth] To access the server, copy and paste this URL:
[I 2022-08-30 09:37:55 auth] http://127.0.0.1:8000/?token=59665677-06c6-4530-ab67-d26cd8865d8b
```
This is the URL the browser window was opened with, and you can see that a `token` was passed as a query parameter. When the request is made to the server, the token is checked and a cookie is set in the browser. The user is now authenticated and doesn't need to pass the token again in other requests.

Other users trying to access the server will be redirected to a login page. They can enter the token there, or completely bypass this step if they paste the above URL. Sharing the token is the responsibility of the user who launched Jupyverse. This simple mechanism effectively prevents access to the server by unkown users.

## No authentication

If you trust everybody who can access the server, you can launch Jupyverse with no authentication whatsoever. It can also be convenient if you run Jupyverse on your personal computer and want to open e.g. JupyterLab in multiple browsers (e.g. Firefox and Google Chrome), since they don't share cookies. This way you won't need to pass any token in the URL.

Enter in a terminal:
```bash
jupyverse --auth.mode=noauth
```
