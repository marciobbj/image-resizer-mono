### Image resizer web app

##### Requirements:
- Python 3.6.5

##### How to run:
- Clone the repo.
- Use the command `git submodule update --init --recursive` to get the frontend and backend.
- Install docker-compose in your environment with pip.
- Go to `ìmage-resizer-api` folder and change the permission of `boot.sh` file with the command `sudo chmod +x boot.sh`.
- Use `docker-compose build` and `docker-compose up`

Both containers front-end and back-end are running @`http://localhost:8080` @`http://localhost:8000` respectively.