This is a base image for use in building/testing gateway policies, Docker builds, etc.  It uses the Python API REST Framework.

http://python-eve.org/

1. Request an account and database in the Dev MongoDB environment

2. Create an env_vars file containing the environment variables to pass into Docker
```
  MONGO_HOST=mongo_server
  MONGO_PORT=27017
  MONGO_USERNAME=evetest
  MONGO_PASSWORD=******
  MONGO_DBNAME=evetest
```

3. Create your API one of three ways

a. Build standalone
```
  git clone https://github.com/kneadproof/eve-mongo-example.git
  cd eve-mongo-example
  virtualenv virtualenv/
  source virtualenv/bin/activate
  pip install -r requirements.txt
  source env_vars
  python run.py
```

b. Build Docker image from scratch
```
  sudo docker build -t eve-mongo-example:v0.1 .
  sudo docker run --name eve-mongo-example -p 5000:5000 --env-file env_vars -it eve-mongo-example:v0.1
```

c. Pull image from registry
```
  sudo docker pull kneadproof/eve-mongo-example:v0.1
  sudo docker run --name eve-mongo-example -p 5000:5000 --env-file env_vars -it eve-mongo-example:v0.1
```

4. Test the connection
```
curl -v http://localhost:5000/people/Proof ; echo
```
