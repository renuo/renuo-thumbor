# Renuo Thumbor Config

This repository contains the configuration files which are required to run [thumbor](https://github.com/thumbor/thumbor) on 
[Heroku](https://www.heroku.com).

## Setup

* Install [pyenv](https://github.com/yyuu/pyenv) and [pyenv-virtualenv](https://github.com/yyuu/pyenv-virtualenv)

```sh
pyenv install 2.7.9
```

* Install virtualenvwrapper

Make sure that this has been added to your environment (e.g. .zshrc):

```sh
eval "$(pyenv init - zsh)"
eval "$(pyenv virtualenv-init -)"
```

Clone the project, setup virtualenv and install dependencies:

```sh
git clone git@github.com:renuo/renuo-thumbor.git
cd renuo-thumbor
pyenv virtualenv 2.7.9 renuo-thumbor-2.7.9
pip install -r requirements.txt
pyenv rehash
```

## Development

```
thumbor -p $PORT -c ./thumbor.conf
```

## Deployment

```
heroku create example
git clone https://github.com/renuo/renuo-thumbor.git
cd renuo-thumbor
git remote add heroku git@heroku.com:example.git
heroku config:set THUMBOR_SECURITY_KEY='<long random string, min 28 characters, e.g. UJwHAZLsRejTyLI88lAriHL7xAXa6q0umiwwpPcP>'
heroku config:set WEB_CONCURRENCY=20
git push heroku master
```

## Config

### THUMBOR_SECURITY_KEY

The THUMBOR_SECURITY_KEY is a shared key (proxy and thumbor app) to validate
that the image can be processed by thumbor.

In thumbor this key is called SECURITY_KEY. See also: https://github.com/thumbor/thumbor/wiki/Security

Generate it randomly, and keep it secret (only shared with the thumbor app).

Example: UJwHAZLsRejTyLI88lAriHL7xAXa6q0umiwwpPcP

## Renuo Thumbs Proxy

See https://github.com/renuo/renuo-thumbs-proxy
