# Frontline volunteer app server

[![Codacy Badge](https://api.codacy.com/project/badge/Grade/e8c2c86f24df476cae7476c86a92bd0d)](https://app.codacy.com/manual/Kailash-Sankar/frontline_server?utm_source=github.com&utm_medium=referral&utm_content=Kailash-Sankar/frontline_server&utm_campaign=Badge_Grade_Dashboard) [![Known Vulnerabilities](https://snyk.io/test/github/Kailash-Sankar/frontline_server/badge.svg?targetFile=package.json)](https://snyk.io/test/github/Kailash-Sankar/frontline_server?targetFile=package.json) ![Docker Image Size (latest by date)](https://img.shields.io/docker/image-size/kailashsankar/frontline_server)



## local setup
    git clone
    npm install

    # update env, follow instructions in example file
    # setup mongodb locally
    cp .env.sample to .env 
    
    # for nodemon, otherwise npm start
    npm run dev

## from docker hub
    docker pull kailashsankar/frontline_server
    docker run -d --restart=always --network=pulse --name=frontline_server -p 0.0.0.0:3080:80 frontline_server:current

## local docker setup

    # move the .env file to a local path
    docker build  -t frontline_server:latest .
    docker run -d --restart=always --name=frontline_server -p 0.0.0.0:3080:80 -v /<path_to_env>/.env:/app/.env frontline_server:latest

## alfred config

    # it's a hacked up cli util to avoid typing large docker commands one by one.
    # help guide is in the repo: https://github.com/Kailash-Sankar/alfred

    # create config like below or customize the steps in alfred services
    frontline_server: {
        path: `/<path_to_repo>/`,
        name: 'frontline_server',
        bind: '0.0.0.0:3080:80',
        type: 'standard',
    },

    alfred --serve frontline_server --dryrun
    alfred --serve frontline_server

## db setup
    # for mongodb, created a mounted volume first
    # docker volume create mongodbdata
    # add below config to alfred


        mongodb: {
            image: 'mongo',
            version: '4.2.1',
            name: 'mongodb',
            bind: '27017-27019:27017-27019',
            type: 'db_hub',
            volume: 'mongodbdata:/data/db'
        }

    alfred --serve mongodb --dryrun
    alfred --serve mongodb

Created with boilterplate: https://github.com/maitraysuthar/rest-api-nodejs-mongodb
