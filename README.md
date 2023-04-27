# LangChain Running on Fly.io

Deploying a minimal Flask + [LangChain](https://github.com/hwchase17/langchain) application on Fly.io.

## App: Best places to eat

The application will give 3 options where to eat in `<place>`. The default value is `Berlin`.

**Prompt: `What are the 3 best places to eat in {place}?`**

You can define your own input variable (`place`) by calling:
```
https://<your-app-name>.fly.dev/<place>
```

Examples:

#### Country
- Norway: `https://<your-app-name>.fly.dev/norway`

#### City
- São Paulo: `https://<your-app-name>.fly.dev/s%C3%A3o%20paulo`

#### Specific area
- Prague Old Town: `https://<your-app-name>.fly.dev/prague%20old%20town`

## Local Development ⚒️

### Create and Activate a Virtual Environment

We'll be using [venv](https://flask.palletsprojects.com/en/2.3.x/installation/#create-an-environment), but you can choose any virtual environment to manage the dependencies (e.g. virtualenv).
```shell
# Unix/macOS
$ python3 -m venv venv
$ . venv/bin/activate

# Windows
$ py -3 -m venv venv
$ venv\Scripts\activate
```

### Install Dependencies from `requirements.txt`

```shell
python -m pip install -r requirements.txt
```

### Set Up `.env` file

The environment variables are stored in the `.env` file.

Rename the `.env.dist` file to `.env`. Update the `OPENAI_API_KEY` environment variable with your own secret key:
```dotenv
FLASK_APP=hello
OPENAI_API_KEY=<your-openai-api-secret-key>
```

The OpenAI API uses API keys for authentication. 
Visit your [OpenAI API Key](https://platform.openai.com/account/api-keys) page to retrieve the API key you'll use in your requests.

### Run the project

```shell
flask run
```

## Deploying to Fly.io 🚀

[flyctl](https://fly.io/docs/hands-on/install-flyctl/) is the command-line utility provided by Fly.io.

If not installed yet, follow these [instructions](https://fly.io/docs/hands-on/install-flyctl/), [sign up](https://fly.io/docs/hands-on/sign-up/) and [log in](https://fly.io/docs/hands-on/sign-in/) to Fly.io.

### Launching Our App

`fly launch` will detect our Python (Flask) App.

```shell
fly launch
```

During the launch you will:
- Choose an app name
- Select Organization
- Choose a region for deployment

The `Procfile` already exists in this project - a new one will be generated for you if your project doesn't have one.

> More details on `fly launch` can be found [here](https://fly.io/docs/languages-and-frameworks/python/#configure-the-app-for-fly).

### Set Environment Variables

Set the `OPENAI_API_KEY` environment variable:
```shell
fly secrets set OPENAI_API_KEY=<your-openai-api-secret-key>
```

### Deploy to Fly.io

```shell
fly deploy
```

> More details on `fly deploy` can be found [here](https://fly.io/docs/languages-and-frameworks/python/#deploying-to-fly).

### Visit Your App

```shell
fly open
```


For detailed documentation on how to deploy a Flask application on [Fly.io](https://fly.io/), check [Run a Python App](https://fly.io/docs/languages-and-frameworks/python/).