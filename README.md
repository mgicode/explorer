# MOAC Explorers, thin and thick

## thin explorer
  - technology node.js
    - chain3.js
    - koa2
    - ws
  - feature
    - fast
    - lightweight - no database
    - restful query api
    - simple explorer
  - future enhancement
    - restful update api

## thick explorer
  - techonology python3
    - django
    - postgresql
    - websocket
    - django rest framework
  - feature
    - precise
    - comprehensive
    - full explorer
  - future enhancement
    - concurrency
    - async

## supported
  - linux
  - macos

## docker image
  - use ubuntu 1804

## deployment
  - apache
  - nginx
  - haproxy

## test
  - thin explorer
    - git submodule update --init koa
    - cd koa
    - npm install
    - screen session for web service with websocket
      - npm start
      - node app.js (if start does not work above)
      - test api query
        - /api/block/:args
        - /api/uncle/:args/:index
        - /api/tx/:args
        - /api/address/:args
    - screen session for websocket feed
      - node feed-ws.js
    -  web browser
      - http://localhost:3000
        - test live update
        - test search
      - some links visit the thick explorer
  - thick explorer
    - thin explorer working
    - git submodule update --init django
    - cd django
    - pip3 install -r requirements.txt
    - ./manage.py migrate ; ./manage.py makemigrations; ./manage.py migrate
    - screen session, sychronize from moac to database, calls api from the thin explorer above
      - ./manage.py sync_ledger --moac 
    - screen session, run the web server
      - ./manage.py runserver
    - browse http://localhost:8000

## requirements
  0. have moac running with --rpc option (--rpcaddr 0.0.0.0 if not on localhost, update koa/config.js in this case)
  1. have git available
  2. have node.js >= 8
  3. have python3 >= 3.6, virtualenv is recommended
  4. have postgresql database running and psql works, update django/local_settings.py for database information
